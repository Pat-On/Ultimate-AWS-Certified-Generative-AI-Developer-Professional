# 21. Evaluating RAG Performance

You can't improve a RAG system you can't measure. Bedrock includes **RAG evaluation jobs** that measure how well a knowledge base or agent built on retrieval is doing.

## The RAG triad

A query comes in, context is retrieved from the knowledge base, and a response is generated from the query plus that context. There is something to measure along each edge:

- **Context relevance:** how relevant the retrieved context is to the original query (retrieval).
- **Groundedness:** how well the response is grounded in the retrieved context (response versus context). Bedrock also calls this **faithfulness**.
- **Answer relevance:** how relevant the produced answer is to the original query.

## What Bedrock can measure

Bedrock uses more subjective measures than the mathematical ones (which the instructor covers in his larger AI engineering course):

- **Correctness:** accuracy in answering the question.
- **Completeness:** how complete the answer is.
- **Helpfulness.**
- **Logical coherence.**
- **Faithfulness:** how well the response aligns with the retrieved text.
- **Citation precision and coverage:** how precise the citations are and how much of the retrieved material they cover.
- **Harmfulness**, and **stereotyping**, including hidden biases in the retrieved context.
- **Refusal:** whether the system is evasive when asked something it doesn't know.

## Providing ground truth

Much of this sounds subjective, so you supply your own idea of what good looks like:

- A **prompt dataset in JSON** with sample **prompts** and **reference responses**, the ideal answers you expect.
- Optionally **reference contexts**, the ideal passages you expect to be retrieved from the knowledge base. You need these if you want to measure retrieval against ground truth.

## LLM as a judge

- Bedrock uses **another foundation model as the judge** (for example Llama, Claude, Nova or Mistral). It gets the prompt, the system's output and your references, and decides how well they match.
- The **specific metrics are defined inside prompts** to the judge model, and different models score in different ways. You can use **several judge models** and see whether they agree.
- The details are documented, and **the specifics aren't important for the exam**.
- **Example (don't memorise it):** the documented **context relevance** prompt for **Nova Pro** gives the judge a question and a passage, and asks it to rate whether the passage contains the information needed to answer the question as **No, Maybe or Yes**, with an explanation first and then the answer in a fixed format (`Explanation: ..., Answer: ...`).
- It is still subjective to some extent, but it gives you a metric to track and try to improve.
