# Features

## Overview

Inji Verify empowers organizations to validate Verifiable Credentials (VCs) instantly through an intuitive web portal. Whether scanning QR codes, uploading documents, or verifying credentials via secure OpenID4VP flows, verifiers can confirm credential authenticity in seconds—reducing manual verification time and ensuring trust across education, healthcare, government, and enterprise sectors..

The platform combines modular SDK components with enterprise-grade security, enabling seamless integration into existing verifier applications while maintaining compliance with W3C VC Data Model standards.

## Standards, Specifications, and Compliance

Inji Verify adheres to industry standards for interoperable and trustworthy credential verification.

### Credential Formats

| Format                          | Description                                                                |
| ------------------------------- | -------------------------------------------------------------------------- |
| **W3C VC Data Model 1.1 & 2.0** | Industry-standard Verifiable Credentials ensuring interoperability         |
| **JSON-LD**                     | Linked data credentials with semantic context                              |
| **SD-JWT**                      | Selective Disclosure JWT credentials with privacy-preserving claim sharing |

### QR Code Encoding Standards

| Standard      | Description                                                                                                                                                                                |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Claim 169** | MOSIP specification for encoding credentials into compact, machine-readable QR codes using CBOR (Concise Binary Object Representation) for efficient, offline-friendly credential delivery |

### Cryptographic Algorithms

| Algorithm                     | Support Status |
| ----------------------------- | -------------- |
| Ed25519 Verification Key 2018 | Supported      |
| Ed25519 Verification Key 2020 | Supported      |
| RSA Verification Key 2018     | Supported      |
| ECC R1 (P-256 / secp256r1)    | Supported      |

### Verification Methods

* `did:web` with proofValue or JWS
* `https://` endpoints with proofValue or JWS

### Protocol Support

* **OpenID4VP**: Cross-device and same-device Verifiable Presentation flows per OpenID specifications

## Core Verification Features

### QR Code Scanning

Verify credentials instantly by scanning QR codes directly through your device's camera, including Claim 169–encoded credentials.

* **Real-time Camera Scanning**: Point your device camera at any QR code to initiate instant verification, eliminating manual data entry and reducing verification time to seconds
* **Claim 169 Support**: Verify compact QR-encoded credentials mapped to Claim 169 standard for offline-friendly credential delivery
* **Mobile Zoom Control**: Adjust magnification using the zoom slider for optimal scanning accuracy, especially useful for small or densely-encoded QR codes
* **Multi-Version Support**: Compatible with QR code versions v1 through v27, ensuring broad interoperability with credentials from various issuers

### Document Upload Verification

Upload credential documents directly to the portal for verification when scanning isn't possible.

* **Multi-Format Support**: Upload PDFs, JPEG, JPG, and PNG files containing embedded QR codes, providing flexibility for different credential formats
* **Extended QR Support**: Process QR code versions up to v32 through the upload feature, supporting higher-density credentials that exceed scan capability
* **Batch Document Processing**: Verify credentials embedded in multi-page documents without extracting individual pages

### OpenID4VP Presentation Verification

Verify Verifiable Presentations securely using OpenID4VP standards for both cross-device and same-device scenarios.

* **Cross-Device Flow**: Generate authorization requests as QR codes that users scan with their mobile wallet (Inji Web or any OpenID4VP-compliant wallet), receive signed Verifiable Presentations, and display validated results
* **Same-Device Flow**: Initiate verification on the same mobile device via deep links, enabling seamless app-to-app credential sharing without a second device
* **Streamlined Online Sharing**: Embed URLs instead of dense VCs in QR codes, reducing complexity while maintaining secure credential retrieval from designated storage locations
* **Inji Web Wallet OpenID4VP Integration**: Establish a secure, standards-compliant credential exchange between Inji Verify (verifier) and Inji Web Wallet (holder), enabling privacy-preserving presentation and verification flows

### Modern Credential Query Support (DCQL)

Inji Verify now describes what it needs from a wallet using DCQL (Digital Credentials Query Language), the OpenID4VP 1.0 standard for expressing credential requirements — replacing the earlier Presentation Exchange format.

* **Precise, Privacy-Preserving Requests**: Verifiers ask for exactly the claims they need, with support for alternative ways to satisfy a request, instead of over-specifying.
* **Stronger Holder Proof**: Verification can require cryptographic proof that the person presenting a credential is the person it was issued to.
* **Replay Protection**: A captured presentation can't be reused in a different verification session.
* **Broader SD-JWT Compatibility**: Recognizes SD-JWT credentials under both the older and newer format identifiers, so wallets on either side of the spec transition still verify successfully.
* **Reliable Credential Matching**: Matches submitted credentials by type more precisely, even when multiple verifier configurations accept the same credential type.
* **Verify UI Enhancements** — Submitted credentials are matched via DCQL type\_values, keeping matching accurate when multiple verifier configurations share a credential type.

