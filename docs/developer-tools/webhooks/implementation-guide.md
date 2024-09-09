---
sidebar_position: 140
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Implementation guide

## Prerequisites

In order to accept events, your server needs to expose an HTTP endpoint with the following requirements:
- it must be accessible over the public internet.
- it must accept HTTP POST requests.
- it must be secured using TLSv1.2, or TLSv1.3 supporting at least one of the following cipher suites:
    - TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    - TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    - TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    - TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

:::warning Secure communications

Because of the possible sensitive content of webhooks, Rabo Smart Pay will only deliver events if a secure connection
with your server can be established.

:::

## Steps

### 1. Implement the destination endpoint
Refer to the [Merchant Webhooks API](/oas/merchant-webhooks-api) specification, and either generate, or implement the
base endpoint.

### 2. Use the SDK to process deliveries
<Tabs groupId="languague">
    <TabItem value="java" label="Java">
        ```java
private SmartPay smartPay = new SmartPay(REFRESH_TOKEN);

@GetMapping("/webhook")
private Response<String> handleWebhook(HttpServletRequest request) {
    try {
        var event = smartPay.processWebhook<Event.OrderStatusFinalizedV1>(request);
        
        applyBusinessLogic(event);
        
        return Response.ok("ack");

    } catch (RuntimeException e) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).build();
    }
}
        ```
    </TabItem>
    <TabItem value="javsscript" label="Javascript">
        ```javascript
const smartPay = new SmartPay(REFRESH_TOKEN);

app.post('/webhook', (req, response) -> {
    try {
        const event = smartPay.processWebhook(req);

        applyBusinessLogic(event)

        response.send("ack");
    } catch (e) {
        response
            .status(500);
            .send(e.toString());
    }
});
        ```
    </TabItem>
</Tabs>

### 3. Apply your business logic
<Tabs groupId="language">
    <TabItem value="java" label="Java">
```java
private void applyBusinessLogic(Event.OrderStatusFinalizedV1 event) {
    var eventId = event.getId();
    var orderId = event.getData().getOrderId();

    if (alreadyProcessedEventIds.contains(eventId)) {
        return;
    }

    shipGoodsToCustomer(orderId);

    alreadyProcessedEventIds.add(eventId);
}
```
    </TabItem>
</Tabs>

### 4. Create a webhook subscription

### 5. (Optional) verify your setup using the Webhook Subscriptions Management API (or Dashboard?)

## Best practices
- Store the event in your database, and acknowledge the delivery before applying business logic. In case your business logic takes too long, or inadvertently raises an error, you will still be able to apply your business logic again, or take mitigating actions at your own pace.
- Store the event identifier in your database you applied your business logic is done. This allows your server to be idempotent, and avoid double processing.