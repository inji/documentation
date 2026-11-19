# Presentation During Issuance with DCQL

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

{% hint style="info" %}
**Migration**:

Replace any presentation\_definition (PEX) block with a dcqlQuery. PEX is not supported.
{% endhint %}
