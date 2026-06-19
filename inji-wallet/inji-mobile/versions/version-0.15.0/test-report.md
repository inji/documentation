# Test Report

## Testing Scope

The scope of testing is to verify fitment to the specification from the perspective of

* Functionality
* Deployability
* Configurability
* Customizability

Verification is performed not only from the end user perspective but also from the System Integrator (SI) point of view. Hence Configurability and Extensibility of the software is also assessed. This ensures the readiness of software for use in multiple countries. Since MOSIP is an "API First" product platform, Verification scope required comprehensive automation testing for all the MOSIP APIs. An automation Test Rig is created for the same.

The Inji testing scope revolves around the following flows:

* Biometric unlock
* Passcode unlock
* VC download via MOSIP
* VC download via esignet
* VC download via Sunbird
* Pinning a VC
* Normal VC sharing with VID
* Deleting VC
* Face Auth on Resident's phone with VID
* Multi language support
* Credential registry
* Backup and restore
* Wallet binding
* Deep link navigation
* OpenID4VP
* QR code Login
* Key Management
* Logout

## Test Approach

Persona based approach has been adopted to perform the IV\&V, by simulating test scenarios that resemble a real-time implementation.

A Persona is a fictional character/user profile created to represent a user type that might use a product/or a service in a similar way. Persona based testing is a software testing technique that puts software testers in the customer's shoes, assesses their needs from the software and thereby determines use cases/scenarios that the customers will execute. The persona needs may be addressed through any of the following.

* Functionality
* Deployability
* Configurability
* Customizability

The verification methods may differ based on how the need was addressed.

For regression check, "MOSIP Test Rig" - an automation testing suite - which is indigenously designed and developed for supporting persona-based testing. MOSIP Test Rig covers the end-to-end test execution and reporting. The end-to-end functional test scenarios are written starting from pre-registration to creation of packet in registration center, processing the packet through the registration processor, generating UIN and authenticating identity using IDA through various permutation and combinations of cases being covered. MOSIP Test Rig will be an open-source artifact which can also be enhanced and used by countries to validate the SI deliveries before going live. Persona classes include both negative and positive personas. Negative persona classes include users like Bribed Registration Office, Malicious Insider etc. The needs of positive persona classes must be met, whereas the needs of negative persona classes must be effectively restricted by the software.

## Verified configuration

Verification is performed on various configurations as mentioned below:

* Default configuration - with 3 Lang
* Virtual countries
  * 1 Lang configuration
  * 2 Lang configuration
  * 3 Lang configuration

## Feature Health

On Android Device:

<figure><img src="../../../../.gitbook/assets/inji_wallet_0.15.0_feature_health_android.png" alt=""><figcaption></figcaption></figure>

On iOS Device:

<figure><img src="../../../../.gitbook/assets/inji_wallet_0.15.0_feature_health_ios.png" alt=""><figcaption></figcaption></figure>

## Test execution statistics

### Functional test results by modules

Below are the test metrics by performing functional testing using mock MDS and mock ABIS. The process followed was black box testing which based its test cases on the specifications of the software component under test. The functional test was performed in combination of individual module testing as well as integration testing. Test data were prepared in line with the user stories. Expected results were monitored by examining the user interface. The coverage includes GUI testing, System testing, End-To-End flows across multiple languages and configurations. The testing cycle included simulation of multiple identity schema and respective UI schema configurations.

| **Total** | **Passed** | **Failed** | **Skipped (N/A)** |
| --------- | ---------- | ---------- | ----------------- |
| 2942      | 2659       | 283        | 0                 |

Test Rate: 100%\
With Pass Rate: 90%

Here is the detailed breakdown of metrics for each module:

| **Module**        | **Total** | **Passed** | **Failed** | **Skipped (N/A)** |
| ----------------- | --------- | ---------- | ---------- | ----------------- |
| On Android Device | 1562      | 1408       | 154        | 0                 |
| On iOS Device     | 1380      | 1251       | 129        | 0                 |

### API verification results by modules

The below section provides details on API test metrics by executing MOSIP functional automation Framework. All external API test executions were performed at module level isolation. Each end point is tested with the test data and expectations of each test data are mapped to assert the test case.

| **Total** | **Passed** | **Failed** | **Ignored** | **Skipped** |
| --------- | ---------- | ---------- | ----------- | ----------- |
| 176       | 143        | 0          | 33          | 0           |

Test Rate: 81%\
With Pass Rate: 100%

### UI Automation results

The below section provides details on UI Automation by executing MOSIP functional automation Framework.

| **Total** | **Passed** | **Failed** | **Skipped** |
| --------- | ---------- | ---------- | ----------- |
| 112       | 112        | 0          | 0           |

