# Test Report

## Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of

* Functionality
* Deployability
* Configurability
* Customizability

Verification is performed not only from the end user perspective but also from the System Integrator (SI) point of view. Hence Configurability and Extensibility of the software is also assessed. This ensures the readiness of software for use in multiple countries. MOSIP is an "API First" product platform.

Testing scope has been focused on the below features:

* Inji Home page
* Issuer and Credential selection
* Authenticating with user credentials
* PDF Generation and Auto download
* Success/Failure notification after downloading the VC PDF
* Retrieve Issuers and Credential list
* Downloading VC
* Multi languages support
* Error Handling
* Theme update
* PDF View
* Issuers support
* Responsive view of the web
* Access violations
* QR Code
* Durian data storage integration
* PDF and CBOR
* OpenID4VP Implementation
* Latest draft changes support for OpenID4VCI
* FAQ Support
* UI UX Design updates
* Swagger update
* Secure Time Bound Storage

## Test Approach

Persona based approach has been adopted to perform the IV\&V, by simulating test scenarios that resemble a real-time implementation.

A Persona is a fictional character/user profile created to represent a user type that might use a product/or a service in a similar way. Persona based testing is a software testing technique that puts software testers in the customer's shoes, assesses their needs from the software and thereby determines use cases/scenarios that the customers will execute. The persona needs may be addressed through any of the following.

* Functionality
* Deployability
* Configurability
* Customizability

The verification methods may differ based on how the need was addressed.

## Verified configuration

Verification is performed on various configurations as mentioned below.

* Default configuration - with 6 Lang
  * English
  * French
  * Arabic
  * Hindi
  * Tamil
  * Kannada

## Feature Health

<figure><img src="../../../../.gitbook/assets/inji_web_0.11.0_test_report_feature_health_1.png" alt=""><figcaption><p>Launch application</p></figcaption></figure>

## Test execution statistics

### Functional test results

Below are the test metrics by performing functional testing. The process followed was black box testing which based its test cases on the specifications of the software component under test. Functional test was performed in combination of individual module testing as well as integration testing. Test data were prepared in line with the user stories. Expected results were monitored by examining the user interface. The coverage includes GUI testing, System testing, End-To-End flows across multiple configurations. The testing cycle included simulation of multiple identity schema and respective UI schema configurations.

<table><thead><tr><th width="187">Total</th><th>Passed</th><th width="216">Failed</th><th>Skipped</th></tr></thead><tbody><tr><td>456</td><td>426</td><td>30</td><td>0</td></tr><tr><td>Test Rate: 100%, With Pass Rate: 93%</td><td></td><td></td><td></td></tr></tbody></table>

Here is the detailed breakdown of metrics for each module:

<table><thead><tr><th width="190">INJI Web UI Verification</th><th>Total</th><th>Passed</th><th>Failed</th><th>Skipped</th></tr></thead><tbody><tr><td>Test cases</td><td>456</td><td>426</td><td>30</td><td>0</td></tr></tbody></table>

### UI Automation and API Test Rig test results

Below are the test metrics by performing UI Automation and API Test rig.

<table><thead><tr><th width="233">Total</th><th>Passed</th><th>Failed</th><th>Skipped/Ignored</th></tr></thead><tbody><tr><td>180</td><td>153</td><td>0</td><td>27</td></tr><tr><td>Test Rate: 83%, With Pass Rate: 99%</td><td></td><td></td><td></td></tr></tbody></table>

Test Rate: 83%,\
With Pass Rate: 99%

Here is the detailed breakdown of metrics for each module:

<table><thead><tr><th width="230">INJI Web UI Automation</th><th>Total</th><th>Passed</th><th>Failed</th><th>Skipped</th></tr></thead><tbody><tr><td>Test cases</td><td>19</td><td>19</td><td>0</td><td>0</td></tr></tbody></table>

<table><thead><tr><th width="232">INJI Web API Test Rig</th><th>Total</th><th>Passed</th><th>Failed</th><th>Skipped/Ignored</th></tr></thead><tbody><tr><td>Test cases</td><td>161</td><td>134</td><td>0</td><td>27</td></tr></tbody></table>

**Note**: Ignored 27 OTP related test cases which are descoped and not applicable

Functional and test rig code base branch which is used for the above metrics is:

Hash:0a7d1b58f5c8b73ba4c0c3520da888f6ce64311a473ac456048cbce124d41197

### Detailed Test metrics

Below are the detailed test metrics by performing manual/automation testing. The project metrics are derived from Defect density, Test coverage, Test execution coverage, test tracking and efficiency.

The various metrics that assist in test tracking and efficiency are as follows:

* Passed Test Cases Coverage: It measures the percentage of passed test cases. (Number of passed tests / Total number of tests executed) x 100
* Failed Test Case Coverage: It measures the percentage of all the failed test cases. (Number of failed tests / Total number of test cases executed) x 100

Git hub link for the xls file:

\<TBD>
