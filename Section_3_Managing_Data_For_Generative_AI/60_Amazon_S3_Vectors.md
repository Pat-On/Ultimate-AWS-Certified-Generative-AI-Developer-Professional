# 60. Amazon S3 Vectors

How OpenSearch works as a vector store for generative AI (the exam's main option), its finer points, and the newer **Amazon S3 Vectors** feature that may take over part of that role.

## OpenSearch as a vector store

- **Bedrock Knowledge Bases** are backed by OpenSearch in the current exam, and OpenSearch also has a **serverless** option.
- **Serverless is not scale to zero.** An idle serverless OpenSearch collection still bills, a few hundred dollars a month, so shut it down when it is not in use.
- OpenSearch vector stores are not limited to Bedrock. They can back RAG on SageMaker AI, on Hugging Face models or on custom models.

## Semantic versus hybrid search

- **Semantic search** embeds the query and returns the chunk whose embedding vector is closest. It compares vectors only, which can miss relevant data.
- **Hybrid search** combines vector search with classic **keyword search**. It needs keyword and metadata fields indexed next to the vectors, and it improves the relevancy of results.

## Vector engines and search algorithms

- Three engines: **FAISS** (Facebook AI Similarity Search, the most used), **NMSLIB** and **Apache Lucene**.
- **Exact nearest neighbor** compares the query with every vector, which is too slow in practice.
- **Approximate nearest neighbor (ANN)** is the practical choice, and it is usually good enough:
  - **HNSW** (Hierarchical Navigable Small World) is fast and efficient but uses a lot of RAM, so it may not scale to a huge dataset.
  - **IVF** (Inverted File) suits very large datasets where RAM is a problem, and it trades recall for speed and memory.

### HNSW parameters to know

| Parameter | Meaning | Trade-off |
| --- | --- | --- |
| `M` | Edges per node | Higher gives a denser graph and higher recall, at the cost of memory |
| `ef_construction` | Size of the dynamic list used while building the k-NN graph | Higher gives a more accurate graph but slower indexing |
| `ef_search` | How thoroughly the graph is explored at query time | Higher gives higher recall but slower search |

## Vector compression

An embedding of about 1,000 dimensions for a 300-character chunk can take more space than the text itself, so compression matters. It usually happens under the hood.

- **Binary vectors** turn floating point values into bits, about **32x compression** against 32-bit floats. They are not useful embeddings on their own, but they speed up distance search.
- **FP16** stores 16-bit instead of 32-bit floating point values. The embedding stays usable with slightly less resolution. It is the **default compression** in HNSW.

## Sharding and indices

- Balance **shard size** against **CPU**.
- **Semantic-only search** needs little cross-shard coordination, so it can use **larger shards, 30 to 50 GB**.
- **Hybrid search** coordinates keyword queries across shards, so it wants **smaller shards, 10 to 30 GB**.
- On OpenSearch Serverless sharding is automatic.
- **Multiple indices**: different document types or domains can have their own index, so each corpus can have its own tuning, shard size and even **embedding model**. This needs **query routing**.
- **Hierarchical indices** are one way to route: a small, fast top-level index sends the query to a detail-level index per domain. A foundation model could make the routing decision instead.

## OpenSearch neural plugin

- Puts an **embedding model into the OpenSearch ingest pipeline and query path**. You send raw text and OpenSearch creates the embedding and runs the vector query itself.
- It can call a **Bedrock embedding model** from inside OpenSearch.
- That makes OpenSearch an alternative to a Bedrock Knowledge Base when you want everything in one system.

## Amazon S3 Vectors

The instructor expects it to replace much of the OpenSearch role for Bedrock knowledge bases, but treats it as too new for the current exam.

- Up to **90% cheaper** than OpenSearch and much simpler.
- Workflow:
  1. Create an **S3 vector bucket**.
  2. Create a **vector index**, giving the dimensions and the distance metric.
  3. Store embeddings with `put_vectors`, with whatever metadata you want.
  4. Query with `query_vectors`.
- A put request holds a vector key, the `float32` data and metadata such as the source text and a genre.
- The open-source **`s3vectors-embed-cli`** is an alternative to boto3 and the AWS CLI. `put` turns text or images into embeddings with Bedrock and stores them, and `query` embeds the query and searches the index.
- You can generate your own vectors, or use the full integration with **Bedrock Knowledge Bases**, which manages everything. It also works with Bedrock inside **SageMaker Unified Studio**.

### Specifics and limits

- **Strongly consistent**: newly added vectors are queryable immediately.
- Data is optimized over time for price and performance.
- Latency is advertised only as **100 ms to 1 s**.
- AWS recommends a **tiered search strategy**: S3 Vectors for infrequently queried vectors, OpenSearch for performance-critical queries.
- The S3 to OpenSearch connection **copies (exports) the data**, so you pay for both if you are not careful.
- OpenSearch can use an **S3 Vectors engine** as its backend, on **managed clusters only**.
- Limits: **10,000 indices per bucket** and **2 billion vectors per index**.

### Best practices

- Insert and delete in large batches, about **500 vectors per API call**. Concurrent requests for smaller batches reach about 2,500 vectors per second.
- Add a **retry mechanism** for queries: only hundreds of queries per second per index are supported before HTTP 429 errors.
- Use **multiple indices** for per-index performance and for data isolation or multi-tenancy.
- Mark metadata fields that never need filtering as **non-filterable**.

## Choosing a vector store (from the slides)

| Scenario | Choice |
| --- | --- |
| SharePoint or Confluence, must respect existing permissions | **Amazon Kendra** |
| Graph relationships (fraud rings, lineage, "who knows who") | **Neptune Analytics** |
| Already on Postgres, need joins and transactions plus vectors | **Aurora PostgreSQL with pgvector** |
| Huge vector corpus, cost pressure, vectors tied to S3 objects | **S3 Vectors** (very low cost, higher latency) |
| Full search platform with a lot of tuning control | **OpenSearch managed** |
| Unpredictable traffic, minimize operations | **OpenSearch Serverless** |

## Exam takeaways

1. OpenSearch is the exam's default vector store for a Bedrock Knowledge Base. S3 Vectors is newer and may replace it.
2. Know semantic versus hybrid search, and that hybrid needs keyword and metadata indexing.
3. HNSW is fast but RAM-heavy. IVF is for huge datasets, at the cost of recall.
4. Know the HNSW parameters `M`, `ef_construction` and `ef_search` and their trade-offs.
5. FP16 is the default compression, and binary vectors give about 32x compression for fast distance checks.
6. Larger shards for semantic search, smaller shards for hybrid search.
7. The neural plugin puts the embedding step inside OpenSearch and can call Bedrock.
8. S3 Vectors is cheap, simple and strongly consistent but slow (100 ms to 1 s), and it pairs with OpenSearch in a tiered strategy.
