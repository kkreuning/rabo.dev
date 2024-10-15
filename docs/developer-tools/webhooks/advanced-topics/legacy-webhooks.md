---
sidebar_position: 100
---

# Legacy webhooks

:::warning Deprecated

Legacy webhooks are only available for existing merchants.

If you are still using legacy webhooks, you won't be able to use newer Rabo Smart Pay features. You are urged to
[migrate to v3 webhooks](./migrating-to-v3-webhooks.md).

:::

In a previous life Rabo Smart Pay used a different mechanism of informing merchants, the so called PING-PULL model.

A merchant would provide a webhook URL through the Dashboard, Omnikassa (as Rabo Smart Pay was known back then) would
send "pings" whenever an Order reached an end-status, and the merchant would then "pull" the events by calling a Rabo
Smart Pay endpoint.

This mechanism, despite best intentions, had downsides:
- Only one webhook URL could be configured.
- Payloads of pings, and events could not be updated due to an archaic, and strict signing scheme.
- Deliveries were not made in real-time, but happened on a schedule.
- It was harder for merchants to implement compared to a "push" based mechanism (like the one used by the v3 webhooks).
- It was not possible to add new event types without breaking backward compatibility.

Because of these Rabo Smart Pay decided to move away from this mechanism.

If you still must support legacy webhooks, you should make use of the
[Omnikassa-SDK](https://github.com/rabobank-nederland/omnikassa-sdk-doc).

:::info What about manual verification?

Legacy webhooks use an arcane authentication mechanism requiring esoteric transmogrification of JSON payloads, precise
incantations of an occult recursive concatenation algorithm, and summoning of primordial cryptographic artifacts
to perform an ancient hashing ritual.

If you really must wander on the path of manual legacy signature verification your best bet is to read the Omninomicon
(aka. the [Omnikassa-SDK](https://github.com/rabobank-nederland/omnikassa-sdk-doc) documentation).

But beware; nearly no mortal alive is able to comprehend the horrors of legacy signatures without going insane, let
alone implement them correctly, and securely in code. You have been warned!

By the way, have you considered [migrating to v3 webhooks](./migrating-to-v3-webhooks.md)?

:::
