---
sidebar_position: 40
---

# Acknowledging events

Rabo Smart Pay expects your server to explicitly acknowledge processed deliveries as to avoid
[retries](./retrying-failed-deliveries.md)

To acknowledge a delivery, your server must:
- respond within 30 seconds of
- repspond with a `200 OK` status code
- respond with a body consisting of the string `ack`

Any other response, or the lack of a timely response, will be considered by Rabo Smart Pay as failed.

:::info You are responsible for acknowledgements

If your server does not behave correctly too many times, or is misconfigured, Rabo Smart Pay may disable the offending webhook subscription on your behalf.

If this happens you should fix the processing on your side before you re-enable the webhook subscription again.

:::
