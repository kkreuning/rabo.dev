---
sidebar_position: 50
---

# Outgoing IP addresses

:::warning don't try this at home

Your server should solely rely on an event's cryptographic signature to determine the event's authenticity.

The list of Rabo Smart Pay outgoing IP addresses may change at any time without a heads up.

:::

Depending on your network setup, you may need to allow-list Rabo Smart Pay's outgoing IP addresses in your firewall to
be able to accept events.

Rabo Smart Pay publishes its outgoing IP addresses in the form of DNS records.

## Resolving ougoing IP addresses

Your server must perform a DSN lookup on the domain `out.pay.rabobank.nl` and write down the IP addresses in the `A`
records.

```bash
dig +short out.pay.rabobank.nl A
```

Add these IP addresses to your firewall's allow-list.

It is up to you to ensure that the list is updated periodically. Failing to do so, and thus blocking event deliveries,
could result in your server not accepting events in time, and getting your webhook subscription disabled.