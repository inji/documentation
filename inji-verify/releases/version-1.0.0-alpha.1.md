# Version 1.0.0-alpha.1

**Release Name**: Inji Verify v1.0.0-alpha.1

**Support**: Developer Release

**Release Date**: <mark style="color:red;">**Coming Soon!**</mark>

{% hint style="success" %}
**Note**:

* **Inji Verify v1.0.0-alpha.1** marks our formal adoption of the [OpenID4VP 1.0 specification](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html). This is an important milestone, and we want to provide clear guidance for all community members.
* **Upgrading Guidance - Upgrading is optional but recommended** for spec compliance. This release is intended for teams ready to align with the finalized OpenID4VP 1.0 standard. Teams running implementations built on pre-1.0 draft specifications are **not mandatory to upgrade** — earlier releases can be continued without any disruption.
* **Backward Compatibility -** For those upgrading to v1.0.0-alpha.1, this release **does not maintain full backward compatibility** with pre-1.0 draft implementations.
* APIs, credential formats, and endpoints that have been updated or replaced are detailed in the Integration Guide and [API Documentation](https://mosip.stoplight.io/docs/inji-verify/67445477d332e-open-id-4-vp-verifier-api-inji-verify) . **Reviewing these sections before upgrading is strongly recommended.**
* **Legacy Support -** For backward compatibility with existing workflows, the release retains limited support for Presentation Definition (PD) based sessions on result-fetch endpoints only. This allows existing integrations to continue functioning during transition periods.
* **For Teams Staying on Draft Specifications- No action is needed.** Older releases will continue to function as-is, with the option to upgrade at a time that suits your roadmap.
  * **Migration Guide**: Link to Migration Guide
{% endhint %}

### **Overview**

We are excited to announce the release of **Inji Verify v1.0.0-alpha.1.**

Inji Verify **v1.0.0-alpha.1** upgrades the platform from OpenID4VP Draft 23 to the [OpenID4VP 1.0](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html) final specification. The core change is the migration from Presentation Exchange (PEX) to **DCQL** (Digital Credentials Query Language) across the full verification flow — authorization requests, VP token submission, validation, and result processing — with backward compatibility retained only for existing PD-based sessions on result-fetch endpoints. The release adds support for cryptographic holder binding (require\_cryptographic\_holder\_binding) for both SD-JWT VC and LDP\_VC formats, accepts both vc+sd-jwt and dc+sd-jwt credential formats, and strengthens security through KB-JWT nonce/aud claim validation and server-side enforcement of VP request expiry and duplicate submission checks. Client metadata and identifier schemes have also been aligned with the v1.0 specification.

{% hint style="info" %}
**Note:** The Inji Verify UI is a _reference implementation_ to demonstrate orchestration. Developers can selectively embed SDK components in the verifier applications as per their needs.
{% endhint %}

### **Repositories: Released/Dependent**

**Inji Verify Repo** → 4 projects (all these projects are of same version) as below:

<table><thead><tr><th width="374">Repositories</th><th>Tags: Released/Dependent</th></tr></thead><tbody><tr><td>inji-verify-service</td><td><strong>v1.0.0-alpha.1</strong></td></tr><tr><td>inji-verify-ui</td><td></td></tr><tr><td>SDK</td><td></td></tr><tr><td>API-Test</td><td></td></tr></tbody></table>

### **Compatible modules**

The following table outlines the tested and certified compatibility of Inji Verify v1.0.0-alpha.1 with other modules.

| Module              | Version                                                           |
| ------------------- | ----------------------------------------------------------------- |
| Inji Wallet         | 1.0.0-alpha.1                                                     |
| Inji Web            | 1.0.0-alpha.1                                                     |
| Pixel-Pass library  | [0.8.0](https://docs.inji.io/inji-verify/releases/version-0.17.0) |
| vc-verifier library | 1.9.0                                                             |

### **Bug Fixes**

Below is the list of fixes as part of the **v1.0.0-alpha.1** release, refer [here](https://github.com/orgs/inji/projects/3/views/7?filterQuery=milestone%3A1.0.0-alpha.1+type%3ABug) for the comprehensive list.

<table><thead><tr><th width="141.65234375">Bug ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-verify/issues/2086">#2086</a></td><td>Verify library contributes global servlet context path when embedded in Certify</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1919">#1919</a></td><td>Upload valid claim 169 QR code shows invalid result intermittentl</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1920">#1920</a></td><td>Scan QR Code feature returns invalid result for valid VC intermittently across multiple camera scenarios</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2045">#2045</a></td><td>Nonce validation gaps in VP request creation</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2062">#2062</a></td><td>Possible race condition in VP submission: status listener notified before transaction commits</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1928">#1928</a></td><td>Open INJI-Verify application Navigate to Verify Credentials Select Scan QR Code tab Disable internet connection (simulate offline mode) Click on Scan QR Code button Observe the behaviour after scan failure / retry</td></tr></tbody></table>

### **User Stories**

<table><thead><tr><th width="145.24609375">Story ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-verify/issues/1721">#1721</a></td><td>Changes in client_id did prefix as per OpenID4VP spec v1.0</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1758">#1758</a></td><td>Changes in client_metadata as per OpenID4VP spec v1.0</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1765">#1765</a></td><td>Handling client_metadata for Pre-registered client_id Scheme as per OpenID4VP spec v1.0</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1768">#1768</a></td><td>DCQL support in Authorization Request as per OpenID4VP spec v1.0</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1703">#1703</a></td><td>Migrate OpenID4VP response handling from PEX to DCQL and implement vp_token validations</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1935">#1935</a></td><td>VP Token DCQL Query Satisfaction at Submission Stage</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1957">#1957</a></td><td>VP Result Processing &#x26; Validation (DCQL + Legacy Support)</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1961">#1961</a></td><td>Inji Verify must support both vc+sd-jwt and dc+sd-jwt as credential format</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1965">#1965</a></td><td>Support require_cryptographic_holder_binding in DCQL during VP submission for LDP_VC</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1988">#1988</a></td><td>Support require_cryptographic_holder_binding in DCQL during VP submission for SD-JWT VC</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1940">#1940</a></td><td>Remove presentation_definition Table</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2034">#2034</a></td><td>Replace acceptVPWithoutHolderProof with DCQL require_cryptographic_holder_binding in Verify UI</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1973">#1973</a></td><td>Enforce VP Request Expiry and Prevent Duplicate VP Submission on Server Side</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2049">#2049</a></td><td>Verify UI: Match Submitted Credentials Using DCQL type_values Instead of Configuration type</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/2043">#2043</a></td><td>Validate nonce and aud claims from Key Binding JWT (KB-JWT) for SD-JWT VP submissions</td></tr></tbody></table>

### **Known Issues**

Below is a list of some key known issues. For a detailed overview and the complete list of issues related to Inji Verify, please click [here](https://github.com/orgs/inji/projects/3/views/5?filterQuery=type%3ABug+-status%3ADone+-status%3ACancelled)

<table><thead><tr><th width="143.3359375">Issue ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://github.com/inji/inji-verify/issues/1845">#1845</a></td><td>We are uploading an invalid QR code, and while it displays an error message stating that the QR code is invalid, the credential details are still visible.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1844">#1844</a></td><td>On iPhone 8 and iPhone 7, uploading the Injiweb QR code PDF shows an error message.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1852">#1852</a></td><td>Inji Verify - Upload not functioning on Mac Safari Browser Versions 16 and below.</td></tr><tr><td><a href="https://github.com/inji/inji-verify/issues/1789">#1789</a></td><td>INJI Verify SDK should be able to support integration with applications built on platforms beyond <em>React (Typescript) applications</em>, such as Angular, PHP, and others.</td></tr></tbody></table>

### **Documentation**

* [Feature documentation](https://docs.inji.io/inji-verify/overview/features)
* [Integration Guide](https://docs.inji.io/inji-verify/technical-overview/integration-guides)
* [API Documentation](https://mosip.stoplight.io/studio/inji-verify)
* [Collab Guide](https://mosip.atlassian.net/wiki/spaces/PROD/pages/1306984580)
* QA Report
