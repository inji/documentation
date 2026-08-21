# Version 1.0.0-alpha.1

**Release Name:** Inji Mobile Wallet 1.0.0-alpha.1

**Release Type:** Alpha

**Release Date:** 18th August 2026

### Overview

This release of Inji Mobile Wallet v1.0.0-alpha.1 introduces the foundational support for [OpenID4VCI 1.0 ](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html) and [OpenID4VP 1.0](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html) , including DCQL-based credential selection, along with support for ECC R1 (ES256) credentials. The release also carries forward a set of technical debt improvements and bug fixes, identified through QA and automation cycles.

This is an alpha release intended primarily for developer and interoperability validation. Some OpenID4VP 1.0 and DCQL capabilities remain under active development. This release is backward compatible with Draft 13 of the OpenID4VCI standard.

### Key Highlights

#### 1. Support for ECC R1

* Added support for ECC R1 (ES256) key type for credential issuance and presentation, alongside the existing Ed25519 support.

#### 2. OpenID4VCI 1.0 Upgrade

* Upgraded the Mobile Wallet's credential issuance flow from the earlier OpenID4VCI Draft 13 implementation to the finalized OpenID4VCI 1.0 specification.

#### 3. OpenID4VP 1.0 Upgrade along with DCQL

* Upgraded the Mobile Wallet's credential presentation flow from OpenID4VP Draft 23 to the finalized OpenID4VP 1.0 specification.
* Added DCQL (Digital Credentials Query Language)-based credential request processing and selection support.

#### 4. Basic UI Changes for DCQL

* Introduced initial UI updates to support credential selection driven by DCQL-based verifier requests, including handling of mandatory and optional credential sets.

#### 5. Conformance Test Suite

* Progressed OpenID4VP and OpenID4VCI Conformance Test Suite compliance work, including implementation of identified fixes.

#### 6. Tech Debt

* **VCI Client library error enhancements:** Improved error handling and error messaging within the `inji-vci-client` library.
* **Test coverage enhancements:** Improved automated test coverage across Wallet, OpenID4VP, and VCI Client modules.
* Resolved critical issues affecting the Personal Data Item (PDI) flow, SD-JWT VP flow, and issues surfaced through automation runs.

### Features Released

