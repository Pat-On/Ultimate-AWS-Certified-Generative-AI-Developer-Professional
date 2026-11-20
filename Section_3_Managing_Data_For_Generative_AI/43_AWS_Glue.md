# 43. AWS Glue

**AWS Glue** builds table definitions and runs ETL (extract, transform, load) automatically. It features heavily on the exam: after machine learning content moved out of the Big Data exam, Glue and **Redshift** filled the gap. Focus on how Glue connects services together in larger applications.

## What Glue does

- **Serverless**: nothing to maintain.
- **Central metadata repository** for a data lake: discovers schemas from unstructured data in **S3** and publishes table definitions (the **Glue Data Catalog**) so **Athena**, **Redshift**, **EMR** (for example Hive), RDS and other SQL-like tools can query it.
- **Custom ETL jobs**: triggered by data arrival, on a schedule or on demand. Fully managed, running on **Apache Spark** without you managing a Spark cluster.

## Glue crawler and Data Catalog

- The **crawler** scans data in S3, usually infers the schema automatically (sometimes needs hints), and can run on a schedule or on demand.
- It populates the **Data Catalog** with table definitions: column names, data types and data location.
- Tools such as Athena, Redshift and Hive then query the unstructured S3 data as if it were relational. The data **stays in S3** and is not copied. Results can be visualized with **QuickSight**.
- Glue is the glue between an unstructured data lake and structured analytics tools.

## Glue and S3 partitions

- The crawler derives **partitions** from how your S3 data is organised, so plan the layout around how you will query.
- Example with hourly sensor data from devices:
  - Query mainly by time range: organise as year, then month, then day, then device.
  - Query mainly by device: put the device ID first, then year, month, day.
- A likely exam question: choose the optimal S3 organisation for the access pattern, so partitions make sense.
