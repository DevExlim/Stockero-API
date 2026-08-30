# Stores and statistics

## Find nearby stores

```text
GET /stores/nearby?zip=10001&radius=25&limit=25
```

Returns nearby Best Buy locations, distance, directions, map coordinates, and active restocks for each store. ZIP searches may refresh the internal store directory before results are returned.

## Get one store

```text
GET /stores/{id}
```

Returns the selected store's public information.

## Get a store's restocks

```text
GET /stores/{id}/restocks
```

Returns reports associated with the selected store.

## Member statistics

```text
GET /stats
```

Returns community statistics available to signed-in paid members.

All store and statistics endpoints require a paid-member session. Location results are approximate and should not be used for emergency or safety-critical navigation.
