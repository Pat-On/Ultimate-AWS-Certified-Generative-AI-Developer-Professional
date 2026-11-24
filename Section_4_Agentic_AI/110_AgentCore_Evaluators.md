# 110. AgentCore Evaluators

**AgentCore Evaluations** assess how well your agent **performs tasks, handles edge cases and stays consistent**. They integrate with **Strands, LangGraph, OpenTelemetry and OpenInference**, and visualize results in **CloudWatch**.

## Cross-region inference

- Evaluations **always use cross-region inference** and **it cannot be turned off**. AWS picks the optimal region to process them.
- Data **stays resident** in the region where the request originated, but may be **transmitted and processed in other regions**, **encrypted** in transit.
- This may be unacceptable under some regulations.

## CloudWatch visualization

- Results are broken down by each configured metric. Evaluations can apply at the **session**, **trace** or **span (tool call)** level.
- The example dashboard tracks five: **faithfulness, helpfulness, correctness, harmfulness and stereotyping**. The last two are **safety** metrics.
- As it is CloudWatch, you can put **alarms and alerts** on them. View them under **GenAI Observability > Bedrock AgentCore** (the AgentCore Observability Insights).

## Built-in evaluators

Provided as **prompt templates**, so you can extend or modify them.

- **Correctness**: factually correct, compared with a known ground truth.
- **Helpfulness**: from the user's standpoint.
- **Conciseness**: the needed information in as few words as possible.
- **Instruction following**: how well the agent's instructions were followed.
- **Faithfulness**: whether the response is supported by the context or sources.
- **Response relevance**: relevance to the user's query.
- **Coherence**: logical structure.
- **Refusal**: whether it is evasive or refuses things it should do.
- **Goal success rate**: whether a defined goal is reached, such as code that runs.
- **Tool selection and tool parameter accuracy**: the right tool and the right parameters.
- **Harmfulness** and **stereotyping**.

In the console they are grouped as **response quality**, **task completion** (goal success rate), **component level** (tool selection and parameter accuracy) and **safety** (harmfulness, stereotyping) metrics.

## Controlling cost

- Each evaluation uses **another LLM** to judge the output, so tokens add up.
- Limit them with **filters** (only certain calls, matching a property condition) and a **sampling rate**, for example 5%. The console allows **0.01% to 100%**.

## Custom evaluators

- Choose a **model to act as judge** and configure it. It is better practice to use a **different model from the agent's**, for a second opinion.
- Define the evaluator with a **plain-text prompt**. The prompt always ends with **conversation history** and **assistant response** placeholders, which give the judge the full context.
- Start from scratch or **load a built-in template** (for example faithfulness) and modify it.
- Set standard model parameters: **temperature, top P, maximum output tokens, stop sequences**.
- Define **scales** that map result ranges to labels. A binary scale maps 0 to "no" and 1 to "yes". Faithfulness is a range, such as 0-25% "not at all" and 25-50% "not generally".
- Choose the **level**: **session**, **trace** or **tool call**. Tool-parameter appropriateness belongs at the tool-call level.

## Console tour

1. In the AgentCore console, go to **Assess > Evaluations**. A warning notes the cross-region inference.
2. **Create an evaluation configuration**: name, optional **enable immediately**, description and a **timeout** (five minutes is conservative, since a longer evaluation uses more resources than you want).
3. Choose the **data source**: an **agent endpoint** (the usual choice) or **CloudWatch log groups**. The log-group option works **outside AgentCore**, for agents that log to CloudWatch from elsewhere.
4. Pick the **built-in and custom evaluators** to run.
5. Optionally add **filters** and a **sampling rate**.
6. Give it **IAM permissions**. **Create and use a new service role** usually does the right thing.
7. Create the configuration. Results appear in **AgentCore Observability** in CloudWatch.

## Exam takeaways

1. Evaluations use an **LLM as judge**, with built-in prompt-template evaluators and **custom evaluators**, applied at **session, trace or tool-call level**.
2. They always use **cross-region inference**, which cannot be disabled, so check **data residency** rules.
3. Control cost with **filters** and a **sampling rate**, and prefer a **different judge model** from the agent's.
4. Results go to **CloudWatch**, with the usual **alarms**.
