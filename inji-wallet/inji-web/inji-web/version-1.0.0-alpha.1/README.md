# Version 1.0.0-alpha.1

**Release Name:** Inji Web Wallet 1.0.0-alpha.1

**Release Type:** Alpha

**Release Date:** 13th August, 2026

### Overview

This release of **Inji Web Wallet v1.0.0-alpha.1** introduces the foundational support for [**OpenID4VP 1.0**](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html), including **DCQL-based credential selection and data share support**, along with compatibility updates required for [**OpenID4VCI 1.0**](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html).

The release focuses on upgrading the Web Wallet from the earlier OpenID4VCI Draft 13 and OpenID4VP Draft 23 implementations towards the finalized **1.0 specifications**, while improving interoperability with Inji Verify and strengthening credential download, presentation, and sharing flows.

This is an **alpha release** intended primarily for developer and interoperability validation. Some OpenID4VP 1.0 and DCQL capabilities remain under active development.

### Key Highlights

#### 1. OpenID4VCI 1.0 Support

* Added support for the **OpenID4VCI 1.0 Well-Known format** required for discovering issuer metadata.
* Added VC download support aligned with the **OpenID4VCI 1.0** implementation.
* Refactored the credential download flow to support the updated VCI 1.0 architecture.
* Completed the OpenID4VCI 1.0 specification upgrade analysis and implementation groundwork.

#### 2. OpenID4VP 1.0 and DCQL Support

* Added backend support in **Mimoto** for **DCQL-based OpenID4VP 1.0 flows**.
* Added DCQL support as part of the **Data Share** flow in Inji Web Wallet.
* Added support for processing credential requests containing **credential sets**.
* Improved credential selection logic for mandatory and optional credentials requested through DCQL.
* Added support for submitting credentials to the verifier with **SD-JWT claim selection** and VP token signing support.

#### 3. Technical Enhancements

* Fixed the Web Wallet flow where users were not automatically redirected back to **Inji Verify** when no matching credential was available.
* Improved the handling of credential-selection and presentation flows between Inji Web Wallet and Inji Verify.
* Added the VCI 1.0 credential download factory refactoring.

### Features Released

<table><thead><tr><th width="449.91796875">Feature / Enhancement / Technical Upgrade</th><th>GitHub Issue</th></tr></thead><tbody><tr><td>Add Support for OpenID4VCI 1.0 Well-Known Format</td><td><a href="https://github.com/inji/inji-web/issues/567">#567</a></td></tr><tr><td>Add VC Download Support for VCI 1.0 (Factory Refactor)</td><td><a href="https://github.com/inji/inji-web/issues/568">#568</a></td></tr><tr><td>Backend for DCQL OpenIDVP 1.0 – Mimoto</td><td><a href="https://github.com/inji/inji-web/issues/657">#657</a></td></tr><tr><td>Add DCQL as Part of Data Share</td><td><a href="https://github.com/inji/inji-web/issues/670">#670</a></td></tr><tr><td>Submission of Credentials to Verifier with SD-JWT Claim Selection and VP Token Signing Support</td><td><a href="https://github.com/inji/inji-web/issues/638">#638</a></td></tr></tbody></table>

### Repositories Released

