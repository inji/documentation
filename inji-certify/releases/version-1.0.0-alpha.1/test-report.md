# Test Report

## Introduction <a href="#heading-h.wlvk58t0cqq" id="heading-h.wlvk58t0cqq"></a>

The scope of testing is to verify fitment to the specification from the perspective of Functionality, Configurability and Customizability. Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the Configurability and Extensibility of the software are also assessed. This ensures the readiness of the software for use in multiple countries and diverse identity ecosystems.

### Overview and Scope <a href="#heading-h.5gemcdhyze5w" id="heading-h.5gemcdhyze5w"></a>

Testing scope has been focused on the following features:

* Inji certify Docker compose testing (Data provider CSV plugin, Data provider Postgres plugin)
* Insurance, MosipId and Mock (Issuance and Data provider (Postgres plugin)), which covered Land registry, school and Farmer use case
* Preauthcode
* Mdoc mdl format

## Test Approach <a href="#heading-h.n25pnjmg0ojk" id="heading-h.n25pnjmg0ojk"></a>

The Functional verification of Inji Certify is performed to ensure alignment with product specifications, business requirements, and the OpenID for Verifiable Credential Issuance flow. The validation covers credential generation, signing, and issuance of W3C-compliant Verifiable Credentials across supported formats such as JSON-LD and SD-JWT, along with integration of issuer configurations, credential schemas, data provider plugins, and dependent services. The testing adopts a use-case-based strategy, validating issuance workflows for configured certificate types and data sources to ensure functional stability, data integrity, interoperability, configurability, and readiness for deployment in diverse credential ecosystems.

* Functionality through automation

## Test Organization <a href="#heading-h.rnaltx8eb3bj" id="heading-h.rnaltx8eb3bj"></a>

**Table**: Test Organization

<table><thead><tr><th width="148.98046875">Name</th><th width="171.41015625">Functional Role</th><th>Responsibilities</th></tr></thead><tbody><tr><td><p>Nitin Hegde</p><p><br></p></td><td>QA Lead</td><td>Verifying the functionality, Automation scenarios development and report preparation</td></tr><tr><td>Chaitanya K</td><td>QA Manager</td><td>Overviewing the test execution and review of the report.</td></tr></tbody></table>

### Test Planning <a href="#heading-h.edem5dhkfg3i" id="heading-h.edem5dhkfg3i"></a>

* Data Readiness: Validate the availability of all services along with configured identity schemas (UIN/VID) to authentication flows.

### Test Environment <a href="#heading-h.c8nbdr61adze" id="heading-h.c8nbdr61adze"></a>

**Table**: Test Environment

<table><thead><tr><th valign="top">Test Environments</th></tr></thead><tbody><tr><td valign="top">Images (qainji env)</td></tr><tr><td valign="top">injistackqa/inji-certify-with-plugins:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-web:develop</td></tr><tr><td valign="top">injistackqa/mimoto:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-verify-service:1.0.x</td></tr><tr><td valign="top">injistackqa/inji-verify-ui:1.0.x</td></tr><tr><td valign="top">Nginx</td></tr><tr><td valign="top">mosipid/softhsm:v2</td></tr><tr><td valign="top">mosipid/kernel-config-server:1.3.0</td></tr><tr><td valign="top">mosipqa/postgres-init:develop</td></tr><tr><td valign="top">injistackqa/apitest-inji-certify:1.0.x</td></tr></tbody></table>



<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Images (released env)</td></tr><tr><td valign="top">mosipid/credential-service:1.3.0</td></tr><tr><td valign="top">mosipid/data-share-service:1.3.0</td></tr><tr><td valign="top">mosipid/data-share-service:1.3.0-beta.2 - Injiweb</td></tr><tr><td valign="top">mosipid/digital-card-service:1.3.0</td></tr><tr><td valign="top">mosipid/esignet-with-plugins:1.6.2</td></tr><tr><td valign="top">mosipid/mock-identity-system:0.11.2</td></tr><tr><td valign="top">sunbird-rc/sunbird-rc-core:v1.0.0</td></tr><tr><td valign="top">sunbird-rc/sunbird-rc-credential-schema:v2.0.0-rc3</td></tr><tr><td valign="top">sunbird-rc/sunbird-rc-credentials-service:v2.0.0-rc3</td></tr><tr><td valign="top">sunbird-rc/sunbird-rc-identity-service:v2.0.0-rc3</td></tr></tbody></table>

## Test Execution Report <a href="#heading-h.l9s7xp54gyaa" id="heading-h.l9s7xp54gyaa"></a>

### Test case execution summary <a href="#heading-h.ytqf5fsvggzh" id="heading-h.ytqf5fsvggzh"></a>

Automation Test Execution was completed in qainji env achieving a 100% execution rate for all planned scenarios. The testing validated core functionalities with a high pass rate, while identified issues on both platforms have been logged for defect resolution.

### Automation Result <a href="#heading-h.fpgckqdvtzlm" id="heading-h.fpgckqdvtzlm"></a>

* Sunbird use case

