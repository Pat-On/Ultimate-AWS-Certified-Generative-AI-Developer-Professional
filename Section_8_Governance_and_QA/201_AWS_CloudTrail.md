# 201. AWS CloudTrail

**Governance, compliance and audit** for an AWS account. **Enabled by default.**

## What it records

The history of **events and API calls** made through the **console, SDK, CLI**, by **IAM users and roles**, and by **AWS services**. It answers **who did what, and when**, for example who terminated an EC2 instance.

- Send logs to **CloudWatch Logs** or **S3**.
- A **trail** applies to **all regions** (the **default**) or a **single region**, for example collecting every region into one S3 bucket.

## Event types

| Type | What it covers | Logged by default |
|---|---|---|
| **Management events** | Operations on resources: `IAM AttachRolePolicy`, creating a subnet, setting up logging | **Yes** |
| **Data events** | High-volume activity: **S3 object level** (`GetObject`, `PutObject`, `DeleteObject`), **Lambda `Invoke`** | **No** |
| **Insights events** | Unusual activity found by **CloudTrail Insights** | No, must be enabled |

Management and data events can be split into **read** (do not modify, such as listing users or instances) and **write** (may modify, such as deleting a DynamoDB table). Write events usually matter more, as they can do damage.

## CloudTrail Insights

**Paid**, and must be **enabled**. It learns a **baseline** of normal management activity, then continuously analyses **write** events for unusual patterns, such as:

- Inaccurate resource provisioning
- Hitting **service limits**
- Bursts of **IAM actions**
- Gaps in **periodic maintenance** activity

Insights events appear in the **console**, can be sent to **S3**, and raise an **EventBridge** event for automation (for example an email).

## Retention

- Events are kept for **90 days**, then deleted.
- For longer, **log them to S3** and query with **Athena** (serverless).

The lecture says all three event types are kept for 90 days. In AWS the built-in **event history** shows **management events** only; data and Insights events need a **trail** or an **event data store**.

## Exam takeaways

1. **Who deleted or changed something?** → **CloudTrail**.
2. **Data events are off by default.**
3. **Unusual API activity** → **CloudTrail Insights**.
4. Beyond **90 days** → **S3 + Athena**.