Test Rate: 100%\
With Pass Rate: 100%

Here is the detailed breakdown of metrics:

| **Module** | **Total** | **Passed** | **Failed** | **Skipped** |
| ---------- | --------- | ---------- | ---------- | ----------- |
| Android    | 60        | 60         | 0          | 0           |
| iOS        | 52        | 52         | 0          | 0           |

### Test Rig Details:

Functional and test rig code base branch which is used for the above metrics is:

Hash Tag:\
SHA: sha256:01511fa220941a03f760550f3373ecc273dd6222000ab8030097858ece94ae29

### VC Verifier Library Verification

| **Total** | **Passed** | **Failed** | **Skipped** |
| --------- | ---------- | ---------- | ----------- |
| 97        | 77         | 20         | 0           |

Test Rate: 100%\
With Pass Rate: 79.38%

### Testing with various device combinations

Below are the test metrics by performing VC Sharing functionality on various device combinations

<figure><img src="../../../../.gitbook/assets/inji_wallet_0.15.0_feature_health_combined.png" alt=""><figcaption></figcaption></figure>

| **Total** | **Passed** | **Failed** | **Skipped** |
| --------- | ---------- | ---------- | ----------- |
| 192       | 192        | 0          | 0           |

Test Rate: 100%\
With Pass Rate: 100%

### Device and Component Details:

#### Tested with Inji components

* mosipqa/artifactory-server:0.10.x-INJI
* mosipid/inji-certify:0.10.0
* mosipid/inji-certify:0.10.0
* mosipqa/inji-verify-service:develop
* mosipqa/inji-verify-ui:develop
* mosipid/data-share-service:1.3.0-beta.2
* mosipqa/inji-web:0.11.0
* mosipqa/mimoto:0.15.x
* mosipqa/artifactory-server:0.10.x-INJI
* mosipqa/inji-certify-with-plugins:develop
* mosipqa/inji-certify-with-plugins:develop
* mosipqa/inji-certify-with-plugins:develop
* mosipqa/inji-certify-with-plugins:develop
* mosipqa/inji-certify-with-plugins:develop
* mosipqa/inji-certify-with-plugins:develop
* mosipqa/dsl-packetcreator:develop
* mosipdev/dsl-packetcreator:develop
* mosipqa/inji-certify-with-plugins:develop

#### Tested with MOSIP components

