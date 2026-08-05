# Version 1.0.0-alpha.1

**Release Name**: Inji Verify v1.0.0-alpha.1

**Support**: Developer Release

**Release Date**: 4th August, 2026&#x20;

{% hint style="success" %}
**Upgrade Notes**: Refer to '[Migrating from PEX to DCQL](../../technical-overview/integration-guides/transition-from-pex-to-dcql.md)' guide to upgrade to DCQL and also refer to '[Removals & Replacements](./#removals--replacements)' in this release.
{% endhint %}

{% hint style="success" %}
**Notes**:

* **Inji Verify v1.0.0-alpha.1** marks our formal adoption of the OpenID4VP 1.0 specification. This is an important milestone, and we want to provide clear guidance for all community members.
* **Upgrading Guidance - Upgrading is optional but recommended** for teams ready to align with the finalized OpenID4VP 1.0 specification. Earlier 'Inji Verify' releases built on draft specifications remain fully functional, and can be continued without disruption, with the option to upgrade at a time that suits your roadmap.
* **Legacy Support -** Note that this release **does not maintain full backward compatibility** with draft specification implementations. Limited support for Presentation Definition (PD) based sessions is retained on result-fetch endpoints only, allowing existing integrations to keep working through the transition.
* APIs, credential formats, and endpoints that have been updated or replaced are detailed in [API Documentation](../../api/api-changes.md). **Reviewing these sections before upgrading is strongly recommended.**
{% endhint %}

### **Overview**

We are excited to bring the release of **Inji Verify v1.0.0-alpha.1.** This release completes Inji Verify's move to DCQL (Digital Credentials Query Language) — the [OpenID4VP 1.0](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html) way of describing what a verifier needs from a wallet — across the entire verification flow: authorization requests, VP token submission, validation, and results. The core change is the migration from Presentation Exchange (PEX) to [**DCQL** (Digital Credentials Query Language)](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#section-6).

Presentation Exchange (`presentation_definition`) is no longer accepted for new requests; only previously completed PD-based verifications remain readable through the result-fetch endpoints.

**Highlights**

