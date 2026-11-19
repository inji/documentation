# Credential Configuration - Validated Metadata

#### What it is

The Add and Update Credential Configuration APIs now require the metadata that ends up in the issuer well-known metadata, and validate it against what the deployment supports.

#### Request attributes

| Attribute                            | Rule                                                                                       |
| ------------------------------------ | ------------------------------------------------------------------------------------------ |
| cryptographicBindingMethodsSupported | Mandatory, non-empty. Values must be supported by the deployment                           |
| proofTypesSupported                  | Mandatory, non-empty. Values must be supported by the deployment                           |
| signatureAlgo                        | Mandatory in DataProvider plugin mode. Optional in VCIssuance mode, but validated if sent  |
| signatureCryptoSuite                 | Required for ldp\_vc. Must not be sent for dc+sd-jwt. Ignored and not stored for mso\_mdoc |

The plugin mode comes from mosip.certify.plugin-mode, not from the request.

#### What the metadata advertises

| Format    | credential\_signing\_alg\_values\_supported  |
| --------- | -------------------------------------------- |
| ldp\_vc   | Crypto suite, e.g. \["Ed25519Signature2020"] |
| dc+sd-jwt | signatureAlgo, e.g. \["ES256"]               |
| mso\_mdoc | COSE identifier, e.g. \[-7]                  |

#### Example (DataProvider mode, ldp\_vc)

```json
{
  "credentialConfigKeyId": "RegistrationReceiptCredential",
  "vcTemplate": "<Base64-encoded Velocity template>",
  "keyManagerAppId": "CERTIFY_VC_SIGN_ED25519",
  "keyManagerRefId": "ED25519_SIGN",
  "signatureAlgo": "EdDSA",
  "signatureCryptoSuite": "Ed25519Signature2020",
  "credentialFormat": "ldp_vc",
  "cryptographicBindingMethodsSupported": ["did:jwk"],
  "proofTypesSupported": { "jwt": { "proof_signing_alg_values_supported": ["ES256", "EdDSA"] } }
}
```

Each proof type must be declared in mosip.certify.credential-config.proof-types-supported, and proof\_signing\_alg\_values\_supported must be a non-empty subset of the algorithms declared for it. See [Credential Issuer Configuration](https://github.com/inji/inji-certify/blob/release-1.0.x/docs/technical_docs/Credential_Issuer_Configuration.md) for the full validation rules.

#### Upgrade actions

* Add jwk to the ldp\_vc and dc+sd-jwt entries of mosip.certify.credential-config.cryptographic-binding-methods-supported if configurations use it:

properties

```
mosip.certify.credential-config.cryptographic-binding-methods-supported={
  'ldp_vc': {'jwk','did:jwk','did:key'},
  'mso_mdoc': {'cose_key'},
  'dc+sd-jwt': {'jwk','did:jwk','did:key'}
}
```

* Every Update request must now send the mandatory attributes, even when it only changes an unrelated field such as the display name.
