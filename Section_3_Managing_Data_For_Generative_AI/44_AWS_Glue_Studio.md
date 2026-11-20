# 44. AWS Glue Studio

**AWS Glue Studio** (also called **visual ETL**) is a visual interface for defining ETL workflows, often without writing code. It is a recently invested-in feature and may start appearing on the exam. The instructor notes AWS seems to be pushing people toward Data Wrangler as well.

## Features

- A **visual job editor** that builds **directed acyclic graphs (DAGs)** for complex workflows, with parallel branches from the same source or from different sources.
- Sources: **S3**, **Kinesis**, **Kafka**, any **JDBC** source, the Glue Data Catalog, and a wide range of external systems (MySQL, SQL Server, Snowflake, Google BigQuery, MongoDB, Salesforce, PayPal, QuickBooks and more).
- Transforms: change schema, SQL queries, filters, drop fields, joins, sampling, and a **custom transform** for your own code.
- Targets: **S3** or the **Glue Data Catalog** (and other destinations such as Snowflake or BigQuery).
- **Partitioning** is supported out of the box and is used automatically to speed up jobs.
- A **visual job dashboard** shows job status, what is running and how long jobs take, for troubleshooting.

## Demo summary

- Reached through ETL jobs, then visual ETL (the naming varies in the console).
- Added an S3 source node (order logs), checked the output schema, then added a **change schema** transform (dropped the description field, cast year and day to integer) and a **filter** transform (drop rows where year is below 2001), and wrote the result to another S3 bucket.
- The graph does not have to be linear: for example the filter could run in parallel with the other transform.
- Existing jobs can be monitored from the jobs page, and sample jobs are available.
