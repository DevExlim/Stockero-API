# Architecture for your app

The safe request path is:

```text
Your web or mobile client
          |
          | HTTPS to your authenticated backend
          v
Your backend / serverless function
          |
          | Authorization: Bearer stk_live_...
          v
Stockero API
```

Your backend should validate its own users, build an allowlisted Stockero query, call Stockero with the secret key, and return only the fields your interface needs.

## Recommended backend responsibilities

- Keep `STOCKERO_API_KEY` in server-only configuration.
- Validate ZIP codes, coordinates, radius, limit, and pagination cursor before forwarding them.
- Set an 8–10 second upstream timeout.
- Cache identical read requests briefly, normally 30–60 seconds.
- Preserve Stockero's `X-Request-Id` in your logs.
- Map Stockero errors to a safe message for your users.
- Use exponential backoff only for `429` and temporary `5xx` responses.
- Never expose admin, Discord, MongoDB, or Google credentials.

## Example application flow

For a local-store screen, your client sends a ZIP code to `GET /api/stores?zip=10001` on your own backend. Your backend calls `GET /stores/nearby?zip=10001&radius=25`, caches the result briefly, and sends the public store/restock fields back to the client.

Do not give clients a general-purpose proxy that accepts any Stockero URL. Explicitly allow the endpoints and query parameters your app needs.
