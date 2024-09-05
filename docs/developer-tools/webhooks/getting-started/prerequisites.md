---
sidebar_position: 10
---

# Prerequisites

In order to accept events, the your server needs to expose an HTTP endpoints with the following requirements:
- it must be accessible over the public internet.
- it must accept HTTP POST requests.
- it must be secured using TLSv1.2, or TLSv1.3 supporting at least one of the following cipher suites:
    - TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    - TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    - TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    - TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

Depending on your server's network setup, the Rabo Smart Pay outgoing IP addresses may need to be [allow-listed](../advanced-topics/outgoing-ip-addresses.md).

:::info Secure communications

Rabo Smart Pay will only deliver events if a secure connection with your server can be established.

:::
