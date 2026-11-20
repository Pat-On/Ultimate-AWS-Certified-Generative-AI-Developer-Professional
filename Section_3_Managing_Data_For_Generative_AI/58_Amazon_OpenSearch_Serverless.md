# 58. Amazon OpenSearch Serverless

**Amazon OpenSearch Serverless** was introduced in January 2023, so it was expected to reach the exam around 2024 or later. Know that it exists.

## Differences from the managed service

- **On-demand auto scaling**: you do not manage the number of underlying servers.
- You work with **collections** instead of **domains** (a way to organise indices). Two collection types: **search** and **time series**.
- **Always encrypted** at rest: you provide a **KMS key**.
- You can enforce your own **data access policies**, and security policies can be configured across many collections at once (the managed service needs separate policies per domain).
- Capacity is measured in **OpenSearch Compute Units (OCUs)**. You can set an **upper limit** to control cost; the lower limit is always **2 OCUs for indexing and 2 for search**.
- The OpenSearch console has separate sections for the managed and serverless versions; setup and use are otherwise similar.
