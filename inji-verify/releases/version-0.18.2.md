# Version 0.18.2

**Release Name**: Inji Verify v0.18.2

**Support**: Developer Release

**Release Date**: <mark style="color:red;">**Coming Soon!**</mark>

### **Overview**

We are excited to announce the release of **Inji Verify v0.18.2.**

This release (**v0.18.2**) is a **patch update** focused on giving ability to configure verify-service to generate an additional library JAR

It does **not introduce new features**, but improves stability, correctness, and reliability of existing functionality in the Inji Verify module.

**Note:** The Inji Verify UI is a _reference implementation_ to demonstrate orchestration. Developers can selectively embed SDK components in the verifier applications as per their needs.

### **Repositories: Released/Dependent**

| **Repositories** | **Tags: Released/Dependent** |
| ---------------- | ---------------------------- |
| Inji Verify      | **v0.18.2**                  |

#### **Projects: Released**

**Inji Verify Repo** as below:

i) inji-verify-service - [https://github.com/inji/inji-verify/tree/release-0.18.x](https://github.com/inji/inji-verify/tree/release-0.18.x)

#### &#x20;**Compatible modules:**

The following table outlines the tested and certified compatibility of Inji Verify 0.18.2 with other modules.

| **Module**         | **Version**                                                                 |
| ------------------ | --------------------------------------------------------------------------- |
| Inji Wallet        | 0.22.1                                                                      |
| Inji Web           | [0.](https://docs.inji.io/inji-wallet/inji-web/inji-web/version-0.16.0)17.0 |
| Pixel-Pass library | [0.8.0](https://docs.inji.io/inji-verify/releases/version-0.17.0)           |

#### &#x20;**Bug Fixes**

Below is the list of fixes as part of the **0.18.2** release:

**Query**: [https://github.com/orgs/inji/projects/3/views/7?filterQuery=milestone%3A0.18.2\&visibleFields=%5B%22Title%22%2C%22Type%22%2C%22Status%22%2C263064096%2C%22Assignees%22%2C346208867%2C342689860%2C346206438%5D](https://github.com/orgs/inji/projects/3/views/7?filterQuery=milestone%3A0.18.2\&visibleFields=%5B%22Title%22%2C%22Type%22%2C%22Status%22%2C263064096%2C%22Assignees%22%2C346208867%2C342689860%2C346206438%5D)

| **Key**                                                  | **Summary**                                                              |
| -------------------------------------------------------- | ------------------------------------------------------------------------ |
| [#2099](https://github.com/inji/inji-verify/issues/2099) | Configure verify-service to generate an additional library JAR - v0.18.2 |

#### **Known Issues**

Below is a list of some key known issues. For a detailed overview and the complete list of issues related to Inji Verify, please click [here](https://github.com/orgs/inji/projects/3/views/5)

| **Jira ID**                                                                                        | **Description**                                                                                                                                                                                                                                                                                                                                                                  |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [https://github.com/inji/inji-verify/issues/1790](https://github.com/inji/inji-verify/issues/1790) | The OpenID4VP (Cross device) component in Inji Verify currently validates a presentation as successful even when a wrong Verifiable Credential (VC) is submitted. As a temporary workaround, implement credential type validation on the Relaying Party (RP) side, by verifying that the received VC matches the expected type defined in the original presentation\_definition. |
| [https://github.com/inji/inji-verify/issues/1845](https://github.com/inji/inji-verify/issues/1845) | We are uploading an invalid QR code, and while it displays an error message stating that the QR code is invalid, the credential details are still visible.                                                                                                                                                                                                                       |
| [https://github.com/inji/inji-verify/issues/1844](https://github.com/inji/inji-verify/issues/1844) | On iPhone 8 and iPhone 7, uploading the Injiweb QR code PDF shows an error message.                                                                                                                                                                                                                                                                                              |
| [https://github.com/inji/inji-verify/issues/1852](https://github.com/inji/inji-verify/issues/1852) | Inji Verify - Upload not functioning on Mac Safari Browser Versions 16 and below.                                                                                                                                                                                                                                                                                                |
| [https://github.com/inji/inji-verify/issues/1789](https://github.com/inji/inji-verify/issues/1789) | INJI Verify SDK should be able to support integration with applications built on platforms beyond _React (Typescript) applications_, such as Angular, PHP, and others.                                                                                                                                                                                                           |
| [https://github.com/inji/inji-verify/issues/1805](https://github.com/inji/inji-verify/issues/1805) | Long-polling listeners are implemented within the service layer, preventing the backend from scaling effectively in a multi-pod (distributed) environment.                                                                                                                                                                                                                       |

### **Documentation**

* [Feature documentation](https://docs.inji.io/inji-verify/overview/features)
* [Integration Guide](https://docs.inji.io/inji-verify/technical-overview/integration-guides)
* [API Documentation](https://mosip.stoplight.io/studio/inji-verify)
* [Collab Guide](https://mosip.atlassian.net/wiki/spaces/PROD/pages/1306984580)
* QA Report
