# Production checklist

Before inviting users:

- [ ] The Stockero key exists only in server-side secrets.
- [ ] The key is absent from Git history, frontend bundles, mobile bundles, and screenshots.
- [ ] Your backend authenticates its own users.
- [ ] Your proxy allowlists endpoints and validates every query parameter.
- [ ] Upstream requests have an 8–10 second timeout.
- [ ] Identical reads are cached for 30–60 seconds.
- [ ] Logs include Stockero `X-Request-Id`, status, and error code but never the key.
- [ ] `401` disables the integration instead of retrying forever.
- [ ] `429` and temporary `5xx` responses use capped exponential backoff.
- [ ] Empty arrays and nullable fields render correctly.
- [ ] Unknown response fields and enum values do not crash the app.
- [ ] Product comments are displayed as plain text, never trusted HTML.
- [ ] The interface tells users that community inventory should be verified before travel.
- [ ] You know how to contact an administrator for revocation.

Test with ZIP codes that return results and ZIP codes with no reports. Also test expired reports, unavailable upstream services, timeout behavior, and a deliberately invalid key.
