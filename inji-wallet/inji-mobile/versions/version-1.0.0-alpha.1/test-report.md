# Test Report

## Introduction <a href="#toc250937750" id="toc250937750"></a>

The scope of testing is to verify fitment to the specification from the perspective of Functionality, Configurability, and Customizability. Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the Configurability and Extensibility of the software are also assessed.

### Overview and Scope <a href="#toc1371880611" id="toc1371880611"></a>

#### Authentication & Security <a href="#toc1065661593" id="toc1065661593"></a>

* Biometric unlock: Verify app access using device-registered biometrics (fingerprint/face) and the fallback to passcode if biometric disabled.
* Passcodes unlock: Validate the setup, verification of a numeric PIN for securing app access.
* Key Management: Validate the rotation of keys within the device with drag and drop options from the application.
* Wallet binding: Validate that the wallet binding (VC activation) and its credentials are securely bound to the specific device.
* Logout: Verify that logging out clears the active session and requires re-authentication to re-enter the application.

#### Credential Management (Download & Storage) <a href="#toc415012739" id="toc415012739"></a>

* VC download via MOSIP: Test fetching credentials using a UIN or VID with OTP authentication against the MOSIP backend.
* VC downloads via Sunbird: Test the successful download and rendering of credentials from Sunbird RC-based registries.
* Credential Offer: Test the end-to-end flow of receiving a credential offer via QR and initiating the issuance process.
* SD JWT VC download: Verify the download and selective disclosure capabilities of credentials in SD-JWT format.
* SVG VC download: Check the download and correct visual rendering of credentials using dynamic SVG templates defined by the issuer.
* Credential registry: Verify the wallet's ability to fetch and display trusted issuers and their metadata from the central registry.
* Backup and restore: Test the backup of credentials to cloud storage and their successful restoration on a new device.
* Deleting VC: Validate the permanent removal of a credential from the wallet and UI.

#### Credential Usage & Sharing <a href="#toc181396602" id="toc181396602"></a>

* BLE (offline) VC sharing: Share VCs offline using Bluetooth Low Energy with face auth and fingerprint biometric authentication.
* Pinning a VC: Verify the functionality to pin frequently used credentials to the top of the home screen for quick access.
* OpenID4VP: Test the online presentation and sharing of credentials to a verifier using the standard OpenID for Verifiable Presentations flow.
* QR code Login: Verify using the wallet to scan a QR code and authenticate user login for third-party Relying Parties.

#### User Experience & Navigation <a href="#toc1552042934" id="toc1552042934"></a>

