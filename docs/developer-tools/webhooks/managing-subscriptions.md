---
sidebar_position: 60
---

# Managing subscriptions

Rabo Smart Pay delivers events to your server using one or more webhook subscriptions, a subscription consist of:
1. A destination in the form of an HTTP endpoints controlled by the merchant.
2. A set of [event types](./accepting-events/available-events.md) that will be delivered to the destination.
3. Optionally a textual description of the webhook.

Webhook subscriptions are managed through the dashboard, or using the [Webhook Subscriptions Management API](#).

The default maximum number of total webhook subscriptions is 32.

## Basic Usage
#### Create a new subscription
TODO(code snippet)

#### Listing all subscriptions
TODO(code snippet)

#### Disable a subscription
TODO(code snippet)

:::info outstanding deliveries on changed webhook subscriptions

Whenever you disable, or delete a webhook subscription that still has outstanding deliveries, Rabo Smart Pay will still
attempt to deliver those events. Keep this in mind when disabling a webhook subscription, the destination might still
receive events afterwards.

If you change the destination of a webhook subscriptions, any outstanding deliveries will be sent to the new
destination.

:::