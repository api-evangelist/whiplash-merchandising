---
name: Manage inventory and inbound shipments
description: Create catalog items (SKUs), send inbound stock via ship notices, and check on-hand quantities by warehouse in Whiplash/Rydership.
api: openapi/whiplash-merchandising-openapi-original.json
operations: [PostApiV2Items, GetApiV2Items, GetApiV2ItemsIdWarehouseQuantities, PostApiV2Shipnotices, GetApiV2ItemsIdTransactions]
---

# Manage inventory and inbound shipments

Base URL: `https://www.getwhiplash.com/api/v2`. Auth: OAuth 2.0 Bearer token.

## Steps

1. **Create/verify the item** — `POST /api/v2/items` (`PostApiV2Items`) to create
   a SKU, or `GET /api/v2/items?search=...` (`GetApiV2Items`) to find an existing one.
2. **Send inbound stock** — `POST /api/v2/shipnotices` (`PostApiV2Shipnotices`)
   to create a ship notice (ASN) declaring which items and quantities are arriving
   at the warehouse; add ship-notice items as needed.
3. **Check on-hand** — `GET /api/v2/items/{id}/warehouse_quantities`
   (`GetApiV2ItemsIdWarehouseQuantities`) for stock by warehouse.
4. **Audit history** — `GET /api/v2/items/{id}/transactions`
   (`GetApiV2ItemsIdTransactions`) for the item's inventory transaction ledger.

## Rules

- Use `fields` for sparse responses and `associations` to embed related records.
- List endpoints paginate with `page` / `per_page` and expose `page_total`.
- Bulk item/ship-notice creation is available via `/bulk` endpoints.