* Multi-language support: Check UI rendering, label translations, and layout stability across all supported languages (Kannada, Hindi, Tamil, Arabic, Filipino, and English).
* Deep link navigation (same device flow): Verify that external links (e.g., inji://) correctly open the app and navigate to specific screens.

## Test Approach <a href="#toc328738645" id="toc328738645"></a>

The Functional verification of the Inji Mobile Wallet application is performed on Android and iOS platforms to ensure alignment with product specifications and business requirements. Analyzed with respect to functional stability, data integrity, and UI consistency.

* Functionality
* Configurability

## Test Organization <a href="#toc17829893" id="toc17829893"></a>

**Table**: Test Organization

| Name        | Functional Role | Responsibilities                                                                |
| ----------- | --------------- | ------------------------------------------------------------------------------- |
| Nitin Hegde | QA Lead         | Verify the functionality, stability of the application, and report preparation. |
| Chaitanya K | QA Manager      | Reviewing the test execution and review of the report.                          |

### Test Planning <a href="#toc17829895" id="toc17829895"></a>

* Data Readiness: Validate the availability of all services along with configured identity schemas (UIN/VID) to support biometric and authentication flows.
* Data Strategy: Refresh test data for every cycle by generating new QR codes for credential offers and preparing specific datasets for Sunbird/e-Signet integrations.

### Test Devices <a href="#toc1392557050" id="toc1392557050"></a>

**Table**: Test Devices

| Device Model     | OS and BLE version |
| ---------------- | ------------------ |
| iPhone 13        | iOS 26.6 BLE 5.0   |
| Realme GT NEO 3T | Android BLE 5.2    |

### Test Environment <a href="#toc1366738592" id="toc1366738592"></a>

Table: Test Environment

<table><thead><tr><th valign="top">Images (qainji env)</th></tr></thead><tbody><tr><td valign="top">injistackqa/inji-verify-service:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-verify-ui:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-certify-with-plugins:1.0.x</td></tr><tr><td valign="top">injistackqa/mimoto:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-web:1.0.x</td></tr></tbody></table>



<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Images (released env)</td></tr><tr><td valign="top">injistack/inji-verify-service:0.18.2</td></tr><tr><td valign="top">injistack/inji-verify-ui:0.18.2</td></tr><tr><td valign="top">injistack/inji-certify-with-plugins:0.14.0</td></tr><tr><td valign="top">injistack/mimoto:0.22.0</td></tr><tr><td valign="top">injistack/inji-web:0.17.0</td></tr><tr><td valign="top">injistack/inji-certify-with-plugins:0.14.0</td></tr><tr><td valign="top">mosipid/authentication-service:1.3.0</td></tr><tr><td valign="top">mosipid/authentication-internal-service:1.3.0</td></tr><tr><td valign="top">mosipid/authentication-otp-service:1.3.0</td></tr><tr><td valign="top">mosipid/kernel-notification-service:1.3.0</td></tr><tr><td valign="top">mosipid/pre-registration-application-service:1.3.0</td></tr></tbody></table>

## Test Execution Report <a href="#toc886927487" id="toc886927487"></a>

### Test case execution summary <a href="#toc163916210" id="toc163916210"></a>

Smoke testing and feature health verification were successfully completed across both Android and iOS platforms. No critical or blocker issues were identified during execution, confirming the overall stability of the build for further testing.

## Defect Metrics <a href="#toc1325625512" id="toc1325625512"></a>

### Known Issues <a href="#toc386987297" id="toc386987297"></a>

This section focuses on the known issues list for the alpha release

Known issue Link - [1.0.0-alpha.1 Known issues Inji wallet](https://github.com/inji/inji-wallet/issues?q=state%3Aopen%20label%3Abug)

## Conclusion <a href="#toc500452841" id="toc500452841"></a>

Smoke testing and feature health verification for Inji Mobile Wallet v1.0.0-alpha.1 were successfully completed across both Android and iOS platforms. The verification covered the core application functionalities, and no critical or blocker defects were identified during execution. The build demonstrated stable behavior across the validated features.

Based on the smoke testing and feature health verification results, the Inji Mobile Wallet v1.0.0-alpha.1 build is considered stable and is recommended for release. The remaining known issues will continue to be tracked and addressed as part of the planned release of roadmap and future iterations.

### QA Approval <a href="#toc1381116270" id="toc1381116270"></a>

The build has successfully met the defined exit criteria and is recommended for release. The approval is based on the following conditions:

* Test Case Execution Completion: 100% of planned scenarios executed.
* Defect Status: No Blocker defects remain open.
* Documentation Sign-off: All test artifacts and reports are finalized.
* Test Environment Stability: The test environment remained stable throughout the execution cycle.



**Table**: Report is signed off details

| Name        | Functional Role | Responsibilities                                       |
| ----------- | --------------- | ------------------------------------------------------ |
| Chaitanya K | QA Manager      | Reviewing the test execution and review of the report. |

## Appendix <a href="#toc1856887429" id="toc1856887429"></a>

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions <a href="#toc287951299" id="toc287951299"></a>

<table><thead><tr><th>Version</th><th>Date</th><th>Author</th><th valign="top">Reviewers</th></tr></thead><tbody><tr><td>V2.0</td><td>04/08/2026</td><td>Nitin Hegde</td><td valign="top"><p>Chaitanya K</p><p><br></p></td></tr></tbody></table>

### Appendix B: Acronyms <a href="#toc28332269" id="toc28332269"></a>

| Acronym   | Literal Translation                   |
| --------- | ------------------------------------- |
| MOSIP     | Modular Open Source Identity Platform |
| UIN       | Unique Identification Number          |
| VID       | Virtual Identification                |
| SVG       | Scalable Vector Graphics              |
| SD-JWT    | Selective Disclosure - JSON Web Token |
| VC        | Verifiable Credentials                |
| OpenID4VP | OpenID for Verifiable Presentations   |
| PDI       | Presentation During Issuance          |

### Document History

It outlines the strategy used to ensure a comprehensive evaluation.

<table><thead><tr><th>Version</th><th>Author</th><th>Date</th><th valign="top">Review</th><th valign="top">Affected Sections</th></tr></thead><tbody><tr><td>V2.0</td><td>Nitin</td><td>04/08/2026</td><td valign="top">Chaitanya Kesiraju</td><td valign="top">Updated for release 1.0.0-alpha.1</td></tr></tbody></table>

