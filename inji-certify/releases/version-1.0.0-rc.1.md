# Version 1.0.0-rc.1

<mark style="color:red;">**Coming Soon!**</mark>



**Release Version:** v1.0.0-rc.1

**Release Type:** Release Candidate (RC)

**Release Date:** November 2026

> **Note:** This release builds on the OpenID4VCI 1.0 foundation delivered in v1.0.0-alpha.1. It contains several breaking changes, listed under Breaking changes. Review them before upgrading.

### Overview

Inji Certify v1.0.0-rc.1 focuses on security hardening, richer Presentation During Issuance (PDI), mdoc specification alignment, and stricter, more transparent credential configuration. It introduces DPoP-constrained access tokens, DCQL-based PDI, an embedded Inji Verify library, an upgraded Velocity template engine, and a set of validation and stability fixes.

**Key changes**

* DPoP-constrained access token support on the credential endpoint.
* DCQL-only VP request configuration for the Interactive Authorization Endpoint (IAE). Presentation Exchange (PEX) is no longer supported.
* Inji Verify embedded as a library (verify-core 1.0.0-rc.1) in the PDI flow.
* mdoc alignment with OpenID4VCI 1.0 (credential response structure, integer COSE algorithm identifiers in issuer metadata).
* Credential Configuration API: cryptographicBindingMethodsSupported, proofTypesSupported and signatureAlgo are validated and mandatory. The properties fallback is removed.
* ldp\_vc configurations advertise their crypto suite in credential\_signing\_alg\_values\_supported.
* Velocity template engine upgraded from 1.7 to 2.4.1 (fixes CVE-2020-13936).
* Compatibility with eSignet 1.8.0.

### Major Features & Enhancements

#### 1. DPoP-Constrained Access Tokens

Certify now acts as a DPoP (RFC 9449) resource server on the credential endpoint. When a wallet presents a DPoP-bound access token, Certify validates the accompanying DPoP proof, so the token can only be used by the holder of the bound key. This protects against access token theft and replay.

* Plain Bearer tokens continue to work.
* A DPoP-bound token (cnf.jkt) presented as Bearer is refused.
* A plain token presented under the DPoP scheme is refused.
* Proofs are single-use (jti replay cache) and checked for typ, alg, signature, htm, htu, iat freshness, ath and cnf.jkt.
* DPoP applies to tokens issued by an external authorization server such as eSignet. Tokens minted by Certify's own /oauth/token (pre-authorized and PDI flows) are Bearer tokens.

#### 2. DCQL Support in Presentation During Issuance

The VP request configuration for the IAE now uses the Digital Credentials Query Language (DCQL), in line with OpenID4VP 1.0. Issuers use a dcqlQuery block to state which credentials the holder must present during issuance. The wallet's vp\_token is keyed by the query, so no presentation\_submission is needed.

> **Breaking change:** Presentation Exchange (presentation\_definition) is no longer supported in the PDI flow from release-1.0.0-rc1

#### 3. Embedded Inji Verify Library in the PDI Flow

PDI now uses Inji Verify as an embedded library (verify-core 1.0.0-rc.1) instead of calling a separately deployed Inji Verify service. This removes a runtime dependency and simplifies deployment.

#### 4. mdoc Alignment with OpenID4VCI 1.0

* The mdoc credential response structure follows the OpenID4VCI 1.0 specification.
* credential\_signing\_alg\_values\_supported for mso\_mdoc configurations is published as integer COSE algorithm identifiers (for example -7 for ES256).

#### 5. Credential Configuration API: Mandatory, Validated Metadata

The Add (POST /credential-configurations) and Update (PUT /credential-configurations/{credentialConfigKeyId}) APIs now require these attributes, for every credential format:

* cryptographicBindingMethodsSupported
* proofTypesSupported
* signatureAlgo (mandatory in DataProvider plugin mode; optional in VCIssuance mode, but validated if sent)

Values are validated against what the Certify deployment supports and are reflected in the issuer well-known metadata. Missing, null or empty values are rejected, and nothing is filled in from deployment properties any more.

The value in the issuer metadata is derived from the configuration:

