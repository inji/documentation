# Version 0.17.0

**Release Name:** Inji Web Wallet 0.17.0

**Release Type:** Developer

**Release Date:** 27th April 2026

### Overview

This release of **Inji Web Wallet 0.17.0** focuses on strengthening the platform through technical debt reduction, API improvements, OpenID4VP enhancements, security and reliability fixes, automation improvements, and continued multi-language support.

The release introduces the **V2 Issuer API**, improves the **OpenID4VP response URI and redirection flow**, addresses SonarCloud reliability issues in Mimoto, improves code coverage, and includes several user-facing bug fixes and API automation improvements.

### Key Highlights

#### 1. Issuers V2 API and Configuration Refactoring

* Introduced a **V2 Issuer Endpoint** to simplify issuer configuration.
* Refactored the existing `mimoto-issuer-config.json` structure.
* Improved the maintainability and scalability of issuer configuration.
* Added automation coverage for the V2 Issuer API and configuration changes.

#### 2. OpenID4VP Enhancements

Improved the OpenID4VP flow to align client identification and redirection behavior with the expected protocol flow.

* Use the **`response_uri`** instead of the redirect URI to identify the pre-registered client.
* Always use the **redirect URI returned by the VP submission endpoint**.
* Updated the DataShare VC verification automation flow to validate response URI-based client identification and redirection behavior.

#### 3. Multi-Language Support

Continued the implementation of locale-aware credential rendering and language handling.

* Added support for passing locale information from the client to APIs according to protocol requirements.
* Added locale-based selection of the credential PDF title instead of always using the first `displayObject`.
* Added handling for JSON-LD language/value structures using `@language` and `@value`.
* Improved the foundation for rendering credentials according to the user's selected language.

#### 4. Code Quality, Reliability and Technical Debt

This release includes several improvements aimed at reducing technical debt and improving long-term maintainability.

* Fixed **SonarCloud reliability issues** in the Mimoto repository.
* Improved Mimoto code coverage.
* Refactored and consolidated crypto utility classes.
* Synchronised release branch changes back into development branches.
* Improved API and configuration maintainability.
* Addressed security and reliability issues identified during development and testing.

### Features and Technical Enhancements

<table data-search="false"><thead><tr><th>Feature / Enhancement / Technical Upgrade</th><th>Jira Ticket</th></tr></thead><tbody><tr><td>V2 Issuer Endpoint and issuer configuration refactoring</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1841">INJIWEB-1841</a></td></tr><tr><td>Analysis for V2 Issuer API and configuration refactoring</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1843">INJIWEB-1843</a></td></tr><tr><td>OpenID4VP response URI-based client identification and redirection</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1874">INJIWEB-1874</a></td></tr><tr><td>Multi-language locale information support</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1822">INJIWEB-1822</a></td></tr><tr><td>Locale-based credential PDF title selection</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1863">INJIWEB-1863</a></td></tr><tr><td>Language-aware PDF content handling</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1865">INJIWEB-1865</a></td></tr><tr><td>Crypto utility refactoring</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1622">INJIWEB-1622</a></td></tr><tr><td>Mimoto code coverage improvements</td><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1871">INJIWEB-1871</a></td></tr></tbody></table>

#### Repositories Released