* mosipid/mock-abis:1.2.0.2
* mosipid/mock-mv:1.2.0.2
* mosipid/hotlist-service:1.2.1.0
* nginxinc/nginx-unprivileged:1.21.6-alpine
* mosipid/admin-service:1.2.1.0
* mosipid/admin-ui:1.2.0.1
* mosipid/artifactory-server:1.4.1-ES
* mosipid/authentication-demo-service:1.2.0.1
* mosipid/authentication-demo-service:1.2.0.1
* mosipdev/authentication-demo-service:develop
* mosipdev/authentication-demo-service:develop
* mosipid/biosdk-server:1.2.0.1
* mosipqa/biosdk-server:develop
* mosipdev/captcha-validation-service:develop
* rancher/fleet-agent:v0.7.0
* mosipid/data-share-service:1.2.0.1
* mosipid/digital-card-service:1.2.0.1
* mosipid/authentication-service:1.2.1.0
* mosipid/authentication-internal-service:1.2.1.0
* mosipid/authentication-otp-service:1.2.1.0
* mosipid/credential-service:1.2.1.0
* mosipdev/credential-request-generator:MOSIP-34070-v1210
* mosipdev/id-repository-identity-service:MOSIP-34070-v1210
* mosipid/id-repository-vid-service:1.2.1.0
* mosipid/inji-verify:0.10.0
* mosipid/data-share-service:1.3.0-beta.2
* mosipid/inji-web:0.11.0
* mosipid/mimoto:0.15.0
* mosipid/kernel-auditmanager-service:1.2.0.1
* mosipid/kernel-auth-service:1.2.0.1
* mosipid/kernel-idgenerator-service:1.2.0.1
* mosipid/kernel-masterdata-service:1.2.1.0
* mosipid/kernel-notification-service:1.2.0.1
* mosipid/kernel-otpmanager-service:1.2.0.1
* mosipid/kernel-pridgenerator-service:1.2.0.1
* mosipid/kernel-ridgenerator-service:1.2.0.1
* mosipid/kernel-syncdata-service:1.2.1.0
* mosipid/kernel-keymanager-service:1.2.0.1
* mosipid/artifactory-server:0.10.0-INJI
* mosipid/esignet:1.4.1
* mosipid/inji-certify:0.10.0
* mosipid/oidc-ui:1.4.1
* mosipid/mock-identity-system:0.9.3
* mosipid/mock-relying-party-service:0.9.3
* mosipid/mock-relying-party-ui:0.9.3
* mosipid/mock-smtp:1.0.0
* mosipid/mosip-file-server:1.2.0.1
* mosipid/artifactory-server:0.10.0-INJI
* mosipid/mock-relying-party-service:0.9.3
* mosipid/mock-relying-party-ui:0.9.3
* mosipid/esignet:1.4.1
* mosipid/inji-certify:0.10.0
* mosipid/oidc-ui:1.4.1
* mosipid/dsl-packetcreator:1.2.0.1
* mosipid/dsl-packetcreator:1.2.0.1
* mosipdev/dsl-packetcreator:develop
* mosipdev/dsl-packetcreator:develop
* mosipid/commons-packet-service:1.2.0.1
* mosipid/pmp-ui:1.2.0.2
* mosipid/partner-management-service:1.2.1.0
* mosipid/policy-management-service:1.2.1.0
* mosipid/pre-registration-application-service:1.2.0.1
* mosipid/pre-registration-batchjob:1.2.0.1
* mosipid/pre-registration-booking-service:1.2.0.1
* mosipid/pre-registration-captcha-service:1.2.0.1
* mosipid/pre-registration-datasync-service:1.2.0.1
* mosipid/pre-registration-ui:1.2.0.1
* mosipid/print:1.2.0.1
* mosipid/registration-client:1.2.0.2
* mosipid/registration-processor-common-camel-bridge:1.2.0.1
* mosipid/registration-processor-stage-group-1:1.2.0.1
* mosipid/registration-processor-stage-group-2:1.2.0.1
* mosipid/registration-processor-stage-group-3:1.2.0.1
* mosipid/registration-processor-stage-group-4:1.2.0.1
* mosipid/registration-processor-stage-group-5:1.2.0.1
* mosipid/registration-processor-stage-group-6:1.2.0.1
* mosipid/registration-processor-stage-group-7:1.2.0.1
* mosipid/registration-processor-notification-service:1.2.0.1
* mosipid/registration-processor-dmz-packet-server:1.2.0.1
* mosipid/registration-processor-reprocessor:1.2.0.1
* mosipid/registration-processor-registration-status-service:1.2.0.1
* mosipid/registration-processor-registration-transaction-service:1.2.0.1
* mosipid/registration-processor-workflow-manager-service:1.2.0.1
* mosipid/resident-service:1.2.1.0
* mosipid/resident-ui:0.9.0
* mosipid/artifactory-server:0.10.0-INJI
* sunbird-rc-credential-schema:v2.0.0-rc3
* sunbird-rc-credentials-service:v2.0.0-rc3
* sunbird-rc-identity-service:v2.0.0-rc3
* sunbird-rc-core:v1.0.0
* mosipid/esignet:1.4.1
* mosipid/inji-certify:0.10.0
* mosipid/oidc-ui:1.4.1
* mosipid/websub-service:1.2.0.1
* mosipid/consolidator-websub-service:1.2.0.1

#### Docker Compose Testing Components

* mosipqa/inji-certify:0.10.x
* mosipqa/inji-web:release-0.11.x
* mosipqa/mimoto:release-0.15.x

#### Devices Used For Testing

* Vivo Y73 with Android 12 BLE 5.0
* SS Galaxy A03 core with Android 11 BLE 4.2
* iPhone 11 with i-OS 15 BLE 5.0
* iPhone 8 with i-OS 16 BLE 5.0
* iPhone 7 with i-OS 15.6 BLE 4.2
* Redmi 7A Android 10 BLE 4.2
* Redmi note 10 lite Android 10 BLE 5.0
* Redmi K20 pro Android 11 BLE 5.0

### Detailed Test Metrics

Below are the detailed test metrics by performing manual/automation testing. The project metrics are derived from Defect density, Test coverage, Test execution coverage, test tracking and efficiency.

The various metrics that assist in test tracking and efficiency are as follows:

* Passed Test Cases Coverage: It measures the percentage of passed test cases. (Number of tests passed / Total number of tests executed) x 100
* Failed Test Case Coverage: It measures the percentage of all the failed test cases. (Number of failed tests / Total number of test cases executed) x 100

## Execution Test Summary

* Testing is conducted on build version mimoto 0.15.0 with ESignet 1.4.1.
* Expired VC is tested for mock through docker compose.
* For deep link navigation, testing is performed against build version ESignet 1.5.0.

Github link for the xls file is [**here**](https://github.com/mosip/test-management/tree/master/inji/0.15.0)
