# 66. Amazon RDS with S3 Document Repositories

Why **Amazon RDS** appears in a generative AI course: it can act as a vector store, and the exam guide names a pattern that pairs RDS with an **S3 document repository**.

## RDS as a vector store

- **RDS** can serve as a vector store for embedding values.
- An **RDS SQL Server vector store** is also an option.

## RDS with S3 document repositories

- The exam guide calls out using **RDS** to query **structured data**, which in turn points to **S3** for large unstructured data it refers to.
- RDS acts as a **catalog**: it holds the metadata for content stored in an unstructured way in S3, which suits really large pieces of data.
- In a **RAG** system, the vector store is backed by RDS. A match returns a **pointer to the content in S3**, not the data itself, and the actual data is fetched from S3.

## Exam takeaways

1. Know the pattern the exam guide names: **RDS as a vector store backed by an S3 document repository**, where the vector store returns pointers to data in S3.
2. RDS can hold structured data and metadata (a catalog) while S3 holds large unstructured data.
3. RDS, including RDS for SQL Server, is an option for storing vector embeddings.
