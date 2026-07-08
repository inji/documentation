# Mimoto

Mimoto is a BFF(Backend for Frontend) for Inji Wallet. It's being used to get default configuration, download verifiable credentials (VC) and activate VC.\
It provides all necessary APIs to the Inji Wallet and acts as a proxy for resident services. Mimoto gets the request from Inji Wallet, performs all the validations and forwards it to respective services. Additionally, it subscribes to the web-sub event to be able to download the VC once it's ready.

Detailed API documentation of Mimoto is available [here](https://mosip.stoplight.io/docs/mimoto).

## Support for downloading VC from multiple Issuers

### Issuers Listing

The user is currently on the `+` button on the Home screen, which will open `Add new card` screen, where all the issuers are displayed Below issuers list API gives out all the issuers list

{% swagger src="../../../../.gitbook/assets/mimoto (1).json" path="/issuers" method="get" %}
[mimoto (1).json](<../../../../.gitbook/assets/mimoto%20(1).json>)
{% endswagger %}

To get complete configuration of the specific issuer, below api is called.

{% swagger src="../../../../.gitbook/assets/mimoto (1).json" path="/issuers/{issuer-id}" method="get" %}
[mimoto (1).json](<../../../../.gitbook/assets/mimoto%20(1).json>)
{% endswagger %}

### Retrieve accessToken for OIDC flow
This endpoint exchanges an OAuth 2.0 authorization code for an access token as part of the OpenID4VCI authorization flow for a Mimoto client registered with an Authorization Server (AS).

The issuer name is used to resolve the corresponding Authorization Server and its token endpoint from the issuer configuration (`issuers-config.json`). The client authenticates with the Authorization Server using the same cryptographic key pair that was registered during client registration. The token request includes a signed client assertion JWT to authenticate the client before the Authorization Server issues an access token.


API: POST /v1/mimoto/get-token/{issuer}

https://mosip.stoplight.io/docs/mimoto/6fc8a9a1587a5-retrieve-access-token-for-oidc-flow

## Online Login

There is a usecase of activating / binding a credential to an Authorization server and using that Authorization Server, an online service can be logged in 
using that binded credential. This usecase is avaiklable within Inji ecosystem as "Mosip or National ID" usecase. 
This usecase uses eSignet as an Authorization Server for the Mosip / National ID credential downloaded from Inji Certify for logging in to health id services.

### Activate credentials


Credentials have to be activated in order to use them for online login. When a user selects **Activate** option, an OTP is sent to the user and credentials are activated.

* To send an OTP to a user, the below API is called.

{% swagger src="../../../../.gitbook/assets/mimoto (1).json" path="/binding-otp" method="post" %}
[mimoto (1).json](<../../../../.gitbook/assets/mimoto%20(1).json>)
{% endswagger %}

* After successful OTP validation, a keypair is generated in the phone and the public key is synced with server. The mimoto receives a certificate and create thumbprint which it stores in the keystore securely. This is called as the **activation process.**

{% swagger src="../../../../.gitbook/assets/mimoto (1).json" path="/wallet-binding" method="post" %}
[mimoto (1).json](<../../../../.gitbook/assets/mimoto%20(1).json>)
{% endswagger %}


## Configuration

The configurable properties for mimoto can be found at [mimoto-default.properties](https://github.com/mosip/mosip-config/blob/collab1/mimoto-default.properties). This property file is maintained as one for each deployment environment. On [this](https://github.com/mosip/mosip-config) repository, each environment configuration is placed in a corresponding branch specific to that environment.

> Refer to [mimoto-default.properties](https://github.com/mosip/mosip-config/blob/collab1/mimoto-default.properties) of Collab environment.

The implementers can choose to use the existing configurations or add new configurations to them.

### Wallet Configurations

**API:** `GET /v1/mimoto/allProperties`

**Reference:** [inji-default.properties](https://github.com/inji/inji-config/blob/collab/inji-default.properties)

```properties
# Timeout for VC download API via OpenID4VCI flow in milliseconds
mosip.inji.openId4VCIDownloadVCTimeout=30000
# Inji documentation URL
mosip.inji.aboutInjiUrl=https://docs.inji.io/inji-wallet/inji-mobile
# Minimum storage space required for making audit entries in MB
mosip.inji.minStorageRequiredForAuditEntry=2
# Minimum storage space required for downloading/receiving VCs in MB
mosip.inji.minStorageRequired=2
# Specifies whether to perform client validation during the OpenID4VP sharing flow
mosip.inji.openid4vpClientValidation=false
# Defines the lifetime of cached data in storage, measured in milliseconds
mosip.inji.cacheTTLInMilliSeconds=3600000

# Specifies whether to perform credential offer VC verification in OpenID4VCI flow (To be removed in future releases)
mosip.inji.disableCredentialOfferVcVerification=true

# OpenID4VP wallet configuration defining the wallet capabilities
mosip.inji.openid4vpWalletConfig={"response_types_supported":["vp_token"],"vp_formats_supported":{"mso_mdoc":{"issuerauth_alg_values":[-7],"deviceauth_alg_values":[-7]},"ldp_vc":{"proof_type_values":["Ed25519Signature2020","JsonWebSignature2020"]},"dc+sd-jwt":{"sd-jwt_alg_values":["EdDSA","ES256"],"kb-jwt_alg_values":["ES256","EdDSA"]},"vc+sd-jwt":{"sd-jwt_alg_values":["EdDSA","ES256"],"kb-jwt_alg_values":["ES256","EdDSA"]}},"client_id_prefixes_supported":["redirect_uri","decentralized_identifier","pre-registered"],"request_object_signing_alg_values_supported":["EdDSA"],"authorization_encryption_alg_values_supported":["ECDH-ES"],"authorization_encryption_enc_values_supported":["A256GCM"],"presentation_definition_uri_supported":true,"request_uri_methods_supported":["get","post"]}
```

[//]: # (TODO: Add swagger)

#### Property Descriptions

1. **`cacheTTLInMilliSeconds`**: Defines the cache expiration time, in milliseconds, for API fallback. If an API request fails, the SDK uses the cached response for the APIs listed in the table below, provided the cache entry has not expired.

**API Fallbacks available as cache**

| API                                        | Endpoint                   |
|:-------------------------------------------|:---------------------------|
| **getAllProperties**                       | `/v1/mimoto/allProperties` |
| **fetchIssuers**                           | `/v1/mimoto/issuers`       |
| **fetchTrustedVerifiersList**              | `/v1/mimoto/verifiers`     |
| **fetchIssuerWellknownConfig**             | `{issuer}/.well-known/...` |
| **fetchIssuerAuthorizationServerMetadata** | `{server}/.well-known/...` |

2. **`minStorageRequired`**: Defines the minimum available device storage required for operations such as VC downloads and VC backup restoration. If sufficient storage is not available, the operation cannot proceed, and an error screen is displayed.
3. **`minStorageRequiredForAuditEntry`**: Defines the minimum available device storage required before initiating operations such as VC sharing, QR-based sharing, and BLE-based VC sharing, as these operations create audit history entries.
4. **`aboutInjiUrl`**: Defines the "About Inji" URL, which is displayed on the application's "About Inji" page.
5. VC Download-related Properties
    1. **`openId4VCIDownloadVCTimeout`**: Timeout, in milliseconds, for downloading a Verifiable Credential (VC) using the OpenID4VCI flow.
    2. **`disableCredentialOfferVcVerification`**: Disables verification of Verifiable Credentials (VCs) received through the OpenID4VCI credential offer flow.
6. OpenID4VP-related Properties
    1. **`openid4vpWalletConfig`**: Defines wallet-specific configuration for the OpenID4VP flow.
    2. **`openid4vpClientValidation`**: Enables or disables client validation against the pre-registered client list for the OpenID4VP flow.
        1. true – validate clients against the pre-registered list.
        2. false – skip client validation.
    3. For more information, see [Inji Wallet Usage](https://github.com/inji/inji-wallet/blob/master/docs/openid4vp/openid4vp-support.md#wallet-configuration-for-the-openid4vp-flow)



{% swagger src="../../../../.gitbook/assets/mimoto (1).json" path="/allProperties" method="get" %}
[mimoto (1).json](<../../../../.gitbook/assets/mimoto%20(1).json>)
{% endswagger %}



### Wallet's Trusted / Pre-registered Verifier list

The Inji Wallet retrieves the list of pre-registered (trusted) verifiers from the Mimoto backend service.

- **Backend Service:** Mimoto
- **API:** `/v1/mimoto/verifiers`

The API response provides the list of trusted verifiers, which is then embedded into the `walletConfig`. This configuration is supplied to the Inji OpenID4VP library to execute **client validation** during the OpenID4VP flow.

[//]: # (TODO: Add swagger)

