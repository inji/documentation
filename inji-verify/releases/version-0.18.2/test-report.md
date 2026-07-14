# Test Report

## Introduction <a href="#cwashaiollb0" id="cwashaiollb0"></a>

The scope of testing for INJI Verify 0.18.2 is focused on giving the ability to configure verify-service to generate an additional library JAR in this patch release and ensure compliance with the relevant OpenID4VP and Verifiable Credential verification specifications. Testing includes positive and negative holder binding scenarios, VP result validation, regression testing of existing verification workflows, and assessment of backward compatibility. The objective is to ensure secure, reliable, and interoperable verification across diverse deployment environments and identity ecosystems.

### Overview and Scope <a href="#vj6a6eyrurf4" id="vj6a6eyrurf4"></a>

* Home Page
* Upload and Scan Feature
* VP Verification
* OVP Flow
* SVG Support and Multi Language
* Same Device and Cross Device flow
* V2 end point for "statusCheckFilters" and “Claims”

## Test Approach <a href="#bh9ap59onup6" id="bh9ap59onup6"></a>

The validation of the Inji Verify patch release is performed through the review and analysis of automated API and UI test execution reports. The testing approach focuses on confirming the successful execution of the existing regression automation suites, analyzing test failures and regressions, and ensuring that the patch changes do not adversely impact existing API functionality or UI behavior.

## Test Organization <a href="#id-86nu1qy9do4u" id="id-86nu1qy9do4u"></a>

**Table 1**: Test Organization

<table><thead><tr><th width="170.08203125">Name</th><th>Functional Role</th><th>Responsibilities</th></tr></thead><tbody><tr><td><p>Nitin Hegde</p><p><br></p></td><td>Lead QA Engineer</td><td>Verifying the functionality, stability of the application, and report preparation.</td></tr><tr><td>Chaitanya K</td><td>QA Manager</td><td>Overviewing the test execution and review of the report.</td></tr></tbody></table>

### Test Planning <a href="#obto6h6wbljr" id="obto6h6wbljr"></a>

* **Data Readiness**: Validate the availability of all services along with configured identity schemas (UIN/VID) to support biometric and authentication flows.
* **Data Strategy**: Refresh test data for every cycle by generating new QR codes.
* **Coverage Distribution**: Execute test scenarios across a broad matrix of browsers on Windows, Android, and iOS devices, spanning multiple user personas to ensure end-to-end compatibility coverage.

### Test Environment <a href="#quxowb48cw7j" id="quxowb48cw7j"></a>

**Table 2**: Test Environment

**Images (qainji env)**

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Images (qainji env)</td></tr><tr><td valign="top">injistackqa/inji-verify-service:0.18.x</td></tr><tr><td valign="top">injistackqa/inji-verify-ui:0.18.x</td></tr><tr><td valign="top">injistackqa/inji-certify-with-plugins:0.14.x</td></tr><tr><td valign="top">injistackqa/inji-web:develop</td></tr></tbody></table>

\
**Images (released env)**

<table data-header-hidden><thead><tr><th valign="top"></th></tr></thead><tbody><tr><td valign="top">Images (released env)</td></tr><tr><td valign="top">injistack/apitest-mimoto:0.22.0</td></tr><tr><td valign="top">injistack /inji-verify-service:0.17.0</td></tr><tr><td valign="top">injistack /inji-verify-ui:0.17.0</td></tr><tr><td valign="top">injistackqa/inji-certify-with-plugins:0.14.0</td></tr><tr><td valign="top">mosipid/authentication-demo-service:1.2.0.1</td></tr><tr><td valign="top">mosipid/authentication-internal-service:1.3.0</td></tr><tr><td valign="top">mosipid /authentication-otp-service:1.3.0</td></tr></tbody></table>

## Test Execution Report <a href="#rolc9xl2f746" id="rolc9xl2f746"></a>

### Automation INJI Verify UI <a href="#id-63ghbpxvkqyl" id="id-63ghbpxvkqyl"></a>

**Table 3**: UI Automation

<table><thead><tr><th width="250.53125">Total</th><th>Pass</th><th>Fail</th><th>Known Issues</th><th>Ignored</th></tr></thead><tbody><tr><td>48</td><td>45</td><td>0</td><td>3</td><td>0</td></tr><tr><td>Test Rate: 100% With Pass Rate: 100%</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Automation INJI Verify API <a href="#gm084xyomvjz" id="gm084xyomvjz"></a>

**Table 4**: API Automation Result

<table><thead><tr><th width="262.00390625">Total</th><th>Pass</th><th>Fail</th><th>Known Issues</th><th>Ignored</th></tr></thead><tbody><tr><td>123</td><td>123</td><td>0</td><td>0</td><td>0</td></tr><tr><td>Test Rate: 100% With Pass Rate: 100%</td><td></td><td></td><td></td><td></td></tr></tbody></table>

### Conclusion <a href="#xormntb8lp6z" id="xormntb8lp6z"></a>

This section summarizes the key findings of test execution. It also provides a final QA recommendation on the build's readiness for release. The functional verification for Inji-verify version 0.18.2 has been successfully completed. The testing cycle achieved a 100% execution rate with a 93% pass rate, API automation achieved a 100% pass rate.

While there are 55 known issues in total, there are zero blocker defects identified. The application has demonstrated functional stability and data integrity consistent with product specifications.

### QA Approval <a href="#ogsoimtu28ap" id="ogsoimtu28ap"></a>

The build has successfully met the defined exit criteria and is recommended for release. The approval is based on the following satisfied conditions:

* Test Case Execution Completion: 100% of planned scenarios executed.
* Defect Status: No Blocker defects remain open.
* Documentation Sign-off: All test artifacts and reports are finalized.
* Test Environment Stability: The test environment remained stable throughout the execution cycle.

\
**Table 5**: Report is signed off details

<table><thead><tr><th width="171.328125">Name</th><th width="194.9140625">Functional Role</th><th>Responsibilities</th></tr></thead><tbody><tr><td>Chaitanya K</td><td>QA Manager</td><td>Overviewing the test execution and review of the report.</td></tr></tbody></table>

## Appendix <a href="#lfamtd5l8vn0" id="lfamtd5l8vn0"></a>

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions <a href="#kec3u85tlgda" id="kec3u85tlgda"></a>

<table><thead><tr><th>Version</th><th>Date</th><th>Author</th><th valign="top">Reviewers</th></tr></thead><tbody><tr><td>V1.0</td><td>9/7/2026</td><td>Nitin Hegde</td><td valign="top">Chaitanya K</td></tr></tbody></table>

### Document History

It outlines the strategy used to ensure a comprehensive evaluation.<br>

<table><thead><tr><th>Version</th><th>Author</th><th>Date</th><th valign="top">Review</th><th valign="top">Affected Sections</th></tr></thead><tbody><tr><td>V1.0</td><td>Nitin</td><td>9/7/2026</td><td valign="top">Chaitanya Kesiraju</td><td valign="top">New Document</td></tr></tbody></table>



For further details on the QA Reports you can refer [here](https://github.com/inji/test-management/tree/master/inji-verify/0.18.2).<br>
