---
sidebar_position: 300
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Payment journey

A single payment consist of the following steps:

1. Your server makes a refresh call to Rabo Smart Pay to obtain an _access-token_.
2. After receiving the _access-token_, your server makes an [order announcement call](#) to announce an _order_.
3. Your webshop redirects your customer to the [Hosted Checkout](./choosing-an-integration/hosted-checkout.md) where
the user completes the payment.
4. Your customer is returned back to your webshop.
5. Your server receives a webhook notifying it of the status of the _order_.




{/*
A single payment consist of the following steps:

1. Your server makes a refresh call to Rabo Smart Pay to obtain an _access-token_.
2. After receiving the _access-token_, your server makes an [order announcement call](#) to announce an _order_.
3. Your webshop either:
    - loads [SmartPay.js](#), allowing you customer to pay while remaining on [your checkout page](#), or
    - redirects your customer to the [Hosted Checkout](#) where the user completes the payment.
4. Optionally, depending on the payment method, your customer is returned back to your webshop.
5. Your server receives a webhook notifying it of the status of the _order_.

## Hosted Checkout
![](img/hosted-checkout-sequence-diagram.svg)

## Embedded Checkout using SmartPay.js
![](img/embedded-checkout-sequence-diagram.svg)
*/}