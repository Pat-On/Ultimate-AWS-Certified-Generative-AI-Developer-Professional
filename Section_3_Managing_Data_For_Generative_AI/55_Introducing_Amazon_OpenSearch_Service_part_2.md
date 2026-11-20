# 55. Introducing Amazon OpenSearch Service (part 2)

How the **managed** Amazon OpenSearch Service differs from plain Elasticsearch. There is also a **serverless** flavor, covered in a later lecture.

## Managed service basics

- You can scale up and down **without downtime**, but you still choose the number of nodes; it is not automatic.
- Pricing: **instance hours, storage and data transfer**. You pay even when the cluster is idle, so shut it down when unused.
- A **domain** is the Amazon term for a cluster: all the resources and configuration needed to run it.
- **Dedicated master nodes**: you choose how many and which instance type. They only manage the domain and hold or process no data, so you rarely need many unless the cluster is massive.
- **Automatic snapshots to S3** for backup.
- **Zone awareness**: spread across multiple Availability Zones in a region for high availability, at the cost of higher latency.
- AWS integrations: **S3** (via Lambda), **Kinesis Data Streams**, **DynamoDB Streams**, **CloudWatch** and **CloudTrail**.

## Security

- Network isolation with **VPC**; encryption at rest and in transit with keys.
- Authentication and access control with **Amazon Cognito** or **IAM**.
- Policy types: **resource-based policies** on the domain (which principals can do what on the OpenSearch API), **identity-based policies** (IAM), and **IP-based policies** tied to IP ranges.
- **All requests must be signed** (the AWS SDK provides signing).
- A cluster can be placed in a VPC for extra security, but you **cannot move it in or out of a VPC later**; decide up front.

## Accessing Dashboards for a VPC cluster

- Dashboards use a web interface, so a VPC-hosted cluster is hard to reach from a browser.
- **Cognito** integration lets users sign in through enterprise identity providers (such as Microsoft Active Directory via **SAML 2.0**) or social providers (Google, Facebook, Amazon), and supports **Cognito user pools**.
- Other ways in: a **reverse proxy** (for example **nginx** on an EC2 host), an **SSH tunnel on port 5601** (the Dashboards port), **Direct Connect** or a **VPN**.

## Anti-patterns (from the AWS Big Data whitepaper)

- **OLTP**: no transactional support; use **RDS** or **DynamoDB** instead.
- **Ad hoc data querying**: AWS would prefer **Athena** for this.
- OpenSearch fits **search and analytics**.
