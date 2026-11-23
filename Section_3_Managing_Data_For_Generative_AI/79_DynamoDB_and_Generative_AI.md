# 79. DynamoDB and Generative AI

**DynamoDB** can now act as a **vector store** with **vector indexes** and the **SearchVectors API**, as well as serving near real-time data and chat history to generative AI applications.

## Roles in GenAI

- A **vector store** encodes the semantic meaning of text as a vector of numbers, so similar items are found by looking up nearby vectors.
- It can **serve your model with near real-time data**, for chatbots and other AI applications that need fast storage and retrieval.
- It can store **chat histories**, giving "long term memory" for AI agents and context awareness in a chatbot.
- The older approach retrieves the whole history of a user. The modern approach embeds what is being discussed now and uses the vector index to return only the **relevant** records.

## Vector indexes

- Similarity search on embeddings stored **alongside your operational data**, in the same table.
- Lives inside DynamoDB: **no separate vector database and no sync pipeline**.
- Queried through the new **SearchVectors API**, which uses **approximate nearest neighbour (ANN)** search rather than comparing every vector.
- Up to **5 vector indexes per table**.
- Flow: embed the query (for example with Bedrock), call SearchVectors, get the top-K similar items, then feed them into the LLM prompt for RAG.

| Feature | Detail |
| --- | --- |
| Distance functions | **COSINE**, **EUCLIDEAN**, **DOT_PRODUCT**. Cosine is the safe default for text embeddings, and dot product is similar to it |
| Partition key and filters | Optional, to scope and scale searches |
| Projections | Work like a **GSI**: only projected attributes are returned |
| Other features | **Streams, TTL, global tables and point-in-time recovery** keep working |

- Use cases: **RAG**, semantic search, agent memory, recommendations.

## Limitations

- **On-demand capacity mode only**.
- Results are **approximate (ANN)**, with no exact search.
- Vectors are stored as **32-bit floats** only.
- Readable **only through SearchVectors**. No Query, Scan, PartiQL, DAX or fine-grained access control.
- **16 MB response limit with no pagination**.
- Inline filters are **equality-only**. Do any other filtering or pagination in your application.
- The **distance function and projection are locked in** at index creation. Changing them means deleting and recreating the index.
- Pricing: index writes and searches are billed **per byte (1 KB minimum)**, on top of normal table charges.

## Why choose it, and the alternatives

| Option | Trade-off |
| --- | --- |
| **DynamoDB** | Data and chat history already there, so no replication. Serverless, low latency, everything in one table. Moderate cost |
| **S3 Vectors** | **Cheaper** for massive, rarely queried vector sets, but **higher latency** |
| **OpenSearch** | **Richer search** (hybrid, full-text, exact k-NN), but more to manage and more expensive, even serverless, which still has an underlying cost when idle |

## DynamoDB and OpenSearch

- DynamoDB has a **zero-ETL integration with OpenSearch**. Create a pipeline from DynamoDB to OpenSearch, then use OpenSearch as the **vector store for a Bedrock knowledge base**.
- This is the pattern for bringing DynamoDB data into a Bedrock knowledge base.

## Exam takeaways

1. DynamoDB vector indexes are queried only via **SearchVectors** (ANN) and support **COSINE, EUCLIDEAN and DOT_PRODUCT**.
2. Limits to remember: **on-demand mode only**, **32-bit floats**, **16 MB unpaginated response**, **equality-only filters**, and distance function and projection **fixed at creation**.
3. Choose DynamoDB when the data is already there and you want low latency, **S3 Vectors** for cheap massive scale with higher latency, and **OpenSearch** for richer search at higher cost.
4. To feed DynamoDB data into a **Bedrock knowledge base**, use the **zero-ETL pipeline to OpenSearch**.
5. DynamoDB also stores **chat history** for agent long-term memory.
