# 105. Agent Squad

**AWS Agent Squad** is another open-source agentic SDK that originated at Amazon. It is a **router** for **orchestration and intelligent intent classification**.

## Status

- The instructor is unsure of its future, as it had not been updated for about five months at recording time.
- It is **called out in the exam guide**, so you should know it.

## How it works

1. A **classifier** takes the prompt and picks the **best-fit agent** from a squad of agents.
2. That agent runs and its **response is returned**.
3. The agent's conversation is saved to a **conversation history**, which feeds the classifier on future inputs. This gives it a **memory component**.

- Fundamentally it only picks the right agent and outputs that one agent's output. It is a **narrow use case** compared with Strands or Bedrock Flows, which can do the same routing.

## Features

- **Python and TypeScript** APIs. TypeScript is the primary API in the examples.
- **Shared context** across agents, as the conversation history is used in classification and passed to the agents.
- Many **prebuilt agents and classifiers**.
- **Tight Bedrock Agents integration**: refer to an existing Bedrock agent by its ID and call it with minimal code.
- Can **extend Bedrock Flows** with **conversation memory and more complex orchestration**, which Flows lacks on its own. This is its main value proposition.
- A recently added **supervisor agent** coordinates multiple specialized agents in more complex ways, bringing it closer to Strands.

## Agent Squad vs Strands

- **Agent Squad** focuses on the **routing problem**.
- **Strands** focuses on **tool use within a single agent loop**.

## Exam takeaways

1. A **routing problem** (choose the best agent for a prompt) points to **Agent Squad**.
2. **Tool use inside an agent loop** points to **Strands**.
3. Agent Squad works with **Bedrock Agents** and extends **Bedrock Flows** with memory and orchestration.
