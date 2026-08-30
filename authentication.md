# Authentication and key security

Send the API key in the standard HTTP `Authorization` header on every private developer request:

```http
Authorization: Bearer stk_live_your_key_here
Accept: application/json
```

Do not send it in a query parameter, URL, cookie, request body, analytics event, crash report, or client-visible log.

## The most important rule

{% hint style="danger" %}
Never call Stockero directly from browser JavaScript, React Native, an iOS app, or an Android app. Users can inspect those applications and steal the key. Your client must call your backend; your backend calls Stockero.
{% endhint %}

Store the value in a secret manager or server environment variable:

```text
STOCKERO_API_KEY=stk_live_...
STOCKERO_API_BASE_URL=https://pokestock.watch/api/v1
```

Do not prefix a public frontend variable such as `NEXT_PUBLIC_`, `VITE_`, or `EXPO_PUBLIC_`.

## Key behavior

- Keys are hashed at rest and cannot be read back after the one-time reveal.
- Each key has explicit read scopes.
- Each key has an expiration date.
- Administrators can see the key prefix and usage metadata, but not the full secret.
- Revocation takes effect on the next request.
- Private API traffic is rate-limited by key.

## Browser sessions are different

PokeStock Watch's own website uses a secure Discord-backed browser session and CSRF protection. That session is for first-party member and admin actions. Third-party developers must not copy or automate browser cookies. API keys are accepted only by approved read endpoints.

## If a key may be exposed

1. Stop the affected deployment.
2. Ask a PokeStock Watch administrator to revoke the key.
3. Remove it from source history, build artifacts, logs, and analytics.
4. Submit a replacement request.
5. Review how it leaked before deploying the replacement.
