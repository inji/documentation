# Inji Verify 1.0.0-rc.1

**Release Name:** Inji Verify 1.0.0-rc.1

**Support:** Release Candidate (RC)

**Release Date:** Coming Soon!

> **Note**:
>
> Inji Verify v1.0.0-rc.1 continues on the OpenID4VP 1.0 baseline established in v1.0.0-alpha.1. The focus of this release is the **W3C Digital Credentials API (DC API)** as an additional credential request channel, and **X.509-based verifier identification**.

**Upgrade Guidance** - Upgrading is recommended for all teams already on v1.0.0-alpha.1. There are no breaking changes relative to alpha.1.

### Overview

We are excited to bring/announce the release of Inji Verify v1.0.0-rc.1.

Inji Verify v1.0.0-rc.1 extends the OpenID4VP 1.0 / DCQL implementation delivered in alpha.1 with the following key changes:

* **W3C Digital Credentials API (DC API) support** — A verifier can now request credentials directly through the browser's Digital Credentials API, in addition to the existing QR code and deep-link flows. The full exchange is covered: 'Authorization Request Creation', 'VP Token Submission', 'Validation' and 'Result Display'. DC API support is available through the Inji Verify SDK and can be enabled per deployment.
* **X.509-based Verifier Identification** — Support for the `x509_san_dns` client identifier prefix along with `x5c` certificate chains in signed request objects, allowing wallets to establish verifier trust directly from a certificate chain.
* **Embeddable**`verify-core` library — `verify-service` has been split into an embeddable `verify-core` library and a deployable `verify-service` application, so verification capabilities can be embedded directly into other Spring Boot applications instead of being consumed only over HTTP. All request validations have been moved from the controller layer into the service layer as part of this restructuring.
* **Bug Fixes** — A set of scanning, upload, error-handling and VP submission issues reported against alpha.1 and earlier have been resolved.

**Note:** The Inji Verify UI is a reference implementation to demonstrate orchestration. Developers can selectively embed SDK components in the verifier applications as per their needs.

### Repositories: Released/Dependent

| Repositories | Tags: Released/Dependent |
| ------------ | ------------------------ |
| Inji Verify  | v1.0.0-rc.1              |
| Vc-verifier  | 1.10.0                   |

### Compatible modules

The following table outlines the tested and certified compatibility of Inji Verify v1.0.0-rc.1 with other modules.

| Module              | Version                                                          |
| ------------------- | ---------------------------------------------------------------- |
| Inji Wallet         | 1.0.0-rc.1 (Yet to release, Will be compatible when it releases) |
| Inji Web            | 1.0.0-rc.1 (Yet to release, Will be compatible when it releases) |
| Pixel-Pass library  | 0.8.0                                                            |
| vc-verifier library | _1.9.0_                                                          |

### User Stories

| Git Issue                                                | Description                                                                                     |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| [#2111](https://github.com/inji/inji-verify/issues/2111) | DC API: Request Flow                                                                            |
| [#2112](https://github.com/inji/inji-verify/issues/2112) | DC API: Response Flow (VP submission + validation + result display)                             |
| [#2238](https://github.com/inji/inji-verify/issues/2238) | Support `x509_san_dns` client\_id\_prefix and `x5c` certificate chains in Inji Verify           |
| [#2148](https://github.com/inji/inji-verify/issues/2148) | Split verify-service into an embeddable `verify-core` library + deployable `verify-service` app |

### Bug Fixes

Below is the list of fixes as part of the v1.0.0-rc.1 release:

Query: [https://github.com/inji/inji-verify/issues?q=milestone%3A1.0.0-rc.1+type%3ABug](https://github.com/inji/inji-verify/issues?q=milestone%3A1.0.0-rc.1+type%3ABug)

| Git Issue                                                | Description                                                                                           |
| -------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [#2277](https://github.com/inji/inji-verify/issues/2277) | Unable to verify Data Share QR codes with the latest build when `VP_SUBMISSION_SUPPORTED=false`       |
| [#2219](https://github.com/inji/inji-verify/issues/2219) | VP submission: missing SD-JWT Key Binding JWT returns `invalid_request` instead of `invalid_vp_token` |
| [#2217](https://github.com/inji/inji-verify/issues/2217) | `credential_sets` in `dcqlQuery` is dropped when building VP request (Verify UI)                      |
| [#2095](https://github.com/inji/inji-verify/issues/2095) | The footer is cropping the error messages on the screen                                               |
| [#1908](https://github.com/inji/inji-verify/issues/1908) | Buttons are not able to hold other language text in them                                              |
| [#1882](https://github.com/inji/inji-verify/issues/1882) | Appropriate error message is not displayed when a partial scan is attempted                           |

### Known Issues

Below is a list of some key known issues. For a detailed overview and the complete list of issues related to Inji Verify, please click [here](https://github.com/inji/inji-verify/issues?q=type%3ABug+-milestone%3A1.0.0-rc.1+-status%3Acancelled+-is%3Aclosed).

| Git Issue                                                | Description                                                                           |
| -------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [#1901](https://github.com/inji/inji-verify/issues/1907) | INJI-VERIFY - Error messages doesn't match the other INJI modeules format             |
| [#1900](https://github.com/inji/inji-verify/issues/1900) | File/Image formats to be supported like SVG for Inji Verify                           |
| [#1847](https://github.com/inji/inji-verify/issues/1847) | INJI-verify - VP verification check list selection is not proper                      |
| [#1811](https://github.com/inji/inji-verify/issues/1811) | INJI-verify - In VP verification to select a VC we have to only click on the checkbox |
| [#2462](https://github.com/inji/inji-verify/issues/2462) | SD\_JWT with expired certificate are getting verified as valid                        |
| [#1851](https://github.com/inji/inji-verify/issues/1851) | Improper Error Message after the QR code is verified twice                            |

### Documentation

* Feature documentation
* Integration Guide
* API Documentation
* Collab Guide
* QA Report
