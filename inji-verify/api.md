---
icon: plug
---

# API

Refer to Inji Verify API Documentation here - [https://mosip.stoplight.io/docs/inji-verify/63da8fc2ca609-open-id-4-vp-verifier-api-inji-verify](https://mosip.stoplight.io/docs/inji-verify/63da8fc2ca609-open-id-4-vp-verifier-api-inji-verify)



***

## Changes which came with 'Inji Verify - 1.0.0-alpha.1'

### API Redesign

Key APIs now return verification _evidence_, not just a final status.

* **/vc-verification** — Still returns the compact SUCCESS / INVALID / EXPIRED / REVOKED outcome, now with formally defined Content-Type headers per format, a 415 for unsupported media types, and structured internal-error bodies (e.g. STATUS\_RETRIEVAL\_ERROR).
* **/v2/vc-verification** — Returns a per-check breakdown: allChecksSuccessful plus schemaAndSignatureCheck, expiryCheck, per-purpose statusCheck entries, and optional claims — each failure carrying a structured error code/message.
* **/vp-result/{txnId}** — Enhanced to return per-credential results instead of one aggregated status, and remains backward compatible with both DCQL and legacy Presentation Definition submissions.
* **/v2/vp-results/{txnId}** — Structured result for the presentation and each credential within it, including holderProofCheck: for SD-JWT, KB-JWT nonce/aud are verified against the Authorization Request; for JSON-LD, the VP signature is verified.
* **/vp-session-results** — The cookie-based endpoint shares the same rich body as /v2/vp-results/{txnId} and gains a full error model (401 VP\_SESSION\_INVALID, MALFORMED\_COOKIE, RESPONSE\_CODE\_NOT\_USED); the session cookie is cleared after processing.

### New /v2 Endpoints

The request and submission flow is re-versioned for OpenID4VP 1.0 (final) and SD-JWT VC draft-10; the /v2 endpoints are **not backward compatible**.

* **/v2/vp-request** — Requires dcql\_query. Supports pre-registered clients (request by value) and decentralized\_identifier: clients (request by reference via requestUri). Caller nonce must be ≥ 16 URL-safe characters, else a secure nonce (≥ 128 bits) is generated. Granular validation errors cover request parsing and the full DCQL structure.
* **/v2/vp-session-request** — Same contract as /v2/vp-request, plus a base64-encoded transaction\_id HttpOnly cookie (15-minute lifetime) for session flows.
* **/v2/vp-request/{requestId}** — Serves the Authorization Request as a signed JWT (application/oauth-authz-req+jwt) for by-reference flows.
* **/v2/vp-submission/direct-post** — vp\_token is a JSON object keyed by DCQL query\_id (arrays of presentations); presentation\_submission is no longer accepted. The full DCQL validation suite runs all-or-nothing before cryptographic verification, alongside state, nonce, and client-id/aud checks; duplicate and expired submissions are rejected. Wallet errors are reported via error/error\_description.

### Standardized Error Responses

All endpoints return typed error bodies: ErrorResponse (errorCode + errorMessage) for 4xx and InternalErrorResponse (timestamp, status, path, error) for 500, with complete per-endpoint error-code tables published in the [API documentation](https://mosip.stoplight.io/docs/inji-verify/67445477d332e-open-id-4-vp-verifier-api-inji-verify).

