# Test Report

## Introduction <a href="#toc245855783" id="toc245855783"></a>

The scope of testing is to verify fitment to the specification from the perspective of Functionality, Configurability and Customizability. Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the Configurability and Extensibility of the software are also assessed. This ensures the readiness of the software for use in multiple countries and diverse identity ecosystems.

### Overview and Scope <a href="#toc245855784" id="toc245855784"></a>

Testing scope has been focused on the following features:

* Inji certify Docker compose testing (Data provider CSV plugin, Data provider Postgres plugin)
* Insurance, MosipId and Mock (Issuance and Data provider (Postgres plugin)), which covered Land registry, school and Farmer use case
* Integration with Inji Web and Inji verify
* DB upgrade scripts testing, Backward compatibility - from Docker setup
* Preauthcode
* Presentation during issuance
* Claim 169
* Mdoc mdl format

## Test Approach <a href="#toc245855785" id="toc245855785"></a>

The Functional verification of the Inji Certify service is performed against its credential issuance APIs to ensure alignment with product specifications and business requirements. It is analyzed for functional stability, data integrity, and consistent API behavior. Validation follows a use-case-based testing strategy, simulating real-world issuance scenarios so that credentials are issued correctly and reliably.

* Functionality
* Combination
* Configurability
* Customizability

## Test Organization <a href="#toc245855786" id="toc245855786"></a>

**Table 1**: Test Organization

| Name        | Functional Role | Responsibilities                                                                     |
| ----------- | --------------- | ------------------------------------------------------------------------------------ |
| Nitin Hegde | QA Lead         | Verifying the functionality, Automation scenarios development and report preparation |
| Chaitanya K | QA Manager      | Overviewing the test execution and review of the report.                             |

### Test Planning <a href="#toc245855787" id="toc245855787"></a>

* Data Readiness: Validate the availability of all services along with configured identity schemas (UIN/VID) to authentication flows.

### Test Environment <a href="#toc245855788" id="toc245855788"></a>

**Table 2**: Test Environment

| Tested on qainji env with components                 |
| ---------------------------------------------------- |
| injistackqa/inji-certify-with-plugins:1.0.x          |
| injistackqa/inji-web:1.0.x                           |
| injistackqa/mimoto:1.0.x                             |
| injistackqa/inji-verify-service:1.0.x                |
| injistack/inji-verify-ui:1.0.0-rc.1                  |
| nginx                                                |
| mosipid/softhsm:v2                                   |
| mosipid/kernel-config-server:1.3.0                   |
| mosipqa/postgres-init:develop                        |
| injistackqa/apitest-inji-certify:1.0.x               |
| Authorization from released env with components      |
| mosipid/credential-service:1.3.1                     |
| mosipid/data-share-service:1.3.1                     |
| mosipid/data-share-service:1.3.0-beta.2              |
| mosipid/digital-card-service:1.3.0                   |
| mosipid/esignet-with-plugins:1.8.0                   |
| mosipid/mock-identity-system:0.13.0                  |
| sunbird-rc/sunbird-rc-core:v1.0.0                    |
| sunbird-rc/sunbird-rc-credential-schema:v2.0.0-rc3   |
| sunbird-rc/sunbird-rc-credentials-service:v2.0.0-rc3 |
| sunbird-rc/sunbird-rc-identity-service:v2.0.0-rc3    |

## Test Execution Report <a href="#toc245855789" id="toc245855789"></a>

### Test case execution summary <a href="#toc245855790" id="toc245855790"></a>

Manual Test Execution was completed in qainji env achieving a 100% execution rate for all planned scenarios. The testing validated core functionalities with a high pass rate, while identified issues on both platforms have been logged for defect resolution.

Table 3: Test Execution Summary

| Total | Pass | Fail | Skip |
| ----- | ---- | ---- | ---- |
| 1199  | 1180 | 19   | 0    |

### Feature health

### Automation Result <a href="#toc245855791" id="toc245855791"></a>

* Sunbird use case

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Total</td><td>Passed</td><td>Failed</td><td>Ignored</td><td>Known issues</td></tr><tr><td>626</td><td>55</td><td>0</td><td>551</td><td>20</td></tr><tr><td colspan="5">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

* Mock Use case

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Total</td><td>Passed</td><td>Failed</td><td>Ignored</td><td>Known issues</td></tr><tr><td>626</td><td>28</td><td>0</td><td>578</td><td>20</td></tr><tr><td colspan="5">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

