---
sidebar_position: 40
---

# Implementation guide

### 1. Implement the destination endpoint
TODO(point to the OpenAPI specification)

### 2. Use the SDK to process events
TODO(code snippet)

### 3. Apply your business logic

### 4. Create a webhook subscription

### 5. (Optional) verify your setup using the Webhook Subscriptions Management API (or Dashboard?)

## Best practices
- Store the event in your database, and acknowledge the delivery before applying business logic. In case your business logic takes too long, or inadvertently raises an error, you will still be able to apply your business logic again, or take mitigating actions at your own pace.
- Store the event identifier in your database you applied your business logic is done. This allows your server to be idempotent, and avoid double processing.