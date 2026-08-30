# Errors, limits, and versioning

## Error format

Every API error uses the same structure:

```json
{
  "error": {
    "code": "AUTHENTICATION_REQUIRED",
    "message": "A valid paid-member session is required.",
    "requestId": "8c510c76-0968-4c85-8c91-25c073bdf966"
  }
}
```

Display the human-readable `message` to the user when appropriate. Record `code` and `requestId` for support, but never log API keys, session cookies, or CSRF tokens.

## Common status codes

| Status | Meaning                                           |
| ------ | ------------------------------------------------- |
| `200`  | Request succeeded                                 |
| `201`  | Report created and published                      |
| `202`  | Report saved; publication is retrying             |
| `400`  | Invalid request or query                          |
| `401`  | Missing, invalid, expired, or revoked credential  |
| `403`  | Role, reporting-access, or CSRF failure           |
| `404`  | Record was not found                              |
| `409`  | Duplicate report, repeated vote, or edit conflict |
| `413`  | Request body exceeds 16 KB                        |
| `429`  | Rate or report limit reached                      |
| `500`  | Unexpected internal error                         |
| `503`  | A required service is temporarily unavailable     |

## Request limits

Private API keys default to 60 requests per key per minute. A separate IP safety limit protects key validation. Limits may be adjusted for an approved integration, but developers must not assume more capacity without written approval.

### Common developer error codes

| Code                     | Meaning                                            | Client action                                    |
| ------------------------ | -------------------------------------------------- | ------------------------------------------------ |
| `INVALID_API_KEY`        | The key is malformed, expired, revoked, or unknown | Stop requests and contact the administrator      |
| `API_KEY_SCOPE_MISSING`  | The key lacks the endpoint's scope                 | Do not retry; request the required access        |
| `API_KEY_NOT_ALLOWED`    | The endpoint accepts browser sessions only         | Do not proxy this operation with the private key |
| `RATE_LIMITED`           | The minute limit was exceeded                      | Wait and retry with exponential backoff          |
| `INVALID_QUERY`          | A query parameter is missing or invalid            | Correct the request; do not retry unchanged      |
| `ZIP_NOT_FOUND`          | The ZIP code could not be resolved                 | Ask the user to check the ZIP code               |
| `ZIP_SEARCH_UNAVAILABLE` | Store search is temporarily unavailable            | Retry later with capped backoff                  |

### Retry guidance

- Do not retry `400`, `401`, `403`, or `404` automatically.
- Retry `429` after a delay that crosses the next minute window.
- Retry `500` or `503` at most a few times using delays such as 1, 2, and 4 seconds plus random jitter.
- Set a total request timeout and show a useful fallback instead of loading forever.

## Versioning

The current base path is `/api/v1`. Backward-compatible fields may be added without changing the version. Removing fields, changing their meaning, or changing enum behavior requires a new API version or a documented migration period.

Clients should handle unknown response fields and unknown enum values safely.

During private beta, breaking changes will be announced directly to approved developers with a migration window whenever practical.
