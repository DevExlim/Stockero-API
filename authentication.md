# Authentication and security

## Current browser authentication

Stockero v1 currently authenticates protected requests with the secure PokeStock Watch browser session. Login is completed through Discord OAuth, followed by a server-side guild and paid-role check.

Production session cookies are:

- Secure
- HttpOnly
- SameSite=Lax
- Limited to the PokeStock Watch host

The server periodically rechecks Discord membership. Losing the required server membership or role revokes access.

## Access levels

| Level         | Access                                                     |
| ------------- | ---------------------------------------------------------- |
| Public        | Service health only                                        |
| Paid member   | Restocks, stores, voting, reporting, and member statistics |
| Moderator     | Paid-member access plus report and member moderation       |
| Administrator | All moderator tools plus store and audit management        |

## CSRF protection

Every request that creates or changes data requires the session's `X-CSRF-Token`. A missing or invalid token returns `403 INVALID_CSRF`.

## Mobile and third-party applications

Do not reuse browser cookies or embed server credentials in a mobile app. A future public/mobile release should add:

1. Discord authorization code flow with PKCE.
2. A dedicated server-side mobile callback.
3. Short-lived Stockero access tokens.
4. Rotating refresh tokens stored as hashes.
5. Role revalidation and token-family revocation.

Until that system exists, Stockero API should be treated as first-party and browser-only.
