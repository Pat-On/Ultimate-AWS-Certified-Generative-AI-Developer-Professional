# 61. Amazon S3 Vectors - Hands On

Creating an **S3 vector bucket** and vector index in the S3 console, then building a **Bedrock knowledge base** that uses **Amazon S3 Vectors** as its vector store, and cleaning up afterwards.

## Creating a vector bucket and index

1. In the S3 console, open **Vector buckets** (listed under the bucket choices) and create a vector bucket. The name must be globally unique because it is still S3.
2. Encryption defaults to **S3 managed keys (SSE-S3)**; you can choose your own **KMS key** instead. Tags are optional.
3. Open the bucket and create a **vector index** with a name, a dimension and a distance metric.
4. Optionally list **non-filterable metadata** keys under additional settings. The index also has its own encryption setting (the example used the bucket settings).

| Setting | Detail |
| --- | --- |
| Dimension | 1 to 4096 (1536 is a common choice). More dimensions means more storage, slower computation and a higher cost; too few may fail to capture semantic meaning and make search less relevant, so experiment |
| Distance metric | **Euclidean** (straight-line distance between vectors) or **cosine similarity** (smoother, tends to group relevant items together; the instructor prefers it) |
| Non-filterable metadata | Metadata you never need to filter by saves performance, but it must be declared **when the index is created**. Filterable metadata can be added any time |

- There is no console UI for inserting data. Insert programmatically with the AWS CLI `put_vectors` request, or with the purpose-built **`s3vectors-embed-cli`** tool.

## Using S3 Vectors in a Bedrock knowledge base

1. In **Bedrock**, create a knowledge base with a vector store (not Kendra). Name it, and let it create its own **IAM role** automatically (you can control this yourself).
2. Add an **S3 data source**: this is only where the raw data comes from, not the vector store. The example used a text file (the lecturer's self-employment book from the course materials) in a bucket created beforehand.
3. Parsing strategy: the **default parser** is enough for plain text with no multimodal content. Alternatives are **Bedrock Data Automation** or your own foundation model.
4. Chunking: **default chunking** splits sensibly and aims for about **300 tokens per chunk**. A custom **Lambda** function allows finer control.
5. Embeddings model: **Titan Text Embeddings v2** (a newer model is fine as long as it is consistent and reasonably modern).
6. Vector store: choose to create a new one and select **Amazon S3 Vectors**, which is built in. The index dimensions are matched automatically to the embedding model (adjustable when choosing the model).
7. Create the knowledge base, open the data source and **sync** it. The sync took about 10 seconds here.
8. Test with **retrieve and generate**, selecting a generation model (**Nova 2 Lite** in the demo). The answer included citations back to the source, and the details view showed the chunks retrieved from the S3 vector store.

- Using S3 Vectors in a knowledge base is just one option choice; the rest of the workflow is unchanged.

## Cleanup

- Even though S3 is cheap, delete resources you do not need.
- **Deleting a knowledge base does not delete the underlying vector store.** Delete the vector bucket as a separate step.
- A vector bucket cannot be deleted until its **index is deleted first**.
