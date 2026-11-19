# 13. Retrieval-Augmented Generation (RAG)

**RAG** is a popular alternative to fine-tuning. In Bedrock, the external data source it queries is called a **knowledge base** (lecture 15).

## The idea

- Think of RAG as an **open-book exam for an LLM**: instead of relying only on what the model learned in training, you query an external database for the answers.
- The flow:
  1. Take the user's prompt, e.g. "What did the President say in his speech yesterday?".
  2. Search the external database (here, news articles) for content that is semantically relevant to the prompt.
  3. **Augment the prompt** with what came back, e.g. "...Consider the text of the following news article in your response: Last night, the President...".
  4. Send the augmented prompt to the foundation model.
- This lets the model answer about things after its training cutoff, or things it never saw.
- Tools and functions (LLM agents, covered later) are a slightly more principled way to wire the search into the system.

### Example: Jeopardy!

The query is "In 1986, Mexico scored as the first country to host this international sports competition twice."

- A **retriever** first encodes the query as an embedding and searches the database (or knowledge base) of trivia for the most relevant documents.
- Those top documents are added to the prompt and handed to the **generator**, which is the foundation model.
- The generator produces the answer, "the World Cup".
- Basically, the generator is handed potential answers from an external database.

## Pros

- A **faster and cheaper way to bring in new or proprietary information** than fine-tuning, at least in the short term. New data just goes into the database, with no expensive fine-tuning run.
- **Updating information** is just a matter of updating a database.
- It can use **semantic search** through a **vector database**. Embeddings encode the meaning of text, so you can find the passage most semantically similar to the prompt (lecture 14).
- It can **reduce hallucination** when the model is asked about something it wasn't trained on, by giving it real information instead of leaving it to make something up. It does not eliminate it.
- If your boss wants "AI search", this is an easy way to deliver it.
- Technically you are **not training a model** with this data (no fine-tuning, no custom model), you are only feeding it into the prompt.

## Cons

The lecture says these probably won't be on the exam.

- At heart it is a search whose results an LLM rephrases, which makes it "the world's most overcomplicated search engine". The search itself can be anything, including a hybrid of a traditional database and a vector store. The model's own training still helps it expand on what it is given.
- **More tokens per prompt**, because the retrieved data goes into every prompt. This adds up, so the saving over fine-tuning can be a false economy.
- **Expensive:** vector stores take a lot of storage and computation.
- **Very sensitive to the prompt template** you use to fold the data in. Small wording changes can change results.
- **Non-deterministic** (lowering the temperature helps), so it is hard to test and evaluate.
- **It can still hallucinate**, even with extra information.
- **Very sensitive to the relevance of what is retrieved.** This is the biggest challenge, and it depends on how the data is stored. Splitting text into fixed-size character chunks doesn't guarantee a chunk holds a coherent idea, and an irrelevant chunk can send the answer off the rails. See chunking in lecture 18.