### DCQL Query Capabilities

* **Per-query holder binding** — require\_cryptographic\_holder\_binding (default true); outcome surfaces as holderProofCheck in results.
* **Type constraints** — meta.type\_values for ldp\_vc (OR-of-ANDs, IRI fragment matching); meta.vct\_values for SD-JWT (exact match).
* **Claim-level requests** — claims paths with optional expected values; claim\_sets for acceptable combinations.
* **Credential combinations** — credential\_sets (OR across options, AND within); optional sets via required: false.
* **Multiplicity** — multiple (default false) allows more than one presentation per query.

### Digital Credentials API (DC API)

Inji Verify now supports the **W3C Digital Credentials API** (OpenID4VP 1.0, Appendix A) as a same-device presentation path. <!-- In addition to --> /Instead of rendering a QR code or deep-linking to a wallet app, the verifier hands the signed Authorization Request to the browser, which mediates credential selection with the user's wallet and returns the presentation to the page. 
Cross-device QR-code flows continue to use `direct_post`; the DC API is for same-device presentations only (for now).

- **Session creation** — `POST /v2/vp-session-request` with `responseMode: "dc_api"`. `responseCodeValidationRequired` must be `false`; response-code redirects do not apply to browser-mediated flows.
- **Signed requests only** — `clientId` must use a signed-request prefix (`decentralized_identifier:` or `x509_san_dns:`), so the wallet can verify verifier identity before releasing credentials. Plain pre-registered client IDs are not accepted for DC API.
- **Origin binding** — `expected_origins` is derived from the request's `Origin` / `Referer` header, stored on the authorization request and embedded in the signed request JWT. The submission's `Origin` / `Referer` must match the stored values.
- **Origin-bound holder proof** — The expected audience becomes `origin:<canonical-origin>` instead of the `clientId`: for SD-JWT the KB-JWT `aud`, and for JSON-LD the `proof.domain`, are validated against the origin.
- **Request JWT shape** — For `dc_api` the signed request omits `state` and `response_uri`, and carries `expected_origins`.
- **Submission** — New endpoint `POST /vp-submission/dc-api` (JSON), called by the verifier SDK rather than the wallet. It correlates by `requestId` (the role `state` plays in direct-post), needs no cookie, and returns `200 OK` with an empty body. Wallet protocol failures are reported on the same endpoint using `error` / `error_description`.
- **Result retrieval** — Unchanged: `POST /vp-session-results` with the existing HttpOnly `transaction_id` cookie.

### SDK and UI integration

- **New SDK props** — `enableDcApi` (default `false`) turns on the DC API path, and `dcApiTimeoutMs` (default `300000`) bounds the request-JWT fetch and `navigator.credentials.get` call; invalid values fall back to 5 minutes.
- **Graceful fallback** — If DC API is enabled but unsupported by the browser or the configured `clientId`, the SDK silently falls back to the deep-link / native-wallet path without surfacing `DC_API_NOT_SUPPORTED`. On desktop that fallback still requires `webWalletBaseUrl`.
- **Mutual exclusivity** — `enableDcApi` and `webWalletBaseUrl` cannot be used together; Verify UI disables DC API automatically when a web wallet is selected.
- **Deployment flag** — `ENABLE_DC_API=true` in verify-ui maps to the SDK's `enableDcApi`. `ENABLE_DC_API` and `CLIENT_ID_X509` are configurable through Helm `extraEnvVars`.

### X.509 Client Identification (`x509_san_dns` + `x5c`)

A verifier can now identify itself with an X.509 certificate instead of a DID, giving deployments that already run a PKI a way to establish verifier trust without DID resolution.

- **Client ID prefix** — `client_id=x509_san_dns:<dns-name>`, used for by-reference flows alongside the existing `decentralized_identifier:` prefix.
- **Certificate chain in the JWT header** — The Authorization Request JWT served from `GET /v2/vp-request/{requestId}` carries `x5c` (the full leaf-first, base64-DER chain) instead of `kid`. The wallet validates the chain and signature directly, and checks that the DNS name in `client_id` is one of the leaf certificate's Subject Alternative Names — no DID document lookup involved.
- **Per-request selection** — A single deployment can serve both by-reference schemes side by side; whether a request JWT gets `kid` or `x5c` is decided per request from its own `client_id` prefix, not from a global setting.
- **Deployment identity check** — The DNS name after the prefix must match the deployment's configured identity (`inji.verify.x509-san-dns.host`, env `INJI_X509_SAN_DNS_HOST`) and must appear as a SAN on the signing certificate in the configured keystore.
- **Errors** — Request-creation failures return `400 Bad Request` with `errorCode: invalid_request` (distinguish causes by `errorMessage`). Signing-time failures are detected when the wallet fetches the JWT and currently surface as `500 Internal Server Error` without a structured body.
- **Not checked** — Whether the host of `response_uri` matches the `x509_san_dns` `client_id`.

