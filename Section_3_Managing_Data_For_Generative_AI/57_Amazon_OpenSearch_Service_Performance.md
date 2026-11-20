# 57. Amazon OpenSearch Service Performance

Notes on avoiding **JVM memory pressure** in an **Amazon OpenSearch Service** cluster.

## Causes

- **Unbalanced shard allocation**: some shards do most of the work and are overloaded while others sit idle. Running out of memory leads to swapping to disk and poor performance.
- **Too many shards** in a cluster: distribution itself costs work and a lot of memory, so fewer shards can perform better.

## Fixes

- If JVM memory pressure errors appear in the logs, reduce the shard count by **deleting older unused indices**.
- Offload old data to an archive (for example **S3 Glacier**) and delete the matching indices, or delete indices that are never used.
