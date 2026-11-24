# 94. S3 Access Logs

Logging all requests to a bucket into another bucket for audit purposes.

## How it works

- Any request made to the bucket, **from any account**, whether **authorized or denied**, is logged as a file in another S3 bucket.
- Enable access logs on the monitored bucket and name the logging bucket.
- The logs can be analyzed with data analysis tools such as **Amazon Athena**.
- The **target logging bucket must be in the same AWS region**.
- The log format is documented in the AWS S3 documentation.

## Warning: logging loop

- **Never** use the monitored bucket as its own logging bucket.
- Each log write is itself a request, which is logged again, creating an **infinite loop**. The bucket grows **exponentially** and costs a lot.

## Exam takeaways

1. Access logs capture **all requests**, allowed or denied, from any account.
2. The logging bucket must be in the **same region** and **different** from the monitored bucket.
3. Analyze logs with **Athena**.
