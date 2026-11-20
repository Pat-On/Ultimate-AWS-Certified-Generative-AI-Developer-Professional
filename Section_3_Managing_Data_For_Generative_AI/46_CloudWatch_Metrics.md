# 46. CloudWatch Metrics

**Amazon CloudWatch Metrics** provide monitoring data for every AWS service, so you can watch everything happening in your accounts.

## Core concepts

- A **metric** is a variable to monitor (for example EC2 **CPUUtilization** or **NetworkIn**, S3 bucket size).
- Metrics belong to **namespaces**, one per service.
- **Dimensions** are attributes of a metric (instance ID, environment and so on). There can be **up to 30 dimensions per metric**.
- Metrics are time-based and carry a timestamp.
- **Dashboards** show many metrics at once.
- **Custom metrics** let you publish your own, for example **EC2 memory usage**, a classic use case.

## Streaming metrics out of CloudWatch

- Continuous, near real-time, low-latency streaming to **Amazon Kinesis Data Firehose**, which you must set up, or directly to third-party providers (Datadog, Dynatrace, New Relic, Splunk, Sumo Logic).
- From Firehose, deliver to **S3** (analyze with **Athena**), **Redshift** (data warehouse) or **OpenSearch** (dashboards and analytics).
- You can stream all namespaces or filter to a subset.

## Console notes

- Metrics are listed by namespace (EC2, EBS, ELB and others), and can be filtered by region, dimension and resource ID.
- EC2 data points arrive every 5 minutes by default; with **detailed monitoring** enabled they arrive every 1 minute.
- Views: line, stacked area, number or pie chart. Graphs can be added to a dashboard, downloaded as CSV or shared.
