# 132. Optimizing Retrieval Performance

This is about **retrieval in RAG**: making sure the lookup in a vector store or knowledge base returns relevant, complete context.

## At the data store level

- The index-level tuning was covered in the **OpenSearch vector store** lectures: optimize the indices and how the data is organized.
- **Hybrid search** (semantic embedding search plus **keyword** search together) improves relevancy.
- You can write a **custom hybrid scoring function** that decides how to combine the semantic score and the keyword relevance score.

## Query pre-processing

Improve the query **before** searching the knowledge base.

| Step | Why |
| --- | --- |
| **Normalize the query's style** to the corpus | A formal query in the style of the content (for example scientific papers) finds more relevant hits than a casual one. |
| **Split multi-part questions** into separate queries | A question about two things rarely matches one chunk covering both. Search each part individually (a separate model may do the split). |
| **Filter out irrelevant questions** | If the question is outside what the knowledge base covers, drop it. |
| **Reduce ambiguity** | A phrase like "the thing I mentioned earlier" means nothing to the knowledge base, so resolve it into an explicit question first. |
| **Extract keywords** | Pull out keywords you may have indexed and search for them directly, which makes hybrid search more efficient. |

## Exam takeaways

1. **Hybrid search** (semantic plus keyword) improves relevancy, and a **custom hybrid scoring function** controls how the two scores combine.
2. Pre-process the query: **match the corpus style, split multi-part questions, discard out-of-scope ones, resolve ambiguity and extract keywords**.
3. Index optimization (OpenSearch) is the lower-level lever.
