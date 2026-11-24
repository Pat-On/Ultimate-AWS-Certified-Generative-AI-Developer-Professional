# 102. Multi-Agent Workflows

Combining several specialized agents instead of one **single-agent system** (one foundation model with a set of tools, sometimes called an **augmented LLM**).

## Multi-agent systems

- Like giving tools to one agent, but **many agents (tools) may be used at once**.
- Agents are **specialized** for different tasks and can run **independently, in sequence or in parallel**.
- Each agent is **self-contained** with its own tools and **memory**, so its context and token space is not polluted by what other agents are doing.
- Examples: coding agents (code review, optimization, re-architecture) working on the same code base, or workflows that need **complex decision making**.
- **Keep it simple**: for a simple use case, use a deterministic workflow or single agent rather than a multi-agent system. Multi-agent systems are more powerful but also **more expensive**.

## Why use multiple agents

- **Too many tools**: one model with a huge toolset struggles to pick the right tool and to focus, because of limited context. Specialists with focused toolsets work better.
- **Complex logic**: if prompts fill up with conditional statements, define the flow with specialized agents instead.

## Patterns

The instructor does not expect the exam to test these patterns, but they help explain agentic AI.

### Orchestrator and workers (manager)

- An **orchestrator** agent only breaks the task into pieces and **delegates to worker agents**. Each worker has its own tools, and workers can run **in parallel**.
- A **synthesizer** combines the results into the final response.
- Example: translating text into many languages at once, with one worker per language and a synthesizer that waits for all of them.

### Routing

- A **router** LLM chooses **one** of many specialized agents and the output returns that agent's response. It suits tasks needing a **single classification**.
- The router matches the prompt against **descriptions** of each agent.
- Examples: choosing **model size by prompt complexity** (a small cheap model for simple prompts and a large one for deep reasoning, which saves cost over time), and classifying **customer service queries** (balance, cancellation, deeper support).
- **Agent Squad** (covered later) does exactly this. **Amazon Bedrock Flows** and **Strands Agents** can too.

### Parallelization

- Like the orchestrator pattern but **without complex orchestration**, because you know up front what to run. Input goes straight to workers and an **aggregator** collects the results.
- **Sectioning**: independent subtasks in parallel, such as running **multiple guardrails** or **multiple evaluations** at once. The aggregator collects the metrics.
- **Voting**: the same task done with **different models or prompts**, and the aggregator tallies the votes to pick the winner. It gives diversity of thought.

### Prompt chaining

- For a **discrete sequence of known steps**. Each LLM processes the **output of the previous one**. It was originally what **Amazon Bedrock Flows** was about.
- You can add **gates** to check the chain is on track and **exit early**, saving the cost of later steps.
- Examples: write a document then translate it, or write an outline then make slides.

### Evaluator-optimizer

- One agent (**generator**) produces a response and another (**evaluator**) assesses it and sends **feedback**. The loop **repeats until quality is good enough**.
- Examples: a code reviewer feeding back on generated code (such as security holes), and complex search with multiple rounds of drilling in.

## Exam takeaways

1. Use multi-agent systems only for **complex problems**. Otherwise keep it simple.
2. The main reasons are **too many tools** and **overly complex prompt logic**.
3. Patterns: **orchestrator-workers-synthesizer, routing, parallelization (sectioning and voting), prompt chaining with gates, evaluator-optimizer**.
4. **Routing** is what Agent Squad does, and routing by prompt complexity saves cost.
