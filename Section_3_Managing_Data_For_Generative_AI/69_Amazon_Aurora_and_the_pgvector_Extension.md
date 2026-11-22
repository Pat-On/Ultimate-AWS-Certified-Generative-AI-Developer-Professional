# 69. Amazon Aurora and the pgvector Extension

Why **Amazon Aurora** matters for this exam: with the **pgvector** extension it can act as a vector store for RAG systems and knowledge bases.

## What pgvector adds

- A new **vector column type**.
- Distance computation with one of three similarity metrics: **cosine**, **L2** or **inner product**.
- Similarity search with **IVF** and **HNSW**, both covered earlier with OpenSearch.
- **Vector operators for SQL**. This is the new part and something OpenSearch cannot do: complex filtering logic on vector store results can be written as SQL expressions that operate directly on the vectors.
- **Structured and vector data in the same place**, so you can hold chunks and structured data together. JSON could do this too, but it is more native in Aurora.

## When to choose it

- Suits **small to medium RAG systems** whose data is **mostly structured**.
- Aurora is more of a monolith, so scaling can be a challenge.
- The SQL integration is the point to remember.

## Exam takeaways

1. Aurora with pgvector can be the vector store for RAG or a knowledge base.
2. It may be the right answer when the RAG system is small to medium and the data is mostly structured.
