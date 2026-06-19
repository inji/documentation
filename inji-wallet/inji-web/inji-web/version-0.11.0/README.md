# Version 0.11.0

**Release Name:** Inji Web 0.11.0

**Support:** Developer

**Release Date:** 29th Jan, 2025

### **Overview**

This release introduces several enhancements, new features, aimed at improving the functionality, security, and user experience of the platform. Key objectives include secure time-bound storage, and UI updates to align with new branding standards.

### **Major Highlights/Features**

* **Secure Time-Bound Storage**: Introduced functionality to set validity periods for credentials before download, ensuring secure and controlled access to stored data.
* **VC Verification During Download**:
  * **RSA VC Verification**: For verifying RSA-based Verifiable Credentials before download within the Inji Web Wallet.
  * **EdDSA VC Verification**: Integrated VC Verifier SDK to enable seamless verification of EdDSA-based Verifiable Credentials during downloads.
* **Mimoto Enhancements and Additions**
  * Trusted Verifiers API - Introduced the Trusted Verifiers API to enhance the verification process and enable secure interaction with trusted verifiers.
  * Main Branch Renamed - The “**Main branch**” in the Mimoto repository has been renamed to “**Master Branch”** for consistency and improved repository management.
  * mDoc VC Format Support - Added support for the mDoc Verifiable Credential (VC) format, allowing seamless integration and verification of mdoc credentials.
  * **Compatibility and Availability**
    * These enhancements are currently available for testing and building using the **Inji Mobile Wallet**.
    * Support for **Inji Web** will be introduced in upcoming releases.
    * Fully compatible with **Inji Mobile Wallet v0.15.0 onwards**, which is part of the ongoing release pipeline.

### **Enhancements**

**Security Fixes**

* All critical security issues addressed and resolved.
* Sonar issues fixed, with the Sonar report.

**UI Enhancements**

* **Inji Web Wallet Home Page**:
  * Incorporated new branding changes for a modern and enhanced user experience.
  * Ensured a fully responsive design for seamless access across devices.
  * Implemented a comprehensive FAQ section for an improved and readily available answers to frequently asked questions.

### **Bugs Fixes**

