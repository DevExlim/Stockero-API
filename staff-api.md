# Staff API

Staff endpoints power the private PokeStock Watch admin panel. They are not intended for public or third-party integrations.

## Moderator endpoints

- `GET /admin/reports` — list reports for review
- `GET /admin/reports/{id}` — retrieve report history, votes, and delivery information
- `PATCH /admin/reports/{id}` — change report status with a required reason
- `GET /admin/users` — list reporters
- `PATCH /admin/users/{id}` — restrict or restore reporting access
- `GET /admin/abuse` — list safety flags
- `PATCH /admin/abuse/{id}` — dismiss a flag, remove a report, or restrict a reporter

## Administrator endpoints

- `GET /admin/stores` — list managed stores
- `PATCH /admin/stores/{id}` — change store information or visibility
- `POST /admin/stores/{id}/merge` — merge a duplicate store
- `GET /admin/audit` — list staff actions

Every mutation requires a reason and is recorded in staff history. Administrator-only information must never be copied into public API responses or public logs.
