# DPoP-Constrained Access Tokens

#### What it is

DPoP (Demonstrating Proof of Possession, [RFC 9449](https://www.rfc-editor.org/rfc/rfc9449.html)) binds an access token to a key pair held by the wallet. A stolen token cannot be replayed without the matching private key.

#### How it works

Inji Certify is the **resource server**. It validates DPoP but does not issue DPoP-bound tokens.

1. The wallet requests a token from an authorization server such as eSignet. The client must be registered with additionalConfig.`dpop_bound_access_tokens: true`.
2. The authorization server puts the thumbprint of the wallet's public key in the token as `cnf.jkt`.
3. The wallet calls the credential endpoint with Authorization: DPoP and a fresh DPoP proof JWT.
4. Certify verifies the token, then the proof, and issues the credential.

| Token                | Presented as          | Result                    |
| -------------------- | --------------------- | ------------------------- |
| Plain (no cnf)       | Bearer                | Accepted                  |
| DPoP-bound (cnf.jkt) | DPoP with valid proof | Accepted                  |
| DPoP-bound           | Bearer                | Refused (downgrade guard) |
| Plain                | DPoP                  | Refused                   |

#### Proof checks

Certify checks that the proof:

* Is a single JWT with typ dpop+jwt
* Uses an allowed asymmetric algorithm and embeds a public jwk
* Has a valid signature
* Has htm equal to the HTTP method and htu equal to the public credential endpoint URL
* Has an iat within the allowed age
* Has ath equal to the hash of the access token
* Has a key thumbprint equal to cnf.jkt
* Has not been used before (jti replay protection)

#### Configuration

| Property                                    | Purpose                                                       | Example                                         |
| ------------------------------------------- | ------------------------------------------------------------- | ----------------------------------------------- |
| mosip.certify.authn.filter-urls             | URLs protected by the token filter                            | { '${server.servlet.path}/issuance/credential'} |
| mosip.certify.domain.url                    | Public issuer URL, used for the htu check                     | http://localhost:8090                           |
| mosip.certify.dpop.allowed-algorithms       | Accepted proof algorithms                                     | ES256,ES384,ES512,RS256,PS256,EdDSA             |
| mosip.certify.dpop.proof-max-age            | Maximum proof age in seconds                                  | 60                                              |
| mosip.certify.dpop.clock-skew               | Clock drift tolerance in seconds                              | 10                                              |
| mosip.certify.dpop.jti.cache-expire-seconds | Replay cache TTL. Must exceed proof-max-age + 2 \* clock-skew | 120                                             |
| mosip.certify.cache.names                   | Must include dpopJti                                          | ...,dpopJti                                     |

Certify refuses to start if the dpopJti cache TTL is missing or too short. In multi-replica deployments use a distributed cache (spring.cache.type=redis), otherwise a replayed proof can pass on a different pod.

{% hint style="info" %}
**Notes**:

* Tokens minted by Certify's own /oauth/token (pre-authorized and PDI flows) are Bearer tokens, so DPoP applies only to tokens from an external authorization server.
* DPoP protects against a stolen token alone, not a captured token plus an unused proof. Use TLS on every hop.
{% endhint %}
