# Version 1.0.0-alpha.1

**Release Version**: v1.0.0-alpha.1

**Release Type:** Developer Release

**Release Date:** Coming Soon!

**Note**

Inji Certify **v1.0.0-alpha.1** marks our formal adoption of the [**OpenID4VCI 1.0 specification**](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html). This is an important milestone, and we want to provide clear guidance for all community members.

**Upgrading is optional but recommended for spec compliance.** This release is intended for teams ready to align with the finalized OpenID4VCI 1.0 standard. Teams running implementations built on a pre-1.0 draft specification are not mandatory to upgrade — the earlier releases can be continued without any disruption.

**For those upgrading to v1.0.0-alpha.1**, this release does **not maintain backward compatibility** with pre-1.0 draft implementations. APIs, credential formats, and endpoints that have been updated or replaced are listed below wherever required. Reviewing that section before upgrading is strongly recommended.

**For those staying on the draft specification**, no action is needed. Older releases will continue to function as-is, with the option to upgrade at a time that suits your roadmap.

#### Overview

Inji Certify **v1.0.0-alpha.1** delivers comprehensive alignment with the OpenID4VCI 1.0 specification and introduces critical enhancements to credential issuance workflows, interoperability, and system stability. This release focuses on modernizing the credential issuance architecture, removing draft implementations, and providing enhanced support for emerging credential formats

**Key Changes:**

* OpenID4VCI 1.0 specification alignment (credential endpoint, well-known metadata, authorization flows)
* Pre-Authorized Code flow and Presentation During Issuance (PDI) enhancement to have OpenID4VCI 1.0 specification alignment
* Credential format transitions (vc+sd-jwt to dc+sd-jwt)
* Nonce endpoint and Interactive Authorization Request (IAR/IAE) alignment

#### Major Features & Enhancements

1. **Credential Issuance Endpoint Enhancement**\
   The credential issuance endpoint has been upgraded to full OpenID4VCI 1.0 compliance. Requests now require a mandatory credential\_configuration\_id field, and the format field is rejected in requests as per the specification. Array-based proof JWT validation is supported, and request/response structures have been updated accordingly. Validation mechanisms have been enhanced and error handling improved throughout the issuance flow.
2. **Issuer Well-Known Metadata Update**\
   The /.well-known/openid-credential-issuer endpoint response has been updated to reflect OpenID4VCI 1.0 adoption. The metadata now exposes the new nonce\_endpoint, includes updated claim display properties per the 1.0 schema, and externalizes metadata configuration for greater flexibility. The full response has been validated against the OpenID4VCI 1.0 specification.
3. **Nonce Endpoint Implementation**\
   A dedicated /nonce endpoint has been introduced for c\_nonce generation and replay attack prevention. Nonces are cryptographically generated with a configurable TTL-based expiration and stored in Redis with automatic expiry. During credential issuance, the nonce is validated and marked as used. As a result, c\_nonce has been removed from the access token response in line with the updated specification. **Breaking Change:** Clients must now call the /nonce endpoint separately, as c\_nonce is no longer included in the token response.
4. **Replace Credential Format: vc+sd-jwt → dc+sd-jwt**\
   The vc+sd-jwt credential format has been replaced with the standardized dc+sd-jwt format as mandated by OpenID4VCI 1.0. **Breaking Change:** The vc+sd-jwt format is no longer supported and all configurations must be updated.
5. **Pre-Authorized Credential Offer API Enhancement**\
   The /pre-authorized-data API has been upgraded to comply with the OpenID4VCI 1.0 specification. The credential\_configuration\_id is now validated against issuer metadata via /.well-known/openid-credential-issuer, and claims are validated against the structures defined in the credential configuration. Unknown or unsupported claims are rejected, while existing API logic outside the claims validation scope remains unchanged.
6. **Interactive Authorization Endpoint (IAR → IAE) & Presentation During Issuance**\
   The Interactive Authorization Request endpoint and Presentation During Issuance flow have been enhanced to align with OpenID4VCI 1.0. The endpoint has been renamed from iar to iae per the specification, with support added for the URN format urn:openid:dcp:iae:openid4vp\_presentation and updated response modes iae-post and iae-post.jwt. Residents can now present an existing Verifiable Credential to obtain another credential. **Breaking Change:** The iar endpoint has been updated to use iae.

#### User Stories Released

