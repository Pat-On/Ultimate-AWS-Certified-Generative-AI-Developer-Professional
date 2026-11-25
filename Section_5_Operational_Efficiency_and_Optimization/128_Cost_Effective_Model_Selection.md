# 128. Cost-Effective Model Selection

Besides token counts, the **model you choose** is the other big cost lever: newer, larger models cost more per token than older, simpler ones.

## Cost and capability trade-off

- Ask whether you really need the largest, most expensive model. In many applications the "smarts" are in the **retrieved data** (RAG, knowledge bases) or in the **tools**, so a **smaller model** may do fine and PhD-level reasoning is not needed.
- **Pre-processing** (summarization, compression, classification, chunking) does not need the latest, most expensive model.

## Dynamic routing

When you cannot know up front how complex a prompt is, **inspect the prompt and route it to a model of matching complexity**. This is how large chat products keep costs down.

- **Amazon Bedrock Intelligent Prompt Routing**: a built-in feature you turn on. It analyzes the prompt, estimates its complexity and routes it to a suitable foundation model.
- Without it, you can build routing yourself:
  - **Bedrock Flows**: a prompt classifier followed by a **conditional** node that sends the prompt to one model or another.
  - A **Lambda function** that intercepts the prompt and applies routing logic.
  - **AWS Agent Squad**, which is built for routing based on prompts.
  - **Strands Agents SDK**: an agent with a **tool that scores prompt complexity**, then routes to a downstream agent or model.

## Measuring price to performance

- Every change has a performance cost, so measure the **price-to-performance ratio**.
- **Amazon Bedrock Evaluations** measures foundation model performance against your prompt dataset, using **human judges**, **LLM judges** (one model judging another, or your whole system) or **predefined metrics**. Its **compare** feature visualizes different models on your prompts.
- Pair the results with **token counting** (tokens per prompt times the model's token price) to estimate the cost of each prompt and system, then weigh cost against measured quality.

## Exam takeaways

1. Use a **smaller or cheaper model** where the intelligence lives in retrieval or tools, and for pre-processing tasks.
2. **Intelligent Prompt Routing** is the built-in Bedrock way to route by prompt complexity. Flows conditionals, Lambda, Agent Squad and Strands are the DIY ways.
3. **Bedrock Evaluations** (human, LLM or metric-based, with a compare view) plus token counts gives the price-to-performance picture.
