---
name: Subscribe to fulfillment webhooks
description: Discover available notification events and register/test a webhook notification subscription in Whiplash/Rydership.
api: openapi/whiplash-merchandising-openapi-original.json
operations: [GetApiV2NotificationEvents, PostApiV2NotificationSubscriptions, GetApiV2NotificationSubscriptionsIdTest, DeleteApiV2NotificationSubscriptionsId]
---

# Subscribe to fulfillment webhooks

Base URL: `https://www.getwhiplash.com/api/v2`. Auth: OAuth 2.0 Bearer token.

## Steps

1. **List available events** — `GET /api/v2/notification_events`
   (`GetApiV2NotificationEvents`) to see the event catalog; capture the
   `notification_event_id` for the event you want (e.g. an order/shipment state change).
2. **Create a subscription** — `POST /api/v2/notification_subscriptions`
   (`PostApiV2NotificationSubscriptions`) with `notification_event_id`, your
   `endpoint` URL, and `notification_type`.
3. **Test delivery** — `GET /api/v2/notification_subscriptions/{id}/test`
   (`GetApiV2NotificationSubscriptionsIdTest`) to fire a test payload at your endpoint.
4. **Remove** — `DELETE /api/v2/notification_subscriptions/{id}`
   (`DeleteApiV2NotificationSubscriptionsId`) to unsubscribe.

## Rules

- Prefer webhooks over polling order/item status.
- Your endpoint must return 2xx quickly; process asynchronously.
- See `asyncapi/whiplash-merchandising-notifications-webhooks.yml` for the event model.