* Mock (Data provider) Land registry Use case

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Total</td><td>Passed</td><td>Failed</td><td>Ignored</td><td>Known issues</td></tr><tr><td>626</td><td>322</td><td>0</td><td>284</td><td>20</td></tr><tr><td colspan="5">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

* MosipId Use case

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Total</td><td>Passed</td><td>Failed</td><td>Ignored</td><td>Known issues</td></tr><tr><td>626</td><td>99</td><td>0</td><td>507</td><td>20</td></tr><tr><td colspan="5">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

* Preauth code(academic) Use case

| Total | Passed | Failed | Ignored | Known issues |
| ----- | ------ | ------ | ------- | ------------ |
| 626   | 35     | 0      | 571     | 20           |

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

* PDI (mdoc) Use case

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Total</td><td>Passed</td><td>Failed</td><td>Ignored</td><td>Known issues</td></tr><tr><td>626</td><td>44</td><td>0</td><td>562</td><td>20</td></tr><tr><td colspan="5">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

* Mdoc mdl Use case

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th></th><th></th></tr></thead><tbody><tr><td>Total</td><td>Passed</td><td>Failed</td><td>Ignored</td><td>Known issues</td></tr><tr><td>626</td><td>34</td><td>0</td><td>572</td><td>20</td></tr><tr><td colspan="5">Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td></tr></tbody></table>

## Defect Metrics <a href="#toc245855792" id="toc245855792"></a>

### Defect Metrics for the Release rc.1 <a href="#toc245855793" id="toc245855793"></a>

The following table depicts only the bugs which are found and not addressed in the current release.

Table 4: Defect Metrics for the Release

| Blocker | Critical | Major | Minor | Total |
| ------- | -------- | ----- | ----- | ----- |
| 0       | 0        | 9     | 3     | 12    |

### Conclusion

The functional verification for Inji Certify rc.1 has been completed. All 1199 planned test cases were executed: 1180 passed, 19 failed and 0 were skipped, a 98.4% pass rate. API automation reported 0 failures in each use case. There are 12 defects on the release list: 9 Major and 3 Minor, with no Blocker or Critical. Testing has demonstrated functional stability and data integrity consistent with product specifications.

There are 12 open defects: 9 Major and 3 Minor. There are no open Blocker or Critical defects. Testing has demonstrated functional stability and data integrity consistent with product specifications.

### QA Approval <a href="#toc245855795" id="toc245855795"></a>

The build has successfully met the defined exit criteria and is recommended for release. The approval is based on the following satisfied conditions:

* Test Case Execution Completion: 100% of planned scenarios executed.
* Defect Status: No Blocker defects remain open.
* Documentation Sign-off: Reports are finalized.
* Test Environment Stability: The test environment remained stable throughout the execution cycle.

Table 5: Report is signed off details

| Name        | Functional Role | Responsibilities |
| ----------- | --------------- | ---------------- |
| Chaitanya K | QA Manager      | <p><br></p>      |

## Appendix <a href="#toc245855796" id="toc245855796"></a>

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions <a href="#toc245855797" id="toc245855797"></a>

<table data-header-hidden><thead><tr><th></th><th></th><th></th><th valign="top"></th></tr></thead><tbody><tr><td>Version</td><td>Date</td><td>Author</td><td valign="top">Reviewers</td></tr><tr><td>V1.0</td><td>17/11/2026</td><td>Nitin Hegde</td><td valign="top">Chaitanya K</td></tr></tbody></table>

### Appendix B: Acronyms <a href="#toc245855798" id="toc245855798"></a>

| Acronym   | Literal Translation                   |
| --------- | ------------------------------------- |
| UIN       | Unique Identification Number          |
| VID       | Virtual Identification                |
| SVG       | Scalable Vector Graphics              |
| SD-JWT    | Selective Disclosure - JSON Web Token |
| VC        | Verifiable Credentials                |
| OpenID4VC | OpenID for Verifiable Credentials     |

### Document History

It outlines the strategy used to ensure a comprehensive evaluation.

<table><thead><tr><th>Version</th><th>Author</th><th>Date</th><th valign="top">Review</th><th valign="top">Affected Sections</th></tr></thead><tbody><tr><td>V1.0</td><td>Nitin Hegde</td><td>17/11/2026</td><td valign="top">Chaitanya Kesiraju</td><td valign="top">New Document</td></tr></tbody></table>

Refer to the github link for more on reports [here](https://github.com/inji/test-management/tree/master/inji-certify/1.0.0%20rc.1).
