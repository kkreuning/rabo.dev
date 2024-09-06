---
sidebar_position: 20
---

# Event idempotency

Rabo Smart Pay tries its hardest to deliver events exactly once. However it may get confused occasionly, and deliver the same event multiple times.

It is important that your server knows how to deal with this, your business logic should only be applied once per event;
you probably don't want to send multiple confirmation e-mails to your customers, or ship two air-fryers instead of one.

Every event contains an event identifier (the `x-smartpay-event-id` field in the delivery's HTTP header), this
identifier is guaranteed to be unique per event. Even if a delivery is retried the event identifier will remain the same for all delivery attemts.

Your server should make use of this fact. Once an event has been processed by you, your server should store the event
identifier somewhere. When a duplicate event comes in with an already known identifier, it can safely be ignored.

TODO(graph)

:::note still acknowledge the duplicate event

In the case of a duplicate event, your server must still acknowledge the event, so that it won't be retried.

:::