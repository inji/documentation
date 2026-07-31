# Transition from PEX to DCQL

## Transition from PEX to DCQL

Backward Compatibility & Presentation Definition to DCQL Migration Guide (v1.0.0-alpha.1)

## Part 1 — Backward Compatibility: DCQL vs. PEX

### Overview

As Inji Verify evolves to adopt **DCQL (Digital Credentials Query Language)** as its primary query protocol, older wallet implementations that only support **PEX (Presentation Exchange)** are no longer compatible with newer verifier versions.

This section defines the compatibility behavior, versioning strategy, and guidance for System Integrators (SIs) and end users — so there is no confusion about what works, what doesn't, and what to do about it.

> **Important:** There is no backward compatibility layer. No fallback from DCQL to PEX will be implemented in any verifier version.

### Background

| **Protocol**                              | **Description**                                                                                                              |
| ----------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| PEX (Presentation Exchange)               | Legacy query protocol (presentation\_definition) used in older wallets and in Inji Verify releases up to 0.18.x              |
| DCQL (Digital Credentials Query Language) | Modern credential query language defined by OpenID4VP 1.0 (final), adopted by Inji Verify from version 1.0.0-alpha.1 onwards |

These two protocols are not interoperable. A verifier built on DCQL cannot process a presentation from a wallet that only speaks PEX, and vice versa.

### Versioning Strategy

| **Inji Verify Version**           | **Supported Protocol**         | **Compatible Wallets**                  |
| --------------------------------- | ------------------------------ | --------------------------------------- |
| Up to 0.18.x (Legacy)             | PEX (presentation\_definition) | Wallets supporting PEX                  |
| 1.0.0-alpha.1 and later (Current) | DCQL (dcql\_query)             | Wallets supporting DCQL / OpenID4VP 1.0 |

* Newer verifier versions exclusively use DCQL for authorization requests and VP token validation.
* Older verifier versions support PEX and remain available for integrators who need legacy wallet support.
* There is no verifier version that supports both query protocols for new verification requests.
* **Result-fetch endpoints in the current version can still return results for both DCQL-based and legacy Presentation Definition submissions, so previously completed verifications remain readable.**

### Compatibility Matrix

| **Wallet Type**             | **Inji Verify ≤ 0.18.x (PEX)** | **Inji Verify 1.0.0-alpha.1+ (DCQL)** |
| --------------------------- | ------------------------------ | ------------------------------------- |
| Wallet supporting DCQL only | ❌ Does not work                | ✅ Works                               |
| Wallet supporting PEX only  | ✅ Works                        | ❌ Does not work                       |
| Wallet supporting both      | ✅ Works                        | ✅ Works                               |

### System Integrator (SI) Guidance

SIs must choose the verifier version based on the wallet ecosystem they intend to support:

#### Scenario A — Supporting Legacy Wallets

* **Use:** Inji Verify version ≤ 0.18.x (PEX-based)
* **When:** Your end users are on older wallets that have not yet migrated to DCQL
* **Trade-off:** You will not benefit from DCQL capabilities, OpenID4VP 1.0 alignment, or other features of newer verifier releases

#### Scenario B — Supporting Modern Wallets

* **Use:** Inji Verify 1.0.0-alpha.1 or later (DCQL-based)
* **When:** Your ecosystem is on modern wallets with DCQL / OpenID4VP 1.0 support
* **Trade-off:** End users on older PEX-only wallets will be unable to complete verification

#### Scenario C — Mixed Ecosystem (Transition Period)

**Recommended approach:** Run two separate verifier deployments — one PEX (legacy version), one DCQL (current version) — and route users based on wallet capability detection at the application layer.

Inji Verify itself does not perform this routing; the SI is responsible for the routing logic.

#### End-User Messaging

When a user with an incompatible (PEX-only) wallet attempts verification against a DCQL verifier, the flow will fail. SIs should surface a clear, actionable message to the end user.

**Recommended message template:**

```
"Your wallet version is not supported by this verifier.
 Please upgrade your wallet to the latest version to continue."
```

Additional guidance for SIs:

* Display this message as early as possible in the verification flow, ideally before the user attempts to share a presentation.
* Provide a link to wallet upgrade/download instructions where applicable.
* Do not surface raw protocol error codes to end users.

#### Migration Roadmap

