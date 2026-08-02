---
name: Create and fulfill an order
description: Create an order in Whiplash/Rydership, add order items, submit it for fulfillment, and retrieve shipping documents.
api: openapi/whiplash-merchandising-openapi-original.json
operations: [PostApiV2Orders, PostApiV2OrdersIdOrderItems, GetApiV2OrdersId, PutApiV2OrdersIdCallAction, GetApiV2OrdersIdShippingDocuments]
---

# Create and fulfill an order

Base URL: `https://www.getwhiplash.com/api/v2`. Auth: OAuth 2.0 authorization_code
access token (Bearer). Access is invite-only.

## Steps

1. **Create the order** — `POST /api/v2/orders` (`PostApiV2Orders`) with the
   shipping address, customer, and shipping method. Capture the returned order `id`.
2. **Add line items** — for each SKU, `POST /api/v2/orders/{id}/order_items`
   (`PostApiV2OrdersIdOrderItems`) referencing the `item_id` and quantity. (Or
   create the order with items inline.)
3. **Submit for fulfillment** — `PUT /api/v2/orders/{id}/call/{action}`
   (`PutApiV2OrdersIdCallAction`) with the appropriate action to release the
   order to the warehouse. Discover valid actions via `GET /api/v2/orders/actions`.
4. **Poll status** — `GET /api/v2/orders/{id}` (`GetApiV2OrdersId`) until the
   order reaches a shipped state.
5. **Retrieve shipping documents** — `GET /api/v2/orders/{id}/shipping_documents`
   (`GetApiV2OrdersIdShippingDocuments`) for labels/packing slips.

## Rules

- Pagination on list endpoints: `page` + `per_page`. Errors return `{ "message": "..." }`.
- 409 Conflict means the order is already in a state that disallows the action —
  re-fetch and reconcile before retrying.
- No idempotency key is supported; avoid blind retries of `POST /orders`.
- Subscribe to webhooks (see the webhook skill) instead of tight polling.
