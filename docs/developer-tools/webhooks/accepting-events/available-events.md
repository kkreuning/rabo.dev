---
sidebar_position: 10
---

# Available events

### test/v1
This event is used to verify your webhook integration.

Your server must treat this event as it would any other.

```json
{
    "id": "ev_z8c2c4txckfq7j7gm2tk9",
    "type": "test/v1",
    "deliveredAt": 1725290562
}
```

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
        "description": "My subscription",
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
    "deliveredAt": 1725290562
}
```