| Format    | credential\_signing\_alg\_values\_supported advertises                        |
| --------- | ----------------------------------------------------------------------------- |
| ldp\_vc   | The crypto suite, e.g. Ed25519Signature2020 (OpenID4VCI 1.0 Appendix A.1.2.2) |
| dc+sd-jwt | The configured signatureAlgo, e.g. ES256                                      |
| mso\_mdoc | The COSE identifier of signatureAlgo, e.g. -7                                 |

#### 6. Velocity Template Engine Upgraded from 1.7 to 2.4.1

Credential templates (vc\_template) are rendered with Velocity 2.4.1, which fixes CVE-2020-13936. Template behaviour changes:

1. \#if **treats empty values as false.** An empty string, list, map or array is now false. An empty phone field is omitted instead of rendered as "". To always render a field, use #if($var || $var == '') or the quiet reference $!{var}.
2. **Loop variables renamed.** $velocityCount becomes $foreach.count; $velocityHasNext becomes $foreach.hasNext.
3. **Reflection blocked.** SecureUberspector is enabled, so templates can no longer call methods on Class, ClassLoader, Runtime or System. Normal field access and the $\_dateTool and $\_esc tools are unaffected.

> **Breaking change:** Review all existing credential templates.

#### 7. eSignet 1.8.0 Compatibility

Certify is validated with eSignet 1.8.0 as the authorization server. Two properties change (see Breaking Changes).

### User Stories Released

