# 64. Amazon RDS

An overview of **Amazon RDS** (Relational Database Service), the engines it supports, what the managed service provides, and **RDS Storage Auto Scaling**.

## What RDS is

- A **managed database service** for databases that use **SQL** as their query language.
- Databases are created in the cloud and managed by AWS.

## Supported engines

- **PostgreSQL**, **MySQL**, **MariaDB**, **Oracle**, **Microsoft SQL Server**, **IBM DB2** and **Aurora** (AWS proprietary database, covered in depth separately).
- Remember the list of engines RDS supports.

## RDS versus running a database on EC2

RDS adds a lot on top of the database itself:

- Fully automated **provisioning** and **operating system patching**.
- **Continuous backups** with **Point in Time Restore** to a specific timestamp.
- **Monitoring dashboards** for performance.
- **Read replicas** to improve read performance.
- **Multi-AZ** for disaster recovery.
- **Maintenance windows** for upgrades.
- **Scaling**: vertical (bigger instance type) and horizontal (adding read replicas).
- Storage is backed by **EBS**.
- Drawback: you **cannot SSH** into RDS instances, because the underlying EC2 instance is not accessible. This is acceptable given everything you would otherwise set up yourself.

## RDS Storage Auto Scaling

- Normally you choose the storage size at creation (for example 20 GB). With Auto Scaling enabled, RDS detects when free space is running low and increases storage automatically, with no downtime or manual operation.
- You must set a **maximum storage threshold** to cap growth.
- Storage increases automatically when all of these hold:
  - Free storage is **less than 10%** of allocated storage.
  - The low-storage condition has lasted **more than 5 minutes**.
  - **6 hours** have passed since the last modification.
- Useful for applications with **unpredictable workloads**.
- Supports **all RDS database engines**.

## Exam takeaways

1. Know the database engines RDS supports.
2. RDS Storage Auto Scaling can come up in the exam: it needs a maximum storage threshold and triggers on under 10% free space for over 5 minutes, at least 6 hours after the last change.
