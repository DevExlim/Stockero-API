# Stores and statistics

## Find nearby stores

```text
GET /stores/nearby?zip=10001&radius=25&limit=25
```

Returns nearby Best Buy locations, distance, directions, map coordinates, and active restocks for each store. ZIP searches may refresh the internal store directory before results are returned.

**Required scope:** `stores:read`

### Parameters

| Parameter               | Rules                                                 |
| ----------------------- | ----------------------------------------------------- |
| `zip`                   | Five-digit US ZIP code                                |
| `latitude`, `longitude` | Alternative coordinate center; both required together |
| `radius`                | 1–100 miles, default 25                               |
| `limit`                 | 1–50 stores, default 25                               |

Provide either `zip` or a coordinate pair. Do not send both unless you intentionally want coordinates to take precedence.

```json
{
  "data": [
    {
      "id": "64f000000000000000000001",
      "name": "Best Buy Chelsea",
      "address": "60 W 23rd St, New York, NY 10010, USA",
      "city": "New York",
      "state": "NY",
      "zipCode": "10010",
      "latitude": 40.742,
      "longitude": -73.992,
      "distanceMiles": 2.4,
      "directions": "https://www.google.com/maps/dir/?api=1&destination=40.742%2C-73.992",
      "activeRestocks": []
    }
  ],
  "meta": {
    "count": 1,
    "nextCursor": null,
    "center": { "latitude": 40.7506, "longitude": -73.9972 },
    "radiusMiles": 25
  }
}
```

## Get one store

```text
GET /stores/{id}
```

Returns the selected store's public information.

**Required scope:** `stores:read`

## Get a store's restocks

```text
GET /stores/{id}/restocks
```

Returns reports associated with the selected store.

**Required scope:** `stores:read`

## Member statistics

```text
GET /stats
```

Returns community statistics available to signed-in paid members.

**Required scope:** `stats:read`

These endpoints accept either an approved API key with the stated scope or a first-party paid-member browser session. Location results are approximate and should not be used for emergency or safety-critical navigation.
