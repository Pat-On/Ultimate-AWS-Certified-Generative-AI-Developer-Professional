# 14. Vector Stores and Semantic Search

The data store behind RAG is critical, because RAG is only as good as its ability to retrieve results relevant to the prompt. In Bedrock this store is the **data store used by a knowledge base** (Bedrock doesn't use the term "RAG" itself). Lecture 15 covers knowledge bases.

## Choosing a data store

- You can use whatever database suits the data you are retrieving:
  - A **graph database** (e.g. Neo4j) for relationships between items, product recommendations or a knowledge graph. It generally gives very good results.
  - **OpenSearch** (or similar) for traditional text search such as TF-IDF. The old-fashioned way is fine, and **hybrid** approaches combine it with semantic search.
- But almost every RAG example today uses a **vector database with semantic search**. It leverages AI: the stored **embeddings** encode the meaning of the data, which in theory gives better results.
- **Elasticsearch and OpenSearch can act as a vector database**, which is why OpenSearch is so often used in Bedrock knowledge bases.

## Embeddings

- An **embedding** is a big vector associated with your data, such as a chunk of text (or an image).
- Think of it as a **point in multidimensional space**, typically hundreds or thousands of dimensions. It represents the meaning of the data.
- Embeddings are computed so that **similar items are close together** in that space. That is why it is called semantic search.
  - Example: "potato" and "rhubarb" (both vegetables) sit near each other, and "Starship Enterprise", "Spaceballs" and "The Orville" form a separate science-fiction neighbourhood.
- **Computing them:** embedding foundation models such as **Titan** can compute them in bulk, which is relatively inexpensive.
  - It is easy because embedding is built into how LLMs work from the start (the prompt becomes tokens that map to embedding vectors). You are repurposing that capability for your own data.

## Vector databases and vector search

- A vector database stores your original data (text or images) **alongside its computed embedding vectors**.
- **Retrieval ("vector search"):**
  1. Compute an embedding vector for what you are searching for (the prompt).
  2. Query the database for the items closest to that vector.
  3. Get back the **top-N most similar items**, which is effectively **K-nearest neighbour**.
- Closeness is usually measured with a **cosine** metric.
- With thousands or millions of vectors, the database doesn't scan every one. It typically uses optimisations to narrow the set it searches.

### Examples of vector databases

- **Existing databases coerced into vector search**, as many vendors have added vector support because of generative AI:
  - OpenSearch and Elasticsearch (the one Bedrock steers you towards, since it is an Amazon product), SQL databases, Neptune, Redis, MongoDB and Cassandra.
- **Purpose-built vector databases:**
  - Commercial: Pinecone (the one the instructor sees most often, and seemingly winning) and Weaviate.
  - Open source: Chroma, Marqo, Vespa, Qdrant, LanceDB, Milvus and vectordb.
- You can store the vectors in whatever database you like and connect Bedrock to it.

## Example: RAG with Star Trek

A RAG system holds all of Data's script lines from Star Trek: The Next Generation. The prompt is "Data, tell me about your daughter Lal."

1. Use a text-to-embedding model to compute an **embedding vector for the prompt**.
2. Query the vector database of Data's lines: a semantic search that returns the vectors closest to the prompt's.
3. **Embed the results in the prompt**: "You are Commander Data from Star Trek. How might Data respond to the question 'Data, tell me about your daughter Lal', taking into account the following related lines from Data: ...", followed by the top five or so lines.
4. The foundation model generates the answer.

The slide's overall shape is **prompt + query + relevant data**. Result quality depends on several choices:
- **K**: how many similar lines go into the prompt.
- **How relevant** the retrieved lines are.
- **How the prompt is phrased**.

So these systems can be sensitive in practice.
