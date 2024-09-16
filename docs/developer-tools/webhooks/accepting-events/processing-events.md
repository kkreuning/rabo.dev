---
sidebar_position: 0
---

# Processing events

![](./img/processing-events-flowchart.svg)

:::info Acknowledge unexpected events

In case your server doesn't know what to do with the event, your server should just acknowledge the event to Rabo Smart
Pay as to avoid getting the delivery [retried](./retrying-failed-deliveries.md).

You should investigate why this event was delivered to you by checking your
[webhook subscriptions](../managing-subscriptions.md).

:::

:::danger Always verify the signature

If you are not using the SDK, your server __[must verify the signature manually](./verifying-signatures.md)__!

:::