| Phase      | Action                                                                                                 |
| ---------- | ------------------------------------------------------------------------------------------------------ |
| Short-term | Integrators on PEX continue using legacy Inji Verify versions (≤ 0.18.x)                               |
| Mid-term   | Wallet providers upgrade their wallets to support DCQL / OpenID4VP 1.0                                 |
| Long-term  | All integrators migrate to DCQL-based verifiers (1.0.0-alpha.1+); PEX-based versions reach end-of-life |

SIs are encouraged to plan wallet upgrade timelines in coordination with their wallet provider to minimize disruption to end users.

***

## Part 2 — Migrating Presentation Definition to DCQL Query

### Overview

As Inji Verify adopts DCQL as its primary query protocol, developers who have built integrations using Presentation Definitions (PD/PEX) need a clear, practical guide to migrate their existing queries to the DCQL format.

This section explains how each component of a Presentation Definition maps to its DCQL equivalent, with step-by-step guidance and real-world examples aligned to OpenID4VP 1.0 (final) and the structures accepted by the current Inji Verify verify-service.

### Understanding the Two Formats

#### Presentation Definition (PD / PEX)

Presentation Definitions are part of the DIF Presentation Exchange (PEX) specification. They describe what credentials a verifier requires using input\_descriptors, constraints, and fields.

**Core PD structure:**

```
{
  "presentation_definition": {
    "id": "example-pd",
    "input_descriptors": [
      {
        "id": "id_credential",
        "name": "National ID",
        "purpose": "Age verification",
        "constraints": {
          "fields": [
            {
              "path": ["$.credentialSubject.dateOfBirth"],
              "filter": { "type": "string" }
            }
          ]
        }
      }
    ]
  }
}
```

#### DCQL Query

DCQL is the credential query language defined in OpenID4VP 1.0. It uses a credentials array with claims entries to express the same requirements more concisely, plus optional claim\_sets and credential\_sets for alternatives.

**Core DCQL structure:**

```
{
  "dcql_query": {
    "credentials": [
      {
        "id": "id_credential",
        "format": "dc+sd-jwt",
        "meta": {
          "vct_values": ["national_id_credential"]
        },
        "claims": [
          { "path": ["dateOfBirth"] }
        ]
      }
    ]
  }
}
```

> **Note:** in the Inji Verify create-verification-request API the query is passed as the dcqlQuery field of the request body; the wire-level authorization request carries it as dcql\_query per OpenID4VP.

### Component Mapping Reference

| PD Component                                             | DCQL Equivalent                                         | Notes                                                              |
| -------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------------------ |
| presentation\_definition.id                              | dcql\_query (root object)                               | No direct ID at query level                                        |
| input\_descriptors\[]                                    | credentials\[]                                          | One-to-one mapping                                                 |
| input\_descriptor.id                                     | credential.id                                           | Same purpose; referenced by credential\_sets                       |
| input\_descriptor.name                                   | Not required                                            | Informational only in PD                                           |
| input\_descriptor.purpose                                | Not required                                            | Use in UI/UX layer instead                                         |
| format (PD level)                                        | credential.format                                       | Per-credential; e.g. dc+sd-jwt, ldp\_vc, mso\_mdoc                 |
| Credential type filter ($.type / $.vct field constraint) | meta.type\_values (ldp\_vc) / meta.vct\_values (sd-jwt) | Type matching moves out of claims into meta                        |
| constraints.fields\[].path                               | claims\[].path                                          | JSONPath string → path array                                       |
| constraints.fields\[].filter                             | claims\[].values                                        | Value-matching logic moves to values                               |
| constraints.fields\[].optional                           | claim\_sets                                             | Alternative claim combinations, in order of preference             |
| submission\_requirements                                 | credential\_sets with options                           | Alternatives across credentials; required: false for optional sets |
| constraints.limit\_disclosure                            | Implied by format                                       | Selective disclosure handled by dc+sd-jwt                          |
| Holder binding checks                                    | require\_cryptographic\_holder\_binding                 | Replaces the earlier acceptVPWithoutHolderProof configuration      |

### Step-by-Step Migration Process

**Step 1 — Inventory Your Presentation Definition**

* List all input\_descriptors in your existing PD
* Note each descriptor's id, name, purpose, and constraints
* Identify the credential format (e.g., ldp\_vc, jwt\_vc\_json, SD-JWT VC)

**Step 2 — Map Each Input Descriptor to a DCQL Credential**

