# 87. Amazon S3 - Replication

**S3 Replication** copies objects asynchronously between buckets, as **Cross-Region Replication (CRR)** or **Same-Region Replication (SRR)**.

## Requirements

- **Versioning** must be enabled on both the source and destination buckets.
- **CRR** uses buckets in different regions, **SRR** in the same region.
- Buckets can be in **different AWS accounts**.
- Copying is **asynchronous**, in the background.
- S3 needs proper **IAM permissions** to read from and write to the buckets.

## Use cases

| Type | Use cases |
| --- | --- |
| **CRR** | Compliance, lower latency access, replication across accounts |
| **SRR** | Log aggregation across buckets, live replication between production and test accounts |

## Exam takeaways

1. Replication needs **versioning on source and destination** and an **IAM role** for S3.
2. It is **asynchronous**, and works across accounts.
3. CRR for compliance and latency, SRR for log aggregation and prod-to-test copies.