| Module          | Version                                                                     |
| --------------- | --------------------------------------------------------------------------- |
| Inji Web Wallet | [1.0.0-alpha.1](https://github.com/inji/inji-web/tree/v1.0.0-alpha.1)       |
| Mimoto          | [1.0.0-alpha.1](https://github.com/inji/mimoto/tree/v1.0.0-alpha.1)         |
| Inji OpenID4VP  | [1.0.0-alpha.1](https://github.com/inji/inji-openid4vp/tree/v1.0.0-alpha.1) |
| Inji Config     | [1.0.0-alpha.2](https://github.com/inji/inji-config/tree/v1.0.0-alpha.2)    |

> **Note:** `inji-config` is released as `1.0.0-alpha.2`, while the other components in this release baseline use `1.0.0-alpha.1`.

### Compatible Modules

| Module       | Version                                                                   |
| ------------ | ------------------------------------------------------------------------- |
| Durian       | [1.3.0-beta.2](https://github.com/mosip/durian/releases/tag/1.3.0-beta.2) |
| Inji Certify | [1.0.0-alpha.1](https://github.com/inji/inji-certify/tree/v1.0.0-alpha.1) |
| Inji Verify  | [1.0.0-alpha.1](https://github.com/inji/inji-verify/tree/v1.0.0-alpha.1)  |
| eSignet      | [1.6.2](https://github.com/mosip/esignet/tree/v1.6.2)                     |

### Known Issues

Below is the list of key known issues specific to this release. For all the known issues, click [**here**](https://github.com/inji/inji-web/issues?q=is%3Aissue%20state%3Aopen%20label%3Abug%20-state%3Aclosed).

<table><thead><tr><th width="277.92578125">GitHub Issue</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-web/issues/689">#689</a></td><td>Observed an invalid session screen when we refresh on the download successful screen</td></tr><tr><td><a href="https://github.com/inji/inji-web/issues/683">#683</a></td><td>Verifier Trust Dialog displays full DID instead of a user-friendly verifier name</td></tr><tr><td><a href="https://github.com/inji/inji-web/issues/679">#679</a></td><td>Data-share QR verification limit shows raw HTTP 401 instead of a clear limit-reached message</td></tr><tr><td><a href="https://github.com/inji/inji-web/issues/677">#677</a></td><td>Verifier information is truncated/overlapped in "Required Card(s) Not Found!" popup</td></tr></tbody></table>

### Bug Fixes

Below is the complete list of bug fixes included in the [**1.0.0-alpha.1** ](https://github.com/inji/inji-web/issues?q=is%3Aissue%20state%3Aclosed%20label%3Abug%20milestone%3A1.0.0-alpha.1%20project%3Ainji%2F6)release.

| GitHub Issue                                        | Description                                                                                                                                       |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| [#558](https://github.com/inji/inji-web/issues/558) | Fixed the issue where the user was not redirected back to Inji Verify when no matching credential was found during the Web Wallet OpenID4VP flow. |
| [#623](https://github.com/inji/inji-web/issues/623) | Fixed the language-selection issue where users had to double-click to select a language.                                                          |
| [#682](https://github.com/inji/inji-web/issues/682) | Fixed the issue where clicking **Continue** with an available credential redirected the user to the Issuers page.                                 |
| [#620](https://github.com/inji/inji-web/issues/620) | Fixed the default **“U” user** being displayed on the homepage when the user was not logged in.                                                   |
| [#656](https://github.com/inji/inji-web/issues/656) | Fixed credential download failures for Mock and Land Registry issuers in the QA environment.                                                      |
| [#658](https://github.com/inji/inji-web/issues/658) | Fixed SVG Farmer VC download failure from the QA Inji environment.                                                                                |
| [#644](https://github.com/inji/inji-web/issues/644) | Fixed credential types not being displayed when Mimoto and Mock Services were running locally.                                                    |
| [#661](https://github.com/inji/inji-web/issues/661) | Fixed Farmer VC download failure after updating the template and context from V2 to V1 on the development integration environment.                |

### Release Documentation

* [IETF SD-JWT Support & Selective Disclosure](../../overview/features/ietf-sd-jwt-vc-and-selective-disclosure.md)
* Verifiable Presentations (OpenIDVP) Support 1.0
* Verifiable Credential Issuance (OpenIDVCI) Support 1.0
* [QA Report](https://app.gitbook.com/o/-M1FyzBr-VmticWYm8QI/s/aY8BQ4hdzhSchZV814Ev/~/edit/~/changes/1331/inji-wallet/inji-web/inji-web/version-1.0.0-alpha.1/test-report)

### Additional Resources

* [Feature Documentation](https://docs.inji.io/inji-wallet/inji-web/overview/features) - Contains detailed explanations of all available features of Inji Web Waller and its usage.
* [Backend Services ](https://docs.inji.io/inji-wallet/inji-web/technical-overview/backend-services)- Provides detailed instructions to set up the backend for the Inji Web Wallet.
* [End User Guide](https://docs.inji.io/inji-wallet/inji-web/functional-overview/end-user-guide) - Offers end-to-end guidance for end users on setup and daily usage.
* [API Documentation](https://docs.mosip.io/inji/inji-web/technical-overview/backend-services/mimoto-bff) - Includes comprehensive details of all APIs, endpoints, request/response formats, and examples.