<table data-search="false"><thead><tr><th width="583.23828125">Feature / Enhancement / Technical Upgrade</th><th>GitHub Issue</th></tr></thead><tbody><tr><td>Integrate OpenID4VP Library and Expand Sample Wallet Capabilities</td><td><a href="https://github.com/inji/inji-wallet/issues/2120">#2120</a></td></tr><tr><td>[Kotlin] OpenIDVP 1.0 Changes — Wallet metadata changes and Client ID prefix</td><td><a href="https://github.com/inji/inji-wallet/issues/2284">#2284</a></td></tr><tr><td>[Swift] OpenIDVP 1.0 Changes — Wallet metadata changes and Client ID prefix</td><td><a href="https://github.com/inji/inji-wallet/issues/2285">#2285</a></td></tr><tr><td>[Kotlin] VP Response Construction and sending VP response to verifier + Parsing with DCQL</td><td><a href="https://github.com/inji/inji-wallet/issues/2286">#2286</a></td></tr><tr><td>[Swift] VP Response Construction &#x26; Parsing with DCQL</td><td><a href="https://github.com/inji/inji-wallet/issues/2287">#2287</a></td></tr><tr><td>[Swift] Encryption Process for direct_post.jwt</td><td><a href="https://github.com/inji/inji-wallet/issues/2288">#2288</a></td></tr><tr><td>[Swift] Terminology Update: client_id_scheme → client_id_prefix</td><td><a href="https://github.com/inji/inji-wallet/issues/2289">#2289</a></td></tr><tr><td>Wallet UI — DCQL-Based Credential Matching and Selection UI for VP Request</td><td><a href="https://github.com/inji/inji-wallet/issues/2416">#2416</a></td></tr><tr><td>[Android - Wallet Code] Credential Offer via Deeplink — Pre-authorized-code and authorized code flow</td><td><a href="https://github.com/inji/inji-wallet/issues/2457">#2457</a></td></tr><tr><td>[iOS - Wallet Code] Credential Offer via Deeplink — Pre-authorized-code and authorized code flow</td><td><a href="https://github.com/inji/inji-wallet/issues/2459">#2459</a></td></tr><tr><td>[Kotlin] OpenID4VP Conformance Test Suite Compliance (Spec Compliance 1.0) — Implementation of Identified Fixes &#x26; Dev Testing</td><td><a href="https://github.com/inji/inji-wallet/issues/2466">#2466</a></td></tr><tr><td>Kotlin: [OpenID4VP] Error response in direct_post.jwt response mode not encrypted</td><td><a href="https://github.com/inji/inji-wallet/issues/2484">#2484</a></td></tr><tr><td>[Kotlin] [OpenID4VP] Improve WalletConfig and VPTokenSigningResult / UnsignedVPToken</td><td><a href="https://github.com/inji/inji-wallet/issues/2498">#2498</a></td></tr><tr><td>[Swift] [OpenID4VP] Improve WalletConfig and VPTokenSigningResult / UnsignedVPToken</td><td><a href="https://github.com/inji/inji-wallet/issues/2499">#2499</a></td></tr><tr><td>OpenID4VP sendVP always uses default Ed25519 wallet key for holder + VP proof signing — ES256-bound credentials fail Inji Verify holder binding (ECC R1 support)</td><td><a href="https://github.com/inji/inji-wallet/issues/2505">#2505</a></td></tr><tr><td>Increase SonarQube Code Coverage to ≥85% for repositories identified during LSH 1.0.0-alpha.1 (Test Coverage Enhancements)</td><td><a href="https://github.com/inji/inji-wallet/issues/2528">#2528</a></td></tr></tbody></table>

### Repositories Released

<table data-search="false"><thead><tr><th>Module</th><th>Version</th></tr></thead><tbody><tr><td>Inji Wallet (Mobile)</td><td><a href="https://github.com/inji/inji-wallet/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Secure Keystore</td><td><a href="https://github.com/inji/secure-keystore/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Secure Keystore (iOS - Swift)</td><td><a href="https://github.com/inji/secure-keystore-ios-swift/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji OpenID4VP (iOS - Swift)</td><td><a href="https://github.com/inji/inji-openid4vp-ios-swift/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Tuvali</td><td><a href="https://github.com/inji/tuvali/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Tuvali (iOS - Swift)</td><td><a href="https://github.com/inji/tuvali-ios-swift/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>PixelPass</td><td><a href="https://github.com/inji/pixelpass/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>PixelPass (iOS - Swift)</td><td><a href="https://github.com/inji/pixelpass-ios-swift/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji VC Renderer</td><td><a href="https://github.com/inji/inji-vc-renderer/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji VC Renderer (iOS - Swift)</td><td><a href="https://github.com/inji/inji-vc-renderer-ios-swift/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji VCI Client</td><td><a href="https://github.com/inji/inji-vci-client/releases/tag/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji VCI Client (iOS - Swift)</td><td><a href="https://github.com/inji/inji-vci-client-ios-swift/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji Config</td><td><a href="https://github.com/inji/inji-config/tree/v1.0.0-alpha.2">1.0.0-alpha.2</a></td></tr><tr><td>Mimoto</td><td><a href="https://github.com/inji/mimoto/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr><tr><td>Inji OpenID4VP</td><td><a href="https://github.com/inji/inji-openid4vp/tree/v1.0.0-alpha.1">1.0.0-alpha.1</a></td></tr></tbody></table>

> Inji Config, Mimoto, and Inji OpenID4VP were already released as part of Inji Web Wallet 1.0.0-alpha.1 and are shared across the Web and Mobile Wallet releases.

### Compatible Modules