| Description                                                                                                                                       | Git Id                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Add support for DPoP-constrained access tokens in Certify                                                                                         | [#963](https://github.com/inji/inji-certify/issues/963)   |
| Support DCQL in the VP request configuration on the IAE endpoint                                                                                  | [#962](https://github.com/inji/inji-certify/issues/962)   |
| Integrate Inji Verify as an embedded library in the PDI flow instead of calling it as a separate service                                          | [#902](https://github.com/inji/inji-certify/issues/902)   |
| Enhance the Interactive Authorization (IAR) endpoint to support OpenID4VCI 1.0-compliant PDI                                                      | [#739](https://github.com/inji/inji-certify/issues/739)   |
| Validate proof\_types\_supported, cryptographic\_binding\_methods\_supported and signing algorithm in the Add/Update Credential Configuration API | [#989](https://github.com/inji/inji-certify/issues/989)   |
| Make binding methods, proof types and signatureAlgo mandatory on Add/Update and remove the properties fallback                                    | [#1099](https://github.com/inji/inji-certify/issues/1099) |
| Advertise the crypto suite in credential\_signing\_alg\_values\_supported for ldp\_vc                                                             | [#1110](https://github.com/inji/inji-certify/issues/1110) |

### Bug Fixes

All bugs fixed in this release are listed [here](https://github.com/inji/inji-certify/issues?q=is%3Aissue+milestone%3A1.0.0-rc.1+type%3ABug).

| Git Id                                                    | Description                                                                                                   |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| [#711](https://github.com/inji/inji-certify/issues/711)   | When invalid sd\_claims are provided, the issuer throws an error and does not fetch the VC                    |
| [#679](https://github.com/inji/inji-certify/issues/679)   | Validation issues for the qrsettings block in the Credential Config API                                       |
| [#686](https://github.com/inji/inji-certify/issues/686)   | Error message mismatch in the mdoc-mDL use case (PDI)                                                         |
| [#878](https://github.com/inji/inji-certify/issues/878)   | invalid\_request returned for unreadable and malformed bodies on non-VCI endpoints, instead of unknown\_error |
| [#1054](https://github.com/inji/inji-certify/issues/1054) | did:jwk holder ID created from the JWK proof header contained base64 padding, breaking OpenID4VP presentation |
| [#1044](https://github.com/inji/inji-certify/issues/1044) | mDoc timestamp format did not comply with ISO specification, failing the OpenID4VP conformance test           |

### Known Issues

All open issues for Inji Certify are listed [here](https://github.com/inji/inji-certify/issues?q=is%3Aissue+state%3Aopen+-milestone%3A1.0.0-rc.1+type%3ABug).

| Git Id                                                  | Description                                                     |
| ------------------------------------------------------- | --------------------------------------------------------------- |
| [#842](https://github.com/inji/inji-certify/issues/842) | Validations to add qrSignatureAlgo in the Credential Config API |
| [#700](https://github.com/inji/inji-certify/issues/700) | Improper validation in Status Update endpoints                  |
| [#730](https://github.com/inji/inji-certify/issues/730) | SVG template: face image and label attribute path mismatch      |

### Breaking Changes

| Change                                                                                                                                             | Required action                                                                                                                                                                                                                                                           | Impact                                                                                              |
| -------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| mdoc credential response structure aligned to OpenID4VCI 1.0                                                                                       | Update wallets/clients to parse the new structure                                                                                                                                                                                                                         | Clients using the previous mdoc response structure cannot read the issued credential                |
| mdoc credential\_signing\_alg\_values\_supported: strings replaced by integer COSE identifiers (e.g. -7)                                           | Update mdoc credential configurations and metadata consumers                                                                                                                                                                                                              | Wallets expecting string algorithm names will not match the published metadata                      |
| ldp\_vc credential\_signing\_alg\_values\_supported now lists the crypto suite (e.g. Ed25519Signature2020) instead of a JWS algorithm (e.g. EdDSA) | Update wallets/clients that read this metadata for ldp\_vc                                                                                                                                                                                                                | Clients matching on the JWS algorithm will not find a match                                         |
| Credential configuration metadata is mandatory; properties fallback removed;                                                                       | Send cryptographicBindingMethodsSupported and proofTypesSupported on every Add and Update, plus signatureAlgo in DataProvider mode. Add jwk to the ldp\_vc and dc+sd-jwt entries of mosip.certify.credential-config.cryptographic-binding-methods-supported if you use it | Requests that omit these attributes, even Updates that change only an unrelated field, are rejected |
| Inji Verify service in PDI replaced by the embedded library                                                                                        | Remove configuration pointing to an external Inji Verify service for PDI                                                                                                                                                                                                  | A separately deployed Inji Verify service is no longer used by Certify                              |
| PEX replaced by DCQL in the PDI VP request                                                                                                         | Change PDI VP request configurations from presentation\_definition to DCQL (dcqlQuery)                                                                                                                                                                                    | PDI requests configured with a Presentation Exchange definition are not supported                   |
| Velocity 1.7 to 2.4.1                                                                                                                              | Review credential templates: empty values are false in #if; $velocityCount and $velocityHasNext become $foreach.count and $foreach.hasNext; reflective calls are blocked                                                                                                  | Templates relying on old behaviour render differently or fail                                       |
| eSignet 1.8.0 configuration                                                                                                                        | Set mosip.esignet.discovery.issuer-id to the eSignet issuer base URL (e.g. https://esignet-mock.released.mosip.net/), not the /v1/esignet URL. For MOSIP ID use cases set mosip.certify.ida.vci-user-info-cache=esignet:userinfo instead of userinfo                      | With the old values, Certify does not work with eSignet 1.8.0                                       |

### Supported Platforms & Components

#### Repositories Released

| Repository                 | Version     | Release Date  |
| -------------------------- | ----------- | ------------- |
| inji-certify               | v1.0.0-rc.1 | November 2026 |
| inji-config                | v1.0.0-rc.1 | November 2026 |
| digital-credential-plugins | v1.0.0-rc.1 | November 2026 |

#### Compatible Modules

| Module                    | Version                   |
| ------------------------- | ------------------------- |
| keymanager                | v1.4.0                    |
| eSignet                   | 1.8.0                     |
| IDA                       | 1.3.0                     |
| Sunbird C                 | v2.0.0                    |
| esignet-mock-services     | v0.11.2                   |
| commons                   | 1.6.0                     |
| inji-verify (verify-core) | 1.0.0-rc.1                |
| mimoto                    | 1.0.0-rc1(yet to release) |
| inji-web                  | 1.0.0-rc1(yet to release) |

### Documentation

* [Feature Documentation](https://docs.inji.io/inji-certify/overview/features)
* [Local Setup](https://docs.inji.io/inji-certify/build-and-deploy/local-setup)
* [API Documentation](https://mosip.stoplight.io/docs/inji-certify)
* Test Report