<table><thead><tr><th width="270.5625">Total</th><th>Passed</th><th>Failed</th><th>Ignored</th><th>Known issues</th></tr></thead><tbody><tr><td>515</td><td>48</td><td>0</td><td>447</td><td>20</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td><td></td><td></td><td></td><td></td></tr></tbody></table>



* Mock Use case

<table><thead><tr><th width="277.04296875">Total</th><th>Passed</th><th>Failed</th><th>Ignored</th><th>Known issues</th></tr></thead><tbody><tr><td>515</td><td>21</td><td>0</td><td>474</td><td>20</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td><td></td><td></td><td></td><td></td></tr></tbody></table>



* Mock (Data provider) Land registry Use case

<table><thead><tr><th width="280.12109375">Total</th><th>Passed</th><th>Failed</th><th>Ignored</th><th>Known issues</th></tr></thead><tbody><tr><td>515</td><td>249</td><td>0</td><td>246</td><td>20</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td><td></td><td></td><td></td><td></td></tr></tbody></table>



* MosipId Use case

<table><thead><tr><th width="285.75">Total</th><th>Passed</th><th>Failed</th><th>Ignored</th><th>Known issues</th></tr></thead><tbody><tr><td>515</td><td>92</td><td>0</td><td>403</td><td>20</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td><td></td><td></td><td></td><td></td></tr></tbody></table>



* Preauth code(academic) Use case

<table><thead><tr><th width="294.87890625">Total</th><th>Passed</th><th>Failed</th><th>Ignored</th><th>Known issues</th></tr></thead><tbody><tr><td>515</td><td>35</td><td>0</td><td>460</td><td>20</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td><td></td><td></td><td></td><td></td></tr></tbody></table>



* Mdoc mdl Use case

<table><thead><tr><th width="298.66796875">Total</th><th>Passed</th><th>Failed</th><th>Ignored</th><th>Known issues</th></tr></thead><tbody><tr><td>515</td><td>18</td><td>0</td><td>477</td><td>20</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 100% and Fail Rate: 0%</td><td></td><td></td><td></td><td></td></tr></tbody></table>

## Defect Metrics <a href="#heading-h.lhwc1sdncbcd" id="heading-h.lhwc1sdncbcd"></a>

### Defect Metrics for the Release 1.0.0-alpha.1 <a href="#heading-h.45xt9qze0ag" id="heading-h.45xt9qze0ag"></a>

The following table depicts only the bugs which are found and not addressed in the current release.

**Table**: Defect Metrics for the Release

| Blocker | Critical | Major | Minor | Total |
| ------- | -------- | ----- | ----- | ----- |
| 0       | 1        | 0     | 0     | 1     |

## Conclusion <a href="#heading-h.uayc265przmt" id="heading-h.uayc265przmt"></a>

This section summarizes the key findings of test execution. It also provides a final QA recommendation on the build's readiness for release. The functional verification for Inji Certify release version 1.0.0-alpha.1 has been successfully completed. The testing cycle achieved a 100% execution rate with a 100% pass rate across a total of 515 automation test cases.

While there are 1 Critical open defects and as known issues, there are zero blocker defects that are open. Testing has demonstrated functional stability and data integrity consistent with product specifications.

### QA Approval <a href="#heading-h.ol3u7z4turvr" id="heading-h.ol3u7z4turvr"></a>

The build has successfully met the defined exit criteria and is recommended for release. The approval is based on the following satisfied conditions:

* Test Case Execution Completion: 100% of planned scenarios executed.
* Defect Status: No Blocker defects remain open.
* Documentation Sign-off: Reports are finalized.
* Test Environment Stability: The test environment remained stable throughout the execution cycle.

\
**Table**: Report is signed off details

| Name        | Functional Role | Responsibilities |
| ----------- | --------------- | ---------------- |
| Chaitanya K | QA Manager      | <p><br></p>      |

## Appendix <a href="#heading-h.le19retwsijh" id="heading-h.le19retwsijh"></a>

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions <a href="#heading-h.kvn32ugst63q" id="heading-h.kvn32ugst63q"></a>

<table><thead><tr><th>Version</th><th>Date</th><th>Author</th><th valign="top">Reviewers</th></tr></thead><tbody><tr><td>V1.0</td><td>28/07/2026</td><td>Nitin Hegde</td><td valign="top">Chaitanya K</td></tr></tbody></table>

### Appendix B: Acronyms <a href="#heading-h.qug7ad6c722t" id="heading-h.qug7ad6c722t"></a>

| Acronym   | Literal Translation                   |
| --------- | ------------------------------------- |
| MOSIP     | Modular Open-Source Identity Platform |
| UIN       | Unique Identification Number          |
| VID       | Virtual Identification                |
| SVG       | Scalable Vector Graphics              |
| SD-JWT    | Selective Disclosure - JSON Web Token |
| VC        | Verifiable Credentials                |
| OpenID4VC | OpenID for Verifiable Credentials     |

Refer to the github link for more on reports [here](https://github.com/inji/test-management/tree/master/inji-certify/1.0.0-alpha.1).\
<br>
