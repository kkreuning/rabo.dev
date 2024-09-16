---
sidebar_position: 50
---

# API idempotency
Rabo Smart Pay supports idempotency, allowing you to retry requests in case of failure for certain calls.

If, for example, you create an order but are unsure of the result because of a network timeout, you can safely retry
the call without the risk of creating an additional order.

## Enabling idempotency
:::info Covered by the SDK

The [Rabo Smart Pay SDK](#) supports idempotency for safe retries without any additional configuration out of the box.

:::

To make an idempotent request you should include the `Idempotency-Key:<key>` HTTP header to your POST requests.

The `<key>` must be a string unique for every call, Rabo Smart Pay recommends using a UUID, but you are free to use any
string with a maximum of 64 character.

Under normal circumstances your request will pass through normally, and Rabo Smart Pay echoes your idempotency key
back to you in a HTTP response header.

Now, when another request is made to Rabo Smart Pay with the same idempotency key, one of the following things happen:
- If a previous request with the same key has been completed, you will receive the cached response.
- If a previous request with the same key is still being processed ("in flight"), you will receive a `409 Conflict`
HTTP status code. In that case you should retry the request later to get a definitive answer.

## Time validity
Rabo Smart Pay will remember idempotency keys for a minimum of 48 hours. This has two implications:
1. A request can _only_ be retried within that time frame.
2. You should not make other requests using the same idempotency key within that time frame.

## Error handling
Not all errors are recoverable, for example if you tried to access a resource that does not exist (and received a
`404 Not Found` HTTP status code) retrying the request will not fix the situation.

You should only retry requests if:
- they are timed out.
- the status code is `408 Request Timeout`, Rabo Smart Pay didn't receive a complete request in time.
- the status code is `409 Conflict`, your initial request might still be in flight.
- the status code is `429 Too Many Requests`, you might be [rate-limited](#).
- the status code is in the `500` range

## Best practices
- Use (random) UUIDs for your idempotency keys.
- Do **not** re-use an internal identifier as an idempotency key (order ids, primary keys, etc.); in case of a
cancelled, or expired order you wouldn't be able to retry the request using that key anymore.
- Store your idempotency key in your system _before_ calling Rabo Smart Pay to ensure that you can actually retry the
request in case of failure.
- When retrying requests, use an exponential backoff strategy to avoid overloading our API endpoints, and triggering
[rate limiting](#).

