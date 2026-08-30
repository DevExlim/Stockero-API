# Server-side quickstart

## 1. Configure secrets

Add these values to your backend or serverless platform, not to frontend configuration:

```text
STOCKERO_API_BASE_URL=https://pokestock.watch/api/v1
STOCKERO_API_KEY=stk_live_...
```

## 2. Check the API from your server

```bash
curl "https://pokestock.watch/api/v1/stores/nearby?zip=10001&radius=15&limit=10" \
  --header "Authorization: Bearer $STOCKERO_API_KEY" \
  --header "Accept: application/json" \
  --header "X-Request-Id: your-unique-request-id"
```

## 3. Confirm the response envelope

List endpoints return `data` and `meta`:

```json
{
  "data": [],
  "meta": { "count": 0, "nextCursor": null }
}
```

An empty `data` array is a successful result, not an API failure.

## 4. Add timeout and error handling

Set a timeout, check `response.ok`, and record `error.code` plus `error.requestId`. Never automatically retry a permanent `400`, `401`, `403`, or `404` response.

## 5. Add short caching

Cache matching reads for approximately 30–60 seconds and avoid polling while the app is in the background.

Continue with the [Node.js example](quickstart-node.md) or [mobile architecture example](quickstart-mobile.md).