* Each input\_descriptor becomes one entry in the credentials\[] array
* Carry over the id
* Set the format at the credential level — use dc+sd-jwt for SD-JWT VCs (the OpenID4VP 1.0 identifier; older drafts used vc+sd-jwt)

**Step 3 — Move Credential Type Matching into meta**

* PD constraints on $.type (W3C VC) become meta.type\_values — an array of arrays of type IRIs (full URIs after JSON-LD expansion; types not defined in any @context remain as-is and are accepted as relative IRIs)
* PD constraints on $.vct (SD-JWT VC) become meta.vct\_values — matched exactly against the credential's vct claim (type inheritance is not currently supported)
* The meta/format pairing is enforced by the verifier: vct\_values is only valid with SD-JWT formats and type\_values only with ldp\_vc; the wrong combination is rejected at request creation (DCQL\_META\_NOT\_MATCHING\_FORMAT)

**Step 4 — Convert Field Paths**

* PD uses JSONPath syntax: $.credentialSubject.dateOfBirth
* DCQL uses a path array of components: \["dateOfBirth"] (relative to the claims of the credential)
* Remove the $.credentialSubject. prefix; each nesting level becomes its own array element
* Array selectors: use an integer index for one element (\["fullName", 0, "value"]) or null for all elements (\["gender", null, "value"])

**Step 5 — Convert Field Filters**

* PD filter objects (JSON Schema) → DCQL values array (allowed values list)
* If the PD filter only checks type ("type": "string"), the DCQL claims entry needs only a path — no values required
* filter.const: "x" → values: \["x"]; filter.enum: \[...] → values: \[...]

**Step 6 — Handle Optionality and Alternatives**

* Optional fields within one credential → give claims an id and express alternatives with claim\_sets (listed in order of preference)
* submission\_requirements across credentials → credential\_sets with options (each option is a list of credential ids that together satisfy the request)
* Purely optional credential sets → required: false on the credential set

**Step 7 — Validate**

* Create a verification request with the DCQL query against a DCQL-compatible verifier (Inji Verify 1.0.0-alpha.1+)
* Confirm the wallet returns the expected claims in the vp\_token
* Verify semantic equivalence with the original PD before deprecating the PD-based flow

### Migration Examples

#### Example 1 — Simple Age Verification (Single Field)

**Before (PD):**

```
{
  "presentation_definition": {
    "id": "age-check",
    "input_descriptors": [
      {
        "id": "age_credential",
        "constraints": {
          "fields": [
            { "path": ["$.credentialSubject.dateOfBirth"] }
          ]
        }
      }
    ]
  }
}
```

**After (DCQL):**

```
{
  "dcql_query": {
    "credentials": [
      {
        "id": "age_credential",
        "format": "dc+sd-jwt",
        "meta": { "vct_values": ["identity_credential"] },
        "claims": [
          { "path": ["dateOfBirth"] }
        ]
      }
    ]
  }
}
```

### Example 2 — Identity Verification (Multiple Fields, W3C VC)

**Before (PD):**

```
{
  "presentation_definition": {
    "id": "identity-check",
    "input_descriptors": [
      {
        "id": "id_credential",
        "format": { "ldp_vc": { "proof_type": ["Ed25519Signature2020"] } },
        "constraints": {
          "fields": [
            { "path": ["$.type"],
              "filter": { "type": "array",
                          "contains": { "const": "MOSIPVerifiableCredential" } } },
            { "path": ["$.credentialSubject.firstName"] },
            { "path": ["$.credentialSubject.lastName"] },
            { "path": ["$.credentialSubject.nationalId"] }
          ]
        }
      }
    ]
  }
}
```

**After (DCQL):**

```
{
  "dcql_query": {
    "credentials": [
      {
        "id": "id_credential",
        "format": "ldp_vc",
        "meta": {
          "type_values": [
            [
              "https://www.w3.org/2018/credentials#VerifiableCredential",
              "https://example.org/credentials#MOSIPVerifiableCredential"
            ]
          ]
        },
        "claims": [
          { "path": ["firstName"] },
          { "path": ["lastName"] },
          { "path": ["nationalId"] }
        ]
      }
    ]
  }
}
```

> **Note:** type\_values uses full type URIs (each inner array is one acceptable combination of types). The Verify UI also uses type\_values to match submitted credentials when multiple verifier configurations share the same credential type.

