# 185. Amazon SNS

**Problem:** one message, **many receivers**. Direct integrations must be written for each new receiver.

**Publish/subscribe:** the producer sends to **one topic**; **every subscriber** receives each message, unless a **filter** limits it.

- Over **12 million subscriptions** per topic and **100,000 topics** per account (adjustable). The exam does **not** test these limits.

## Subscribers

Email, SMS, mobile push, **HTTP(S)** endpoints, **SQS**, **Lambda**, **Data Firehose** (on to S3 or Redshift).

## Who publishes

Many AWS services: CloudWatch alarms, Auto Scaling notifications, CloudFormation state changes, Budgets, S3 events, DMS, Lambda, DynamoDB, RDS events.

## Publishing

| Method | Steps |
|---|---|
| **Topic publish** (SDK) | Create topic → subscribe → publish |
| **Direct publish** (mobile SDK) | Platform application → platform endpoint → publish; **Google GCM, Apple APNS, Amazon ADM** |

## Security

Same model as SQS: **HTTPS** in transit, **KMS** at rest, client-side encryption (the client's job), **IAM policies**, and **SNS access policies** for **cross-account** access or to let services such as **S3** publish.

## Exam takeaways

1. **One-to-many** = SNS; **buffered work queue** = SQS.
2. **SNS → many SQS queues** is the **fan-out** pattern.
