# Test Report

## Introduction <a href="#wd3np1tby5qm" id="wd3np1tby5qm"></a>

The scope of testing is to verify fitment to the specification from the perspective of Functionality, Configurability and Customizability. Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the Configurability and Extensibility of the software are also assessed. This ensures the readiness of the software for use in multiple countries and diverse identity ecosystems.

### Overview and Scope <a href="#uaew48h2zsu3" id="uaew48h2zsu3"></a>

Authentication & Security

* Verifier Authentication: Validate login, logout, session management, and re-authentication.
* DID-based Client Authentication: Verify decentralized\_identifier client\_id and DID validation.
* VP Request Security: Validate server-side VP request expiry, nonce validation, and duplicate VP submission prevention.

Authentication & Security

* Verifier Authentication: Validate login, logout, session management, and re-authentication.
* DID-based Client Authentication: Verify decentralized\_identifier client\_id and DID validation.
* VP Request Security: Validate server-side VP request expiry, nonce validation, and duplicate VP submission prevention.

Verification Request Management

* Authorization Request: Validate OpenID4VP Authorization Request generation.
* QR Code & Deep Link: Verify QR code and deep link generation for wallet verification.
* VP Session Management: Validate VP session creation, retrieval, and status updates.

Credential Verification

* DCQL Processing: Validate DCQL query processing and credential matching using type\_values.
* Credential Formats: Verify SD-JWT VC, LDP VC, and DC+SD-JWT credential verification.
* Holder Binding: Validate cryptographic holder binding and selective disclosure.

OpenID4VP Compliance

* Client Metadata: Validate vp\_formats\_supported, ldp\_vc, and updated OpenID4VP v1.0 client metadata.
* Protocol Compliance: Verify Authorization Request and VP Response compliance with OpenID4VP v1.0.

Verification Results & Error Handling

* Verification Results: Validate verification status, verified claims, and audit logging.
* Error Handling: Verify protocol-compliant error responses for invalid client IDs, expired requests, duplicate submissions, invalid nonce, and malformed VP tokens.

## Test Approach <a href="#id-2qybi3rytw2o" id="id-2qybi3rytw2o"></a>

The Functional verification of the Inji verify application is performed on Android and iOS platforms to ensure alignment with product specifications and business requirements. Analyzed with respect to functional stability, data integrity, and UI consistency. The validation adopts a persona-based testing strategy, simulating real-world user scenarios across diverse device matrices and multi-language configurations to ensure robustness in both online and offline environments.

* Functionality

## Test Organization <a href="#v93b1k5n5t1" id="v93b1k5n5t1"></a>

**Table**: Test Organization

<table><thead><tr><th width="148.27734375">Name</th><th width="198.5625">Functional Role</th><th>Responsibilities</th></tr></thead><tbody><tr><td><p>Nitin</p><p><br></p></td><td>QA Lead Engineer</td><td>Verifying the functionality, stability of the application,and report preparation. and performing combination testing.</td></tr><tr><td>Chaitanya K</td><td>QA Manager</td><td>Overviewing the test execution and review of the report.</td></tr></tbody></table>

### Test Planning <a href="#w4q9wuyu11ck" id="w4q9wuyu11ck"></a>

* Data Readiness: Validate the availability of all services along with configured identity schemas (UIN/VID) to support biometric and authentication flows.
* Data Strategy: Refresh test data for every cycle by generating new QR codes.
* Coverage Distribution: Execute test scenarios across a broad matrix of browsers on Windows, Android, and iOS devices, spanning multiple user personas to ensure end-to-end compatibility coverage.

### Test Devices <a href="#id-4ea1uhu0zvs3" id="id-4ea1uhu0zvs3"></a>

Table: Test Devices

| Device Model             | OS and BLE version |
| ------------------------ | ------------------ |
| iPhone 11                | iOS 26.1 BLE 5.0   |
| ONE PLUS 12R             | Android 15 BLE 5.3 |
| Xiaomi Redmi NOTE 13 Pro | Android 15 BLE 5.2 |

### Browser Versions <a href="#id-14ch9gnz4owd" id="id-14ch9gnz4owd"></a>

Used the below browser versions in testing INJI Verify

* Chrome: Version 123.0.6312.124
* Firefox: Version 125.0.1
* Edge: Version 124.0.2478.51
* Safari : Version 17

### Test Environment <a href="#li5do5ohq2bq" id="li5do5ohq2bq"></a>

Table: Test Environment

