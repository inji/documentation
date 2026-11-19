# Test Report

## Introduction <a href="#toc245975189" id="toc245975189"></a>

The scope of testing is to verify fitment to the specification from the perspective of Functionality, Configurability and Customizability. Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the Configurability and Extensibility of the software are also assessed. This ensures the readiness of the software for use in multiple countries and diverse identity ecosystems.

### Overview and Scope <a href="#toc245975190" id="toc245975190"></a>

Landing and discovery

* Home page
* Issuer listing, search, and credential-type selection
* Multi-issuer support

Issuance and download

* Authentication with user credentials (e-Signet / issuer login)
* Verifiable credential (VC) download
* PDF generation and auto-download
* SVG credential rendering
* SD-JWT and Claim 169 support

Wallet and storage

* Login with Google and passcode
* Durian data-storage integration
* Time-bound / expiry-based storage

Presentation and sharing

* OpenID4VP
* QR code sharing
* Authorization-endpoint discovery via the auth server’s well-known configuration

Platform

* Localization (languages and locale)
* Error handling

## Test Approach <a href="#toc245975191" id="toc245975191"></a>

The Functional verification of the Inji Web application is performed on Windows, Android and iOS platforms to ensure alignment with product specifications and business requirements. Analyzed with respect to functional stability, data integrity, and UI consistency. The validation adopts a persona-based testing strategy, simulating real-world user scenarios across diverse device matrices and multi-language configurations to ensure robustness in both online and offline environments.

* Functionality
* API & UI Automation
* Configurability&#x20;
* Customizability

## Test Organization <a href="#toc245975192" id="toc245975192"></a>

Table 1: Test Organization

<table><thead><tr><th width="186.875">Name</th><th>Functional Role</th><th>Responsibilities</th></tr></thead><tbody><tr><td><p>Nitin Hegde</p><p><br></p></td><td>Lead QA</td><td>Verifying the functionality, stability of the application, and report preparation.</td></tr><tr><td>Chaitanya K</td><td>QA Manager</td><td>Overviewing the test execution and review of the report.</td></tr></tbody></table>

### Test Planning <a href="#toc245975193" id="toc245975193"></a>

* Data Readiness: Verify that all required services are up and that identity schemas (UIN/VID) are correctly configured to support biometric and authentication flows.
* Coverage Distribution: Run test scenarios across a broad matrix of browsers on Windows and Mac, covering multiple user personas, to ensure complete end-to-end compatibility coverage.

### Browser Versions <a href="#toc245975194" id="toc245975194"></a>

Used the below browser versions in testing INJI WEB

* Chrome: Version 145.0.7632.160
* Firefox: Version 148.0 (64-bit)
* Edge: Version 145.0.3800.82
* Safari : Version 17

### Test Environment <a href="#toc245975195" id="toc245975195"></a>

Table 2: Test Environment

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Images (qainji env)</td></tr><tr><td valign="top">INJI Web - Injistackqa/ui-test:1.0.x</td></tr><tr><td valign="top">Injistackqa/inji-web:1.0.x</td></tr><tr><td valign="top">Injistackqa/apitest-mimoto:1.0.x</td></tr><tr><td valign="top">Injistackqa/mimoto:1.0.x</td></tr></tbody></table>

## Test Execution Report <a href="#toc245975196" id="toc245975196"></a>

### Test case execution summary <a href="#toc245975197" id="toc245975197"></a>

Table 3: Test Execution Summary

### Automation INJI Web UI

Table 4: UI Automation

<table><thead><tr><th>Total</th><th>Pass</th><th>Fail</th><th>Known Issues</th><th>Ignored</th></tr></thead><tbody><tr><td>26</td><td>26</td><td>0</td><td>0</td><td>0</td></tr><tr><td colspan="5">Test Rate: 100% With Pass Rate: 100%</td></tr></tbody></table>

### Automation INJI Web API Mimoto <a href="#toc245975199" id="toc245975199"></a>

Table 5: API Automation Result

<table><thead><tr><th>Total</th><th>Pass</th><th>Fail</th><th>Known Issues</th><th>Ignored</th></tr></thead><tbody><tr><td>397</td><td>361</td><td>0</td><td>3</td><td>33</td></tr><tr><td colspan="5">Test Rate: 90% With Pass Rate: 100%</td></tr></tbody></table>

## Defect Metrics <a href="#toc245975200" id="toc245975200"></a>

### Defect Metrics for the Release 1.0.0-RC1 <a href="#toc245975201" id="toc245975201"></a>

The following table depicts only the bugs which are found and not addressed in the current release.

Table 6: Defect Metrics for the Release

| Blocker | Critical | Major | Minor | Total |
| ------- | -------- | ----- | ----- | ----- |
| 0       | 0        | 5     | 0     | 5     |

### Known Issues Metrics <a href="#toc245975202" id="toc245975202"></a>

This section focuses on a separate category of issues that are known but not addressed in the current release. It provides a count and severity distribution for these defects across releases.

Table 7: Defect Metrics for the known issues

| Blocker | Critical | Major | Minor | Total |
| ------- | -------- | ----- | ----- | ----- |
| 0       | 0        | 60    | 28    | 88    |

## Conclusion <a href="#toc245975203" id="toc245975203"></a>

This section summarizes the key findings of test execution. It also provides a final QA recommendation on the build's readiness for release. The functional verification for Inji-web version 1.0.0-RC1 has been successfully completed. The testing cycle achieved a 100% execution rate with a 92% pass rate across a total of 1413 test cases. Additionally, API automation achieved a 100% pass rate.

While there are 5 open defects (0 Critical, 5 Major, 0 Minor) and 88 known issues in total, there are zero blocker defects identified. The application has demonstrated functional stability and data integrity consistent with product specifications.

### QA Approval <a href="#toc245975204" id="toc245975204"></a>

The build has successfully met the defined exit criteria and is recommended for release. The approval is based on the following satisfied conditions:

* Test Case Execution Completion: 100% of planned scenarios executed.
* Defect Status: No Blocker defects remain open.
* Documentation Sign-off: All test artifacts and reports are finalized.
* Test Environment Stability: The test environment remained stable throughout the execution cycle.

Table 8: Report is signed off details

| Name        | Functional Role | Responsibilities |
| ----------- | --------------- | ---------------- |
| Chaitanya K | QA Manager      | <p><br></p>      |
| Nitin Hegde | Lead QA         | <p><br></p>      |

## Appendix <a href="#toc245975205" id="toc245975205"></a>

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions <a href="#toc245975206" id="toc245975206"></a>

<table><thead><tr><th></th><th>Date</th><th>Author</th><th valign="top">Reviewers</th></tr></thead><tbody><tr><td>V1.0</td><td>15/11/2026</td><td>Nitin</td><td valign="top">Chaitanya K</td></tr></tbody></table>

\
Refer to the github link for more on reports [here](https://github.com/inji/test-management/tree/master/inji-web/1.0.0%20rc.1).