| Module          | Version                                                    |
| --------------- | ---------------------------------------------------------- |
| Inji Web Wallet | [0.17.0](https://github.com/inji/inji-web/tree/v0.17.0)    |
| Mimoto          | [0.22.0](https://github.com/inji/mimoto/tree/v0.22.0)      |
| Inji Config     | [0.16.0](https://github.com/inji/inji-config/tree/v0.16.0) |

#### Compatible Modules

| Module       | Version                                                                   |
| ------------ | ------------------------------------------------------------------------- |
| Durian       | [1.3.0-beta.2](https://github.com/mosip/durian/releases/tag/1.3.0-beta.2) |
| Inji Certify | [0.14.0](https://github.com/inji/inji-certify/tree/v0.14.0)               |
| Inji Verify  | [0.17.0](https://github.com/inji/inji-verify/tree/v0.17.0)                |
| eSignet      | [1.7.1](https://github.com/mosip/esignet/tree/v1.7.1)                     |

#### Known Issues

Below is the list of key known issues specific to this release. For all the known issues, click [here](https://mosip.atlassian.net/issues/?jql=project%3D%22Inji%20Web%22%20and%20type%20in%20%28bug%29%20and%20status%20not%20in%20%28closed%2C%20canceled%29%20order%20by%20created%20DESC).

| Jira Ticket                                                     | Description                                                                                   |
| --------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| [INJIWEB-1893](https://mosip.atlassian.net/browse/INJIWEB-1893) | Inji Web: Land Registry multilingual VC is not downloading from QA Inji.                      |
| [INJIWEB-1879](https://mosip.atlassian.net/browse/INJIWEB-1879) | Inji Web: Issuer name is updated after refresh in Stored Cards for multilingual-supported VC. |
| [INJIWEB-1878](https://mosip.atlassian.net/browse/INJIWEB-1878) | Inji Web: For multilingual VC, the PDF content is not translated after changing the language. |

#### Bug Fixes

Below is the complete list of bug fixes included in the [0.17.0](https://mosip.atlassian.net/issues?jql=project%20%3D%20%22INJIWEB%22%20AND%20fixversion%20%3D%200.17.0%20AND%20type%20%3D%20Bug) release.

<table data-search="false"><thead><tr><th>Jira Ticket</th><th>Description</th></tr></thead><tbody><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-570">INJIWEB-570</a></td><td>Fixed an issue where expressions were displayed directly in the downloaded VC when field values were not provided during policy creation.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-594">INJIWEB-594</a></td><td>Fixed an issue where some options were not visible when the browser zoom level was increased.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-824">INJIWEB-824</a></td><td>Improved error handling when Mimoto is unavailable while verifying a VC through Inji Verify.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1435">INJIWEB-1435</a></td><td>Made the <code>authorization_servers</code> parameter optional as required by the protocol.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1833">INJIWEB-1833</a></td><td>Fixed an issue where the Download API was re-triggered when an error occurred from the Certify endpoint.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1834">INJIWEB-1834</a></td><td>Fixed an issue where double scrollbars were displayed on the VC after selecting the View Card option.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1888">INJIWEB-1888</a></td><td>Updated handling for the <code>logo</code> field name change in the well-known response.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1890">INJIWEB-1890</a></td><td>Updated the Docker image tag and added missing configuration in the develop branch.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1863">INJIWEB-1863</a></td><td>Added locale-based selection of the credential PDF title instead of always using the first <code>displayObject</code>.</td></tr><tr><td><a href="https://mosip.atlassian.net/browse/INJIWEB-1865">INJIWEB-1865</a></td><td>Added handling for <code>@language</code> and <code>@value</code> to generate PDF content based on the selected language.</td></tr></tbody></table>

### Release Documentation

* [Issuer Configuration and Onboarding (V2 API)](../../overview/features/issuer-configuration-and-onboarding-v2-api.md)

### Additional Resources

* [Feature Documentation](https://docs.inji.io/inji-wallet/inji-web/overview/features) - Contains detailed explanations of all available features of Inji Web Waller and its usage.
* [Backend Services ](https://docs.inji.io/inji-wallet/inji-web/technical-overview/backend-services)- Provides detailed instructions to set up the backend for the Inji Web Wallet.
* [End User Guide](https://docs.inji.io/inji-wallet/inji-web/functional-overview/end-user-guide) - Offers end-to-end guidance for end users on setup and daily usage.
* [API Documentation](https://docs.mosip.io/inji/inji-web/technical-overview/backend-services/mimoto-bff) - Includes comprehensive details of all APIs, endpoints, request/response formats, and examples.

