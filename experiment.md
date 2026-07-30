---
hidden: true
---

# Experiment

## Experiment



***



## Inji Verify — Transition from PEX to DCQL

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



***



## Features Page Conten - To review

### DCQL Support

The entire verification flow — authorization requests, VP token submission, validation, and result processing — now uses **DCQL (Digital Credentials Query Language)** in place of Presentation Exchange (presentation\_definition). Only the result-fetch endpoints retain backward compatibility with legacy Presentation Definition submissions.

* **Cryptographic Holder Binding** — DCQL's require\_cryptographic\_holder\_binding governs holder proof for both SD-JWT VC and LDP\_VC submissions, replacing acceptVPWithoutHolderProof.
* **Expanded SD-JWT Support** — Both vc+sd-jwt and dc+sd-jwt formats are accepted.
* **Replay Attack Prevention** — KB-JWT nonce and aud claims are validated for SD-JWT submissions, so a presentation cannot be reused across sessions.
* **Server-Side Request Integrity** — VP request expiry and duplicate submissions are enforced server-side and reported back to wallets.
* **Protocol Compliance** — vp\_formats\_supported replaces vp\_formats; client\_id prefix moves from did: to decentralized\_identifier:; client\_metadata is rejected for pre-registered clients.
* **Verify UI Enhancements** — Submitted credentials are matched via DCQL type\_values, keeping matching accurate when multiple verifier configurations share a credential type.

### API Redesign:

Key APIs now return verification _evidence_, not just a final status.

* /vc-verification — Still returns the compact SUCCESS / INVALID / EXPIRED / REVOKED outcome, now with formally defined Content-Type headers per format, a 415 for unsupported media types, and structured internal-error bodies (e.g. STATUS\_RETRIEVAL\_ERROR).
* /v2/vc-verification — Returns a per-check breakdown: allChecksSuccessful plus schemaAndSignatureCheck, expiryCheck, per-purpose statusCheck entries, and optional claims — each failure carrying a structured error code/message.
* /vp-result/{txnId} — Enhanced to return per-credential results instead of one aggregated status, and remains backward compatible with both DCQL and legacy Presentation Definition submissions.
* /v2/vp-results/{txnId} — Structured result for the presentation and each credential within it, including holderProofCheck: for SD-JWT, KB-JWT nonce/aud are verified against the Authorization Request; for JSON-LD, the VP signature is verified.
* /vp-session-results — The cookie-based endpoint shares the same rich body as /v2/vp-results/{txnId} and gains a full error model (401 VP\_SESSION\_INVALID, MALFORMED\_COOKIE, RESPONSE\_CODE\_NOT\_USED); the session cookie is cleared after processing.

### New /v2 Endpoints

The request and submission flow is re-versioned for OpenID4VP 1.0 (final) and SD-JWT VC draft-10; the /v2 endpoints are **not backward compatible**.

* /v2/vp-request — Requires dcql\_query. Supports pre-registered clients (request by value) and decentralized\_identifier: clients (request by reference via requestUri). Caller nonce must be ≥ 16 URL-safe characters, else a secure nonce (≥ 128 bits) is generated. Granular validation errors cover request parsing and the full DCQL structure.
* /v2/vp-session-request — Same contract as /v2/vp-request, plus a base64-encoded transaction\_id HttpOnly cookie (15-minute lifetime) for session flows.
* /v2/vp-request/{requestId} — Serves the Authorization Request as a signed JWT (application/oauth-authz-req+jwt) for by-reference flows.
* /v2/vp-submission/direct-post — vp\_token is a JSON object keyed by DCQL query\_id (arrays of presentations); presentation\_submission is no longer accepted. The full DCQL validation suite runs all-or-nothing before cryptographic verification, alongside state, nonce, and client-id/aud checks; duplicate and expired submissions are rejected. Wallet errors are reported via error/error\_description.

### DCQL Query Capabilities

* **Per-query holder binding** — require\_cryptographic\_holder\_binding (default true); outcome surfaces as holderProofCheck in results.
* **Type constraints** — meta.type\_values for ldp\_vc (OR-of-ANDs, IRI fragment matching); meta.vct\_values for SD-JWT (exact match).
* **Claim-level requests** — claims paths with optional expected values; claim\_sets for acceptable combinations.
* **Credential combinations** — credential\_sets (OR across options, AND within); optional sets via required: false.
* **Multiplicity** — multiple (default false) allows more than one presentation per query.

