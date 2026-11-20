# 59. Using and Tuning OpenSearch as a Vector Store

How **OpenSearch** is used as a vector store for generative AI, and the tuning points likely to appear on the exam.

## OpenSearch as a vector store

- **OpenSearch** (including **OpenSearch Serverless**) is a prominent option for backing a **Bedrock knowledge base**, and the exam treats it as the primary implementation.
- **Serverless does not mean scale to zero**: an idle serverless vector store still costs a few hundred dollars a month.
- **Amazon S3 Vectors** is a newer, simpler alternative (S3 creates vectors from your data and ties to a knowledge base); probably too new for the exam, but worth knowing.
- OpenSearch vector stores are not limited to Bedrock; they also work with **SageMaker AI** systems (Hugging Face or custom models) for RAG.

## Semantic versus hybrid search

- **Semantic search**: compare embedding vectors only and return the chunk of the closest vector.
- **Hybrid search**: combine vector search with traditional **keyword search** to improve relevance. It requires indexing keywords and metadata in addition to vectors.

## Vector search engines and algorithms

- Three engines: **FAISS** (Facebook AI Similarity Search, most commonly used), **NMSLIB** and **Apache Lucene**.
- **Exact nearest neighbor** compares against every vector and is too slow in practice. **Approximate nearest neighbor (ANN)** is the usual trade-off.

| ANN algorithm | Characteristics |
|---|---|
| **HNSW** (hierarchical navigable small world) | Fast, but uses a lot of RAM; scales less well to huge datasets |
| **IVF** (inverted file) | Better for huge datasets or RAM limits, trading away some recall |

- **HNSW parameters**:
  - **m**: edges per node. Higher gives a denser graph, higher recall and more memory.
  - **ef_construction**: size of the dynamic list used building the k-NN graph. Higher gives a more accurate graph but slower indexing.
  - **ef_search**: how thoroughly the graph is explored at query time. Higher gives better recall but slower search.

## Vector compression

- Vectors often have 1000 or more dimensions, so embeddings can take more space than the text itself.
- **Binary vectors**: floats reduced to single bits, **32x compression**. Not useful as embeddings on their own but useful for fast distance search.
- **fp16**: quantizes 32-bit floats to **16-bit** floats; still a useful embedding, and the **default** under the hood for HNSW.

## Sharding and multi-index design

- Balance shard size against CPU. **Semantic-only search** involves little cross-shard coordination, so **larger shards (about 30 to 50 GB)** are fine; **hybrid search** needs **smaller shards** because keyword queries coordinate across shards. Serverless handles this automatically.
- **Multiple indices** for different document types or domains allow individual tuning, shard sizes and even different embedding models, but need **query routing**.
- **Hierarchical indices**: a small, fast top-level index only routes to a detailed index per domain. A foundation model could also make the routing decision.

## Neural plugin

- The **neural plugin** integrates an embedding model into OpenSearch ingest and search pipelines, so you send raw text and OpenSearch computes the embedding and runs the vector query itself. It is an alternative to a Bedrock knowledge base.
- It integrates with **Bedrock**, so a Bedrock embedding model can be called from within OpenSearch.
