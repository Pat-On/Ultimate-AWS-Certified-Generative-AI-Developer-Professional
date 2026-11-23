# 89. Amazon S3 - Replication - Hands On

Setting up **cross-region replication** between two versioned buckets and seeing what is and is not replicated.

## Steps

1. Create an origin bucket in `eu-west-1` with **versioning enabled**, and upload a file (`beach.jpg`).
2. Create a replica bucket in another region (`us-east-1`), or the same region for SRR, also with **versioning enabled**.
3. On the origin bucket, go to **Management**, then **Replication rules**, and create a rule (`DemoReplicationRule`), enabled and applied to all objects.
4. Set the destination to the replica bucket, in this account or another. The console detects the region, here making it **cross-region replication**.
5. Create a new **IAM role** for the rule and save it.
6. When asked whether to replicate existing objects, answer no. Existing objects need a separate batch operation.
7. Upload `coffee.jpg` to the origin bucket. It appears in the replica after about 10 seconds, with the **same version ID**.
8. Upload `beach.jpg` again to create a new version, so that it is replicated.
9. Edit the rule and enable **delete marker replication**.
10. Delete `coffee.jpg` in the origin. This creates a delete marker, which is replicated to the replica bucket.
11. Permanently delete a specific version of `beach.jpg` in the origin. It is **not** replicated.

## What the demo showed

- Replication only covers objects uploaded **after** the rule exists. Existing objects stay unreplicated unless you use a batch operation.
- **Version IDs are preserved** in the replica.
- **Delete marker replication is off by default**, and is a rule setting.
- Only delete markers are replicated. **Permanent deletes of a version ID are not**.

## Exam takeaways

1. Enable **versioning on both buckets** before creating a replication rule.
2. Only **new objects** replicate. Use **S3 Batch Replication** for existing ones.
3. **Delete markers** replicate only if enabled, and **version-specific deletes never replicate**.
4. Version IDs are the same in source and destination.
