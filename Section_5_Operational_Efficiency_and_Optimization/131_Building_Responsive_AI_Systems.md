# 131. Building Responsive AI Systems

Responsiveness is how fast the system **feels** to the end user. Many techniques from earlier lectures apply.

## Ways to speed up the response

- **Parallel requests** for complex workflows: the **orchestrator and synthesizer** multi-agent pattern splits a prompt into parts, runs specialized workers at the same time and combines their outputs. Any agent SDK can do this, and **Step Functions** can too.
- **Caching and pre-computing** predictable queries (semantic or prompt caching).
- **Streaming**: start returning the response as it is generated, so users can read while it is still being produced.
- **Latency-optimized inference** for foundation models (a Bedrock feature): add `performanceConfig={'latency': 'optimized'}` to the API call (for example the Converse API). It optimizes **time to first token (TTFT)**, **output tokens per second (OTPS)** and **end-to-end latency (E2E)**, which is what the user actually sees.
- **Intelligent Prompt Routing**: simple prompts go to smaller, faster models, so it helps responsiveness as well as cost.

## Prompt and context hygiene

- Keep prompts **concise**: less to process and a better, faster answer.
- Put the **important content first**, in case a prompt is truncated.
- **Context pruning**: drop RAG results that are not valuable or are redundant.
- **Limit response size**: set `maxTokens`, state a length in the prompt, or force a JSON format.
- **Break complex tasks into steps** and show each step's result as it finishes.

## Exam takeaways

1. Run independent work in **parallel** (orchestrator, workers, synthesizer, or Step Functions).
2. **Stream** responses, **cache** repeated queries and use **latency-optimized inference** (`performanceConfig` latency optimized).
3. Latency-optimized inference targets **TTFT, OTPS and end-to-end latency**.
4. **Intelligent Prompt Routing** improves both cost and responsiveness.
5. Concise prompts, pruned context and limited response sizes all make responses faster.
