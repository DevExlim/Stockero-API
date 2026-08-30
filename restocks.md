# Restocks

## List restocks

```text
GET /restocks
```

Returns published member-visible reports. Without a `status` parameter, only active and low-stock reports are returned.

### Query parameters

| Parameter                        | Description                                      |
| -------------------------------- | ------------------------------------------------ |
| `zip`                            | Five-digit US ZIP code                           |
| `latitude`, `longitude`          | Coordinate search; both must be supplied         |
| `radius`                         | Search radius from 1 to 100 miles; default 25    |
| `product`                        | Product text search                              |
| `status`                         | `active`, `low_stock`, or `sold_out`             |
| `storeId`                        | Restrict results to one store                    |
| `limit`                          | 1–100 results; default 25                        |
| `cursor`                         | Cursor returned by the previous response         |
| `sort`                           | `newest`, `oldest`, or `distance`                |
| `north`, `south`, `east`, `west` | Map bounding box; all four are required together |

## Get one report

```text
GET /restocks/{id}
```

Returns product, quantity, status, timestamps, store information, reporter level, vote totals, and a directions link.

## Submit a report

```text
POST /restocks
```

Requires a paid-member session and CSRF token.

```json
{
  "storeId": "64f000000000000000000001",
  "productName": "Pokémon Elite Trainer Box",
  "quantity": 6,
  "comments": "Located on the front display"
}
```

The report is saved first and then published to the configured Discord channel. A `201` response means immediate publication succeeded. A `202` response means the report was saved and Discord delivery will retry.

Current beta submission rules:

- At least one minute between reports
- Maximum three reports per rolling hour
- Maximum ten reports per rolling day
- Similar active reports by the same person at the same store are blocked for four hours

## Vote on stock

```text
POST /restocks/{id}/vote
```

```json
{
  "vote": "sold_out"
}
```

Allowed values are `confirmed`, `low_stock`, and `sold_out`.

- Members cannot confirm their own reports.
- Two low-stock votes change an active report to low stock.
- Three sold-out votes change a report to sold out.
- Repeating the same vote returns a conflict response.
