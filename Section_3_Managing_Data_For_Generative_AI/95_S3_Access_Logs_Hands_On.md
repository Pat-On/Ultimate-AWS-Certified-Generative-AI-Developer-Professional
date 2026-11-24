# 95. S3 Access Logs - Hands On

Enabling **S3 server access logging** on a bucket and checking what gets delivered to the logging bucket.

## Steps

1. Create a separate bucket to act as the **logging bucket**, in the same region as the monitored bucket.
2. Open the bucket to monitor, go to **Properties**, scroll to **Server access logging** and edit it, then enable it.
3. Choose the logging bucket as the **destination**. The console shows its region (`eu-west-1`).
4. Optionally set a **destination prefix** (for example `logs/`). It was left empty in the demo.
5. Pick the **log object key format**. The console shows an example key. The second option lets you choose between the **S3 event time** and the **log file delivery time**, which changes the final key. The default was kept.
6. Save the changes. The console warns that the **bucket policy of the target bucket will be updated**.
7. Generate activity by opening objects and uploading a file (a JPEG) in the monitored bucket.
8. Check the logging bucket. Nothing appears at first, because logs are delivered with a delay. In the demo it took a couple of hours.
9. Open the logging bucket's **Permissions** to see the updated bucket policy, which allows the **S3 logging service** to put objects into it.
10. Open one of the log files. It is hard to read, but each entry has the API call, the result (success or error), who made the request, the bucket, the time, and more.

## Key points

- Enabling logging automatically adds a **bucket policy to the logging bucket** that grants the S3 logging service permission to write.
- Log delivery is **not immediate** and can take hours.
- **Any request** to the bucket is logged, from any account, whether authorized or denied.
- The logs can be analyzed with data analysis tools. The log format is documented by AWS.

## Exam takeaways

1. S3 access logs are for **auditing** all requests made to a bucket.
2. The **logging bucket must be in the same region** as the monitored bucket.
3. Never use the **monitored bucket as its own logging bucket**. It creates a **logging loop** and the bucket grows exponentially.
