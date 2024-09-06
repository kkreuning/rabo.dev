---
sidebar_position: 50
---

# Retrying failed deliveries
If it so happens that a delivery fails Rabo Smart Pay will, usually, retry the delivery later at a later time.

A retried delivery means that Rabo Smart Pay will deliver the original event, including the same identifier, again to
your server.

Delayes between retries are calculated using an exponential backoff algorithm as to not overload your server, or
network.

## Failure reasons
Depending on the reason of the failure, Rabo Smart Pay may decide to not retry the delivery but do something else
instead.

| status code / reason  | issue                                             | will retry    |
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

## Delays between attempts
Rabo Smart Pay will retry failed deliveries up to at least 20 times, after that it will start feeling sad for the event, stop retrying, and maybe disable your webhook subscription for you.

| retry attempt | delay until next attempt  |
|--------------:|---------------------------|
| 1             | 2 seconds                 |
| 2             | 4 seconds                 |
| 3             | 8 seconds                 |
| 4             | 16 seconds                |
| 5             | 32 seconds                |
| 6             | ~1 minute                 |
| 7             | ~2 minutes                |
| 8             | ~4 minutes                |
| 9             | ~9 minutes                |
| 10            | ~17 minutes               |
| 11            | 34 minutes                |
| 12            | ~1 hour                   |
| 13            | ~2.2 hours                |
| 14            | ~4.5 hours                |
| 15            | ~9 hours                  |
| 16            | ~18.2 hours               |
| 17            | ~1.5 days                 |
| 18            | ~3 days                   |
| 19            | ~6 days                   |
| 20            | ~12 days                  |
