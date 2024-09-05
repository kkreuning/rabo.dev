---
sidebar_position: 0
---

# Introduction
:::info v3 documentation only

This document describes the Rabo Smart Pay v3 webhooks mechanism.

If you are still using legacy webhooks, you are urged to
[migrate to v3 webhooks](./advanced-topics/migrating-to-v3-webhooks.md).

:::

Rabo Smart Pay informs you of important events through its webhook mechanism.

Whenever events of interest occurs, Rabo Smart Pay will make HTTP requests to your server. Your server should then 
process these events, and act on them, e.g. by creating shipments, sending e-mails to your customers, etc.

If you are new to Rabo Smart Pay webhooks, start by understanding the [webhook lifecycle](./webhook-lifecycle.md).

When you are ready to integrate webhooks into your platform, see the [implementation guide](./implementation-guide.md).

In case you want to know how to manage your webhooks, see
[webhook subscriptions](./advanced-topics/migrating-to-v3-webhooks.md).
