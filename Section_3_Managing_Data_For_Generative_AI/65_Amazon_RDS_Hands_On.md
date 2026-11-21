# 65. Amazon RDS - Hands On

Creating a first **Amazon RDS** MySQL instance with Standard Create, connecting to it from a SQL client, and a tour of the management features (read replicas, monitoring, snapshots) and the cleanup. The SQL itself is out of scope for the exam.

## Steps

1. In the RDS console choose **Databases**, then **Create database**.
2. Pick **Standard Create** (the alternative is **Easy Create**); it is longer but shows every option.
3. Choose the engine and version, then a template.
4. Set availability, identifier and credentials.
5. Choose the instance class and storage.
6. Configure connectivity, authentication, monitoring and additional configuration, then create the database. Creation takes a few minutes until the status is **Available**.
7. Install a SQL client (**SQLElectron**, a GUI client, was used), add a MySQL connection using the instance endpoint, port 3306, user `admin`, the password and the initial database `mydb`, and test it.
8. Run a `CREATE TABLE`, an `INSERT` and a select to confirm the database works.
9. Look at the read replica, monitoring and snapshot options, then delete the database.

## Settings that mattered

| Setting | Choice in the demo | Notes |
| --- | --- | --- |
| Engine | **MySQL** (8.0.28, the default offered) | Six engine types: **Aurora**, MySQL, MariaDB, PostgreSQL, Oracle, Microsoft SQL Server. Whichever version is preselected is fine |
| Template | **Production**, with options changed to stay in the free tier | **Free tier** and **Dev/Test** templates preselect options; Production gives full control |
| Availability | **Single DB instance** | Alternatives are **Multi-AZ** (standby instance) and **Multi-AZ DB Cluster** |
| Identifier and credentials | `database-1`, user `admin`, password | |
| Instance class | Burstable, `db.t3.micro` | Size of the underlying EC2 instance. Classes are standard, memory optimised and burstable |
| Storage | **gp2**, 10 to 20 GB | Production would use an **io1** EBS volume (higher performance) |
| Storage autoscaling | Enabled, maximum 1,000 GB | Grows the volume automatically when it nears a threshold |
| Compute connection | Not connected to an EC2 resource | Choosing an EC2 instance configures networking and security groups automatically, which helps beginners |
| Networking | A specified **VPC**, a **subnet group**, **public access: Yes** | Public access was needed to connect from a local computer. No AZ preference |
| Security group | New, `demo-database-mysql` | MySQL port is **3306** |
| Authentication | **Password authentication** | Other options: **IAM database authentication** (IAM users and roles access RDS directly) and **Kerberos** |
| Monitoring | **Enhanced monitoring** disabled | Enhanced monitoring gives 60-second granularity |
| Initial database name | `mydb` | |
| Backups | **Automated**, retention **7 days** | Retention is 1 to 35 days; 0 disables automated backups. A backup window can be set or left at no preference |
| Log exports | Optional export to **CloudWatch Logs** | For example the audit log, for long-term retention |
| Maintenance | Optional window for **minor version upgrades** | |
| Deletion protection | Optional | Guards against accidental deletion |

- The console showed an estimate of about **$17 per month** (17.34 USD), which does not reflect the free tier. The instructor said a `db.t2.micro` instance qualifies for the free tier, although the demo selected `db.t3.micro`.

## Connecting and troubleshooting

- The instance page shows the **endpoint**, port 3306 and the linked security group.
- The security group had an inbound rule on **TCP 3306** from the creator's IP address only.
- If the connection fails, check that the database is set to **public access** and that the **security group** allows your IP. Loosening the rule to anywhere (IPv4) is an option for testing.

## Management features shown

- **Read replica**: created directly from the instance to add read capacity. The creation dialog also asks whether the replica should be **Multi-AZ** for recovery.
- **Monitoring**: CPU utilisation and database connection counts, among many other metrics, useful for deciding when to scale.
- **Snapshots**: snapshot the database and restore it anywhere, restore to a **point in time**, or migrate a snapshot to another region.
- RDS is a managed service: read replicas, Multi-AZ and instance type changes are handled by the service.

## Cleanup

- Delete the database when finished.
- **Deletion protection** must be disabled first: choose **Modify**, scroll to the bottom, disable it, continue and apply immediately.
- Then delete, skipping the final snapshot, typing the confirmation phrase and acknowledging that everything is lost.
