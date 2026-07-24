# Version 1.0.0-alpha.1

**Release Version**: v1.0.0-alpha.1

**Release Type:** Developer Release

**Release Date:** <mark style="color:red;">**Coming Soon!**</mark>



{% hint style="success" %}
**Note**

Inji Certify **v1.0.0-alpha.1** marks our formal adoption of the [**OpenID4VCI 1.0 specification**](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html). This is an important milestone, and we want to provide clear guidance for all community members.

* **Upgrading is optional but recommended for spec compliance.** This release is intended for teams ready to align with the finalized OpenID4VCI 1.0 standard. Teams running implementations built on a pre-1.0 draft specification are not mandatory to upgrade — the earlier releases can be continued without any disruption.
* **For those upgrading to v1.0.0-alpha.1**, this release does **not maintain backward compatibility** with pre-1.0 draft implementations. APIs, credential formats, and endpoints that have been updated or replaced are listed below wherever required. Reviewing that section before upgrading is strongly recommended.
* **For those staying on the draft specification**, no action is needed. Older releases will continue to function as-is, with the option to upgrade at a time that suits your roadmap.
{% endhint %}

### Overview

Inji Certify **v1.0.0-alpha.1** delivers comprehensive alignment with the [OpenID4VCI 1.0](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html) specification and introduces critical enhancements to credential issuance workflows, interoperability, and system stability. This release focuses on modernizing the credential issuance architecture, removing draft implementations, and providing enhanced support for emerging credential formats.

**Key Changes:**

* OpenID4VCI 1.0 specification alignment (credential endpoint, well-known metadata, authorization flows)
* Pre-Authorized Code flow and Presentation During Issuance (PDI) enhancement to have OpenID4VCI 1.0 specification alignment
* Credential format transitions (**vc+sd-jwt** to **dc+sd-jwt**)
* Nonce endpoint and Interactive Authorization Request (IAR/IAE) alignment

#### Major Features & Enhancements

1. **Credential Issuance Endpoint Enhancement**\
   The credential issuance endpoint has been upgraded to full OpenID4VCI 1.0 compliance. Requests now require a mandatory credential\_configuration\_id field, and the format field is rejected in requests as per the specification. Array-based proof JWT validation is supported, and request/response structures have been updated accordingly. Validation mechanisms have been enhanced and error handling improved throughout the issuance flow.
2. **Issuer Well-Known Metadata Update**\
   The /.well-known/openid-credential-issuer endpoint response has been updated to reflect OpenID4VCI 1.0 adoption. The metadata now exposes the new nonce\_endpoint, includes updated claim display properties per the 1.0 schema, and externalizes metadata configuration for greater flexibility. The full response has been validated against the OpenID4VCI 1.0 specification.
3. **Nonce Endpoint Implementation**\
   A dedicated /nonce endpoint has been introduced for c\_nonce generation and replay attack prevention. Nonces are cryptographically generated with a configurable TTL-based expiration and stored in Redis with automatic expiry. During credential issuance, the nonce is validated and marked as used. As a result, c\_nonce has been removed from the access token response in line with the updated specification. \
   **Breaking Change:** Clients must now call the /nonce endpoint separately, as c\_nonce is no longer included in the token response.
4. **Replace Credential Format: vc+sd-jwt → dc+sd-jwt**\
   The vc+sd-jwt credential format has been replaced with the standardized dc+sd-jwt format as mandated by OpenID4VCI 1.0. \
   **Breaking Change:** The vc+sd-jwt format is no longer supported and all configurations must be updated.
5. **Pre-Authorized Credential Offer API Enhancement**\
   The /pre-authorized-data API has been upgraded to comply with the OpenID4VCI 1.0 specification. The credential\_configuration\_id is now validated against issuer metadata via /.well-known/openid-credential-issuer, and claims are validated against the structures defined in the credential configuration. Unknown or unsupported claims are rejected, while existing API logic outside the claims validation scope remains unchanged.
6. **Interactive Authorization Endpoint (IAR → IAE) & Presentation During Issuance**\
   The Interactive Authorization Request endpoint and Presentation During Issuance flow have been enhanced to align with OpenID4VCI 1.0. The endpoint has been renamed from iar to iae per the specification, with support added for the URN format urn:openid:dcp:iae:openid4vp\_presentation and updated response modes iae-post and iae-post.jwt. Residents can now present an existing Verifiable Credential to obtain another credential. \
   **Breaking Change:** The iar endpoint has been updated to use iae.

#### User Stories Released

