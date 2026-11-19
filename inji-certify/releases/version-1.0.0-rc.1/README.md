# Version 1.0.0-rc.1

<mark style="color:red;">**Coming Soon!**</mark>

**Release Version:** v1.0.0-rc.1

**Release Type:** Release Candidate (RC)

**Release Date:** 18th November, 2026

{% hint style="info" %}
**Note:** This release builds on the OpenID4VCI 1.0 foundation delivered in [v1.0.0-alpha.1](../version-1.0.0-alpha.1/). It contains several breaking changes listed under Breaking changes and 'Upgrade actions', Do review them before upgrade.
{% endhint %}

### Overview

Inji Certify v1.0.0-rc.1 makes credential issuance safer and easier to configure. It adds stronger protection for credential requests, improves compatibility with current OpenID4VCI standards, and **catches incomplete configuration earlier**.

It introduces DPoP-constrained access tokens, DCQL-based PDI, an embedded Inji Verify library, an upgraded Velocity template engine, and a set of validation and stability fixes.

It also simplifies Presentation During Issuance by **bringing the required Inji Verify capability into Inji Certify itself**. If you use this flow or manage credential configurations, do review the 'Breaking change' and 'Upgrade actions' through this release notes before deploying.

### Major Features & Enhancements

**Summary of Key Changes**:

* DPoP-constrained access token support on the credential endpoint.
* DCQL-only VP request configuration for the Interactive Authorization Endpoint (IAE). Presentation Exchange (PEX) is no longer supported.
* Inji Verify embedded as a library verify-core 1.0.0-rc.1 in the PDI flow.
* mdoc alignment with OpenID4VCI 1.0 (credential response structure, integer COSE algorithm identifiers in issuer metadata).
* Credential Configuration API: `cryptographicBindingMethodsSupported`, `proofTypesSupported` and `signatureAlgo` are validated and mandatory. The properties fallback is removed.
* `ldp_vc` configurations advertise their crypto suite in `credential_signing_alg_values_supported`.
* Velocity template engine upgraded from 1.7 to 2.4.1 (fixes CVE-2020-13936).
* Compatibility with eSignet 1.8.0.

#### 1. DPoP-Constrained Access Tokens

Certify can now check that a supported access token is being used by the wallet it was issued to. This helps protect against a copied token being reused by someone else.

Existing bearer-token integrations continue to work. Wallets using DPoP gain additional protection against token replay and misuse, which means that Inji Certify validates the DPoP proof, including its key binding, request binding, freshness, and single-use identifier.

Certify now acts as a DPoP (RFC 9449) resource server on the credential endpoint. When a wallet presents a DPoP-bound access token, Certify validates the accompanying DPoP proof, so the token can only be used by the holder of the bound key. This protects against access token theft and replay.

* Plain Bearer tokens continue to work.
* A DPoP-bound token (cnf.jkt) presented as Bearer is refused.
* A plain token presented under the DPoP scheme is refused.
* Proofs are single-use (jti replay cache) and checked for typ, alg, signature, htm, htu, iat freshness, ath and cnf.jkt.
* DPoP applies to tokens issued by an external authorization server such as eSignet. Tokens minted by Certify's own /oauth/token (pre-authorized and PDI flows) are Bearer tokens.

#### 2. DCQL Support in Presentation During Issuance

Presentation During Issuance now uses the current OpenID4VP query model. This gives issuers and wallets a clearer way to agree on which credential the wallet must present.

Certify also includes the Inji Verify library for this flow, so you no longer need to run a separate verifier service.

Which means that the VP request configuration for the IAE now uses the Digital Credentials Query Language (DCQL), in line with OpenID4VP 1.0. Issuers use a dcqlQuery block to state which credentials the holder must present during issuance. The wallet's vp\_token is keyed by the query, so no presentation\_submission is needed.

{% hint style="danger" %}
**Breaking change:**&#x20;

* Presentation Exchange (presentation\_definition) is no longer supported in the PDI flow starting version-1.0.0-rc.1 release.
{% endhint %}

{% hint style="success" %}
**Before upgrade**:

