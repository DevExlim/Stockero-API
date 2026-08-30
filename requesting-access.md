# Requesting access

Stockero is currently intended for a small number of trusted integrations. You must be signed in to PokeStock Watch before requesting a key.

## Request and approval flow

1. Open **Developers** in the PokeStock Watch member navigation.
2. Enter the app name, platform, expected daily requests, and a clear description.
3. Confirm that the key will be stored only on a secure server.
4. Wait for an administrator to approve or reject the request.
5. After approval, return to **Developers** and choose **Reveal API key once**.
6. Copy the full `stk_live_…` value immediately to your server's secret manager or environment configuration.

The full key is displayed once. PokeStock Watch stores an irreversible hash after it is claimed and cannot recover it for you. If it is lost, ask an administrator to revoke it and submit a replacement request.

## What to include in a good request

- Who will use the app
- Whether it is a web, iOS, Android, desktop, or backend integration
- Which API data the app displays
- How often it polls Stockero
- Estimated requests per day
- A website or private repository link, when available

Approval applies only to the app described in the request. A materially different app needs a separate review.

## Expiration and revocation

Private-beta keys expire 90 days after approval unless the administrator configures another lifetime. A key can be revoked immediately if it is leaked, misused, or no longer needed. Your app must handle `401 INVALID_API_KEY` without entering a retry loop.
