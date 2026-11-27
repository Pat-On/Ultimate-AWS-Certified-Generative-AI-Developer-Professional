# 196. CloudWatch Logs - Hands On

## Log groups and streams

- Many log groups are created by services (**Lambda, DataSync, Glue**); one in the demo received **SSM Run Command** output.
- That group had **one stream per instance and output** (`stdout`, `stderr`).
- Inside a stream you can **search** for a word such as `http` or `installing`.

## Metric filters

1. Define a **filter pattern** (for example `installing`).
2. **Test** it against sample log data.
3. Name the filter, and set the **metric namespace**, **metric name**, **value** (for example `1` to count matches), default value and unit.
4. The metric appears in **CloudWatch Metrics** once **new** matching log events arrive.
5. You can create an **alarm** on it.

## Other settings on a log group

| Setting | Notes |
|---|---|
| **Subscription filters** | To **OpenSearch** (shown as Elasticsearch), **Kinesis Data Streams**, **Data Firehose** or **Lambda**; **up to two** per log group |
| **Retention** | Never expire, up to **120 months** (10 years) |
| **Export to S3** | Time range, optional stream prefix, bucket and prefix |
| **New log group** | Retention and an optional **KMS key** for encryption |

## Logs Insights

- Choose log groups and a **time range** (the demo found nothing in 1 hour, 18 records in 60 days).
- **Export** results and **save** queries.
- Sample queries include **Lambda latency per 5 minutes** and **top 10 byte transfers by source and destination IP** in VPC Flow Logs.

## Exam takeaways

1. **Metric filter → metric → alarm** turns log text into alerts.
2. Remember the limit of **two subscription filters per log group** shown in the lecture.
