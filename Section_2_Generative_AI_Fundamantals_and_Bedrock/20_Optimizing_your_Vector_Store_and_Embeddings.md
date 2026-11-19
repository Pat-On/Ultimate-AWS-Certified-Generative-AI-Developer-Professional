# 20. Optimizing your Vector Store and Embeddings

Chunking (lectures 18 and 19) is one way to tune the retrieval stage of RAG. This lecture covers three more: the size of the embedding vectors, attaching metadata to chunks, and keeping the knowledge base up to date.

## Vector size (dimensions)

- Embedding vectors translate chunks into points in space, and **how close two vectors are shows how semantically similar the texts are**. The question is how big those vectors need to be. This is about **vector size, not chunk size**.
- **Smaller vectors** mean fewer dimensions per chunk, so **less cost** to store, process and send, but a **trade-off in retrieval quality**, because too few dimensions lose meaning.
- **Larger vectors** waste space and money if you don't need them.
- **Amazon Titan embeddings default to 1024 or more dimensions** (the instructor has seen 1024 and 1536 cited). That may be more than you need: for a chunk of a few hundred characters, the embedding can cost more to store than the text.
- Balance dimensionality against **domain fit**: if the concepts you search for are simple, with few categories that could be confused, try smaller vectors and save money. If they are complex, larger vectors may help. Experiment.

## Sparse versus dense embeddings

- **Sparse** vectors are large and **mostly empty**. The example is **one-hot encoding**: one dimension per animal, with a 1 in the matching one and 0 everywhere else, so a chicken has a 1 in "chicken" and 0 in "squid", "lemur" and the rest.
- **Dense** vectors are smaller and **packed with semantic information**: floating-point values in every dimension that together place the chunk in multidimensional space. **This is what you generally use** for generative AI.
- **Trade-off:**
  - Sparse vectors give **greater similarity factors**, so they are used a lot in recommender systems (comparing what two people bought), and classical AI has ways to compress them. That is hard to do on a GPU, so it is rarely seen in generative AI.
  - Dense vectors are **more efficient**, in memory and in general.

### Similarity factor and cosine similarity

- A **similarity factor** is a measure of how close two vectors are. The common one is **cosine similarity**: the cosine of the angle between the two vectors. It works in any number of dimensions.
- Identical vectors give 1 and completely different ones give 0.
- It is also smooth, with no sharp discontinuities, which makes it useful mathematically. Remember this one.

## Metadata

- A vector store can hold more than the vector and the chunk text. Typically you store the **chunk and its embedding**, but you can also attach **metadata**.
- Pass a **`metadata.json`** file when creating the knowledge base to say what is content and what is metadata. Metadata is **not chunked**, but it stays attached to each chunk and can be retrieved with it. Example for the chunk "A chicken is a domesticated bird commonly raised for meat and eggs.":
  ```json
  { "section": "introduction", "topic": "biology", "keywords": ["chicken", "domesticated", "bird", "meat", "eggs"] }
  ```
- **Hybrid retrieval:** search first by semantic similarity of the vectors, then use the metadata to **fine-tune or rerank** the results by how relevant each chunk's metadata is to the prompt. Reranking is covered later in the course.
- Other useful metadata: a **document ID** (to get back to the source document), a **category**, **access-control** information (to keep content out of certain uses), **data lineage** (where it came from, for **citations** in the answer), and any other context.

## Keeping the knowledge base up to date

- Stale data hurts results. One pattern: **new or changed content triggers a Lambda function** (for example an S3 event), which starts a **batch update** (`StartIngestionJob`) so embeddings are generated in batches, for efficiency.
- **Don't sync on every change.** If many updates land in S3, calling `StartIngestionJob` over and over, even every second, backs up fast. Better to queue the work (for example with AWS Batch, plus EventBridge) and sync on a schedule.
- For the exam, you should understand that a Lambda function can kick off knowledge base updates. Fancier ways come later in the course.
