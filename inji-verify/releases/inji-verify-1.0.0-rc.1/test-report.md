# Test Report

## Introduction

The scope of testing is to verify fitment to the specification from the perspective of **Functionality, Configurability** and **Customizability**. Verification is performed not only from the end-user perspective but also from the System Integrator (SI) point of view. Hence, the **Configurability** and **Extensibility** of the software are also assessed. This ensures the readiness of the software for use in multiple countries and diverse identity ecosystems.

### Overview and Scope

* Home Page
* Offline / online VC check --- scan or upload QR (QRCodeVerification)
* OpenID4VP online sharing
* Cross-device (QR)
* Same-device (deep link / web wallet)
* Same-device Digital Credentials API (response\_mode=dc\_api), with fallback when unsupported
* Client ID schemes --- pre-registered, decentralized\_identifier: (kid), x509\_san\_dns: (x5c)
* DCQL --- including credentials and credential\_sets
* Trust checks --- integration with MOSIP Domain Trust List and Status List services (external to this repo)
* SVG Support and Multi Language
* V2 end point for "**statusCheckFilters**" and "**Claims**"

## Test Approach

The **Functional verification** of the Inji verify application is performed on Android and iOS platforms to ensure alignment with product specifications and business requirements. Analyzed with respect to functional stability, data integrity, and UI consistency. The validation adopts a **persona-based** testing strategy, simulating real-world user scenarios across diverse device matrices and multi-language configurations to ensure robustness in both online and offline environments.

☐ Functionality

> ☐ Combination
>
> ☐ Configurability
>
> ☐ Customizability
>
> ☐ Library verification (vc-verifier)

## Test Organization

**Table 1: Test Organization**

| **Name**    | **Functional Role** | **Responsibilities**                                                                                                  |
| ----------- | ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Nitin       | QA Lead Engineer    | Verifying the functionality, stability of the application,and report preparation. and performing combination testing. |
| Chaitanya K | QA Manager          | Overviewing the test execution and review of the report.                                                              |

### Test Planning

* **Data Readiness:** Validate the availability of all services along with configured identity schemas (UIN/VID) to support biometric and authentication flows.
* **Data Strategy:** Refresh test data for every cycle by generating new QR codes.
* **Coverage Distribution:** Execute test scenarios across a broad matrix of browsers on Windows, Android, and iOS devices, spanning multiple user personas to ensure end-to-end compatibility coverage.

### Test Devices

**Table 2: Test Devices**

| **Device Model** | **OS and BLE version** |
| ---------------- | ---------------------- |
| iPhone 11        | iOS 26.1 BLE 5.0       |
| iPhone 13        | iOS 18.6.2 BLE 5.0     |
| ONE PLUS 9       | Android 15 BLE 5.3     |
| Moto edge        | Android 15 BLE 5.4     |

### Browser Versions

Used the below browser versions in testing INJI Verify

* Chrome: Version 123.0.6312.124
* Firefox: Version 125.0.1
* Edge: Version 124.0.2478.51
* Safari : Version 17

### Test Environment

**Table 3: Test Environment**

| **Images (qainji env)**                                |
| ------------------------------------------------------ |
| injistackqa/inji-verify-service:1.0.x                  |
| injistackqa/inji-verify-ui: 1.0.x                      |
| <p>injistackqa/inji-certify-with-plugins:<br>1.0.x</p> |
| injistackqa/inji-web:develop                           |

| **Images (released env)**                     |
| --------------------------------------------- |
| injistack/apitest-mimoto:0.22.0               |
| injistack /inji-verify-service:0.18.2         |
| injistack /inji-verify-ui:0.18.2              |
| injistackqa/inji-certify-with-plugins:0.14.0  |
| mosipid/authentication-demo-service:1.2.0.1   |
| mosipid/authentication-internal-service:1.3.1 |
| mosipid /authentication-otp-service:1.3.1     |

## Test Execution Report

### Test case execution summary

**Table 4: Test Execution Summary**

| **Platform** | **Total** | **Pass** | **Fail** | **Skip** |
| ------------ | --------- | -------- | -------- | -------- |
| INJI Verify  | 1887      | 1802     | 85       | 0        |

**Test Rate: 100% With Pass Rate: 95%**

### Automation INJI Verify UI

**Table 5: UI Automation**

| **Total** | **Pass** | **Fail** | **Known Issues** | **Ignored** |
| --------- | -------- | -------- | ---------------- | ----------- |
| 48        | 48       | 0        | 0                | 0           |

**Test Rate: 100% With Pass Rate: 100%**

### Automation INJI Verify API

**Table 6: API Automation Result**

| **Total** | **Pass** | **Fail** | **Known Issues** | **Ignored** |
| --------- | -------- | -------- | ---------------- | ----------- |
| 279       | 279      | 0        | 0                | 0           |

**Test Rate: 100% With Pass Rate: 100%**

## Defect Metrics

### Defect Metrics for the Release 1.0.x-RC1

The following table depicts only the bugs which are found and not addressed in the current release.

**Table 7: Defect Metrics for the Release**

| **Blocker** | **Critical** | **Major** | **Minor** | **Total** |
| ----------- | ------------ | --------- | --------- | --------- |
| 0           | 0            | 5         | 2         | 7         |

### Known Issues Metrics

This section focuses on a separate category of issues that are known but not addressed in the current release. It provides a count and severity distribution for these defects across releases.

**Table 8: Defect Metrics for the known issues**

| **Blocker** | **Critical** | **Major** | **Minor** | **Total** |
| ----------- | ------------ | --------- | --------- | --------- |
| 0           | 0            | 49        | 6         | 56        |

## Conclusion

This section summarizes the key findings of test execution. It also provides a final QA recommendation on the build's readiness for release. The functional verification for Inji-verify version 1.0.x-RC1 has been successfully completed. The testing cycle achieved a **100% execution rate** with a **95% pass rate** across a total of **1887 test cases**. Additionally, API automation achieved a **100% pass rate**.

While there are **7 open defects** (0 Critical, 5 Major, 2 Minor) and **56 known issues in total**, there are **zero blocker defects** identified. The application has demonstrated functional stability and data integrity consistent with product specifications.

### QA Approval

The build has successfully met the defined exit criteria and is **recommended for release**. The approval is based on the following satisfied conditions:

* **Test Case Execution Completion:** 100% of planned scenarios executed.
* **Defect Status:** No Blocker defects remain open.
* **Documentation Sign-off:** All test artifacts and reports are finalized.
* **Test Environment Stability:** The test environment remained stable throughout the execution cycle.

**Table 9: Report is signed off details**

| **Name**    | **Functional Role** | **Responsibilities** |
| ----------- | ------------------- | -------------------- |
| Chaitanya K | QA Manager          |                      |

## Appendix

This includes additional reference information for the report. It contains a history of document versions and a list of acronyms and their meanings.

### Appendix A: Versions

|      | **Date**  | **Author** | **Reviewers** |
| ---- | --------- | ---------- | ------------- |
| V1.0 | 3/11/2026 | Nitin      | Chaitanya K   |

**Document History**

It outlines the strategy used to ensure a comprehensive evaluation.

| **Version** | **Author** | **Date**  | **Review**                   | **Affected Sections** |
| ----------- | ---------- | --------- | ---------------------------- | --------------------- |
| V1.0        | Nitin      | 4/11/2026 | <p>Chaitanya<br>Kesiraju</p> | New Document          |

Github link for more on reports is [here](https://github.com/inji/test-management/tree/master/inji-verify/1.0.0-rc.1).
