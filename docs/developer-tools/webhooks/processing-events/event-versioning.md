---
sidebar_position: 40
---

# Event versioning
All events are versioned, the stuff after the `/` in the type denotes the version.

If Rabo Smart Pay changes the payload of an event, it will do so in a backward compatible way, e.g. by adding new
fields. Existing implementations will ignore new fields that they are not aware of.

In cases where breaking changes to existing versions are inevitable Rabo Smart Pay will create a new version for with
the breaking changes. You can [upgrade event versions](./upgrading-event-versions.md) at your own pace.

:::note

Rabo Smart Pay will not remove older versions of events as long as they are still in use. However when a version is
deprecated, you won't be able to create subscriptions targeting that version anymore.

:::
