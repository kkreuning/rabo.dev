---
sidebar_position: 0
---

# Overview
Rabo Smart Pay expects your server to answer a delivery with a `200 OK` HTTP response status code, and just the string
`ack` as response body.

In case of a different response, Rabo Smart Pay will act as descrived below:

| status code           | issue                                             | will retry    |
|-----------------------|---------------------------------------------------|:-------------:|
| network timeout       | Your server is not reachable by Rabo Smart Pay    | ✅            |
| write timeout         | Your server didn't respond in time                | ✅            |
| `100` - `199`         | Webhook subscription misconfigured                |               |
| `200` without `ack`   | Webhook subscription misconfigured                |               |
| `201` - `299`         | Webhook subscription misconfigured                |               |
| `300` - `399`         | Webhook subscription misconfigured                |               |
| `400` - `499`         | Your server didn't accept the delivery            | ✅            |
| `500` - `599`         | Your server has issues processing the event       | ✅            |

Deliveries with invalid signatures must never be answered with a `200 OK` status, a `400 Bad Request` would suffice.

:::info you are responsible for your server!

If your server does not behave correctly too often, or is (semi-)permanently misconfigured, Rabo Smart Pay may disable
the offending webhook subscription on your behalf.

:::
