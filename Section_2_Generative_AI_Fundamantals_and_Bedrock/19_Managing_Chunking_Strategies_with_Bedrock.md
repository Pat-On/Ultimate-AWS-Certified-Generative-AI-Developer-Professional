# 19. Managing Chunking Strategies with Bedrock

Bedrock knowledge bases offer four ways to control how documents are split into chunks, and so the granularity of what is stored (the theory is in lecture 18, the console walk-through in lecture 16). Tokens are what LLMs encode words into. One token is not always one word, but you can think of them that way here.

## Standard chunking

Simple, heuristic splitting.

- **Fixed size:** you set the **tokens per chunk** and an **overlap percentage**.
  - Overlap repeats a little text from the neighbouring chunks, so context at the boundaries isn't lost.
  - Example: "Space, the final frontier. These are the voyages of the starship Enterprise." with a chunk size of 5 and 20% overlap (one token) gives "Space the final frontier These", then "These are the voyages of", then "of the starship Enterprise". Real chunk sizes would be much larger, because snippets this small carry no meaning on their own.
- **Default:** **300 tokens per chunk, honouring sentence boundaries.** A chunk may run a little over 300 tokens to keep a complete sentence, since a sentence is a coherent thought and shouldn't be cut. This is a good starting point: it captures fairly complex ideas without getting too big.
- **No chunking:** **each document is its own chunk**. Use it when you have already split your data into individual documents yourself, which gives you full control in pre-processing.

## Hierarchical chunking

- **Nested parent and child chunks:** larger parent chunks split into smaller child chunks.
- The **initial search hits the child chunks**, which gives precision, because small embeddings match very specific text.
- Bedrock then **goes up to the parent** for more surrounding context, which wins back the comprehensiveness that small chunks give up.
- Slide example (1 token = 1 word for simplicity): **parent size 6, child size 3, overlap 1**. The child chunks are "Space the final", "final frontier These", and so on. A hit on a child returns its size-6 parent.

## Semantic chunking

- Uses a **foundation model** to split the text by **meaning** (keeping an idea together), instead of by fixed size or sentence count. If a passage is all one idea and fits within your maximum, it is kept whole.
- You specify three things:
  - **Maximum tokens per chunk**, while still honouring sentence boundaries.
  - **Buffer size:** how many surrounding sentences are considered for each sentence when computing embeddings. A buffer of 1 means each sentence is judged with the one before and the one after, three sentences in all.
    - **Too large** a buffer introduces noise (irrelevant information pulled in).
    - **Too small** a buffer misses important context, though results can be more precise.
    - The instructor thinks this trade-off is the kind of thing the exam might test.
  - **Breakpoint percentile threshold:** how semantically different text must be before it is split. A **higher threshold gives more distinguishable chunks, but fewer and larger ones**.
- It **costs money**: you pay for the underlying foundation model, which can add up on large amounts of data, so use it deliberately.

## Choosing

| Strategy | Strength | Cost or catch |
| --- | --- | --- |
| Fixed size (default 300 tokens) | Simple, predictable | Can split an idea across chunks |
| No chunking | Full control; you pre-chunk | Your own pre-processing work |
| Hierarchical | Precise match, plus wider context from the parent | More structure to tune |
| Semantic | Chunks follow meaning | Foundation model charges; buffer and threshold to tune |
