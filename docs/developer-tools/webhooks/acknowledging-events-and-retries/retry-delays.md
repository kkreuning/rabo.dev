---
sidebar_position: 20
---

# Retry delays

When an event delivery fails in a retryable manner, Rabo Smart Pay will retry the delivery at a later time.

The retry mechanism uses an exponential backoff to calculate the delay as to not overload your server, or network.

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

After that Rabo Smart Pay starts feeling sad for the event, stop retrying, and maybe disable your webhook subscription
for you.
