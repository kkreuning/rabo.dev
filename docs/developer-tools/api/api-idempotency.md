---
sidebar_position: 50
---

# API idempotency
Rabo Smart Pay supports idempotency, allowing you to retry requests in case of failure for certain calls.

If, for example, you create an order but are unsure of the result because of a network timeout, you can safely retry
the call without the risk of creating an additional order.

## Enabling idempotency
:::info covered by the SDK

The [Rabo Smart Pay SDK](#) supports idempotency for safe retries without any additional configuration out of the box.

:::

To make an idempotent request you should include the `idempotency-key:<key>` HTTP header to your POST requests.

The `<key>` must be a string unique for every call, Rabo Smart Pay recommends using a UUID, but you are free to use any
string with a maximum of 64 character.

Rabo Smart Pay will process the request as usual unless it has already seen the idempotency key before, in that case it
will return the response to the first request made with the idempotency key.

Rabo Smart Pay will echo the idempotency key back to you in the form of a HTTP response header.

To verify that a request was processed idempotently, you should compare the key in the `idempotency-key` HTTP response
header to the idempotency key that you passed.

## Time validity
Rabo Smart Pay will remember idempotency keys for a minimum of 48 hours. This has two implications:
1. A request can _only_ be retried within that time frame.
2. You should not make other requests using the same idempotency key within that time frame.

## Error handling
Not all errors are recoverable, if you tried to access a resource that does not
exist (by receiving a `404 Not Found` HTTP status code) retrying the request
will not fix the situation. You should only retry requests in case of timeouts,
and HTTP status codes in the 500 range.

If you are too fast with your retry you may receive a `422 Unprocessable Entity`
HTTP response code because Rabo Smart Pay is still processing your request. In
that case you should retry the request again later.

## Best practices
- Use (random) UUIDs for your idempotency keys.
- Do **not** re-use an internal identifier as an idempotency key (order ids, primary keys, etc.); in case of a
cancelled, or expired order you wouldn't be able to retry the request using that key anymore.
- Store your idempotency key in your system _before_ calling Rabo Smart Pay to ensure that you can actually retry the
request in case of failure.
- When retrying requests, use an exponential backoff strategy to avoid overloading our API endpoints, and triggering
[rate limiting](#).

