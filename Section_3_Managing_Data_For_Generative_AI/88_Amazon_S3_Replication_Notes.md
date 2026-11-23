# 88. Amazon S3 - Replication - Notes

Behaviours of **S3 Replication** to remember.

- After enabling replication, **only new objects** are replicated. Use **S3 Batch Replication** for existing objects and objects that failed replication.
- **Delete markers** can optionally be replicated from source to target.
- Deletes with a **version ID** are **not replicated**, to avoid malicious deletes.
- There is **no chaining**. If bucket 1 replicates to bucket 2, and bucket 2 to bucket 3, objects created in bucket 1 are not replicated to bucket 3.
