# Stockero API

Stockero is the private, read-only developer API for PokeStock Watch. An approved integration can retrieve published community restocks, discover nearby Best Buy stores, and read aggregate community statistics without connecting directly to MongoDB or the Discord bot.

{% hint style="warning" %}
**Private beta:** access is manually approved. An API key belongs to one app and one developer. Do not share, resell, or expose it in browser or mobile application code.
{% endhint %}

## Base URL

```text
https://pokestock.watch/api/v1
```

Every API response is JSON. Dates are ISO 8601 UTC strings, resource IDs are 24-character hexadecimal strings, and enum values use `snake_case`.

## What private keys can access

| Scope           | What it permits                                              |
| --------------- | ------------------------------------------------------------ |
| `restocks:read` | List published restocks and retrieve one report              |
| `stores:read`   | Find nearby stores, retrieve one store, and list its reports |
| `stats:read`    | Read aggregate member-visible statistics                     |

API keys cannot create reports, vote, send Discord alerts, moderate users, or access admin data. Those actions remain protected by the PokeStock Watch website session.

## First successful request

```bash
curl "https://pokestock.watch/api/v1/restocks?zip=10001&radius=10&limit=10" \
  --header "Authorization: Bearer $STOCKERO_API_KEY" \
  --header "Accept: application/json"
```

Start with [Requesting access](requesting-access.md), then follow the [server-side quickstart](quickstart.md).
