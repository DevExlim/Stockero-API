# Pagination and polling

## Cursor pagination

`GET /restocks` returns a `meta.nextCursor`. When it is not `null`, pass it unchanged as the next request's `cursor` while keeping the other filters and sort order identical.

```text
GET /restocks?zip=10001&limit=25&sort=newest
GET /restocks?zip=10001&limit=25&sort=newest&cursor=64f0...
```

Do not decode or generate cursors. If the filters change, discard the old cursor and begin a new listing.

Distance sorting does not currently provide a continuation cursor. Use an appropriate `limit` and location radius.

## Polling recommendations

- Cache identical responses for 30–60 seconds.
- For an actively visible local feed, poll no faster than once per minute.
- Stop polling while a web tab or mobile app is in the background.
- Add 0–10 seconds of random jitter so all app instances do not refresh simultaneously.
- After `429`, wait at least until the next minute and use exponential backoff.
- After `5xx`, retry at most a few times with backoff.
- Never retry `401` continuously. Disable the integration and request key review.

For a single small integration, this approach is simpler and safer than maintaining a permanent connection.
