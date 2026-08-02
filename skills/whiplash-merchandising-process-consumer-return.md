---
name: Process a consumer return
description: Look up the original order and create/track a consumer return (RMA) in Whiplash/Rydership.
api: openapi/whiplash-merchandising-openapi-original.json
operations: [GetApiV2Orders, PostApiV2ConsumerReturns, GetApiV2ConsumerReturnsId, PutApiV2ConsumerReturnsId]
---

# Process a consumer return

Base URL: `https://www.getwhiplash.com/api/v2`. Auth: OAuth 2.0 Bearer token.

## Steps

1. **Find the original order** — `GET /api/v2/orders?search=...` (`GetApiV2Orders`)
   to locate the order and its `id` / customer.
2. **Create the return** — `POST /api/v2/consumer_returns`
   (`PostApiV2ConsumerReturns`) referencing `order_id` and the return items
   (`item_id` / `order_item_id`). For exchanges, set `exchange_order_id`.
3. **Track it** — `GET /api/v2/consumer_returns/{id}` (`GetApiV2ConsumerReturnsId`)
   to follow the return's warehouse processing.
4. **Update if needed** — `PUT /api/v2/consumer_returns/{id}`
   (`PutApiV2ConsumerReturnsId`) to adjust the return.

## Rules

- Bulk returns: `POST /api/v2/consumer_returns/bulk`.
- 422 Unprocessable Entity signals validation failures — read `message`.
- Attach custom data with `/{id}/meta_fields`.
