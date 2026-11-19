# 16. Hands-On with Knowledge Bases

A walk-through of creating a knowledge base with its own OpenSearch Serverless vector store, then querying it in the console. It is the first step towards the larger agentic systems built later. The console UI changes often, so things may not be exactly where they appear in the video. Use a **region that supports Bedrock**.

## Creating the knowledge base

- In the Bedrock console, **Knowledge Bases** is under **Build**.
- A knowledge base can be created with:
  - a **vector store** (used here, for more control);
  - a **structured data store**, connected to a database or table;
  - **Kendra** (covered later).
- Give it a name and let Bedrock **create its own IAM permissions**. Setting your own gives finer control, but getting the permissions right is tricky.

## Data source

- The data source is the data you import into the vector store, **not the vector store itself**.
- Options: **S3**, SharePoint, Salesforce, Confluence, a **web crawler**, or a custom data source.
- The demo uses the **full text of the instructor's old self-employment book** (`book.txt` from the course materials):
  1. Create an S3 bucket (names are **globally unique**, and the defaults are fine) and upload `book.txt`.
  2. Back in Bedrock, browse S3 to select it. A newly created bucket may not show up until you refresh the whole page.

### Parser

- **Default parser:** fine for plain text, as here.
- **Bedrock Data Automation (BDA):** extracts structured data from unstructured, multimodal content (images of IDs, passports, forms, PDFs, audio, video).
- **Foundation model as parser:** has a model extract meaning from PDFs, images, tables and forms.
- Choose according to the nature of your data.

### Chunking strategy

- **Default chunking:** about **300 tokens per chunk** (roughly 300 words), without splitting sentences. Each chunk becomes one embedding vector, and retrieval returns the chunks most relevant to the query. It works if a passage's meaning fits in a window that size.
- This settles lecture 15's open question: the default is 300 **tokens**.
- Other options:
  - **Custom:** set your own tokens per chunk and the **overlap** between chunks.
  - **Hierarchical:** a **parent-child** structure. The search matches the small, precise **child** chunks, then goes up to the **parent** for a more complete context.
  - **Semantic:** a **foundation model** splits the text by concept or topic change. It is more expensive because it uses a model.
  - **No chunking:** you pre-process the data yourself, one chunk per document, for ultimate control.

### Other optional settings

- A **Lambda function** as a transformation step, so data goes through your own code for chunking and processing before it reaches the vector store.
- Your own **KMS key** for security.
- A **data deletion policy**. By default, the vector store *data* is deleted when the data source is deleted.

## Embedding model and vector store

- Pick an **embedding model** to turn the chunks into vectors. The demo uses **Titan Embeddings G1** with on-demand inference.
  - If none are listed, you may be in a region without Bedrock, or may need to request model access.
- **Vector store:** quick-create a new one or connect an existing one. The choices:
  - **OpenSearch Serverless:** the default the exam focuses on, and used here.
  - **Neptune Analytics:** for graph-structured data, such as social networks.
  - **Aurora** (PostgreSQL vector add-on): suits medium-sized data where SQL capabilities matter.
  - **S3 Vectors:** in preview at recording time and not in scope for the exam. It is simpler and cheaper, and the instructor's pick for a new system.
- Optional extras are a KMS key for OpenSearch and more redundancy at more cost.
- Review and create. Creating the OpenSearch Serverless store took about **five minutes**.

## Sync and test

1. The knowledge base starts empty: **sync the data source** to index the content. The small book took about 10 seconds.
2. Choose **Test knowledge base** and select **retrieval and response generation**, which acts as a simple test agent.
3. Pick a model to generate the responses (the demo uses the latest Claude Sonnet), which needs model access.
4. Ask a question about the content: "What are some steps to follow before deciding to become self-employed?"

Results:
- The answer is drawn from the book and has **citations**. Clicking one links to the source.
- **Details** shows the original chunks retrieved, the **top five** most relevant (about 300 tokens each).
- Chunks can carry **metadata**, used here for citations. It could also support **hybrid search** on metadata keys alongside the vectors, which is covered later.

## Cost and cleanup

- Later exercises build on this knowledge base (a guardrail, then an agent), so you can leave it up if you will continue straight away.
- **OpenSearch Serverless keeps billing even when idle**: the simplest instance costs a couple of hundred dollars a month.
- **Deleting the knowledge base deletes only its data, not the vector store.** The console now warns about this. As a second step, go to **OpenSearch → Serverless → Dashboard** and **delete the collection**.
- If you won't reach the agent lectures soon, tear it down and recreate it later. The next lecture repeats this warning.
