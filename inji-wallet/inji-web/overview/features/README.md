# Features

**Inji Web Wallet** is a browser-based, open-source digital wallet designed for secure **download, verification, storage, and sharing** of Verifiable Credentials (VCs). It supports **OpenID4VCI**, **OpenID4VP**, **IETF** **SD-JWT**, and **W3C VC** standards; no app install required.

### **Multiple Credential Format Support**

Inji Wallet is designed for interoperability and flexibility by supporting a wide range of credential formats:

* **W3C Verifiable Credentials (JSON-LD VCs) Data Model 1.1 & 2.0**
  * Standards-based credential format is widely adopted across ecosystems.
  * Suitable for general-purpose credential issuance and verification.
  * Supports OpenID4VP-based live presentation of JSON-LD & IETF SD-JWT VCs to any compliant verifier
* **ISO 18013-5 (mDL)**
  * Mobile Driving License and Mobile Document specification.
  * Supports use cases like identity verification in transport, law enforcement, and service access.
* **IETF SD-JWT**
  * **IETF** **SD-JWT Verifiable Credentials**: Enables holders to download and share credentials in IETF **SD-JWT format**. This allows users to share only the necessary attributes while keeping other data private, ensuring **privacy-preserving credential sharing**.
  * Allows users to share only the required claims with verifiers via the OpenIDVP flow, where these selectively disclosable claims can be shared as per the user's needs.

This multi-format support allows Inji Wallet to work seamlessly across different ecosystems, ensuring **compatibility, security, and user privacy**.

### Login with Any Identity Provider (IdP)

* Supports Google and other OpenID-compliant IdPs
* Credentials are stored securely in the browser-based wallet after login, enabling access across sessions and devices, depending on the configuration.
* Verifiable Credentials are now stored in the **“Stored Cards”** section.
* You can view and download the credential as a PDF file locally on your system, or print it out once downloaded.
* You can reset your passcode if you forget it during login. However, the option to change the passcode after logging in is currently not available.

### Guest Mode (No Login Required)

* Ideal for privacy-sensitive or public campaigns
* Credentials are downloaded directly to the local device (not stored in the wallet)

### Credential Download Options

* OpenID for VC Issuance: Interoperable with trusted issuers
* Supports Draft 13 & v1.0 of Specification
* Example Issuers:
  * Republic of Veridonia National ID Department - National ID
  * StayProtected Insurance - Insurance Credentials
  * Republic of Veridonia Tax Department - Tax ID
  * AgroVeritas Property & Land Registry - Land Record

### **Credential Sharing Options**

* OpenID for VP Presentation: Interoperable with trusted verifiers
* Supports Draft 23 & v1.0 of Specification
* Example Verifiers:
  * Veridonia Age-Gate Services — Age Verification
  * StayProtected Insurance — Claims Verification
  * Republic of Veridonia Tax Department — Tax ID Verification
  * AgroVeritas Property & Land Registry — Ownership Verification

### **Claim 169 QR Code Support**

* Supports **standardized QR codes** for initiating credential download and sharing flows.
* Download credentials containing embedded Claim 169 QR blocks
* Store and render these QR blocks for display
* Allow users to present the QR-based identity data when required
* Ensure proper validation and security checks (size, format, signature, structure)

### **SVG-based Credential Rendering** <a href="#id-4.-svg-based-credential-rendering" id="id-4.-svg-based-credential-rendering"></a>

* Inji Web Wallet now supports **SVG-based credential rendering** for **Data Model 2.0 VCs**.
* This allows credentials issued under the Data Model 2.0 schema to be displayed as **secure, dynamic SVG visuals** within the wallet.
* The rendering ensures that displayed information (such as name, ID, issuer, and other attributes) directly corresponds to the **cryptographically verified credential data**.
* This enhancement improves **readability**, **user trust**, and **consistency** while maintaining alignment with the underlying verifiable data.
* Support for SVG rendering for other data models may be added in future versions.

### Verifying Credential Authenticity

* Inji Web Wallet uses robust cryptography to verify that the VC is:
  * Digitally signed by a trusted issuer
  * Cryptographically valid based on its proof type
  * Tamper-evident and verifiable using Inji Verify or any compliant verifier

## Storage Options

| Type                      | Description                                     |
| ------------------------- | ----------------------------------------------- |
| **Web Wallet Storage**    | Stored securely in the web wallet after login   |
| **Local Storage (Guest)** | Downloaded PDF with embedded QR for offline use |

## Credential Sharing Options