| Module       | Version                                                                   |
| ------------ | ------------------------------------------------------------------------- |
| Inji Certify | [1.0.0-alpha.1](https://github.com/inji/inji-certify/tree/v1.0.0-alpha.1) |
| Inji Verify  | [1.0.0-alpha.1](https://github.com/inji/inji-verify/tree/v1.0.0-alpha.1)  |
| eSignet      | [1.6.2](https://github.com/mosip/esignet/tree/v1.6.2)                     |

### Known Issues

Below is the list of key known issues specific to this release. For the complete list, [click here](https://github.com/inji/inji-wallet/issues?q=state%3Aopen%20label%3Abug).

<table><thead><tr><th width="583.0625">Description</th><th>GitHub Issue</th></tr></thead><tbody><tr><td>iOS: OVP DID by Reference Flow Fails, Whereas the Same Flow Works on Android</td><td><a href="https://github.com/inji/inji-wallet/issues/2552">#2552</a></td></tr><tr><td>[OpenID4VP] [Android] ldp_vp with holder binding key type EC (secp256k1) is not verifiable</td><td><a href="https://github.com/inji/inji-wallet/issues/2541">#2541</a></td></tr><tr><td>VP submission is failing for mso_mdoc VC for OpenID Conformance Test Suite</td><td><a href="https://github.com/inji/inji-wallet/issues/2536">#2536</a></td></tr><tr><td>mso_mdoc VC response is not as per OpenID4VCI spec 1.0</td><td><a href="https://github.com/inji/inji-wallet/issues/2535">#2535</a></td></tr><tr><td>OpenID4VP sendVP always uses default Ed25519 wallet key for holder + VP proof signing — ES256-bound credentials fail Inji Verify holder binding</td><td><a href="https://github.com/inji/inji-wallet/issues/2505">#2505</a></td></tr><tr><td>Button alignment is not proper on Inji tour guide slides</td><td><a href="https://github.com/inji/inji-wallet/issues/2490">#2490</a></td></tr></tbody></table>

### Bug Fixes

Below is the complete list of bug fixes included in the [1.0.0-alpha.1](https://github.com/inji/inji-wallet/issues?q=is%3Aissue%20state%3Aclosed%20label%3Abug%20type%3ABug) release.

<table><thead><tr><th width="588.7421875">Description</th><th>GitHub Issue</th></tr></thead><tbody><tr><td>Fixed issue where downloading National Identity VC in the Inji Wallet failed and displayed a "Server issue" error.</td><td><a href="https://github.com/inji/inji-wallet/issues/2500">#2500</a></td></tr><tr><td>Fixed VC download failure occurring for credentials bound to ES256 keys.</td><td><a href="https://github.com/inji/inji-wallet/issues/2487">#2487</a></td></tr><tr><td>Added a description for each API schema on the home screen.</td><td><a href="https://github.com/inji/inji-wallet/issues/2335">#2335</a></td></tr><tr><td>Added the decoded payload for all schemas to improve readability for users.</td><td><a href="https://github.com/inji/inji-wallet/issues/2334">#2334</a></td></tr><tr><td>Fixed the mock UI issue where only the download button was highlighted while other buttons were not.</td><td><a href="https://github.com/inji/inji-wallet/issues/2333">#2333</a></td></tr></tbody></table>

### Release Documentation

* [OpenID4VP Library Integration Guide](../../technical-overview/integration-guide/building-verifiable-credentials-wallet-with-inji-libraries/openid4vp.md)
* [OpenID4VCI Library Integration Guide](../../technical-overview/integration-guide/building-verifiable-credentials-wallet-with-inji-libraries/vci-client.md)
* [QA Report](test-report.md)

### Additional Resources

* [Features](https://docs.inji.io/inji-wallet/inji-mobile/overview/features)
* [Integration Guides](https://docs.inji.io/inji-wallet/inji-mobile/technical-overview/integration-guide)
* [End User Guide](https://docs.inji.io/inji-wallet/inji-mobile/functional-overview/end-user-guide)
* [API Documentation](https://mosip.stoplight.io/docs/mimoto/5bf5a1n68g4tq-mimoto)

