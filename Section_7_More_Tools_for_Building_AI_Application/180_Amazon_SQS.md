# 180. Amazon SQS

A **queue** buffers messages and **decouples** applications. **Producers** send messages; **consumers** **poll** for them, process them and **delete** them.

## Standard queue

| Property | Value |
|---|---|
| Throughput and queue length | **Unlimited** |
| Retention | Default **4 days**, maximum **14 days** |
| Latency | Under 10 ms to publish and receive |
| Message size | Up to **1,024 KB** |
| Delivery | **At least once** (duplicates possible) |
| Ordering | **Best effort** |

- **Produce:** the `SendMessage` API. The message persists until a consumer deletes it.
- **Consume:** EC2, your own servers or Lambda; up to **10 messages per poll**; remove them with `DeleteMessage`.
- Applications must **tolerate duplicates** and disorder.
- **Scale horizontally** by adding consumers.

## Common architectures

- **SQS + Auto Scaling group:** a CloudWatch alarm on **`ApproximateNumberOfMessages`** (queue length) adds instances.
- **Decoupled tiers:** the front end queues requests (such as video processing); a back-end group processes them and writes to S3. Each tier scales **independently** and can use suitable instances (for example GPUs).

## Security

**HTTPS** in transit, **KMS** at rest, optional client-side encryption (done by the client), **IAM policies**, and **SQS access policies** (like S3 bucket policies) for **cross-account** access or to let **SNS or S3** write to the queue.

## Exam takeaways

1. **Decoupling = SQS.**
2. Retention **4 / 14 days**, **10** messages per receive, **at-least-once**.
3. Scale consumers on **queue length**.
