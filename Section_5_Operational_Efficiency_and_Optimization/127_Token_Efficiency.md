# 127. Token Efficiency

Models charge **per token**, so controlling the tokens going in and out of a foundation model is the first way to control cost. Measure first, then optimize.

## Measuring tokens

- **Count Tokens API** (Bedrock): returns the token count for a prompt **without running it**, and it **costs nothing**. Use it to compare how efficiently different models tokenize, to estimate cost before inference, and to fit a prompt into a token limit or a smaller model's window.
- **CloudWatch** logs `InputTokenCount` and `OutputTokenCount`, so you can see which prompts and approaches give the lowest count and so the lowest cost.
- CloudWatch also tracks the **count and time of requests**, **time to first token** (TTFT, how soon a streamed response starts, vital for responsiveness), **throttles**, and **server and client errors**. At model level it tracks latency, invocation count and throttling.

## Techniques

| Technique | What to do |
| --- | --- |
| **Context window optimization / context pruning** | Most tokens often come from the **context added to the prompt** (RAG chunks), not the prompt itself. Balance chunk size against relevance, **limit the number of chunks** (do you need the top 10, or do the top 2 or 5 do?), and **filter chunks by metadata** or keywords (hybrid search) to drop irrelevant ones. |
| **Conversation history** | Past turns are re-sent as short-term memory and eat tokens. **Summarize older parts** of a long chat, or **cut off** beyond a window size, if cost matters more than perfect recall. |
| **Response size controls** | Set **`maxTokens`**. Or write it into the prompt ("respond in 50 words or less"), which costs input tokens but usually wins overall. Give **examples** of the verbosity you want. Use **structured (JSON) output** to force a format and length. |
| **Prompt compression** | Have a **smaller model summarize** big chats or documents before the big model sees them. The small model's cost must be lower than the saving, and it **adds latency**. |
| **Knowledge Bases instead of whole documents** | Retrieve only the relevant chunks of a document from an external store instead of stuffing the whole document into the prompt. |

## Exam takeaways

1. The **Count Tokens API** gives a free token count without running the prompt, so it is the tool for estimating cost and fitting limits.
2. CloudWatch tracks input and output token counts and **time to first token**.
3. The biggest token source in RAG is usually the **retrieved context**: retrieve fewer and better chunks, and filter by metadata.
4. Shrink long conversations by **summarizing** older turns or applying a **context window**.
5. Limit output with `maxTokens`, prompt instructions, examples and JSON output.
6. **Prompt compression** with a small model trades lower token cost for added latency.