<table><thead><tr><th width="228.7578125">Feature</th><th width="420.47265625">Description</th><th>Git Id</th></tr></thead><tbody><tr><td>Credential Issuance endpoint Enhancement</td><td>Enhancement of Credential Issuance Endpoint to Support OpenID4VCI 1.0 Features</td><td><a href="https://github.com/inji/inji-certify/issues/678">#678</a></td></tr><tr><td>Enhance pre-authorized credential offer API , claims validation</td><td>Enhance pre-authorized credential offer API , claims validation as per OpenID4VCI 1.0 issuer metadata response</td><td><a href="https://github.com/inji/inji-certify/issues/845">#845</a></td></tr><tr><td>Presentation During Issuance endpoint changes to support 1.0 Spec</td><td>Enhance Interactive Authorization (IAR) Endpoint to Support OpenID4VCI 1.0-Compliant Presentation During Issuance</td><td><a href="https://github.com/inji/inji-certify/issues/739">#739</a></td></tr><tr><td>Issuer Well-known metadata to adopt 1.0 OpenID4VCI changes</td><td>Update Credential Issuer Well-Known Metadata for OpenID4VCI 1.0 Adoption</td><td><a href="https://github.com/inji/inji-certify/issues/676">#676</a></td></tr><tr><td>Replace format vc+sd_jwt to dc_sd_jwt</td><td>Replace Credential Format from vc+sd-jwt to dc+sd-jwt for OpenID4VCI 1.0 Compliance</td><td><a href="https://github.com/inji/inji-certify/issues/677">#677</a></td></tr><tr><td>Nonce endpoint implementation</td><td>Implementation of nonce_endpoint for c_nonce generation and replay attack prevention</td><td><a href="https://github.com/inji/inji-certify/issues/675">#675</a></td></tr><tr><td>Integrate Inji Verify as embedded library in PDI flow</td><td>Integrate Inji Verify as an Embedded Library in the Presentation During Issuance Flow Instead of Calling It as a Separate Service</td><td><a href="https://github.com/inji/inji-certify/issues/902">#902</a></td></tr></tbody></table>

### Bug Fixes

The following bugs have been addressed in this release.

<table><thead><tr><th width="148.1171875">Bug ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-certify/issues/690">#690</a></td><td>Error message mismatch in mock -mdl use case</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/686">#686</a></td><td>Error messages mismatch in mdoc-mdl use case(PDI)</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/681">#681</a></td><td>Getting Canonicalization error when try to get VC intermittently</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/715">#715</a></td><td>"uri" field is mandatory if logo is present in issuer metadata</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/716">#716</a></td><td>nonce Should Be Optional in Verifiable Credential Issuance</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/863">#863</a></td><td>Not able to configure Vc issuance plugin for Mosipid use cases in release-0.14.x</td></tr></tbody></table>

### Known Issues

Below is the list of known issues related to the release v1.0.0-alpha.1. To access all open issues related to Inji Certify please click [here](https://github.com/orgs/inji/projects/1/views/8?visibleFields=%5B%22Title%22%2C273524858%2C%22Assignees%22%2C%22Status%22%2C%22Linked+pull+requests%22%2C%22Sub-issues+progress%22%2C354699068%5D\&filterQuery=label%3Abug+-status%3ADone+-status%3ATesting)

<table><thead><tr><th width="151.17578125">Issue ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-certify/issues/842">#842</a></td><td>Validations to add "qrSignatureAlgo" in credential config API</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/679">#679</a></td><td>Validations issues for qrsettings block in Credential config API</td></tr><tr><td><a href="https://github.com/inji/inji-certify/issues/878">#878</a></td><td>unknown_error returned for negative scenarios</td></tr></tbody></table>

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

### Repositories Released

Supported Platforms & Components

| Repository                                                                                           | Version        |
| ---------------------------------------------------------------------------------------------------- | -------------- |
| [inji-certify](https://github.com/inji/inji-certify/releases/tag/v0.15.0)                            | v1.0.0-alpha.1 |
| [inji-config](https://github.com/inji/inji-config/releases/tag/v0.15.0)                              | v1.0.0         |
| [keymanager](https://github.com/mosip/keymanager/releases/tag/v1.4.0)                                | v1.4.0         |
| [digital-credential-plugins](https://github.com/inji/digital-credential-plugins/releases/tag/v0.6.0) | v1.0.0-alpha.1 |

### Compatible Modules

| Modules               | Version                                                                         |
| --------------------- | ------------------------------------------------------------------------------- |
| eSignet               | 1.6.2                                                                           |
| IDA                   | 1.3.0                                                                           |
| Sunbird C             | [v2.0.0](https://github.com/Sunbird-RC/sunbird-rc-core/releases/tag/v2.0.0-rc3) |
| esignet-mock-services | [v0.11.2](https://github.com/mosip/esignet-mock-services/tree/v0.11.2)          |
| commons               | [1.6.0](https://github.com/mosip/commons/tree/v1.3.0)                           |
| mimoto                | 0.20.1                                                                          |
| inji-web              | 0.16.0                                                                          |

### Documentation

* Feature Documentation
* Local Setup
* API Documentation
* Test Report
