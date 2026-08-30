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

Display the human-readable `message` to the user when appropriate. Record `code` and `requestId` for support, but never log session cookies or CSRF tokens.

## Common status codes

| Status | Meaning                                           |
| ------ | ------------------------------------------------- |
| `200`  | Request succeeded                                 |
| `201`  | Report created and published                      |
| `202`  | Report saved; publication is retrying             |
| `400`  | Invalid request or query                          |
| `401`  | Missing, invalid, or expired session              |
| `403`  | Role, reporting-access, or CSRF failure           |
| `404`  | Record was not found                              |
| `409`  | Duplicate report, repeated vote, or edit conflict |
| `413`  | Request body exceeds 16 KB                        |
| `429`  | Rate or report limit reached                      |
| `500`  | Unexpected internal error                         |
| `503`  | A required service is temporarily unavailable     |

## Request limits

The default API request limits are 120 paid-member requests and 60 staff requests per IP per minute. Limits may change during beta. Clients should stop retrying rapidly after `429` and wait before trying again.

## Versioning

The current base path is `/api/v1`. Backward-compatible fields may be added without changing the version. Removing fields, changing their meaning, or changing enum behavior requires a new API version or a documented migration period.

Clients should handle unknown response fields and unknown enum values safely.
