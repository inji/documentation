# Configuration

## Configuration for Inji Wallet

The configurable properties for Inji Wallet can be found at [inji-default.properties](https://github.com/inji/inji-config/blob/master/inji-default.properties). This property file is maintained as one for each deployment environment. On [this](https://github.com/inji/inji-config) repository, each environment configuration is placed in a corresponding branch specific to that environment.

> Refer to [inji-default.properties](https://github.com/inji/inji-config/blob/collab/inji-default.properties) of Collab environment.

These values will be used by Inji Wallet via Mimoto. Mimoto loads all the configurations and exposes an API which is used by the Inji Wallet application to fetch and store the configurations in the local storage.

API used to fetch these configurations:

```http
GET /v1/mimoto/allProperties
```

For example, in the Collab environment:

```text
https://api.collab.mosip.net/v1/mimoto/allProperties
```

The implementers can choose to use the existing configurations or add new configurations to them.

## Properties Used by Mobile

| Property | Default | Purpose |
| --- | --- | --- |
| `mosip.inji.allowedAuthType` | `demo,otp,bio-Finger,bio-Iris,bio-Face` | Allowed auth types for IDA-based flows. |
| `mosip.inji.allowedEkycAuthType` | `demo,otp,bio-Finger,bio-Iris,bio-Face` | Allowed eKYC auth types. |
| `mosip.inji.allowedInternalAuthType` | `otp,bio-Finger,bio-Iris,bio-Face` | Allowed internal auth types. |
| `mosip.inji.faceSdkModelUrl` | `https://${mosip.api.public.host}/inji` | Base path for downloading face SDK model assets. |
| `mosip.inji.modelDownloadMaxRetry` | `10` | Maximum retry count for face model download. |
| `mosip.inji.vcDownloadMaxRetry` | `10` | Maximum retry count while polling/downloading credentials. |
| `mosip.inji.vcDownloadPoolInterval` | `6000` | Poll interval, in milliseconds, for VC download status checks. |
| `mosip.inji.audience` | `ida-binding` | Audience value used in wallet binding/token flows. |
| `mosip.inji.issuer` | `residentapp` | Issuer value used in wallet binding/token flows. |
| `mosip.inji.warningDomainName` | `https://${mosip.api.public.host}` | Domain shown/used by warning screens and request handling. |
| `mosip.inji.openId4VCIDownloadVCTimeout` | `30000` | Timeout, in milliseconds, for OpenID4VCI credential download calls. |
| `mosip.inji.aboutInjiUrl` | Environment-specific docs URL | URL opened from the About Inji Wallet screen. |
| `mosip.inji.minStorageRequiredForAuditEntry` | `2` | Minimum free storage, in MB, before audit entries are written. |
| `mosip.inji.minStorageRequired` | `2` | Minimum free storage, in MB, before downloaded or received VCs are stored. |
| `mosip.inji.openid4vpClientValidation` | `true` | Enables pre-registered verifier validation in OpenID4VP sharing. |

## Related Mimoto Configuration

Several wallet behaviors are configured in [`mimoto-default.properties`](https://github.com/inji/inji-config/blob/master/mimoto-default.properties), not `inji-default.properties`. Common examples:

| Property | Purpose |
| --- | --- |
| `mosip.openid.issuers` | File name for issuer configuration, usually `mimoto-issuers-config.json`. |
| `mosip.openid.verifiers` | File name for trusted verifier configuration, usually `mimoto-trusted-verifiers.json`. |
| `mosip.inji.web.url` and `mosip.inji.web.redirect.url` | Inji Web URL and redirect URL used by OVP flows. |
| `mosip.inji.qr.data.size.limit`, `mosip.inji.qr.code.height`, `mosip.inji.qr.code.width` | QR generation limits and size defaults. |
| `mosip.inji.ovp.qrdata.pattern`, `mosip.inji.ovp.redirect.url.pattern`, `mosip.inji.ovp.error.redirect.url.pattern` | OpenID4VP QR and redirect URL templates. |
| `wallet.passcode.*` | Wallet passcode retry and lock behavior. |
| `cache.*.expiry-time-in-min` | Cache expiry for issuer config and well-known responses. |

## App Build-Time Configuration

Some customization is build-time configuration in the mobile app, not server-side configuration:

| Variable | Used by | Purpose |
| --- | --- | --- |
| `MIMOTO_HOST` | `shared/constants.ts` | Base URL used by wallet API calls to Mimoto. |
| `ESIGNET_HOST` | `shared/constants.ts` | Base URL used by linked authorization calls. |
| `APPLICATION_THEME` | `components/ui/styleUtils.ts`, `app.config.ts`, `SplashScreen.tsx` | Selects default vs purple theme and adaptive splash image. |
| `LIVENESS_DETECTION` | `shared/constants.ts` | Enables/disables liveness detection checks. |
| `DEBUG_MODE` | `shared/constants.ts` | Enables debug behavior in the app. |

Keep deployment config, Mimoto config, and mobile build-time variables in sync. `MIMOTO_HOST` only sets the wallet's Mimoto base URL; issuer and token endpoints are configured on the Mimoto side, primarily through `mimoto-issuers-config.json`, and must be valid for the selected Mimoto deployment.
