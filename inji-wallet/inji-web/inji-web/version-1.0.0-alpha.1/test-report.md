# Test Report

### Introduction

The scope of testing is to verify fitment to the specification from the perspective of **Functionality, Configurability and Customizability**.

Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the Configurability and Extensibility of the software are also assessed.

This ensures the readiness of the software for use in multiple countries and diverse identity ecosystems.

### Overview and Scope

The functional verification covers the following areas:

* Inji Home page
* Issuer and Credential selection
* Authenticating with user credentials
* PDF Generation and Auto download
* Retrieve Issuers and Credential list
* Downloading VC
* Multi languages support
* Error Handling
* Issuers support
* QR Code
* Durian data storage integration
* Login with Google and Passcode
* OpenID4VP Implementation and DCQL-Based VP Request
* Secure Time Bound Storage
* Locale Support
* Authorization endpoint discovery through auth server well-known
* SD-JWT support
* SVG Support
* Claim 169

### Test Approach

The functional verification of the Inji Web application is performed on **Windows, Android and iOS** platforms to ensure alignment with product specifications and business requirements.

The application is analyzed with respect to:

* Functional stability
* Data integrity
* UI consistency

The validation adopts a **persona-based testing strategy**, simulating real-world user scenarios across diverse device matrices and multi-language configurations to ensure robustness in both online and offline environments.

#### Test Areas

* Functionality
* API & UI Automation
* Configurability

### Test Organization

#### Table 1: Test Organization

| Name        | Functional Role | Responsibilities                                                                   |
| ----------- | --------------- | ---------------------------------------------------------------------------------- |
| Mrudula     | QA Engineer     | Verifying the functionality, stability of the application, and report preparation. |
| Chaitanya K | QA Manager      | Overviewing the test execution and review of the report.                           |

### Test Planning

#### Data Readiness

Validate the availability of all services along with configured identity schemas (**UIN/VID**) to support biometric and authentication flows.

#### Coverage Distribution

Execute test scenarios across a broad matrix of browsers on Windows and Mac systems, spanning multiple user personas to ensure end-to-end compatibility.

### Browser Versions

The following browser version was used for testing Inji Web:

* **Chrome:** Version 151.0.7922.138

### Test Environment

#### Table 2: Test Environment

| Images (qainji env)                    |
| -------------------------------------- |
| `INJI Web - Injistackqa/ui-test:1.0.x` |
| `injistackqa/inji-web:1.0.x`           |
| `Injistackqa/apitest-mimoto:1.0.x`     |
| `injistackqa/mimoto:1.0.x`             |

### Known Issues Metrics

This section focuses on the known issues list for the alpha release.

**Known issue link:** Issues · inji/inji-web

### Conclusion

This section summarizes the key findings of test execution and provides a final QA recommendation on the build's readiness for release.

The functional verification for **Inji Web 1.0.0-alpha.1** has been successfully completed.

### QA Approval

The build has successfully met the defined exit criteria and is **recommended for release**.

The approval is based on the following satisfied conditions:

* **Test Case Execution Completion:** 100% of planned scenarios executed.
* **Defect Status:** No Blocker defects remain open.
* **Documentation Sign-off:** All test artifacts and reports are finalized.
* **Test Environment Stability:** The test environment remained stable throughout the execution cycle.

#### Table 8: Report Sign-off Details

| Name        | Functional Role | Responsibilities                                         |
| ----------- | --------------- | -------------------------------------------------------- |
| Chaitanya K | QA Manager      | Overviewing the test execution and review of the report. |

## Appendix

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions

It outlines the strategy used to ensure a comprehensive evaluation.

<table><thead><tr><th>Version</th><th>Date</th><th>Author</th><th width="187">Reviewers</th></tr></thead><tbody><tr><td>V1.0</td><td>14/8/2026</td><td>Mrudula</td><td>Chaitanya K</td></tr></tbody></table>

