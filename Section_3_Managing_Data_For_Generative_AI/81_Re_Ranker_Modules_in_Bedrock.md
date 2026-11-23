# 81. Re-Ranker Modules in Bedrock

**Re-ranker models** in **Amazon Bedrock** improve the relevance of the chunks retrieved from a knowledge base for **RAG**.

## What re-ranking does

- Retrieved chunks may not be very relevant to the original query, even when they are close in vector distance.
- Semantic search is only the starting point. The re-ranker **calculates the relevance of each chunk to the query** and **reorders** the results so the best come first.

## How to use it

- The **Rerank operation** in the Bedrock API ranks whatever documents you supply relative to a query, whenever you choose to call it.
- Alternatively, specify a **reranker model** when querying your **knowledge base**.
- Built-in model choices are from **Amazon** and **Cohere**.
- They are available only in **limited regions**, so check availability in your Bedrock region first.

## Exam takeaways

1. Re-ranking reorders retrieved chunks by **relevance to the query**, beyond embedding distance.
2. Use the **Rerank API operation** for arbitrary documents, or set a reranker model on a **knowledge base** query.
3. Models come from **Amazon or Cohere**, in **limited regions** only.