* **Stronger holder proof** — `require_cryptographic_holder_binding` lets verifiers demand cryptographic proof of holder possession for both SD-JWT VC and LDP\_VC presentations, replacing the older `acceptVPWithoutHolderProof` flag.
* **Wider SD-JWT compatibility** — both `vc+sd-jwt` and `dc+sd-jwt` format identifiers are accepted, so wallets built against either the draft or final SD-JWT VC spec continue to verify.
* **Replay protection** — KB-JWT `nonce` and `aud` claims are validated on every SD-JWT submission, so a captured presentation can't be resubmitted elsewhere.
* **Tamper-resistant sessions** — VP request expiry and duplicate submissions are now enforced server-side, not left to the wallet to self-report.
* **More accurate credential matching** — the Verify UI matches submitted credentials against DCQL `type_values`, keeping matches correct when multiple verifier configurations share a credential type.
* **Spec-aligned protocol fields** — client ID scheme, `client_metadata` handling, and supported-formats fields are updated to match OpenID4VP 1.0. Full field-level detail: [API Changes](../../api/#changes-which-came-with-inji-verify-1.0.0-alpha.1).

{% hint style="info" %}
**Note:** The Inji Verify UI is a _reference implementation_ to demonstrate orchestration. Developers can selectively embed SDK components in the verifier applications as per their needs.
{% endhint %}

### **Repositories: Released/Dependent**

**Inji Verify Repo** → 4 projects (all these projects are of same version) as below:

<table><thead><tr><th width="373.5390625">Repositories</th><th>Tags: Released/Dependent</th></tr></thead><tbody><tr><td><strong>vc-verifier</strong></td><td><a href="https://github.com/inji/vc-verifier/tree/v1.9.0">v1.9.0</a></td></tr><tr><td><strong>inji-verify</strong></td><td><a href="https://github.com/inji/inji-verify/tree/v1.0.0-alpha.1">v1.0.0-alpha.1</a></td></tr></tbody></table>

### **Compatible modules**

The following table outlines the tested and certified compatibility of Inji Verify v1.0.0-alpha.1 with other modules.

| Module             | Version                                                           |
| ------------------ | ----------------------------------------------------------------- |
| Pixel-Pass library | [0.8.0](https://docs.inji.io/inji-verify/releases/version-0.17.0) |
| Inji Wallet        | 1.0.0-alpha.1 (Release Coming Soon)                               |
| Inji Web           | 1.0.0-alpha.1 (Release Coming Soon)                               |

### **Bug Fixes**

Below is the list of fixes as part of the **v1.0.0-alpha.1** release, refer [here](https://github.com/inji/inji-verify/issues?q=type%3ABug%20milestone%3A1.0.0-alpha.1) for the comprehensive list.

<table><thead><tr><th width="141.65234375">Bug ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-verify/issues/2086">#2086</a></td><td>Verify library contributes global servlet context path when embedded in Certify.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1919">#1919</a></td><td>Upload valid claim 169 QR code shows invalid result intermittently.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1920">#1920</a></td><td>Scan QR Code feature returns invalid result for valid VC intermittently across multiple camera scenarios.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2045">#2045</a></td><td>Nonce validation gaps in VP request creation.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2062">#2062</a></td><td>Possible race condition in VP submission: status listener notified before transaction commits.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1928">#1928</a></td><td>Open INJI-Verify application Navigate to Verify Credentials Select Scan QR Code tab Disable internet connection (simulate offline mode) Click on Scan QR Code button Observe the behaviour after scan failure / retry.</td></tr></tbody></table>

### **User Stories**

<table><thead><tr><th width="145.24609375">Story ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-verify/issues/1721">#1721</a></td><td>Changes in client_id did prefix as per OpenID4VP spec v1.0.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1758">#1758</a></td><td>Changes in client_metadata as per OpenID4VP spec v1.0.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1765">#1765</a></td><td>Handling client_metadata for Pre-registered client_id Scheme as per OpenID4VP spec v1.0.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1768">#1768</a></td><td>DCQL support in Authorization Request as per OpenID4VP spec v1.0</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1703">#1703</a></td><td>Migrate OpenID4VP response handling from PEX to DCQL and implement vp_token validations.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1935">#1935</a></td><td>VP Token DCQL Query Satisfaction at Submission Stage.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1957">#1957</a></td><td>VP Result Processing &#x26; Validation (DCQL + Legacy Support).</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1961">#1961</a></td><td>Inji Verify must support both vc+sd-jwt and dc+sd-jwt as credential format.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1965">#1965</a></td><td>Support require_cryptographic_holder_binding in DCQL during VP submission for LDP_VC.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1988">#1988</a></td><td>Support require_cryptographic_holder_binding in DCQL during VP submission for SD-JWT VC.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1940">#1940</a></td><td>Remove presentation_definition Table.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2034">#2034</a></td><td>Replace acceptVPWithoutHolderProof with DCQL require_cryptographic_holder_binding in Verify UI.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1973">#1973</a></td><td>Enforce VP Request Expiry and Prevent Duplicate VP Submission on Server Side.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2049">#2049</a></td><td>Verify UI: Match Submitted Credentials Using DCQL type_values Instead of Configuration type.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2043">#2043</a></td><td>Validate nonce and aud claims from Key Binding JWT (KB-JWT) for SD-JWT VP submissions.</td></tr></tbody></table>

### **Known Issues**

Below is a list of some key known issues. For a detailed overview and the complete list of issues related to Inji Verify, please click [here](https://github.com/inji/inji-verify/issues?q=type%3ABug%20-milestone%3A1.0.0-alpha.1%20-is%3Aclosed).

<table><thead><tr><th width="143.3359375">Issue ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-verify/issues/1845">#1845</a></td><td>We are uploading an invalid QR code, and while it displays an error message stating that the QR code is invalid, the credential details are still visible.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1844">#1844</a></td><td>On iPhone 8 and iPhone 7, uploading the Injiweb QR code PDF shows an error message.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1852">#1852</a></td><td>Inji Verify - Upload not functioning on Mac Safari Browser Versions 16 and below.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1789">#1789</a></td><td>INJI Verify SDK should be able to support integration with applications built on platforms beyond <em>React (Typescript) applications</em>, such as Angular, PHP, and others.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2178">#2178</a></td><td>The latest Inji Verify release cannot support complete end-to-end testing of VP (Verifiable Presentation) flow and Data Share flow when integrated with Inji Web.</td></tr></tbody></table>

### **API Changes**

Refer [here](../../api/api-changes.md) for 'Changes to API' and 'New APIs'.

### Removals & Replacements

The following are no longer supported in this release. See the [PEX to DCQL Migration Guide](../../technical-overview/integration-guides/transition-from-pex-to-dcql.md) to update existing integrations.

<table><thead><tr><th width="202.15625">Removed</th><th width="183.609375">Replaced By</th><th>What This Means</th></tr></thead><tbody><tr><td>Presentation Exchange (<code>presentation_definition</code>, <code>presentationDefinitionId</code>)</td><td>DCQL (<code>dcql_query</code>)</td><td>New requests using PD are rejected; previously completed PD-based results remain readable via result-fetch endpoints only.</td></tr><tr><td><code>acceptVPWithoutHolderProof</code></td><td><code>require_cryptographic_holder_binding</code></td><td>Holder-proof enforcement is now expressed inside the DCQL query itself.</td></tr><tr><td><code>presentation_submission</code></td><td>— (DCQL-only)</td><td>This field is no longer accepted; DCQL query IDs identify submissions instead.</td></tr><tr><td>Legacy request endpoints (<code>/vp-request</code>, <code>/vp-session-request</code>, <code>/vp-request/{requestId}</code>, <code>/vp-submission/direct-post</code>)</td><td><code>/v2</code> counterparts</td><td>Existing integrations calling these paths must move to the <code>/v2</code> endpoints.</td></tr></tbody></table>

### **Documentation**

* [Feature documentation](https://docs.inji.io/inji-verify/overview/features)
* [Integration Guide](https://docs.inji.io/inji-verify/technical-overview/integration-guides)
* [API Documentation](https://mosip.stoplight.io/docs/inji-verify/67445477d332e-open-id-4-vp-verifier-api-inji-verify)
* [Collab Guide](../../functional-overview/releases-1/inji-verify-collab-guide.md)
* [QA Report](test-report.md)
