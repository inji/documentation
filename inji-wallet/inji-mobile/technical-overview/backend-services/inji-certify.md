# Inji Certify

## Overview

The Inji Certify service is utilized by Inji Wallet for downloading the VC.

### Download VC

The user is currently on the `Add new card` screen and chooses an issuer(For example, Republic of Veridonia National ID Department).

* Inji Wallet utilizes the `react-native-app-auth` library for authorization flow.
  * It first redirects the user to the authorization server configured respective to the Issuer (For example, e-Signet).
  * The user performs authentication (For example, on the eSignet UI, the input the necessary information such as a unique ID and OTP (One-time Password)).
  * Post successful authentication, the user is redirected back to the Inji Wallet app with an authorization code.
  * Inji Wallet then exchanges the authorization code for an access token.
* Using the access token, Inji Wallet makes a request to the credential endpoint from Inji Certify to download the credential.

#### VC Issuance endpoint

{% openapi-operation spec="api" path="/vci/credential" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

For credential request, refer credential\_endpoint attribute in issuer's configuration response.

Read More