1. Replace each `presentation_definition` with its equivalent `dcqlQuery`
2. Remove 'Presentation During Issuance' settings that point to an external Inji Verify service
3. Apply the included database upgrade scripts
{% endhint %}

#### 3. Embedded Inji Verify Library in the PDI Flow

PDI now uses Inji Verify as an embedded library verify-core 1.0.0-rc.1 instead of calling a separately deployed Inji Verify service. This removes a runtime dependency and simplifies deployment.

#### 4. mdoc Alignment with OpenID4VCI 1.0

mdoc credential responses and issuer metadata now follow OpenID4VCI 1.0 conventions more closely. Wallets and metadata consumers can identify compatible signing algorithms more reliably.

* The mdoc credential response structure follows the OpenID4VCI 1.0 specification.
* `credential_signing_alg_values_supported` for `mso_mdoc` configurations is published as integer COSE algorithm identifiers (for example `-7` for `ES256`).

{% hint style="success" %}
**Before upgrade**:&#x20;

* Update mdoc configurations and metadata consumers to use integer COSE algorithm identifiers, such as `-7` for `ES256`, rather than string algorithm names.
{% endhint %}

#### 5. Credential Configuration API: Mandatory, Validated Metadata

Credential configuration APIs now require the metadata that Certify publishes to wallets. This means incomplete or unsupported settings are found when you create or update a configuration, rather than being filled from deployment defaults.

The Add (POST /credential-configurations) and Update (PUT /credential-configurations/{credentialConfigKeyId}) APIs now require these attributes, for every credential format:

* cryptographicBindingMethodsSupported
* proofTypesSupported
* signatureAlgo (mandatory in DataProvider plugin mode; optional in VCIssuance mode, but validated if sent)

Values are validated against what the Certify deployment supports and are reflected in the issuer well-known metadata. Missing, null or empty values are rejected, and nothing is filled in from deployment properties any more.

The value in the issuer metadata is derived from the configuration:

<table><thead><tr><th width="188.02734375">Format</th><th>credential_signing_alg_values_supported advertises</th></tr></thead><tbody><tr><td>ldp_vc</td><td>The crypto suite, e.g. Ed25519Signature2020 (OpenID4VCI 1.0 Appendix A.1.2.2)</td></tr><tr><td>dc+sd-jwt</td><td>The configured signatureAlgo, e.g. ES256</td></tr><tr><td>mso_mdoc</td><td>The COSE identifier of signatureAlgo, e.g. -7</td></tr></tbody></table>

{% hint style="success" %}
**Before upgrade**: Send `cryptographicBindingMethodsSupported` and `proofTypesSupported` in every affected Add or Update request. In DataProvider mode, also send `signatureAlgo`.&#x20;
{% endhint %}

#### 6. Velocity Template Engine Upgraded from 1.7 to 2.4.1