### Standardized Error Responses

All endpoints return typed error bodies: ErrorResponse (errorCode + errorMessage) for 4xx and InternalErrorResponse (timestamp, status, path, error) for 500, with complete per-endpoint error-code tables published in the [API documentation](https://mosip.stoplight.io/docs/inji-verify/67445477d332e-open-id-4-vp-verifier-api-inji-verify).

### Removed

* **PEX** — presentationDefinition / presentationDefinitionId rejected; /vp-definition/{id} removed.
* acceptVPWithoutHolderProof — replaced by require\_cryptographic\_holder\_binding.
* presentation\_submission — the flow is DCQL-only.
* **Legacy paths** — /vp-request, /vp-session-request, /vp-request/{requestId}, /vp-submission/direct-post replaced by /v2 counterparts.





***







***

## Older content - (Purge after revisit)

### Template

### Installation template guide

> Thank you for downloading this template from The Good Docs Project! Before using the template, read this template guide for information about how to complete each section. Want to explore more templates? Check them out in our [templates GitLab repository](https://gitlab.com/tgdp/templates).

#### Introduction

An installation guide covers all the steps necessary to install the product and set it up for further use. You need an installation guide to install:

* Operating systems, applications, plugins, and extensions.
* SaaS (Software as a Service) applications.
* Open source software (OSS) product documentation.
* Hardware device product documentation.

There are two categories of an installation guide:

* **Standalone**: An independent installation guide document or page that includes all the necessary information required to install the software or application, including system requirements and step-by-step instructions.
* **Integrated**: An installation guide document or page integrated inside an existing README document.

#### Identify your audience

An installation guide is for users who have the sufficient technical expertise required to understand the installation instructions provided. If your proposed audience requires some technical expertise to install the product, you should highlight and list these requirements in the prerequisites section of the document.

#### Why do you need an installation guide?

An installation guide can:

* Help a user get started using your product.
* Reduce the number of support requests related to installation issues.
* Establish consistency in the existing developer experience.
* Ensure increased retention of a user who explores your product.
* Confirm a user has everything they need to configure, customize, and/or upgrade your product.

Installation guides are often confused with how-to guides. It is essential to distinguish between an installation guide and a how-to guide document. ​ An installation guide shows how to install the product (as a procedure), while a "how-to" topic shows how to do something with the product after it's been installed. The difference lies in the purpose of the instructions. An installation guide describes the process of setting up and configuring a specific software, application, or service. A how-to guide describes how to accomplish a particular task using a specific product or technology (which would already be installed). ​ The key differences are listed in the following table:

|          | **installation guide**                                                                                                                                                                                                                                                                                                                                                                          | **how-to guide**                                                                                                                                                                                                                                               |
| -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Audience | Systems administrators and users who require detailed instructions and technical details when setting-up and installing a software product.                                                                                                                                                                                                                                                     | Users with a less technical background who want to set-up and install a software product.                                                                                                                                                                      |
| Scope    | An installation guide provides specific instructions on how to install and set up a particular software product.                                                                                                                                                                                                                                                                                | A how-to guide takes the user through a series of steps required to perform a specific task to solve a particular problem.                                                                                                                                     |
| Format   | An installation guide is a prerequisite document a user reads before considering How-to Guides; because you need the product itself installed before you solve any problem related to that product. Due to the broad scope and availability of different variables and conditions in which an installation guide would function, an installation guide should be independent of a how-to guide. | how-to guide (or even a Tutorial) may include installation steps of the software or an application that needs to be installed as part of the How-to solution process. A hyperlink within the how-to guide would link back to the dedicated installation guide. |

#### Before writing an installation guide

Before you start working on your installation guide, identify the following:

* The target user who needs to follow your installation guide. This helps determine the appropriate level of information.
* The specific version of the software or application to be installed and the system requirements for installation.
* Software prerequisites or libraries dependencies.
* Installation options such as following an installation wizard or customized installation.
* Identify common issues that may arise during the installation process, and provide troubleshooting tips to help users overcome these issues.

#### Writing the installation guide

This section provides details about writing the installation guide.

**About the "Introduction" section**

In this section, state the purpose of the installation guide. Optionally, you can specify the benefits of this installation such as increased performance, better system stability, and enhanced security. ​ Optional: add a link to a demo of the installed product or a sandbox to try out the product.

**About the "Installation types" section**

In this section, explain what is included within the installation guide. This can include a list of different versions to be installed as an option. Make sure you highlight the differences between the installation scenarios. These can be outlined in a table with columns indicating the name of the installation type, a description of the installation type, and a link to the relevant installation steps within the guide.

If your product can be used in different environments, include a table specifying the different installation types. This table can help users choose the relevant installation type based on their needs. For example, you can classify the installation type based on:

* Main or lite version when a product has installable options with different functionalities.
* Operating system types such as installation for Windows, Linux, and MacOS.
* Cloud providers for products that require self-hosting to work such as CodeSpaces, CodeSandBox, and GitPod.

Add an introductory sentence to the table. Also, include links for all the available options. |

**About the "Overview" section**

In this section, explain the intended result of the installation, such as the commands, command aliases, major flags, available plugins, files downloaded, or application programs.

Also, include a sequential end-to-end summary of the installation process that can serve as a quick link or reference section for users. Consider displaying this information in a table with one column summarizing the specific process and a second column linking to a relevant document. ​ Optionally, you can include links to previous versions, if applicable. Consider formatting this list of versions in a table.

**About the "System requirements" section**

In this section, explain the different installation types and subsequent requirements for each type. This section leads into the next section on specific prerequisites.

Based on your use case, you can adjust the structure of this section by using it in reverse order. For example, you could list the installation type as the heading and system requirements for that type as a sub-section. For example, "Install on Linux > System Requirements" and "Install on Windows > System Requirements", instead of "System Requirements > Install on Linux > Install on Windows."

**About the "Before you begin" section**

In this section, explain the prerequisites. Prerequisites tell the user what they require to accomplish a goal, such as:

* Necessary dependencies or packages.
* Required version for your system or other system requirements.
* Specialist knowledge or skills.

**About the "Installation steps" section**

​In this section, describe what the user needs to do to install the software. When writing this section:

* Use numeric steps.
* Categorize the steps into subheadings, as required.
* Create subheadings based on the complexity of the installation.
* Add a one-sentence description of the step.
* Start each step with an active verb such as "open" and "download".
* Explain the expected result after completing each step.
* Include checks for success if each step is done correctly and/or tips if the installation didn't work at each step.
* Mention installation options where required, but mention which path is recommended.
* Add visuals (GIFs, images, or videos) where required.
* Add code block examples and snippets where required.

**About the "Verify installation" section**

In this section, include test commands, intended outputs, or other steps to confirm the installation was successful.

**About the "Post installation" section**

In this section, provide an overview of options once the installation is completed. Include links to other relevant resources if available.

**About the "Configuration options" section**

In this section, provide information regarding post-installation configuration options. Describe the requirements for configuring the installed product. Provide links to other resources if available.

**About the "Upgrade options" section**

In this section, provide information about upgrade options (also known as an update options), if relevant. Describe how to install updates from a range of possible options. Provide a link to available updates with specific version numbers, release dates, and key features.

**About the "Downgrade options" section**

In this section, provide downgrade options, if supported.

**About the "Uninstallation options" section**

In this section, clearly describe the procedure to uninstall the product.

**About the "Troubleshooting" section**

In this section, list a number of anticipated problems and associated solutions. This section helps solve problems encountered during installation. Start with a problem statement, then indicate the cause and provide a solution. Include any important additional information, such as restarting the computer.

You can also include steps or contact information for additional support.

**About the "Next steps" section**

In this section, include essential or recommended steps to take after installing the product. Provide links to further resources, if available. Also, include support/contact information for issue reports and feedback.

**About the "Product version history" section**

​In this section, you can list previous versions in a table, providing the version number and whether the version was major, minor, or a patch release. Always ensure the change history is consistent across the documentation. Refer to [semver.org](https://semver.org) to learn about the semantic versioning specification.

**About the "Definition of terms" section**

This section is optional. Provide a glossary table describing the terms, acronyms, and abbreviations used in the installation guide.

***

> Explore other templates from [The Good Docs Project](https://thegooddocsproject.dev/). Use our [feedback form](https://thegooddocsproject.dev/feedback/?template=Installation%20guide%20guide) to give feedback on this template.
