# 68. Amazon Aurora - Hands On

Creating an **Amazon Aurora** MySQL-compatible cluster with a writer and a reader instance, looking at its endpoints, replica auto scaling and global database options, then deleting it. Following along costs money, and creating the database is optional.

## Steps

1. In the RDS console choose **Standard Create** and pick the **Aurora** engine type, MySQL-compatible or PostgreSQL-compatible (MySQL was used).
2. Pick an engine version, using the filters if a feature is needed, then the **Production** template.
3. Set the cluster identifier, master username and password.
4. Choose the cluster storage configuration and the instance class.
5. Enable an **Aurora replica** in another AZ.
6. Configure connectivity, authentication, monitoring and additional options, then create the cluster.
7. Once it is available, the **regional cluster** shows a **writer instance** and a **reader instance** in different AZs, with a cluster-level writer endpoint and reader endpoint.
8. Explore the replica options, the replica auto scaling policy and **Add AWS Region**, cancelling each.
9. Delete the reader instance, then the writer instance, then the cluster.

## Settings that mattered

| Setting | Choice in the demo | Notes |
| --- | --- | --- |
| Engine | **Aurora MySQL-compatible**, version 3.04.1 (console default) | Version selector filters for **global database**, **parallel query** and **Serverless v2** support. The default may differ |
| Template | **Production** | Allows configuring everything |
| Identifier and credentials | Cluster identifier database two, master user `admin`, password | |
| Cluster storage | Not stated | **Aurora Standard** suits cost-effective workloads with modest I/O. **Aurora I/O-Optimized** suits high read and write I/O |
| Instance class | Burstable **db.t3.medium** | Memory optimised and burstable classes, with an option to include previous generation classes |
| Serverless v2 | Not used | Needs a compatible version. Pick a minimum and maximum **Aurora capacity unit (ACU)** instead of an instance type, and the database scales between them |
| Availability | Create an **Aurora replica** (reader) in a different AZ | Better availability, cross-AZ reads and fast failover, at extra cost |
| Compute connection | Not connected to an EC2 resource | |
| Network | **IPv4**, default VPC and default subnet group, **public access: Yes** | **Dual stack** mode if the VPC also has IPv6 |
| Security group | New, named demo database Aurora | |
| Port | **3306** | MySQL port |
| Local write forwarding | Option shown | Writes sent to a read replica are forwarded to the writer, which simplifies connection management |
| Authentication | Options shown | **IAM** database authentication or **Kerberos** (external authentication) |
| Enhanced monitoring | Disabled | |
| Initial database name | my DB | |
| Backup retention | **1 day** | |
| Other options | Shown, not covered | **Encryption**, **backtrack** (rewind the database), **log exports**, **deletion protection** |

## Endpoints and features seen

- The cluster shows a **writer endpoint** and a **reader endpoint**. Applications should connect through these, because they always lead to the current writer and reader instances.
- Each instance also has its own **dedicated endpoint**.
- Cluster actions: **add readers** for more read capacity, create a **cross-region read replica**, **restore to a point in time**.
- **Replica auto scaling** uses a policy based on average Aurora replica utilisation or average number of connections. The demo example kept replicas at a target of **60%**, with a configurable scaling period and a capacity of **1 to 15 replicas**.
- **Add AWS Region** creates a **global Aurora** database. It needs a version with **global database** support and an instance size that supports it, so a larger instance type was needed here and the action was not possible on db.t3.medium.

## Cost and cleanup

- The console shows monthly costs, and the second instance adds to them. Delete everything when finished.
- The cluster cannot be deleted directly. Delete the **reader instance** first and the **writer instance** second, typing the confirmation phrase each time, then delete the **cluster**.