Velocity was updated from 1.7 to 2.4.1 to address [CVE-2020-13936](https://nvd.nist.gov/vuln/detail/CVE-2020-13936) and limit unsafe reflective access in credential templates.

Credential templates (`vc_template`) are rendered with Velocity 2.4.1, which fixes `CVE-2020-13936`. Template behaviour changes:

1. \#if **treats empty values as false.** An empty string, list, map or array is now false. An empty phone field is omitted instead of rendered as "" to always render a field, use #if($var || $var == '') or the quiet reference $!{var}.
2. **Loop variables renamed**: $velocityCount becomes $foreach.count; $velocityHasNext becomes $foreach.hasNext.
3. **Reflection blocked**: SecureUberspector is enabled, so templates can no longer call methods on Class, ClassLoader, Runtime or System. Normal field access and the $\_dateTool and $\_esc tools are unaffected.

**Breaking change**: Review existing templates before upgrade. Empty values, loop variables, and reflective access behave differently in Velocity 2.4.1.

#### 7. eSignet 1.8.0 Compatibility

Certify is validated with eSignet 1.8.0 as the authorization server. Two properties change (see Breaking Changes).

### User Stories Released

<table><thead><tr><th width="125.453125">Git ID</th><th>Description</th></tr></thead><tbody><tr><td> <a href="https://github.com/inji/inji-certify/issues/963">#963</a> </td><td>Add support for DPoP-constrained access tokens in Certify</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/962">#962</a> </td><td>Support DCQL in the VP request configuration on the IAE endpoint</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/902">#902</a> </td><td>Integrate Inji Verify as an embedded library in the PDI flow instead of calling it as a separate service</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/739">#739</a> </td><td>Enhance the Interactive Authorization (IAR) endpoint to support OpenID4VCI 1.0-compliant PDI</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/989">#989</a> </td><td>Validate proof_types_supported, cryptographic_binding_methods_supported and signing algorithm in the Add/Update Credential Configuration API</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/1099">#1099</a> </td><td>Make binding methods, proof types and signatureAlgo mandatory on Add/Update and remove the properties fallback</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/1110">#1110</a> </td><td>Advertise the crypto suite in credential_signing_alg_values_supported for ldp_vc</td></tr></tbody></table>

### Bug Fixes

All bugs fixed in this release are listed [here](https://github.com/inji/inji-certify/issues?q=is%3Aissue+milestone%3A1.0.0-rc.1+type%3ABug).

<table><thead><tr><th width="122.79296875">Git ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-certify/issues/711">#711</a></td><td>When invalid sd_claims are provided, the issuer throws an error and does not fetch the VC</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/679">#679</a></td><td>Validation issues for the qrsettings block in the Credential Config API</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/686">#686</a></td><td>Error message mismatch in the mdoc-mDL use case (PDI)</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/878">#878</a></td><td>invalid_request returned for unreadable and malformed bodies on non-VCI endpoints, instead of unknown_error</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/1054">#1054</a></td><td>did:jwk holder ID created from the JWK proof header contained base64 padding, breaking OpenID4VP presentation</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/1044">#1044</a></td><td>mDoc timestamp format did not comply with ISO specification, failing the OpenID4VP conformance test</td></tr></tbody></table>

### Known Issues

All open issues for Inji Certify are listed [here](https://github.com/inji/inji-certify/issues?q=is%3Aissue+state%3Aopen+-milestone%3A1.0.0-rc.1+type%3ABug).

<table><thead><tr><th width="144.71484375">Git ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-certify/issues/842">#842</a></td><td>Validations to add qrSignatureAlgo in the Credential Config API</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/700">#700</a></td><td>Improper validation in Status Update endpoints</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/730">#730</a></td><td>SVG template: face image and label attribute path mismatch</td></tr></tbody></table>

### Breaking Changes

<table><thead><tr><th width="265.859375">Change</th><th width="265.91796875">Required action</th><th>Impact</th></tr></thead><tbody><tr><td>mdoc credential response structure aligned to OpenID4VCI 1.0</td><td>Update wallets/clients to parse the new structure</td><td>Clients using the previous mdoc response structure cannot read the issued credential</td></tr><tr><td>mdoc credential_signing_alg_values_supported: strings replaced by integer COSE identifiers (e.g. -7)</td><td>Update mdoc credential configurations and metadata consumers</td><td>Wallets expecting string algorithm names will not match the published metadata</td></tr><tr><td>ldp_vc credential_signing_alg_values_supported now lists the crypto suite (e.g. Ed25519Signature2020) instead of a JWS algorithm (e.g. EdDSA)</td><td>Update wallets/clients that read this metadata for ldp_vc</td><td>Clients matching on the JWS algorithm will not find a match</td></tr><tr><td>Credential configuration metadata is mandatory; properties fallback removed;</td><td>Send cryptographicBindingMethodsSupported and proofTypesSupported on every Add and Update, plus signatureAlgo in DataProvider mode. Add jwk to the ldp_vc and dc+sd-jwt entries of mosip.certify.credential-config.cryptographic-binding-methods-supported if you use it</td><td>Requests that omit these attributes, even Updates that change only an unrelated field, are rejected</td></tr><tr><td>Inji Verify service in PDI replaced by the embedded library</td><td>Remove configuration pointing to an external Inji Verify service for PDI</td><td>A separately deployed Inji Verify service is no longer used by Certify</td></tr><tr><td>PEX replaced by DCQL in the PDI VP request</td><td>Change PDI VP request configurations from presentation_definition to DCQL (dcqlQuery)</td><td>PDI requests configured with a Presentation Exchange definition are not supported</td></tr><tr><td>Velocity 1.7 to 2.4.1</td><td>Review credential templates: empty values are false in #if; $velocityCount and $velocityHasNext become $foreach.count and $foreach.hasNext; reflective calls are blocked</td><td>Templates relying on old behaviour render differently or fail</td></tr><tr><td>eSignet 1.8.0 configuration</td><td>Set mosip.esignet.discovery.issuer-id to the eSignet issuer base URL (e.g. https://esignet-mock.released.mosip.net/), not the /v1/esignet URL. For MOSIP ID use cases set mosip.certify.ida.vci-user-info-cache=esignet:userinfo instead of userinfo</td><td>With the old values, Certify does not work with eSignet 1.8.0</td></tr></tbody></table>

### Repositories Released

| Repository                 | Version                                                                            |
| -------------------------- | ---------------------------------------------------------------------------------- |
| inji-certify               | [v1.0.0-rc.1](https://github.com/inji/inji-certify/tree/v1.0.0-rc.1)               |
| inji-config                | [v1.0.0-rc.1](https://github.com/inji/inji-config/tree/v1.0.0-rc.1)                |
| digital-credential-plugins | [v1.0.0-rc.1](https://github.com/inji/digital-credential-plugins/tree/v1.0.0-rc.1) |

### Compatible Modules

| Module                    | Version                                                                         |
| ------------------------- | ------------------------------------------------------------------------------- |
| keymanager                | [v1.4.0](https://github.com/mosip/keymanager/tree/v1.4.0)                       |
| eSignet                   | [1.8.0](https://github.com/mosip/esignet/tree/v1.8.0)                           |
| IDA                       | [1.3.0](https://github.com/mosip/id-authentication/tree/v1.3.0)                 |
| Sunbird C                 | [v2.0.0](https://github.com/Sunbird-RC/sunbird-rc-core/releases/tag/v2.0.0-rc3) |
| esignet-mock-services     | [v0.11.2](https://github.com/mosip/esignet-mock-services/tree/v0.11.2)          |
| commons                   | [1.6.0](https://github.com/mosip/commons/tree/v1.3.0)                           |
| inji-verify (verify-core) | [1.0.0-rc.1](https://github.com/inji/inji-verify/tree/v1.0.0-rc.1)              |
| mimoto                    | 1.0.0-rc1(yet to release)                                                       |
| inji-web                  | 1.0.0-rc1(yet to release)                                                       |

### Documentation

* [Feature Documentation](https://docs.inji.io/inji-certify/overview/features)
* [Local Setup](https://docs.inji.io/inji-certify/build-and-deploy/local-setup)
* [API Documentation](https://mosip.stoplight.io/docs/inji-certify)
* [Test Report](test-report.md)







***

## Features

### 1. DPoP-Constrained Access Tokens

#### What it is

DPoP (Demonstrating Proof of Possession, [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449.html)) binds an access token to a key pair held by the wallet. A stolen token cannot be replayed without the matching private key.

#### How it works

Inji Certify is the **resource server**. It validates DPoP but does not issue DPoP-bound tokens.

1. The wallet requests a token from an authorization server such as eSignet. The client must be registered with additionalConfig.`dpop_bound_access_tokens: true`.
2. The authorization server puts the thumbprint of the wallet's public key in the token as `cnf.jkt`.
3. The wallet calls the credential endpoint with Authorization: DPoP and a fresh DPoP proof JWT.
4. Certify verifies the token, then the proof, and issues the credential.

| Token                | Presented as          | Result                    |
| -------------------- | --------------------- | ------------------------- |
| Plain (no cnf)       | Bearer                | Accepted                  |
| DPoP-bound (cnf.jkt) | DPoP with valid proof | Accepted                  |
| DPoP-bound           | Bearer                | Refused (downgrade guard) |
| Plain                | DPoP                  | Refused                   |

#### Proof checks

Certify checks that the proof:

* Is a single JWT with typ dpop+jwt
* Uses an allowed asymmetric algorithm and embeds a public jwk
* Has a valid signature
* Has htm equal to the HTTP method and htu equal to the public credential endpoint URL
* Has an iat within the allowed age
* Has ath equal to the hash of the access token
* Has a key thumbprint equal to cnf.jkt
* Has not been used before (jti replay protection)

#### Configuration

| Property                                    | Purpose                                                       | Example                                         |
| ------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------- |
| mosip.certify.authn.filter-urls             | URLs protected by the token filter                            | { '${server.servlet.path}/issuance/credential'} |
| mosip.certify.domain.url                    | Public issuer URL, used for the htu check                     | http://localhost:8090                           |
| mosip.certify.dpop.allowed-algorithms       | Accepted proof algorithms                                     | ES256,ES384,ES512,RS256,PS256,EdDSA             |
| mosip.certify.dpop.proof-max-age            | Maximum proof age in seconds                                  | 60                                              |
| mosip.certify.dpop.clock-skew               | Clock drift tolerance in seconds                              | 10                                              |
| mosip.certify.dpop.jti.cache-expire-seconds | Replay cache TTL. Must exceed proof-max-age + 2 \* clock-skew | 120                                             |
| mosip.certify.cache.names                   | Must include dpopJti                                          | ...,dpopJti                                     |

Certify refuses to start if the dpopJti cache TTL is missing or too short. In multi-replica deployments use a distributed cache (spring.cache.type=redis), otherwise a replayed proof can pass on a different pod.

#### Notes

* Tokens minted by Certify's own /oauth/token (pre-authorized and PDI flows) are Bearer tokens, so DPoP applies only to tokens from an external authorization server.
* DPoP protects against a stolen token alone, not a captured token plus an unused proof. Use TLS on every hop.

### 2. Presentation During Issuance with DCQL

#### What it is

In Presentation During Issuance (PDI), the holder presents an existing credential before a new one is issued. Certify now describes this request with DCQL, as defined by OpenID4VP 1.0.

#### How it works

1. Certify reads the dcqlQuery block from the VP request configuration file (mosip.certify.vp-request.config-file-url).
2. The embedded Inji Verify library turns it into an OpenID4VP authorization request.
3. Certify returns the query as dcql\_query inside openid4vp\_request in the Interactive Authorization Response.
4. The wallet builds a vp\_token keyed by the credential query id, and posts it to /oauth/iae.
5. The embedded library verifies the vp\_token. Only vp\_token and state are required; there is no presentation\_submission.

#### Sample configuration

```json
{
  "dcqlQuery": {
    "credentials": [
      {
        "id": "mosip_verifiable_credential_id",
        "format": "ldp_vc",
        "meta": {
          "type_values": [[
            "https://www.w3.org/2018/credentials#VerifiableCredential",
            "https://inji.github.io/inji-config/contexts/mosip-identity-context.json#MOSIPVerifiableCredential"
          ]]
        }
      }
    ],
    "credential_sets": [
      { "options": [ [ "mosip_verifiable_credential_id" ] ] }
    ]
  }
}
```

| Field                            | Meaning                                                     |
| -------------------------------- | ----------------------------------------------------------- |
| credentials\[].id                | Unique ID the wallet echoes back in the vp\_token           |
| credentials\[].format            | ldp\_vc, dc+sd-jwt or mso\_mdoc                             |
| credentials\[].meta.type\_values | Format-specific type constraint                             |
| credential\_sets\[].options      | Alternative sets of credential IDs that satisfy the request |

#### Migration

Replace any presentation\_definition (PEX) block with a dcqlQuery. PEX is not supported.

### 3. Embedded Inji Verify Library

#### What it is

Certify now embeds Inji Verify's verify-core (1.0.0-rc.1) to build and verify presentations in the PDI flow. No separate Inji Verify service is called.

#### Benefits

* One less deployable and no network hop on the issuance path.
* Less TLS and configuration surface, and no verifier-unreachable failure mode.

#### How it works

Certify depends on the verify-core artifact and wires its beans into the application context. VerifiablePresentationRequestService builds the OpenID4VP request from the DCQL query, and VerifiablePresentationSubmissionService verifies the wallet's vp\_token.

#### Migration

Remove configuration that points PDI at an external Inji Verify service, and drop the unused Inji Verify database artifacts from your Certify deployment.

### 5. Credential Configuration: Validated Metadata

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
