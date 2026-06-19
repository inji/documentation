# eSignet

The eSignet service is utilized by Inji Wallet for online login. Users have the ability to log in to any service provider portal that is integrated with eSignet.

## Online login

### QR code scanning and login to the service provider portal

The user is required to open the portal integrated with eSignet and utilize the app scanner to scan the QR code.

After successfully scanning the QR code, Inji Wallet will access the API below and transmit the link code.

#### Link Transaction endpoint V2

{% openapi-operation spec="api" path="/linked-authorization/v2/link-transaction" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

After successfully completing the offline face authentication and selecting the required and optional information, the two specified APIs are invoked.

#### Linked Authentication Endpoint V2

{% openapi-operation spec="api" path="/linked-authorization/v2/authenticate" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}

#### Linked Consent Endpoint V2

{% openapi-operation spec="api" path="/linked-authorization/v2/consent" method="post" %}
[OpenAPI api](https://4401d86825a13bf607936cc3a9f3897a.r2.cloudflarestorage.com/gitbook-x-prod-openapi/raw/a642986d423ac4ddb8b24e8d67b93a4e7b72f36ba27efafa5dd7ad15507aba07.txt?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=dce48141f43c0191a2ad043a6888781c%2F20260619%2Fauto%2Fs3%2Faws4_request&X-Amz-Date=20260619T063153Z&X-Amz-Expires=172800&X-Amz-Signature=9b94089a8690b19e0b374d14c6d4fa809f268501594b2b68b212edd04cb0b2a0&X-Amz-SignedHeaders=host&x-amz-checksum-mode=ENABLED&x-id=GetObject)
{% endopenapi-operation %}
