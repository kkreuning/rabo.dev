---
sidebar_position: 100
---

# Legacy webhooks

:::warning deprecated

Legacy webhooks are only available for existing merchants.

If you are still using legacy webhooks, you won't be able to use newer Rabo Smart Pay features. It it recommended that
you [migrate to v3 webhooks](./migrating-to-v3-webhooks.md).

:::

In a previous life Rabo Smart Pay used a different mechanism of informing merchants, to so called PING-PULL model.

A merchant would provide a webhook URL through the Dashboard, Omnikassa (as Rabo Smart Pay was known back then) would
send "pings" whenever an Order reached an end-status, and the merchant would then "pull" the events by calling a Rabo
Smart Pay endpoint.

This mechanism, despite best intentions, had downsides:
- Only one webhook URL could be configured.
- Because of the archaic way of signing pings, and events there was no way of updating payloads.
- Deliveries were not made in real-time, but happened on a schedule.
- It was harder for merchants to implement compared to a "push" based mechanism (like the one used by the v3 webhooks).
- It was impossible to add new event types without breaking backward compatibility.

It was the last point that forced Rabo Smart Pay to implement a new webhook mechanism.

If you still must support legacy webhooks, you should use the [Omnikassa-SDK](#) to process these types of
webhooks.

:::info What about manual verification?

The legacy webhooks use an arcane authentication mechanism requiring esoteric transmogrification of JSON payloads,
precise incantations of occult recursive concatenation algorithms, and summoning of primordial cryptographic artifacts
to perform an ancient hashing ritual.

If you really must wander on the path of manual legacy signature verification, and learn the dark arts your best bet is
to read the Omninomicon (aka. the [Omnikassa-SDK](#) source code).

But beware; nearly no mortal alive is able to comprehend these horros without going insane, let alone implement them
correctly in code. You have been warned!

By the way, have you considered [migrating to v3 webhooks](./migrating-to-v3-webhooks.md)?
:::
