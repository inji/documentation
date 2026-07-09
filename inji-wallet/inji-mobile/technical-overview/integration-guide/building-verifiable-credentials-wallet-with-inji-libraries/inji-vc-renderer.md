# Inji VC Renderer

## Overview

Inji VC Renderer is a library designed to render Verifiable Credentials (VCs) by converting SVG templates into visual SVG images. The library dynamically replaces placeholders in SVG templates with actual Verifiable Credential JSON data, strictly following the JSON Pointer Algorithm (RFC6901) for value extraction.

**Key Responsibilities:**

* **VC Rendering Library**

    * Downloads SVG templates from the VC's render method
    * Replaces template placeholders with actual VC data
    * Supports multiple rendering methods and generates visual credential displays
    * Follows JSON Pointer Algorithm (RFC6901) for accurate data extraction

* **Library Consumer App**

    * Provides the Verifiable Credential data
    * Handles the display of credentials


## Supported Features

### Core Capabilities

* **SVG Template Processing**: Downloads SVG templates from URLs specified in the VC render method
* **Dynamic Placeholder Replacement**: Replaces Mustache-style placeholders with actual VC data using JSON Pointer Algorithm (RFC6901)
* **VC Data Model 2.0 Support**: Compatible with the latest Verifiable Credential specification
* **QR Code Embedding**: Optionally embeds QR codes within SVG templates for credential verification

### Supported Credential Formats

Currently supported credential format:
- **ldp_vc** - Linked Data Proofs Verifiable Credentials

## Libraries Available In

Inji VC Renderer is available in Kotlin and Swift, supporting Android, JVM and iOS platforms.

- **Kotlin**: [Android (AAR) & JVM (JAR)](https://github.com/inji/inji-vc-renderer/tree/master/kotlin)
- **Swift**: [iOS](https://github.com/inji/inji-vc-renderer-ios-swift/tree/master)

### Core Methods

The library provides a primary API for rendering credential display content:

#### `generateCredentialDisplayContent()`

Converts a Verifiable Credential into visual SVG representation by processing render methods and replacing template placeholders.

**Parameters:**

* `credentialFormat` - Enum specifying the credential format (currently supports `ldp_vc`)
* `vcJsonString` - The Verifiable Credential in stringified JSON format
* `wellKnownJson` (Optional) - Well-known metadata in stringified JSON format
* `qrCodeData` (Optional) - Custom data for QR code generation. If provided, QR code is generated using this value; if not provided or empty, the full VC JSON string is used as fallback. **Note**: `qrCodeData` should be pre-encoded (e.g., Base45-encoded)

**Returns:**

* List of rendered SVG templates as strings
* Multiple SVG templates are returned if multiple render methods are present in the VC

> **For comprehensive API documentation and detailed usage examples, refer to the respective repository documentation:**
> - [Kotlin/Java Repository](https://github.com/inji/inji-vc-renderer/tree/master/kotlin#api)
> - [Swift/iOS Repository](https://github.com/inji/inji-vc-renderer-ios-swift/tree/master#api)

### Rendering Process Flow

The library follows these steps to render credential display content:

1. **Render Method Extraction** - Extracts render method information from the VC JSON
2. **SVG Template Download** - Downloads the SVG template from the URL specified in the render method
3. **Placeholder Replacement** - Uses JSON Pointer Algorithm (RFC6901) to extract values from VC JSON and replace placeholders in the SVG
4. **QR Code Generation** - Optionally generates and embeds a QR code (if `qrCodeData` is provided)
5. **Output Generation** - Returns the fully rendered SVG as a string

If multiple render methods exist in the VC, this process is repeated for each, and all rendered SVGs are returned as a list.

---

> Refer to the [Inji Certify documentation](../../../../../inji-certify/overview/features/README.md#9-svg-rendering-support) for details on issuing credentials with SVG Rendering Support and the corresponding credential structure.


