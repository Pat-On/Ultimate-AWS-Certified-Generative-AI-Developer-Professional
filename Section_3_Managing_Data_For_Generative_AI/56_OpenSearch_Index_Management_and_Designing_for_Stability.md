# 56. OpenSearch Index Management and Designing for Stability

Storage tiers, index management automation, replication across clusters, and sizing and stability guidance for **Amazon OpenSearch Service**.

## Storage tiers

| Tier | Backing | Notes |
|---|---|---|
| **Hot** (default) | Instance store or **EBS** on the data nodes | Fastest and most expensive |
| **UltraWarm** (also "warm") | **S3** plus a caching layer | Slower, much cheaper; best for indices with few writes, such as immutable log data. Requires a **dedicated master node** (in practice three) |
| **Cold** | **S3** | Cheapest; for periodic research or forensic analysis of old data. Requires a dedicated master **and UltraWarm enabled**. Not compatible with **T2 or T3** data node instance types. With fine-grained access control, map users to the **cold manager role** in Dashboards |

- Data can be migrated between tiers at any time, and this can be automated.

## Index State Management (ISM)

ISM automates index management policies:

- Delete old indices after a period (for example keep three years of monthly indices).
- Move indices to **read-only** (for example for compliance).
- Move indices from hot to UltraWarm to cold over time.
- Reduce the **replica count** as data ages.
- Automate index **snapshots**.
- Policies run every **30 to 48 minutes** (random jitter avoids running on all indices at once).
- Can send notifications when done, including to **Amazon Chime**.

## Roll ups, transforms and replication

- **Index rollups**: periodically summarize old data into a smaller index (fewer fields, coarser time buckets) to cut storage cost.
- **Index transforms**: create a different view of the data for analysis, via grouping and aggregations (sum, average and so on), rather than summarizing for storage.
- **Cross-cluster replication**: replicates indices, mappings and metadata across domains for **high availability** (another data center or region) and **lower latency** for global users. A **follower index** pulls from a **leader index**. Requires **fine-grained access control** and **node-to-node encryption**.
- **Remote reindex**: copy a single index from one cluster to another on demand.

## Stability and sizing

- Use **at least three dedicated master nodes**. One is a single point of failure; two risks a **split brain** (two masters, no authority). A third node breaks the tie.
- Running out of **disk space** is the number one problem with OpenSearch and Elasticsearch clusters.
- **Storage estimate**: source data x (1 + number of replicas) x **1.45** (overhead).
- **Shard count estimate**: (source data x (1 + room for growth) x (1 + indexing overhead, about **10%**)) / desired shard size. Exact index sizes can be queried to compute the real overhead. Shards per node rarely need limiting, since disk space runs out first.
- Use **at least three data nodes** for the same reasons. OpenSearch is storage heavy, so pick instances for storage: **M6g** search instances, **I3** search instances for larger needs, and the largest I3 size (16xlarge) for petabyte scale.
