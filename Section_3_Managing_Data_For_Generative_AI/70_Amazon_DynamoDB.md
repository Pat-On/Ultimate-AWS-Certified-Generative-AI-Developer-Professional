# 70. Amazon DynamoDB

An introduction to **Amazon DynamoDB**, a serverless NoSQL database: why NoSQL exists next to SQL, the table and item model, the two primary key options and how to choose a partition key.

## SQL versus NoSQL

- A traditional architecture has clients, an application layer (load balancer plus EC2 instances in an Auto Scaling group) and a database layer such as **Amazon RDS** on MySQL or PostgreSQL.
- Relational (RDBMS) databases give the **SQL** query language, strong data modelling through tables and schemas, joins, aggregations and complex computations.
- Their scaling is mostly **vertical**: a more powerful CPU, more RAM or better disk I/O.
- Horizontal scaling only increases **read** capability, through more EC2 instances at the application layer or **RDS read replicas**. The number of replicas is limited, and RDS has no horizontal write scaling.
- **NoSQL** (not only SQL, or non-SQL) databases are non-relational and distributed, which gives horizontal scalability. **MongoDB** and **DynamoDB** are well-known examples.
- For simplicity, assume NoSQL databases have no query joins (or very limited support) and no aggregations such as SUM or AVG, although they are evolving. All the data needed must therefore sit in one row.
- They scale horizontally for both reads and writes by adding instances behind the scenes.
- Neither SQL nor NoSQL is right or wrong: it depends on data modelling, the application, user queries and scaling needs.

## DynamoDB features

- **Fully managed**, highly available NoSQL database with replication across multiple AZs out of the box. It is not a relational database.
- Fully distributed, scaling to millions of requests per second, trillions of rows and hundreds of terabytes of storage, with fast and consistent low-latency retrieval.
- Integrated with **IAM** for security, authorisation and administration.
- **DynamoDB Streams** enable event-driven programming.
- Low cost, with auto scaling.
- Two table classes for different storage tiers: **Standard** and **Infrequent Access (IA)**.

## Tables, items and attributes

- A table has a **primary key**, which must be decided before the table is created.
- A table can hold an unlimited number of rows, also called **items** (the course uses the terms interchangeably).
- Each item has **attributes**, similar to columns but more powerful: they can be nested, added over time without defining them all at creation, and be null. An attribute may be missing from some items.
- Maximum item size is **400 KB**.
- Supported data types:

| Category | Types |
| --- | --- |
| Scalar | string, number, binary, boolean, null |
| Document | list, map (gives nesting) |
| Set | string set, number set, binary set |

## Primary key options

The exam will definitely test this.

| Option | Also called | Rule |
| --- | --- | --- |
| **Partition key** only | Hash | Must be unique per item and diverse enough to distribute data |
| **Partition key + sort key** | Hash plus range | The combination must be unique per item. Data is grouped by partition key |

- Partition key example: a users table with a user ID as partition key. Other attributes (first name, last name, age) can be missing on some items.
- Partition plus sort key example: a users-game table with user ID as partition key and game ID as sort key. A user can attend many games, so the same partition key can appear on several rows with different sort keys, but the user ID and game ID combination is unique. The remaining attributes (such as score and result) are ordinary attributes.
- Choosing a good partition key matters because it determines how well data is distributed.

## Choosing a partition key

Exam-style exercise: for a movie database, pick the best partition key to maximise data distribution from movie ID, producer name, lead actor name or movie language.

- **Movie ID** is the answer: it is unique per row.
- Movie language is a poor choice: there are few values and most movies would be English, so data skews towards one value.
- Always choose the attribute with the **highest cardinality**, the one that can take the most values.

## Exam takeaways

1. Know the two primary key types and that the key is chosen before the table is created.
2. Choose the partition key with the highest cardinality so data is evenly distributed.
