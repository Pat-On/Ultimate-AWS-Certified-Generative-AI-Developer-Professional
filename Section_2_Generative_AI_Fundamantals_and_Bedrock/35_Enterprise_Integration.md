# 35. Enterprise Integration

A few points about enterprise integration that appear in the AWS training materials for this certification. They are specific enough that you probably need to know them.

## Knowledge bases are the integration point for enterprise data

- Bedrock **knowledge bases** are the one-stop integration point for **internal data and document management systems**.
- They can take data from **S3**, but also from **SharePoint**, **Atlassian Confluence** and many other sources outside AWS.
- Bedrock **integrates that external data into your vector stores natively** and indexes it for you.

## Cross-account access

It comes up in every exam. The specific scenario: your **Bedrock foundation model and the OpenSearch store behind your knowledge base are in different accounts**.

- **OpenSearch has a remote inference connector**, which supports **semantic search across accounts**. With it, a Bedrock knowledge base backed by OpenSearch can be used across accounts.
- The connector alone isn't enough: you also need the **right IAM roles**. The **Bedrock account** that runs the model needs a role that **allows `InvokeModel` access from the OpenSearch account**.

## Event-driven architecture

- When integrating with enterprise systems, put a **buffer between your AWS side and the enterprise side**. This gives **loose coupling** with downstream systems.
- Use **SQS**, **Kafka** or another pub/sub system.
- **Example flow:** documents are uploaded, **EventBridge** picks them up, a **Lambda** function does something with them in Bedrock, and the result goes to an internal data warehouse, ticketing system or CRM outside AWS. An **SQS queue between them** means that if the warehouse or ticketing system is down, the events are **queued, not lost**.
- Generative AI work produces events as it runs, and those events can be queued before they reach the enterprise systems.
