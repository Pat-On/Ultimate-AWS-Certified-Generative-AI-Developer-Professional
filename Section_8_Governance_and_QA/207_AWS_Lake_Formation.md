# 207. AWS Lake Formation

Makes it easier to **set up a secure data lake** ("in days"). Announced in **2018**; **built on top of AWS Glue**.

## What it manages

- **Loading data** from sources and **monitoring** the flows: **S3**, relational or NoSQL databases, in AWS or **on premises**
- **Crawlers, ETL jobs, Data Catalog** and **partitions**
- **Transformations** and cleaning, including conversion to **Parquet** or **ORC** (anything Glue and Spark can do)
- **Encryption** and keys, **access control** and **auditing**

The result is an **S3 data lake** that **Athena**, **Redshift / Redshift Spectrum** and **EMR** can query.

**Pricing:** Lake Formation itself is free; you pay for the services underneath (Glue, S3, EMR, Athena, Redshift).

## Building a data lake

1. Create an **IAM user** for the **data analyst**.
2. Create a **Glue connection** to the data sources.
3. Create an **S3 bucket** for the lake.
4. **Register the S3 path** in Lake Formation and grant permissions.
5. Create a **database** in Lake Formation for the Data Catalog and grant permissions.
6. Use **blueprints** to build **workflows** (for example from database snapshots).
7. Run the workflow and grant **`SELECT`** to the users of Athena, Redshift Spectrum or EMR.

## Data permissions

- Grant to **IAM users and roles**, **SAML** users and groups, or **external AWS accounts**.
- Use **policy tags** (called **LF-Tags** in AWS) on databases, tables or columns, or grant explicitly.
- Choose the actions (select, insert, delete and so on) per **table** or **column**.

## Data filters

Applied when granting **`SELECT`** on a table; created in the console or with the **`CreateDataCellsFilter`** API.

| Security level | Filter |
|---|---|
| **Column** | All rows, chosen columns |
| **Row** | All columns, plus a row filter |
| **Cell** | Chosen columns and chosen rows |

## Governed tables

- A type of S3 table with **ACID transactions** across several tables; the choice **cannot be changed** afterwards.
- Works with **streaming data** (Kinesis), can be queried with **Athena**, and **compacts storage automatically**.
- Row and cell-level security applies to governed and ordinary S3 tables. These features **cost extra**, based on usage.
- AWS has since announced the **end of support** for governed tables; check the current documentation. The course material still lists them.

## Troubleshooting

| Problem | Check |
|---|---|
| **Cross-account** access | The recipient is a **data lake administrator**; **AWS RAM** for sharing with accounts outside your organisation; **IAM** cross-account permissions |
| **Manifests** in Athena or Redshift queries | **Not supported** |
| **Encrypted Data Catalog** | IAM permissions on the **KMS key** |
| Cannot create **blueprints or workflows** | **IAM** permissions |

## Exam takeaways

1. **Secure data lake** on S3 → **Lake Formation**.
2. **Column, row or cell-level** (fine-grained) permissions → **Lake Formation** (data filters).
3. Lake Formation itself is free; underlying services (and the extra table features) are charged.
4. Cross-account problems → **RAM**, IAM and data lake administrator.
