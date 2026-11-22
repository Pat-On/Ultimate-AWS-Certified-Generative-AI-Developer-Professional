# 77. Amazon DynamoDB DAX - Hands On

Walking through creating a **DAX cluster** in the console, then looking at its endpoint, nodes, monitoring and settings. DAX is **not in the free tier**, so the lecturer advises following along without creating it, and deleted the cluster afterwards.

## Steps

1. In the DynamoDB console choose **DAX** on the left, then create a cluster named `DemoDAX`.
2. Pick a **node family** and size. The **r** types are memory optimised and the **t** types are burstable, recommended for lower throughput. The demo used a `t2.small`.
3. Set the **cluster size**. A single node was used for the demo.
4. Choose a **subnet group** and VPC. Three subnets allow three nodes in a highly available setup.
5. Choose a **security group** for access to the cluster. The demo used the default one for simplicity.
6. Leave **AZ allocation** on automatic.
7. Create an **IAM service role** (`DAXtoDynamoDB`) so the cluster can reach DynamoDB, with read and write access to all tables. It could be limited to specific tables.
8. Enable encryption in transit and at rest, and select the existing **parameter group**.
9. Set the **maintenance window**, or choose no preference, add tags, then review and create.
10. On the created cluster, look at the **cluster endpoint**, **nodes**, **monitoring**, **events** and **settings**. Then delete the cluster along with its CloudWatch alarms.

## Settings that mattered

| Setting | Notes |
| --- | --- |
| Node family | **r** for memory, **t** for bursting at lower throughput |
| Cluster size | 1 to 11 nodes in the console. **3 nodes** gives multi-AZ. With 1 or 2 nodes availability is reduced |
| Subnet group and VPC | The cluster lives in a VPC. One subnet per node for high availability |
| Security group ports | Open **8111**, or **9111** when using in-transit encryption |
| IAM service role | Gives DAX access to DynamoDB tables |
| Parameter group | Holds the **item TTL** and **query TTL**, both **5 minutes** by default |
| Maintenance window | DAX is patched and upgraded, which is why multi-AZ helps |

## What the demo showed

- The **cluster endpoint** is what the application should use to benefit from DAX.
- Nodes can be **added** over time, but the **node type cannot be changed**. A new cluster is needed for that.
- The monitoring tab shows CloudWatch metrics and alarms such as **cache hits and misses** for items and queries, and CPU utilisation, so you can tell whether DAX is effective.
- Parameter groups, network and security configuration, the maintenance window and tags are editable under settings.

## Exam takeaways

1. The application connects to the **DAX cluster endpoint**, and DAX needs an **IAM role** to reach DynamoDB.
2. Open port **8111** (or **9111** with in-transit encryption) in the security group.
3. Use **3 nodes across AZs** for availability. Node types cannot be changed in place.
4. Track **cache hits and misses** in CloudWatch to check DAX is helping.
