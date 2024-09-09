---
sidebar_position: 5
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Verifying signatures
Rabo Smart Pay signs all deliveries using a cryptographically secure signature, this allows your server to
mathematically verify that a delivery is, indeed, originating from Rabo Smart Pay.

Rabo Smart Pay uses [JSON Web Signatures](https://en.wikipedia.org/wiki/JSON_Web_Signature) with a detached payload as
its, authentication mechanism.

Rabo Smart Pay publishes its public keys at
[https://pay.rabobank.nl/.well-known/jwks.json](https://pay.rabobank.nl/.well-known/jwks.json). When verifying a
signature you must always use one of the published keys!

## Verifying signatures using the SDK
:::info covered by the SDK

When using the `smartPay.processWebhook` or equivalent method of the SDK, signature validation is taken care of
automatically.

:::

To manually verify the signature of an event, you need to provide the "raw" bytes of the HTTP request's body, together
with the signature from the HTTP header `x-smartpay-signature`.

<Tabs groupId="languague">
    <TabItem value="java" label="Java">
      ```java
SmartPay smartPay = new SmartPay(REFRESH_TOKEN);
String signature = request.headers(SmartPay.Headers.X_SMARTPAY_SIGNATURE);
byte[] body = request.bodyAsBytes();

// highlight-next-line
boolean isValid = smartPay.verifySignature(signature, body);

if (isValid) {
  // good to go
} else {
  // something went wroing
}
      ```
  </TabItem>
  <TabItem value="javsscript" label="Javascript">
      ```javascript
const smartPay = new SmartPay(REFRESH_TOKEN);
const signature = req.headers['x-smartpay-signature'];
const body = req.body;

// highlight-next-line
const isValid = smartPay.verifySignature(signature, body);

if (isValid) {
  // good to go
} else {
  // something went wroing
}
      ```
  </TabItem>
</Tabs>

## Verifying signatures without the SDK
:::warning don't try this at home

The [Rabo Smart Pay SDK](#) provides tooling to verify signatures. You should use the SDK whenever possible.

:::

If you are for some reason unable to use the SDK, you must follow the steps outlined below after you received the
delivery.

1. Get the value of the HTTP request header with name `x-smartpay-signature`. This will be the _detached-jws_.
2. Split the _detached-jws_ on the dot character (`.`), the first part will be the _header_, the last part will be the _signature_.
3. Get the body of the HTTP request as an array of bytes, this will be the _payload_.
4. Craft a _JWS_ using the _header_, _payload_, and _signature_ as input.
5. Read the _key identifier_ (`kid`) from the JWS.
6. Download the Rabo Smart Pay public keys from [https://pay.rabobank.nl/.well-known/jwks.json](https://pay.rabobank.nl/.well-known/jwks.json).
7. Find the _public key_ that matches with the _key identifier_ of the _JWK_.
8. Verify the _JWK_ using the _public key_.

This is, at its core, what the SDK does when verifying signatures.
