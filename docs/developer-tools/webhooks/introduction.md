---
sidebar_position: 0
pagination_label: Webhooks
---

# Introduction

:::info v3 documentation only

This document describes the Rabo Smart Pay v3 webhooks mechanism.

If you are still using legacy webhooks, you are urged to
[migrate to v3 webhooks](./advanced-topics/migrating-to-v3-webhooks.md).

:::

Whenever an event of interest occurs, Rabo Smart Pay will inform you, so that you can programmatically act in response.

For example:
- Create a shipment for your customer once a payment is authorized.
- Update your customer's membership when a monthly automated payment succeeds.
- Send an e-mail to your customer when a subscription is about to expire.

Rabo Smart Pay allows you to create, and manage subscriptions for specific types of events, these events will then be
delivered to your server in the form of a HTTP POST request. Once received, your server must then verify the events
authenticity, and apply your business logic.


If you are new to Rabo Smart Pay webhooks, start by understanding the [webhook lifecycle](./webhook-lifecycle.md).

When you are ready to integrate webhooks into your platform, see the [implementation guide](./implementation-guide.md).

In case you want to know how to manage your webhooks, see [managing subscriptions](./managing-subscriptions.md).
