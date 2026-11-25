# 135. Exponential Backoff and Connection Pooling

Both are general techniques for systems that call each other, not specific to Bedrock or generative AI, but the exam-prep material gives oddly specific numbers for them.

## Exponential backoff

How to **retry failed API calls in a controlled way**. If a back end goes down and every client hammers it again immediately, that makes things worse. Backing off gives the service room to recover.

- Configure it with **custom retry policies in the AWS SDK clients** (for example Boto3).
- Guidance from the material:
  - Start at **100 ms**.
  - **Backoff factor of 2**.
  - **Max retry count of 3 to 5**.
  - **Jitter of plus or minus 100 ms**, so thousands of clients do not all retry at the same moment.

## Connection pooling

For HTTP clients calling services over REST. Opening a new HTTP connection for every request is expensive, so keep a **pool of open connections** and reuse them, which avoids repeated handshaking.

- Guidance from the material:
  - **10 to 20 connections per instance**.
  - **Connection TTL of 60 to 300 seconds**.
- The aim is a balance between **resource utilization** and **connection reuse efficiency**.

## Exam takeaways

1. **Exponential backoff** = controlled retries with growing delays: 100 ms start, factor 2, 3 to 5 retries, plus or minus 100 ms **jitter**.
2. **Jitter** prevents synchronized retries from many clients.
3. **Connection pooling** = reuse open HTTP connections: **10 to 20 per instance, TTL 60 to 300 seconds**.
