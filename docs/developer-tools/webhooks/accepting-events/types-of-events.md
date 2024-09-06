---
sidebar_position: 10
---

# Types of events

Whenever Rabo Smart Pay delivers an event, the HTTP request to your server will include an `x-smartpay-event-type`
containing the, well, type of the event.

Which events are delivered to which destinations is managed through
[webhook subscriptions](../managing-subscriptions.md).

If your server receives an event that it does not know of that delivery should be acknowledged regardless, as to avoid
getting the delivery [retried](./retrying-failed-deliveries.md). Next you should probably check your subscriptions, and
remove the unexpected event from the webhook subscription.

:::info covered by the SDK

When using the `smartPay.processWebhook` or equivalent method of the SDK, parsing the correct event type, and dealing
with unexpected types is taken care of automatically.

:::

## Available events

### order.status.finalized/v1
This event indicates that an order has reached a final status, and thus will not change anymore.

In case where the final state of the order is successful, this is your trigger to e.g. create a shipment, or update your
customer's credit in your systems.

```json
{
    "id": "ev_z8c2c4txckfq7j7gm2tk9",
    "type": "order.status.finalized/v1",
    "subscription": {
        "id": "wsb_akn89a3no4n2rcas4jssa",
        "description": "My webhook subscription",
    },
    "data": {
        "orderId": "ae918f42-ed83-4af7-b831-20b46d9d1dfc",
        "status": "completed",
        "amount": {
            "total": 1337,
            "paid": 1337
        },
        "metadata": "...merchant-defined-metadata..."
    },
"timestamp": 1725290562
}
```

## Versioning
All events are versioned, the stuff after the `/` in the type denotes the version.

If Rabo Smart Pay changes the payload of an event, it will do so in a backward compatible way, e.g. by adding new
fields. Existing implementations therefor must ignore new fields that they are not aware of.

In cases where breaking changes are inevitable Rabo Smart Pay will create a new version of the event. You can
[upgrade event versions](./upgrading-event-versions.md) at your own pace.

:::note

Rabo Smart Pay will not remove older versions of events as long as they are still in use. However when a version is
deprecated, you won't be able to create subscriptions targeting that version anymore.

:::