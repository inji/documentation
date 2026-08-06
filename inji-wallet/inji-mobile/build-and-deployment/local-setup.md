---
icon: list-tree
---

# Local Setup

This is the docker-compose setup to run mimoto which act as BFF for Inji Wallet and backend for Inji web. This docker compose setup is intended only for local use and not for production deployment.

## What is in the docker-compose folder?

* **`certs`** folder holds the p12 file which is created as part of OIDC client onboarding.
* **`config`** folder holds the mimoto system properties file, issuer configuration and credential template.
* **`docker-compose.yml`** file with the mimoto setup.

## How to run this setup?

1. **Prepare the environment:**
   * The `docker-compose` folder's `config` directory holds the configuration files Mimoto needs to act as BFF for Inji Wallet.
   * **Create a `certs` folder** in the `docker-compose` directory and add the OIDC client certificate (see below).
   * **Update the configuration files:**
     * `mimoto-issuers-config.json` — add identity providers as issuers. See [Credential Providers](../technical-overview/customization-overview/credential_providers.md) for how to structure each entry.
     * `mimoto-trusted-verifiers.json` — add the verifiers' clientId, redirect and response URIs, for Verifiable Credential Online Sharing.
     * Update the **Esignet host** reference in `mimoto-default.properties` (or `application-local.properties` if running Mimoto via IDE).
     * Set the `oidc_p12_password` environment variable in `docker-compose.yml` to match the password used for `oidckeystore.p12`.
   * **Create an OIDC client** and generate `oidckeystore.p12`, placed inside the `certs` folder. Follow [Credential Providers](../technical-overview/customization-overview/credential_providers.md) for this process.
   * **Update `mimoto-issuers-config.json`** with the `client_id` and `client_alias` from your OIDC onboarding.

2. **If you're only running Inji Wallet (mobile), do this before starting the services:** remove the `datashare` and `minio` services from `docker-compose.yml` (and the `datashare` dependency from `mimoto-service`'s `depends_on`), and set `qr_code_type` to `"EmbeddedVC"` for all issuers in `mimoto-issuers-config.json`. This also means you don't need to pull the datashare/minio images at all.

3. **\[Optional] Configure Google OAuth Client Credentials**
   * Only needed for Mimoto's own "Login with Google" feature — not required to run Inji Wallet locally. `docker-compose.yml` ships with working placeholder values, so this can be skipped for a wallet-only setup.
   * If you do need it, refer to [How to create Google Client Credentials](#how-to-create-google-client-credentials) below, then add the generated credentials to `docker-compose.yml`:
     ```yaml
         environment:
           - GOOGLE_OAUTH_CLIENT_ID=<your-client-id>
           - GOOGLE_OAUTH_CLIENT_SECRET=<your-client-secret>
     ```

4. **Start the services:**
   ```bash
   docker-compose up
   ```
   Use the `-d` flag to run in detached (background) mode.

5. **Stop the services:**
   ```bash
   docker-compose down
   ```
   To stop and remove a single service: `docker-compose stop <service_name>` then `docker-compose rm <service_name>`.

6. **Removing the Docker Volume:** if you update `oidckeystore.p12`, Mimoto may fail to start — the new file won't contain the keys already stored in the database's key alias table, and their absence breaks encryption/decryption. Fix it by clearing the stale data:
   ```bash
   docker volume rm docker-compose_postgres-data
   ```

7. **Access APIs as:**
   * `http://localhost:8099/v1/mimoto/allProperties`
   * `http://localhost:8099/v1/mimoto/issuers`
   * `http://localhost:8099/v1/mimoto/issuers/{issuer-id}`
   * `http://localhost:8099/v1/mimoto/issuers/{issuer-id}/well-known-proxy`

## How to create Google Client Credentials

To enable Google OAuth2.0 authentication, follow these steps:

1. **Go to the Google Cloud Console**: Visit [Google Cloud Console](https://console.cloud.google.com/).
2. **Create a New Project**: If you don't already have a project, create one from the project dropdown.
3. **Enable the OAuth Consent Screen**: "APIs & Services" > "OAuth consent screen". Select "External" and configure the required fields. Save.
4. **Create OAuth 2.0 Credentials**: "APIs & Services" > "Credentials" > "Create Credentials" > "OAuth 2.0 Client IDs" > "Web application".
5. **Authorized JavaScript Origins**: `http://localhost:8099`
6. **Authorized Redirect URIs**: `http://localhost:8099/v1/mimoto/oauth2/callback/google`
7. **Save and Retrieve Client Credentials**: you'll receive a `Client ID` and `Client Secret` — add them to `docker-compose.yml` as shown in step 3 above.

## Inji Mobile Wallet Configuration

Set the eSignet host Mimoto should use — update `mosip.esignet.host` in `mimoto-default.properties` (or `application-local.properties` if running Mimoto via IDE) to point to the eSignet instance for your target environment:

```properties
mosip.esignet.host=<Host url of e-signet service> (E.g. https://esignet.env.mosip.net)
```

Then point your local Inji Wallet build at this Mimoto instance — set `MIMOTO_HOST` to your ngrok URL (not `localhost`) in the wallet app's `.env` file (see [Setup → Command to build the application](./README.md#2-command-to-build-the-application)).

Note:
- For local env use [ngrok](https://ngrok.com/docs/getting-started/).
- Replace `http://localhost:8099` by the ngrok public domain at the following places:
  - `token_endpoint` in `mimoto-issuers-config.json`
  - `mosipbox.public.url`, `mosip.api.public.url` in `mimoto-default.properties`
- After editing `mimoto-issuers-config.json`, restart `nginx` then `mimoto-service` for the change to take effect 
