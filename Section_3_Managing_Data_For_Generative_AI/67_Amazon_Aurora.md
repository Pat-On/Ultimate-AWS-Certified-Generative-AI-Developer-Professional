# 67. Amazon Aurora

A high-level overview of **Amazon Aurora**: how it relates to RDS, its storage design, replicas and endpoints, and its main features. The exam increasingly asks about Aurora, without needing deep knowledge.

## What Aurora is

- A **proprietary AWS database**, not open source, but **compatible with PostgreSQL and MySQL**. It has compatible drivers, so connecting as to a PostgreSQL or MySQL database works.
- **Cloud-optimised**, with about **5x the performance of MySQL on RDS** and **3x the performance of PostgreSQL on RDS**, plus other performance gains.
- Costs about **20% more than RDS**, but is efficient enough that it saves money at scale.
- **High availability by default**, because it is cloud-native.

## Storage

- Storage **grows automatically** from **10 GB up to 256 TB**, so there is no disk monitoring to do.
- Up to **15 read replicas**, with replication faster than MySQL and typical **replica lag under 10 ms**.
- Failover is much faster than **Multi-AZ** on RDS MySQL.

### Six copies across three AZs

- Every write is stored as **six copies across three AZs**.
- **4 of 6 copies** are needed for writes and **3 of 6** for reads, so losing one AZ does not stop writes or reads.
- **Self-healing**: corrupted or bad data is repaired with **peer-to-peer replication** in the backend.
- Data is striped across **hundreds of volumes**, which reduces risk.
- The storage is a **shared logical volume** that replicates, self-heals and auto-expands. It is a design detail that is not managed directly.

## Cluster architecture

- Aurora works like Multi-AZ for RDS, with **one master (writer) instance** that takes all writes.
- If the master fails, **failover takes under 30 seconds on average**, and any read replica can be promoted to master.
- Up to **15 read replicas** serve reads and scale the read workload. They support **cross-region replication**.
- **Replica auto scaling** keeps the right number of read replicas as load changes.

| Endpoint | Behaviour |
| --- | --- |
| **Writer endpoint** | A DNS name that always points to the master. Clients keep using it after a failover and are redirected automatically |
| **Reader endpoint** | Connection load balancing across all read replicas, including those added by auto scaling. Load balancing happens at the **connection level, not the statement level** |

## Features

- Automatic failover, backup and recovery, isolation and security, industry compliance.
- **Push-button scaling** through auto scaling.
- **Automated patching with zero downtime**, advanced monitoring and routine maintenance.
- **Backtrack** restores data to any point in time without relying on backups. You can rewind to one time and then pick another, such as moving from 4 PM to 5 PM yesterday.

## Exam takeaways

1. Aurora is AWS proprietary and compatible with PostgreSQL and MySQL drivers.
2. Storage auto-expands from 10 GB to 256 TB, keeping six copies across three AZs (4 of 6 for writes, 3 of 6 for reads) with self-healing.
3. One master takes writes, with up to 15 read replicas that can be promoted, and failover in under 30 seconds.
4. Remember the **writer endpoint** and **reader endpoint**. The reader endpoint load balances at connection level across replicas, including auto-scaled ones.
5. **Backtrack** gives point-in-time restore without backups.
6. Aurora costs about 20% more than RDS, with up to 5x MySQL and 3x PostgreSQL performance.