Below is the [**list**](https://mosip.atlassian.net/issues/INJIWEB-1024?jql=project%20%3D%20%22Inji%20Web%22%20AND%20fixversion%20IN%20%281.0.0%2C%200.11.0%29%20AND%20type%20%3D%20Bug%20ORDER%20BY%20created%20DESC) of fixes as part of the **0.11.0** release:

<table><thead><tr><th width="230">Jira issue</th><th>Issue description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1000"><strong>Inji Web-1000</strong></a></td><td>Inji Web: Could not open help and About Inji pages in mobile phone</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1024"><strong>Inji Web-1024</strong></a></td><td>Inji Web: zerotimes and maximum limit(1000000000) are not properly handled while downloading the VC</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1001"><strong>Inji Web-1001</strong></a></td><td>Inji Web: Overlapping observed for credentials when opened in mobile phone</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-966"><strong>Inji Web-966</strong></a></td><td>Inji Web: For Hindi full stop observed like "।" and also "." in FAQ page</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-965"><strong>Inji Web-965</strong></a></td><td>Inji Web: In some languages in the last FAQ Online Sharing translating to selected lang but not the Embedded VC</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-876"><strong>Inji Web-876</strong></a></td><td>Inji Web: Intermediately We are not able to download the Sunbird VC in Inji Web</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-762"><strong>Inji Web-762</strong></a></td><td>Inji Web: Error description is not proper when the record is not available in durian</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-761"><strong>Inji Web-761</strong></a></td><td>Inji Web: Cientid is different and redirect URI are from different domains</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-661"><strong>Inji Web-661</strong></a></td><td>Security testing: Inji web - DEBUG mode is set in mosip-config</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-657"><strong>Inji Web-657</strong></a></td><td>Security testing: Inji web UI landing page is not fully visible, the footer blocks the view of partners</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-655"><strong>Inji Web-655</strong></a></td><td>Security testing: Inji web - blank page error response during URL tampering</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-651"><strong>Inji Web-651</strong></a></td><td>snyk dependency analysis: Inji web (develop)</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-650"><strong>Inji Web-650</strong></a></td><td>Security hotspot on Inji Web: develop branch</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-625"><strong>Inji Web-625</strong></a></td><td>Inji - QR code generated in Inji Web and in Inji Mobile are not matching</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-599"><strong>Inji Web-599</strong></a></td><td>Inji Web: Getting invalid credentials error message for valid data, when we leave authentication page idle for sometime</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-290"><strong>Inji Web-290</strong></a></td><td>Inji Web: QR code is not working on VC card</td></tr></tbody></table>

### **Known Open Bugs**

Below is the list of **known** issues. To read in detail click [**here**](https://mosip.atlassian.net/issues/?jql=project%3D%22Inji%20Web%22%20and%20type%20in%20%28bug%29%20and%20status%20not%20in%20%28closed%2C%20canceled%29%20order%20by%20created%20DESC)**.**

<table><thead><tr><th width="229">Jira ID</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-625"><strong>Inji Web-625</strong></a></td><td>Inji - QR code generated in Inji Web and in Inji Mobile are not matching.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1148"><strong>Inji Web-1148</strong></a></td><td>Inji Web: In Arabic lang, consent option strings and buttons are overlapping in tablet portrait mode</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1146"><strong>Inji Web-1146</strong></a></td><td>Inji Web: In Arabic lang, lang selection option is not properly aligned in in tablet portrait mode</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1144"><strong>Inji Web-1144</strong></a></td><td>Inji Web: Scroll down on share visibility page working as back button</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1143"><strong>Inji Web-1143</strong></a></td><td>Inji Web: On share visibility if click on outside page dropdowns are selected in tablet</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1142"><strong>Inji Web-1142</strong></a></td><td>Inji Web: Credentials search bar is not properly aligned in tablet view</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-966"><strong>Inji Web-966</strong></a></td><td>Inji Web: For Hindi full stop observed like "।" and also "." in FAQ page</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-965"><strong>Inji Web-965</strong></a></td><td>Inji Web: In some languages in the last FAQ Online Sharing translating to selected lang but not the Embedded VC.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-626"><strong>Inji Web-626</strong></a></td><td>Inji Web: Field values in json decoded from CBOR and the values in VC PDF are different</td></tr></tbody></table>

### **Compatible Modules**

The following table outlines the tested and certified compatibility of **Inji Web 0.11.0** with other modules.

| Module           | Version                                                          |
| ---------------- | ---------------------------------------------------------------- |
| **eSignet**      | [**v1.4.1**](https://github.com/mosip/esignet/tree/v1.4.1)       |
| **Inji Verify**  | [**v0.10.0**](https://github.com/mosip/inji-verify/tree/v0.10.0) |
| **Inji Certify** | [**v.0.9.1**](https://github.com/mosip/inji-certify/tree/v0.9.1) |

### **Repositories Released**

| Repositories           | Tags Released                                                                |
| ---------------------- | ---------------------------------------------------------------------------- |
| **Inji-web**           | [**v0.11.0**](https://github.com/mosip/inji-web/tree/v0.11.0)                |
| **mimoto**             | [**v0.15.0**](https://github.com/mosip/mimoto/tree/v0.15.0)                  |
| **Inji-config**        | [**v0.4.0**](https://github.com/mosip/inji-config/tree/v0.4.0)               |
| **vc-verifier**        | [**v1.1.0-beta.1**](https://github.com/mosip/vc-verifier/tree/V1.1.0-beta.1) |
| **durian(data share)** | [**v1.3.0-beta.2**](https://github.com/mosip/durian/tree/1.3.0-beta.2)       |

### Documentation

* [**Build and Deployment**](../../build-and-deploy/)
* [**Feature Documentation**](https://docs.mosip.io/inji/inji-web/functional-overview/features)
* [**User Guide**](https://docs.mosip.io/inji/inji-web/functional-overview/end-user-guide)
* [**QA Report**](https://docs.inji.io/inji-wallet/inji-web/inji-web/version-0.11.0/test-report)
* [**API Documentation**](https://docs.mosip.io/inji/inji-web/technical-overview/backend-services/mimoto-bff)
