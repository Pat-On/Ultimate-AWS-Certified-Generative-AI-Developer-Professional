# 76. Amazon DynamoDB DAX

**DynamoDB Accelerator (DAX)**, a managed in-memory cache for DynamoDB, what it fixes, how a cluster is laid out and how it compares with ElastiCache.

## What DAX is

- A **fully managed, highly available, seamless in-memory cache** for DynamoDB.
- Caches the most popular data and gives **microsecond latency** for cached reads and queries.
- Needs **no application logic changes**, because it is compatible with the existing DynamoDB APIs. You create a DAX cluster and point the application at it.
- It solves the **hot key** problem. Reading one item too many times can throttle your RCU, but if DAX caches it the problem goes away.

## How it works

- The application talks to the **DAX cluster**, which fetches data from the DynamoDB tables when it is not cached.
- The default cache **TTL is 5 minutes**.
- The cluster is made of **cache nodes** that you **provision in advance**, up to **10 nodes** per cluster.
- Use a **multi-AZ** setup, with at least **3 nodes** (one per AZ) recommended in production.
- Security: encryption at rest, IAM, VPC security and CloudTrail integration.

## DAX versus ElastiCache

| | Caches | Use |
| --- | --- | --- |
| **DAX** | Individual objects, queries and scans | Simple access patterns against DynamoDB |
| **ElastiCache** | Results your application computed | Expensive logic such as a scan followed by a sum and a filter, so it is not repeated every time |

- They can be combined. Store the aggregated result in ElastiCache and read it from there instead of re-querying DAX and aggregating again on the client.
- The exam may ask you to choose between them.

## Exam takeaways

1. DAX is the answer to **hot key or read throttling** on DynamoDB, with no code changes and microsecond reads.
2. Defaults to remember: **5 minute TTL**, **up to 10 nodes**, **3 nodes across AZs** for production.
3. DAX caches raw items, queries and scans. Use **ElastiCache** for the results of application-side computation.
