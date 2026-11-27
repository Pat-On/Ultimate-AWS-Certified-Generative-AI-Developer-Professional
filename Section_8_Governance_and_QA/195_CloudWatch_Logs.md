# 195. CloudWatch Logs

The place to **store application logs** in AWS.

## Structure

| Term | Meaning |
|---|---|
| **Log group** | Any name; usually one application |
| **Log stream** | One instance, log file or container within the application |
| **Retention** | Never expire, or from **1 day to 10 years** |

Logs are **encrypted by default**; you can use your own **KMS** key.

## Sources

- **SDK**, **CloudWatch Unified Agent** (the older CloudWatch Logs Agent is deprecated)
- **Elastic Beanstalk**, **ECS** containers, **Lambda** functions
- **VPC Flow Logs** (network traffic metadata), **API Gateway** requests
- **CloudTrail** (based on a filter), **Route 53** DNS queries

## Logs Insights

A **query engine** with its own query language.

- Choose a time range; get a **visualisation** and the matching log lines.
- Fields are detected automatically: **filter, aggregate, sort, limit**.
- **Save** queries, export results, add them to **dashboards**; sample queries are provided.
- Query **several log groups**, even **across accounts**.
- It is **not real time**: it queries historical data when you run it.

## Getting logs out

| Way | Timing | Destinations |
|---|---|---|
| **Export** (`CreateExportTask`) | Batch, **up to 12 hours** | **S3** |
| **Subscription** (with a **subscription filter**) | Real time | **Kinesis Data Streams**, **Data Firehose**, **Lambda** |

- **Kinesis Data Streams** suits further processing: Firehose, Kinesis Data Analytics (now Managed Service for Apache Flink), EC2 or Lambda.
- **Data Firehose** delivers in **near real time** to **S3** or **OpenSearch**.
- A **Lambda** function (your own or a managed one) can send data to **OpenSearch**.

## Cross-account and cross-region aggregation

Subscription filters can gather logs from many accounts and regions into one place, for example one Kinesis Data Stream → Firehose → S3.

1. **Sender account:** a **subscription filter** that points to a **subscription destination**.
2. **Destination:** a virtual representation of the recipient's stream, with a **destination access policy** allowing the sender.
3. **Recipient account:** an **IAM role** that may put records into the stream and that the sender can assume.

## Exam takeaways

1. **Real-time** log delivery → **subscriptions**; **S3 export** is batch (up to 12 hours).
2. **Logs Insights** queries stored logs; it is not real time.
3. Cross-account → **subscription destination + access policy + IAM role**.