<table><thead><tr><th valign="top">Images (qainji env)</th></tr></thead><tbody><tr><td valign="top">injistackqa/inji-verify-service:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-verify-ui:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-certify-with-plugins:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-web:develop</td></tr></tbody></table>

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Images (released env)</td></tr><tr><td valign="top">injistack/apitest-mimoto:0.22.0</td></tr><tr><td valign="top">injistack /inji-verify-service:0.18.2</td></tr><tr><td valign="top">injistack /inji-verify-ui:0.18.2</td></tr><tr><td valign="top">injistackqa/inji-certify-with-plugins:0.14.0</td></tr><tr><td valign="top">mosipid/authentication-demo-service:1.2.0.1</td></tr><tr><td valign="top">mosipid/authentication-internal-service:1.3.0</td></tr><tr><td valign="top">mosipid /authentication-otp-service:1.3.0</td></tr></tbody></table>

## Test Execution Report <a href="#y1trhgcl1nny" id="y1trhgcl1nny"></a>

### Automation INJI Verify API <a href="#id-6k5d1f5l24k" id="id-6k5d1f5l24k"></a>

Table: API Automation Result

<table><thead><tr><th width="281.9140625">Total</th><th>Pass</th><th>Fail</th><th>Known Issues</th><th>Ignored</th></tr></thead><tbody><tr><td>204</td><td>204</td><td>0</td><td>0</td><td>0</td></tr><tr><td>Test Rate: 100% With Pass Rate: 100%</td><td></td><td></td><td></td><td></td></tr></tbody></table>

## Defect Metrics <a href="#bad9uqj4llpt" id="bad9uqj4llpt"></a>

### Known Issues Metrics <a href="#id-6qvk948pt1gf" id="id-6qvk948pt1gf"></a>

This section focuses on the known issues list

For a detailed overview and the complete list of issues related to Inji Verify, please click[ ](https://github.com/inji/inji-verify/issues?q=type%3ABug%20-milestone%3A1.0.0-alpha.1%20-is%3Aclosed)[here](https://github.com/inji/inji-verify/issues?q=type%3ABug%20-milestone%3A1.0.0-alpha.1%20-is%3Aclosed).

## Conclusion <a href="#id-2phijwbj3v0y" id="id-2phijwbj3v0y"></a>

Smoke testing and feature health verification for INJI Verify v1.0.0-alpha.1 were successfully completed. The verification covered the core verifier functionalities, including OpenID4VP authorization request generation, VP session management, credential verification, DCQL processing, client metadata validation, and end-to-end verification flows. No critical or blocker defects were identified during execution, and the build demonstrated stable behavior across the validated features.

Based on the smoke testing and feature health verification results, the INJI Verify v1.0.0-alpha.1 build is considered stable and is recommended for release. Any remaining known issues will continue to be tracked and addressed as part of the planned release roadmap and future iterations.

### QA Approval <a href="#ilmt46bbaytj" id="ilmt46bbaytj"></a>

The build has successfully met the defined exit criteria and is recommended for release. The approval is based on the following satisfied conditions:

* Test Case Execution Completion: 100% of planned scenarios executed.
* Defect Status: No Blocker defects remain open.
* Documentation Sign-off: All test artifacts and reports are finalized.
* Test Environment Stability: The test environment remained stable throughout the execution cycle.

Table: Report is signed off details

| Name        | Functional Role |                                                          |
| ----------- | --------------- | -------------------------------------------------------- |
| Chaitanya K | QA Manager      | Overviewing the test execution and review of the report. |

## Appendix <a href="#yh1dble9a14s" id="yh1dble9a14s"></a>

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions <a href="#cpic2cg3cg36" id="cpic2cg3cg36"></a>

<table><thead><tr><th>Version</th><th>Date</th><th>Author</th><th valign="top">Reviewers</th></tr></thead><tbody><tr><td>V1.0</td><td>04/08/2026</td><td>Nitin</td><td valign="top">Chaitanya K</td></tr></tbody></table>

### Document History

It outlines the strategy used to ensure a comprehensive evaluation.

<table><thead><tr><th>Version</th><th>Author</th><th>Date</th><th valign="top">Review</th><th valign="top">Affected Sections</th></tr></thead><tbody><tr><td>V1.0</td><td>Nitin Hegde</td><td>04/08/2026</td><td valign="top">Chaitanya Kesiraju</td><td valign="top">New Document</td></tr></tbody></table>

Github link for more on reports is [here](https://github.com/inji/test-management/tree/master/inji-verify/1.0.0-alpha.1).\
<br>
