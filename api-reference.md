# API reference

## Read-only developer endpoints

| Method | Path                    | Required scope  | Purpose                                        |
| ------ | ----------------------- | --------------- | ---------------------------------------------- |
| `GET`  | `/restocks`             | `restocks:read` | List published community restocks              |
| `GET`  | `/restocks/{id}`        | `restocks:read` | Retrieve one published restock                 |
| `GET`  | `/stores/nearby`        | `stores:read`   | Find Best Buy stores near a ZIP or coordinates |
| `GET`  | `/stores/{id}`          | `stores:read`   | Retrieve one public store                      |
| `GET`  | `/stores/{id}/restocks` | `stores:read`   | List reports for one store                     |
| `GET`  | `/stats`                | `stats:read`    | Retrieve aggregate member-visible statistics   |

## Public utility endpoints

| Method | Path       | Purpose                       |
| ------ | ---------- | ----------------------------- |
| `GET`  | `/health`  | Service health for monitoring |
| `GET`  | `/openapi` | OpenAPI 3.1 JSON document     |

## Not available to API keys

Report submission, voting, developer-key management, and all `/admin/*` endpoints require a PokeStock Watch browser session. A bearer key receives `403 API_KEY_NOT_ALLOWED` on these routes.

Response fields may be added during beta. Clients must ignore unknown fields safely.
