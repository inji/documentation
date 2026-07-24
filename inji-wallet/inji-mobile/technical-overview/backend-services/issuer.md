# Issuer

## Overview

The **Issuer** is one of the backend services that Inji Wallet interacts with to obtain Verifiable Credentials (VCs). As defined by the **OpenID for Verifiable Credential Issuance (OpenID4VCI)** specification, an Issuer is responsible for issuing credentials to eligible users.

Within the Inji ecosystem, **Inji Certify** acts as the Issuer. It exposes the OpenID4VCI endpoints that Inji Wallet uses to request and download issued Verifiable Credentials. User authentication is handled by a separate authorization server (eSignet) before the credential issuance process begins. Once downloaded, Inji Wallet securely stores and manages these credentials on the user's device.

## Credential Download Flow

The following steps describe how Inji Wallet downloads a Verifiable Credential from an Issuer.

1. The user opens the **Add New Card** screen in Inji Wallet and selects an issuer (for example, *Republic of Veridonia National ID Department*).

2. Inji Wallet initiates the authorization flow.
  * The wallet redirects the user to the authorization server configured for the selected issuer (for example, **eSignet**).
  * The user authenticates using the configured authentication mechanism, such as a unique identifier and a One-Time Password (OTP).
  * Upon successful authentication, the authorization server redirects the user back to Inji Wallet with an authorization code.
  * Inji Wallet exchanges the authorization code for an access token.

3. Using the access token, Inji Wallet invokes the Issuer's credential endpoint exposed by **Inji Certify** to download the issued Verifiable Credential.

### Credential Endpoint

The credential issuance endpoint is designed in accordance with the OpenID for Verifiable Credential Issuance (OpenID4VCI) specification. The endpoint URL is provided in the Issuer Metadata response through the `credential_endpoint` attribute.

#### VC Issuance Endpoint

{% openapi-operation spec="api" path="/vci/credential" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

> **For more details**: Refer to the [Inji Certify Documentation](../../../../inji-certify/overview/README.md) to understand credential issuance workflows.
