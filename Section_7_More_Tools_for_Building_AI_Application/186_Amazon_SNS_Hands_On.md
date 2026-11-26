# 186. Amazon SNS Hands On

- **Type:** Practice lab

## Topic types

| Type | Behaviour |
|---|---|
| **Standard** | Best-effort ordering, at-least-once delivery, highest throughput; many subscriber types |
| **FIFO** | Strict ordering, exactly-once delivery, name ends in `.fifo`; the lecture gives 300 publishes per second and **SQS-only** subscribers |

FIFO limits have been raised over time; check the current figures.

Create **`MyFirstTopic`** (standard), with optional **encryption** and an **access policy** that controls who may publish (for example, letting an S3 bucket write events).

## Subscribe

- Protocols to remember: **Data Firehose, SQS, Lambda, Email, Email-JSON, HTTP, HTTPS, SMS**.
- Create an **email** subscription. It stays **pending confirmation** until the link in the email is clicked.
- An optional **filter policy** delivers only a subset of messages.

## Test

Publish "hello world": it arrives by email. For **SQS fan-out**, subscribe several queues to the topic.

**Clean up:** delete the subscription, then the topic.

## Exam takeaways

1. Email subscriptions need **confirmation**.
2. **Filter policies** work per subscription.