| **Feature**                                                       | **Description**                                                                                                                   | **Git Id**                                              |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| Credential Issuance endpoint Enhancement                          | Enhancement of Credential Issuance Endpoint to Support OpenID4VCI 1.0 Features                                                    | [#678](https://github.com/inji/inji-certify/issues/678) |
| Enhance pre-authorized credential offer API , claims validation   | Enhance pre-authorized credential offer API , claims validation as per OpenID4VCI 1.0 issuer metadata response                    | [#845](https://github.com/inji/inji-certify/issues/845) |
| Presentation During Issuance endpoint changes to support 1.0 Spec | Enhance Interactive Authorization (IAR) Endpoint to Support OpenID4VCI 1.0-Compliant Presentation During Issuance                 | [#739](https://github.com/inji/inji-certify/issues/739) |
| Issuer Well-known metadata to adopt 1.0 OpenID4VCI changes        | Update Credential Issuer Well-Known Metadata for OpenID4VCI 1.0 Adoption                                                          | [#676](https://github.com/inji/inji-certify/issues/676) |
| Replace format vc+sd\_jwt to dc\_sd\_jwt                          | Replace Credential Format from vc+sd-jwt to dc+sd-jwt for OpenID4VCI 1.0 Compliance                                               | [#677](https://github.com/inji/inji-certify/issues/677) |
| Nonce endpoint implementation                                     | Implementation of nonce\_endpoint for c\_nonce generation and replay attack prevention                                            | [#675](https://github.com/inji/inji-certify/issues/675) |
| Integrate Inji Verify as embedded library in PDI flow             | Integrate Inji Verify as an Embedded Library in the Presentation During Issuance Flow Instead of Calling It as a Separate Service | [#902](https://github.com/inji/inji-certify/issues/902) |

#### The following bugs have been addressed in this release:

| **Git Id**                                              | **Description**                                                                  |
| ------------------------------------------------------- | -------------------------------------------------------------------------------- |
| [#690](https://github.com/inji/inji-certify/issues/690) | Error message mismatch in mock -mdl use case                                     |
| [#686](https://github.com/inji/inji-certify/issues/686) | Error messages mismatch in mdoc-mdl use case(PDI)                                |
| [#681](https://github.com/inji/inji-certify/issues/681) | Getting Canonicalization error when try to get VC intermittently                 |
| [#715](https://github.com/inji/inji-certify/issues/715) | "uri" field is mandatory if logo is present in issuer metadata                   |
| [#716](https://github.com/inji/inji-certify/issues/716) | nonce Should Be Optional in Verifiable Credential Issuance                       |
| [#863](https://github.com/inji/inji-certify/issues/863) | Not able to configure Vc issuance plugin for Mosipid use cases in release-0.14.x |

#### Known Issues

Below is the list of known issues related to the release v1.0.0-alpha.1. To access all open issues related to Inji Certify please click [here](https://github.com/orgs/inji/projects/1/views/8?visibleFields=%5B%22Title%22%2C273524858%2C%22Assignees%22%2C%22Status%22%2C%22Linked+pull+requests%22%2C%22Sub-issues+progress%22%2C354699068%5D\&filterQuery=label%3Abug+-status%3ADone+-status%3ATesting)

| **Git Id**                                              | **Description**                                                  |
| ------------------------------------------------------- | ---------------------------------------------------------------- |
| [#842](https://github.com/inji/inji-certify/issues/842) | Validations to add "qrSignatureAlgo" in credential config API    |
| [#679](https://github.com/inji/inji-certify/issues/679) | Validations issues for qrsettings block in Credential config API |
| [#878](https://github.com/inji/inji-certify/issues/878) | unknown\_error returned for negative scenarios                   |

***

### Breaking Changes

#### Replaced APIs & Formats

1. vc+sd-jwt format - replaced by dc+sd-jwt
   * **Required Action:** Update credential configurations to use dc+sd-jwt format
   * **Impact:** Clients must upgrade configuration or credential issuance will fail
2. iar endpoint - replaced by iae
   * **Required Action:** Update IAR request endpoints to use iae (per OpenID4VCI 1.0 spec)
   * **Impact:** Requests to iar endpoint will be rejected
3. c\_nonce in access token response - Removed
   * **Required Action:** Clients must now call /nonce endpoint to retrieve c\_nonce
   * **Impact:** Access token responses no longer include c\_nonce; separate endpoint call required

***

### Supported Platforms & Components

#### Repositories Released

| Repository                                                                                           | Version        | Release Date |
| ---------------------------------------------------------------------------------------------------- | -------------- | ------------ |
| [inji-certify](https://github.com/inji/inji-certify/releases/tag/v0.15.0)                            | v1.0.0-alpha.1 | July 2026    |
| [inji-config](https://github.com/inji/inji-config/releases/tag/v0.15.0)                              | v1.0.0         | July 2026    |
| [keymanager](https://github.com/mosip/keymanager/releases/tag/v1.4.0)                                | v1.4.0         | –            |
| [digital-credential-plugins](https://github.com/inji/digital-credential-plugins/releases/tag/v0.6.0) | v1.0.0-alpha.1 | –            |

### Compatible Modules

| **Modules**           | **Version**                                                                     |
| --------------------- | ------------------------------------------------------------------------------- |
| eSignet               | 1.6.2                                                                           |
| IDA                   | 1.3.0                                                                           |
| Sunbird C             | [v2.0.0](https://github.com/Sunbird-RC/sunbird-rc-core/releases/tag/v2.0.0-rc3) |
| esignet-mock-services | [v0.11.2](https://github.com/mosip/esignet-mock-services/tree/v0.11.2)          |
| commons               | [1.6.0](https://github.com/mosip/commons/tree/v1.3.0)                           |
| mimoto                | [0.20.](https://github.com/inji/mimoto/releases)1                               |
| inji-web              | [0.1](https://github.com/inji/inji-web/releases/tag/v0.15.0)6.0                 |

### Documentation

* Feature Documentation
* Local Setup
* API Documentation
* Test Report