### Embeddable `verify-core` Library

`verify-service` has been split into two Maven modules under a `verify-service-parent` aggregator:

- `verify-core` — An embeddable library carrying the verification domain logic (VP request creation, DCQL validation, VP token verification, result processing). Applications such as Certify can depend on it directly instead of calling Inji Verify over HTTP.
- `verify-service` — The deployable Spring Boot application: controllers, OpenAPI, actuator, caching and datasource wiring on top of `verify-core`.
- **Validation moved to the service layer** — Request validations previously performed in controllers now live in the service layer, so embedding applications get the same validation behaviour as the HTTP API.
- **Quality gates** — Sonar analysis is configured for the new `io.inji.verify:verify-core` module.

### SD-JWT Credential Verification

Verify selective disclosure credentials while preserving holder privacy.

* **Selective Attribute Display**: Visually distinguish disclosed claims from undisclosed attributes, providing transparency about what information is shared
* **Cross-Flow Compatibility**: Verify SD-JWT VCs via QR scanning, upload, and VP verification flows with consistent behavior
* **Privacy-Preserving Validation**: Confirm credential authenticity without requiring disclosure of all embedded claims

### Real-Time Verification

Instant validation results without processing delays.

* **Immediate Feedback**: Verification results displayed within seconds of submission
* **No Queue Processing**: Direct validation without batch processing delays
* **Live Status Updates**: Progress indicators during credential processing

## Credential Display & Status

### Revocation Status Checking

Ensure credentials are current and valid by checking issuer revocation status.

* **Real-time Status Verification**: Query credential status against issuer registries to detect revoked credentials immediately
* **Visual Status Indicators**: Display clear valid, invalid, or revoked status with color-coded results for instant comprehension
* **Trust Maintenance**: Prevent acceptance of invalidated credentials, protecting organizational integrity

### Credential Status Display

Clear visual presentation of verification results.

* **Valid Credentials**: Green indicators confirm active, verified credentials with full claim display
* **Invalid Credentials**: Red indicators highlight credentials that fail cryptographic validation
* **Expired Credentials**: Amber indicators show credentials past their validity period

### Multilingual Credential Display

View and verify credentials in multiple languages for global accessibility.

* **Localized Claim Values**: Display credential claims in the holder's or verifier's preferred language based on issuer-provided translations
* **11 Language Support**: Interface available in English, Portuguese, Spanish, French, Arabic, Khmer, Tamil, Hindi, and Kannada
* **Regional Accessibility**: Improve verification experiences across diverse populations and geographic regions

### SVG Credential Rendering

Display credentials with issuer-intended visual presentation and branding.

* **Original Design Preservation**: Render credentials in Scalable Vector Graphics format maintaining layout, typography, and visual elements
* **Brand Consistency**: Display credentials exactly as issuers designed them, ensuring visual authenticity alongside cryptographic validation
* **High-Resolution Output**: Crisp credential display across all screen sizes and resolutions

### Error Handling & User Guidance

Guide users through verification issues with actionable feedback.

* **Invalid QR Detection**: Clear messaging when QR codes contain malformed or unreadable data
* **Expired Credential Alerts**: Informative notices when credentials have passed validity dates
* **Decoding Failure Guidance**: Step-by-step instructions for resolving upload or scanning issues
* **API v2 Diagnostic Information**: The redesigned /vc-verification and /vp-result/{txnId} endpoints now return diagnostic details beyond simple pass/fail status, including specific failure reasons (expiry, revocation, signature issues, policy mismatches). This enables applications to provide targeted, actionable error guidance to users with precise next steps, significantly reducing the need for custom error handling logic on the integrator side

## Integrations & SDK

Also read:

* [Integration Guide](https://github.com/mosip/documentation/blob/inji/docs/inji-verify/overview/docs/inji-verify/technical-overview/integration-guides/openid4vp-vp-verification-integration-guide.md)

### Modular SDK Components

Embed verification capabilities directly into your verifier applications using plug-and-play components.

* **Scan/Upload Component**: Integrate QR code scanning or file upload functionality into your application without building from scratch
* **OpenID4VP VP Verification Component**: Add cross-device and same-device VP verification flows aligned with OpenID4VP specifications
* **Independent NPM Modules**: Import only the components you need, reducing bundle size and dependency overhead

| Component       | Technology                | Purpose                             |
| --------------- | ------------------------- | ----------------------------------- |
| Scan/Upload     | TypeScript / React 18.2.0 | QR code capture and file upload     |
| VP Verification | TypeScript / React 18.2.0 | OpenID4VP presentation verification |

### PixelPass Library Integration

Decode QR codes accurately using the integrated PixelPass SDK.

* **CBOR Decoding**: Process CBOR-encoded QR codes for compact credential verification
* **Reliable Data Extraction**: Ensure accurate decoding of embedded credential data for downstream validation
* **Library Version**: Integrated [PixelPass v0.8.0-RC2](https://www.npmjs.com/package/@injistack/pixelpass/v/0.8.0-RC2?activeTab=versions) for secure processing

### Backend Verification Services

Robust server-side verification with persistent data storage.

* **VC-Verifier Library Integration**: Server-side verification supporting Ed25519 and RSA cryptographic standards
* **PostgreSQL Database**: Durable data storage replacing in-memory solutions, ensuring verification continuity and audit trails
* **VP Proof Verification**: Validate both Verifiable Credentials and Verifiable Presentations server-side
* **Server-Side VP Verification with ECC R1**: Verify Verifiable Presentations on the server using R1-curve cryptography, centralizing trust decisions, reducing client-side complexity, and aligning with modern decentralized identity standards

### API Documentation

* [Inji Verify APIs](https://mosip.stoplight.io/docs/inji-verify/63da8fc2ca609-open-id-4-vp-verifier-api-inji-verify)

## Ecosystem Compatibility

### MOSIP UIN-Based VC Support

Verify credentials issued using MOSIP Unique Identification Numbers.

* **MOSIP Ecosystem Integration**: Seamlessly validate UIN-based credentials within MOSIP identity frameworks
* **Expanded Interoperability**: Support verification of national ID credentials across MOSIP-aligned implementations

### DID Method Support

* **did:web**: Resolve issuer keys from web-hosted DID documents
* **HTTPS Endpoints**: Direct key resolution from issuer-hosted verification endpoints

## Deployment & Platform Support

### Docker Compose Deployment

Simplify installation and deployment with containerized setup.

* **Quick Setup**: Deploy the complete verification stack with a single Docker Compose command
* **Environment Consistency**: Ensure identical configurations across development, staging, and production environments
* **Resource Isolation**: Run verification services in isolated containers for security and performance

### Scalable Architecture

Handle growing verification volumes without performance degradation.

* **Horizontal Scaling**: Distribute load across multiple verification instances
* **Optimized Performance**: Efficient resource utilization under varying demand
* **Enterprise-Ready**: Support high-volume verification scenarios for large organizations

### UI Theme Customization

Adapt the verification portal appearance to match organizational branding.

* **Custom Theming**: Configure colors, logos, and visual elements to align with your organization's identity
* **White-Label Ready**: Deploy branded verification portals for country-specific or enterprise implementations

### Supported Browsers

| Browser         | Minimum Version |
| --------------- | --------------- |
| Google Chrome   | 103.0+          |
| Mozilla Firefox | 100.0+          |
| Microsoft Edge  | 104.0+          |
| Safari (macOS)  | 14.1+           |

### Camera Requirements for Scanning

| Requirement | Specification           |
| ----------- | ----------------------- |
| Resolution  | 12 megapixels or higher |
| Quality     | 1020p minimum           |
| Lighting    | Well-lit environment    |
| Effects     | No filters or dark mode |

### QR Code Version Compatibility

| Feature | Supported Versions | Notes                                     |
| ------- | ------------------ | ----------------------------------------- |
| Scan    | v1 - v22           | Consistent performance                    |
| Scan    | v23 - v27          | Variable results based on content density |
| Upload  | v1 - v32           | Full support                              |

## Additional Capabilities

Features that enhance the overall verification experience:

### Responsive Interface Design

Optimal verification experience across all devices and screen sizes.

* **Mobile-First Design**: Full functionality on smartphones with back camera scanning capability
* **Desktop Optimization**: Enhanced layout for larger screens with keyboard accessibility
* **Cross-Browser Compatibility**: Consistent experience across Chrome, Firefox, Edge, and Safari

### Enhanced Security

Protect sensitive credential data throughout the verification process.

* **Digital Signature Validation**: Cryptographic verification ensures credential authenticity and detects tampering
* **Encryption Protection**: Secure handling of sensitive information during processing
* **PixelPass Security**: Secure QR code processing through audited library implementation

## Upcoming Features

Refer to Roadmap 2026 to keep updated about the upcoming features [here](../../../readme/roadmap/).
