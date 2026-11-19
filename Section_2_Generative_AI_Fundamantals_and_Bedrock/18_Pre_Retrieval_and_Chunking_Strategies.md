# 18. Pre-Retrieval and Chunking Strategies

The exam expects more depth on RAG than the high-level view in lectures 13 to 15. To get it, break up the "R": what does the retrieval stage actually do, and how can each part be tuned?

## The three stages

1. **Pre-retrieval**: everything done before data is looked up at runtime.
   - **Indexing:** how data is stored in the vector store, including **granularity / chunking**.
   - **Data extraction:** how the data is extracted in the first place.
   - **Query rewriting:** rewriting an incoming query so it finds the data more effectively.
2. **Retrieval:** the lookup itself. How it works depends on the vector store, and is not terribly interesting in itself.
3. **Post-retrieval:** making sense of what came back: possibly **reranking**, deciding what is most relevant, and **augmenting** the information further, before finally **generating** the response.

## Pre-retrieval: granularity

The choices you make in storing data strongly affect response quality.

- You want enough context around what you retrieve, but not so much that you lose **relevance** to what is being asked.
- Pieces that are too small are also a problem: you pick up snippets with no meaning of their own. It is "kind of an art".
- **Example: a Lieutenant Commander Data simulator built from his script lines.** Options include:
  - every set of lines he had, line by line, or individual sentences;
  - fixed-length blocks of text;
  - including the other characters' surrounding lines for context, instead of only his;
  - **summaries** of the lines, possibly produced by an LLM, so you don't store the raw data at all.
- **Chunking** is the process of splitting your data up before storage, so that specific chunks can be matched to a query later.

## More on chunking

- Don't feed the foundation model **more than it can handle**.
  - Smaller models limit how many tokens fit in the context.
  - Even below the limit, too much context can send a model off the rails, so sometimes less is more.
  - Most modern LLMs handle millions of tokens, so it is less of a hard barrier, but there is still a limit to what they process effectively.
- **Fixed, simple rules:** chunk by every sentence, every paragraph, or every N tokens.
- **Semantic chunking:** make each chunk hold **semantically independent** information, i.e. text that conveys the same thought stays together. Approaches:
  - **Embedding-based** (LlamaIndex, LangChain);
  - **Model-based** (BERT);
  - **LLM-based:** tell a large language model to do the chunking. You give it a big block of text that fits its context window, and it works out how to split it up. This is **costly and slow**, so avoid it unless you need it.

### Sample LLM chunking prompt

From the paper "Dense Retrieval: What Retrieval Granularity Should We Use?" (also used in LlamaIndex), the prompt asks the LLM to decompose the content into clear, simple **propositions** that can be interpreted out of context:

1. Split compound sentences into simple ones, keeping the original phrasing where possible.
2. Separate descriptive information attached to a named entity into its own proposition.
3. **Decontextualise** each proposition by adding the needed modifiers and replacing pronouns ("it", "he", "she", "they", "this", "that") with the full name of what they refer to.
4. Return the results as a **JSON list of strings**.

Bedrock's built-in chunking options, including its semantic and hierarchical modes, are in lecture 16 and covered further in lecture 19.
