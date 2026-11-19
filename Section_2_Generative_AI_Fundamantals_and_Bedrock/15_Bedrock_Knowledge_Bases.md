# 15. Bedrock Knowledge Bases

In Bedrock, RAG is wrapped up as **knowledge bases**. The idea is the same as RAG in lecture 13, and the store behind it is the vector store from lecture 14.

## What goes into a knowledge base

- **Data sources**
  - Your own documents in **S3**, structured or unstructured: raw text, JSON, structured data (optionally with a JSON schema).
  - A **web crawler**: point it at a set of web pages (which you presumably have permission to crawl).
  - Third-party connectors: **Confluence, Salesforce and SharePoint**.
- **An embedding model**
  - Needed to compute the embedding vectors for each chunk of your documents. You must have **model access** to it.
  - Currently **Cohere** or **Amazon Titan**.
  - You can control the **vector dimension**, i.e. how many dimensions each vector has.
- **A vector store**
  - For development, a **serverless OpenSearch** instance (OpenSearch has built-in vector support) is selected by default.
  - Other options: **MemoryDB** (now with vector capabilities), **Aurora**, **MongoDB Atlas**, **Pinecone** and **Redis Enterprise Cloud**.
- **Chunking:** you control how the data is split, since a big document can't go into the store as a single entry. You want to retrieve only the pieces relevant to the user's question.
  - You control the **chunk size** and the **overlap between chunks**.
  - The default is about 300 **tokens** per chunk (lecture 16 confirms this in the console). The lecture said "characters" from memory, but the slide describes chunk size in tokens.
  - Arbitrary fixed-size slicing is what people usually do, but a coherent thought per entry is better. Splitting by sentence or paragraph, using structured data, or using a graph database for a knowledge graph can all do better. Chunking strategies come up again in lectures 18 and 19.

## How the pipeline fits together

- **Ingestion:** source documents go through Bedrock, which creates embedding vectors for each chunk, and these are stored in the vector store.
- **At query time**, Bedrock retrieves the relevant chunks from the vector store by semantic search and adds them as context to the prompt that goes to the foundation model.

## Ways to use a knowledge base

1. **"Chat with your document"** in the Bedrock console: basically automatic RAG, and a quick-and-dirty way to get a RAG system running. Give it data in S3 and pick a foundation model to talk to it. Behind the scenes:
   - The user query triggers a **semantic search** in the vector store (e.g. OpenSearch), which returns the most relevant documents. This is the **context**.
   - The context is combined with the query into an **augmented query**.
   - That goes to the Bedrock foundation model, which produces the **response**.
2. **Directly from your application** through the Bedrock APIs (`Retrieve` and `RetrieveAndGenerate`, lecture 7).
3. **As part of an agent**, called **agentic RAG** or an LLM agent, which a later example covers.

## Hands-on preview

The next lecture creates a knowledge base on an OpenSearch vector store, using the full text of the instructor's old book on self-employment as the source data.