| Method                     | Description                                                                                                                                                                                                                                                                                                   | Connectivity |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ |
| **Scan PDF**               | Scan PDF on verifier portal (Inji Verify)                                                                                                                                                                                                                                                                     | Online       |
| **Print or Screenshot**    | For physical presentation or screen scanning                                                                                                                                                                                                                                                                  | Offline      |
| **Upload PDF**             | Used in verifier workflows like Inji Verify                                                                                                                                                                                                                                                                   | Online       |
| **OpenID4VP Presentation** | <ul><li>Users can present <strong>JSON-LD VCs</strong> &#x26; I<strong>ETF SD-JWT</strong> through an <strong>OpenID4VP-compliant</strong> flow.</li><li>Enables secure, real-time credential sharing with user consent.</li><li>Fully interoperable with Inji Verify and other compliant verifiers</li></ul> | Online       |

## User Experience Highlights

* Browser-based; no app installation needed
* Clear distinction between **wallet-stored** and **locally stored** credentials
* Guided flows and contextual help for all users

<table data-search="false"><thead><tr><th>Format</th><th>Signature Algorithm</th><th>Web Wallet (Login)</th><th>Guest Mode (Without Login)</th><th>Notes</th></tr></thead><tbody><tr><td>W3C JSON-LD</td><td>ED25519 2018</td><td>Supported</td><td>Supported</td><td>Compact, fast signatures with high security</td></tr><tr><td>W3C JSON-LD</td><td>ED25519 2020</td><td>Supported</td><td>Supported</td><td>Enhanced key format with better structure</td></tr><tr><td>W3C JSON-LD</td><td>RS256 (RSA with SHA-256)</td><td>Supported</td><td>Supported</td><td>Backward compatibility; legacy systems</td></tr><tr><td>W3C JSON-LD</td><td>ECC K1</td><td>Supported</td><td>Supported</td><td>Common in OpenID ecosystem</td></tr><tr><td>W3C JSON-LD</td><td>ECC R1</td><td>Planned</td><td>Planned</td><td>Strong elliptic curve variant</td></tr><tr><td>W3C Data Integrity 2.0</td><td>RS256</td><td>Planned</td><td>Planned</td><td>JWS with canonicalized digest</td></tr><tr><td>W3C Data Integrity 2.0</td><td>EdDSA (Ed25519)</td><td>Planned</td><td>Planned</td><td>Based on JWS EdDSA</td></tr><tr><td>W3C Data Integrity 2.0</td><td>ES256K</td><td>Planned</td><td>Planned</td><td>JWS-based signing with secp256k1</td></tr><tr><td>W3C Data Integrity 2.0</td><td>ES256</td><td>Planned</td><td>Planned</td><td>Strong elliptic curve variant</td></tr><tr><td>JWT VC</td><td>RS256</td><td>Planned</td><td>Planned</td><td>Planned under VC-JWT compliance</td></tr><tr><td>JWT VC</td><td>ES256K</td><td>Planned</td><td>Planned</td><td>Awaiting certification</td></tr><tr><td>JWT VC</td><td>ES256</td><td>Planned</td><td>Planned</td><td>Under consideration</td></tr><tr><td>JWT VC</td><td>x509 (PKI v3)</td><td>Planned</td><td>Planned</td><td>Public key in JWT header; x509 cert chain planned</td></tr><tr><td>SD-JWT VC</td><td>RS256</td><td>Supported</td><td>Supported</td><td>SD-JWT verification being integrated</td></tr><tr><td>SD-JWT VC</td><td>ES256K</td><td>Supported</td><td>Supported</td><td>Selective Disclosure compatible</td></tr><tr><td>SD-JWT VC</td><td>ES256</td><td>Planned</td><td>Supported</td><td>Strong elliptic curve variant</td></tr><tr><td>SD-JWT VC</td><td>EdDSA (Ed25519)</td><td>Supported</td><td>Supported</td><td>Not yet supported in Certify (issuer side)</td></tr><tr><td>SD-JWT VC</td><td>x509 (PKI v3)</td><td>In Progress</td><td>In Progress</td><td>Used for advanced SD-JWT scenarios</td></tr><tr><td>mDoc / mDL</td><td>RS256</td><td>Planned</td><td>Planned</td><td>Used in mobile document ecosystems</td></tr><tr><td>mDoc / mDL</td><td>EdDSA(Ed25519)</td><td>Planned</td><td>Planned</td><td>Widely used in mobile identity contexts</td></tr><tr><td>mDoc / mDL</td><td>ES256K</td><td>Planned</td><td>Planned</td><td>Used in various driver license implementations</td></tr><tr><td>mDoc / mDL</td><td>ES256</td><td>Planned</td><td>Planned</td><td>Emerging support for high-security mobile documents</td></tr><tr><td>mDoc / mDL</td><td>x509 (PKI v3)</td><td>Planned</td><td>Planned</td><td>x509 certificate chain</td></tr></tbody></table>

{% include "../../../../docs/.gitbook/includes/useful-links.md" %}

## Read More

* [Inji Web Wallet User Guide](https://docs.inji.io/inji-wallet/inji-web/functional-overview/end-user-guide)
* [Feature Workflows](https://docs.inji.io/inji-wallet/inji-web/functional-overview/workflow)