#### Example 3 — Multi-Credential Request with Value Filter and Alternatives (Complex)

**Before (PD):**

```
{
  "presentation_definition": {
    "id": "insurance-check",
    "input_descriptors": [
      {
        "id": "id_doc",
        "constraints": {
          "fields": [
            { "path": ["$.credentialSubject.dateOfBirth"] }
          ]
        }
      },
      {
        "id": "insurance_doc",
        "constraints": {
          "fields": [
            { "path": ["$.credentialSubject.policyNumber"] },
            { "path": ["$.credentialSubject.policyStatus"],
              "filter": { "type": "string", "const": "active" } }
          ]
        }
      }
    ],
    "submission_requirements": [
      { "rule": "pick", "count": 1, "from": "A" }
    ]
  }
}
```

**After (DCQL):**

```
{
  "dcql_query": {
    "credentials": [
      {
        "id": "id_doc",
        "format": "dc+sd-jwt",
        "meta": { "vct_values": ["identity_credential"] },
        "claims": [
          { "path": ["dateOfBirth"] }
        ]
      },
      {
        "id": "insurance_doc",
        "format": "dc+sd-jwt",
        "meta": { "vct_values": ["insurance_credential"] },
        "claims": [
          { "id": "policy_number", "path": ["policyNumber"] },
          { "id": "policy_status", "path": ["policyStatus"],
            "values": ["active"] }
        ],
        "claim_sets": [
          ["policy_number", "policy_status"],
          ["policy_number"]
        ]
      }
    ],
    "credential_sets": [
      { "options": [ ["id_doc"], ["insurance_doc"] ] }
    ]
  }
}
```

Here claim\_sets lists acceptable claim combinations in order of preference, and credential\_sets.options expresses that presenting either credential satisfies the request — the DCQL equivalent of a PEX pick submission requirement.

### Edge Cases & Handling

| Scenario                    | PD Behavior                                              | DCQL Handling                                                                                     |
| --------------------------- | -------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Optional fields             | optional: true on field constraint                       | Give claims an id and use claim\_sets to list acceptable combinations; or omit the claim entirely |
| Nested claims               | $.credentialSubject.address.city                         | \["address", "city"] — each level is a separate array element                                     |
| Array element (specific)    | $.credentialSubject.fullName\[0].value                   | \["fullName", 0, "value"] — integer index selects one element                                     |
| Array element (any/all)     | JSONPath wildcard \[\*]                                  | \["gender", null, "value"] — null selects all elements                                            |
| Enum / allowed values       | filter.enum: \["active", "valid"]                        | values: \["active", "valid"]                                                                      |
| Constant value match        | filter.const: "active"                                   | values: \["active"]                                                                               |
| Credential type matching    | Field constraint on $.type or $.vct                      | meta.type\_values (ldp\_vc) or meta.vct\_values (dc+sd-jwt)                                       |
| Multiple credential formats | format at PD level                                       | format per credential in credentials\[]                                                           |
| Selective disclosure        | limit\_disclosure: "required"                            | Use dc+sd-jwt format — disclosure handled by the format itself                                    |
| Holder binding              | Verifier-side configuration (acceptVPWithoutHolderProof) | require\_cryptographic\_holder\_binding parameter, supported for SD-JWT VC and LDP\_VC            |

### Best Practices

* **Maintain semantic equivalence** — always verify the DCQL query returns the same claims as the original PD before deprecating PD-based flows
* **Use the correct format identifiers** — dc+sd-jwt is the OpenID4VP 1.0 identifier for SD-JWT VCs; vc+sd-jwt appears only in older draft-based integrations
* **Always constrain credential type via** meta — set vct\_values or type\_values so wallets match the intended credential, not just any credential with similar claims
* **Keep claim paths minimal** — only request claims strictly required for the verification use case; over-requesting reduces user trust
* **Test with real wallets** — validate DCQL queries against actual wallet implementations, not just spec compliance
* **Version your queries** — tag DCQL queries with a version identifier for traceability across deployments
* **Document the migration** — record the original PD and its DCQL equivalent in your integration documentation for audit purposes

**3. Points to Note**

* No fallback implementation from DCQL to PEX
* No dual-protocol support for new verification requests within a single verifier version
* No automatic wallet version detection within Inji Verify
* No Automated PD-to-DCQL conversion tooling

