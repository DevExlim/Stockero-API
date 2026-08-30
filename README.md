# Stockero API

Stockero API powers the PokeStock Watch member map, community restock reports, stock votes, store discovery, and staff tools.

> **Current availability:** Stockero API v1 is a first-party beta API. It is used by the PokeStock Watch website and requires a current paid-member Discord session. Public API keys and mobile access tokens are not available yet.

## Base URL

```text
https://pokestock.watch/api/v1
```

All request and response bodies use JSON. Dates are ISO 8601 UTC strings, IDs are 24-character hexadecimal strings, and enum values use `snake_case`.

## What the API provides

- Nearby Best Buy store discovery by ZIP code or coordinates
- Active community restock reports
- New report submission and Discord publication
- Confirmed, low-stock, and sold-out votes
- Member statistics
- Audited staff moderation tools
- Service health information

## Health check

`GET /health` is the only endpoint designed for unauthenticated monitoring.

```json
{
  "data": {
    "overall": "operational",
    "checkedAt": "2026-08-29T14:04:30.735Z",
    "services": []
  }
}
```

The machine-readable OpenAPI 3.1 definition is maintained in `docs/openapi-v1.json` in the project repository.
