# Online Login

## Overview

**Online Login** enables users to securely access digital services using a verifiable credential stored in the Inji Wallet. Instead of using traditional usernames and passwords, users can authenticate themselves by presenting a trusted digital credential, completing user verification, and consenting to share only the required information with the service provider.

---

## Example Use Case
This use case is applicable to any service provider portal that supports wallet-based authentication through a compatible Authorization Server (AS).

The following example demonstrates the online login flow within the Inji ecosystem using **eSignet** as the Authorization Server.

* **Authorization Server (AS):** eSignet
* **Service Provider:** Health ID Services Portal
* **Credential Issuer:** Republic of Veridonia National ID Department
* **Credential:** Veridonia National ID

In this example, a user downloads the Veridonia National ID credential into the Inji Wallet and later uses it to securely sign in to the Health ID Services Portal.

---

## User Journey

1. Open the **Inji Wallet** application.
2. Tap the **+** button and download a credential from the **Republic of Veridonia National ID Department**.
3. After the credential is downloaded, open the credential menu (⋮) and activate it.
4. Open the **Health ID Services** portal and select **Sign in with eSignet**.
5. A QR code is displayed on the portal. Using the Inji Wallet, scan the QR code from the **Share** tab or the credential's **QR Login** option.
6. Complete the face authentication.
7. Review the requested claims and choose the information to share.
8. Provide consent.
9. The requested claims are securely shared, and the user is successfully signed in to the Health ID Services portal.

---

## APIs Involved

The user is required to open the portal integrated with eSignet and utilize the app scanner to scan the QR code.


### Link Login Transaction
After successfully scanning the QR code, Inji Wallet will access the API below and transmit the link code.

{% openapi-operation spec="api" path="/linked-authorization/v2/link-transaction" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Authenticate User

After successful face authentication, the wallet authenticates the user.

{% openapi-operation spec="api" path="/linked-authorization/v2/authenticate" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

### Submit User Consent

Once the user approves the requested claims, the wallet submits the consent.

{% openapi-operation spec="api" path="/linked-authorization/v2/consent" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

---

## Benefits

* Passwordless authentication using digital credentials.
* User-controlled sharing of identity attributes.
* Explicit consent before any information is shared.
* Reusable across multiple service provider portals.
* Secure authentication using trusted verifiable credentials.

---

## Reference

For details about the Wallet Authentication APIs, refer to the [eSignet Wallet Authenticator documentation](https://docs.esignet.io/esignet-authentication/develop/integration/wallet/wallet-authenticator#wallet-authentication-apis)
