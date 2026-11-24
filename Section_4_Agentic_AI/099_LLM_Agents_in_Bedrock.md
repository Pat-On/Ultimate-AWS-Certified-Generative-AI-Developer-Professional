# 99. LLM Agents in Bedrock

How **LLM agents** (Agentic AI) work in **Amazon Bedrock**: an agent gives **tools** to a foundation model, which decides which tools to use and for what purpose.

## What an agent is

- An agent **extends a foundation model** with the ability to reach outside data and services and fold the results into its response.
- Conceptually (as Nvidia describes it) an agent has a **core** built on a foundation model, a **planning module**, **tools** and **memory**.
  - Source: https://developer.nvidia.com/blog/introduction-to-llm-agents
- **Planning module**: guidance given to the LLM on how to break a request into sub-questions and approach it step by step.
- **Memory**: in practice the **chat history** plus **external data stores**.
- The model learns when and how to use each tool, and how to pass parameters, only from **plain-English descriptions**. This differs from traditional development, with its tightly defined APIs and hard-coded rules for when to call them.

## Tools in practice

- Tools are just **functions** provided to the framework's API. In Bedrock a tool can be a **Lambda function** (Python, JavaScript or any Lambda language) that accepts the agent's parameters and returns a response in the format the agent expects.
- Tools can reach outside information, **knowledge bases or retrievers**, other modules and services.

## Action groups

In Bedrock, an **action group** defines a tool.

- The action group holds a **prompt that tells the foundation model when to use it**, for example "use this function to determine the current weather in a city". It typically contains a **Lambda function** that does the work.
- You define the **parameters** the Lambda function expects. For each one give a **name, description, type** (string, integer and so on) and whether it is **required**.
- The **parameter description is important**. The FM uses it to extract the value from the user's prompt and format it correctly.
- You can let the agent **ask the user for required information that is missing**, such as the city in a weather query.
- Parameters can be defined with **JSON / OpenAPI-style schemas** or visually in a **table in the Bedrock console**.

## Knowledge bases, agentic RAG and code interpreter

- You can attach **one or more knowledge bases** to an agent. They query vector stores for semantic search.
- A plain-English instruction tells the agent when to use each, for example "use this for questions about self-employment".
- RAG used inside an agent is sometimes called **agentic RAG**. It is just **another tool** in the agent's toolbox.
- The optional **code interpreter** lets the agent **write its own code** (Python) to answer questions, do calculations or **produce charts**.

## Deploying an agent

- Before production, create an **alias**. It is an endpoint, a **deployed snapshot** (versioned) of the agent.
- **On-Demand throughput (ODT)**: the agent runs at **quotas set at the account level**. Use it for reasonable traffic.
- **Provisioned throughput (PT)**: you **purchase a higher rate and number of tokens**. Use it for very high traffic and large queries.
- Applications call **InvokeAgent** with the **alias ID** against the **Agents for Amazon Bedrock Runtime endpoint** (the `bedrock-agent-runtime` API).
- Bedrock Agents is now **Bedrock Agents Classic**, being replaced by **AgentCore**.

## Example agent in the next lecture

- A foundation model.
- A **knowledge base** built around a self-employment book, created earlier in the course.
- A **weather action group** backed by Lambda, hard-coded to return 75 degrees and sunny.
- The **guardrail** created earlier.

## Exam takeaways

1. In Bedrock, **tools = action groups**, usually backed by **Lambda** functions.
2. **Plain-English descriptions** of the action group and of each parameter drive tool choice and parameter extraction.
3. A **knowledge base is just another tool**, which is agentic RAG. The **code interpreter** lets the agent write code and charts.
4. Create an **alias** to deploy. Choose **ODT** for normal traffic and **PT** for high traffic.
5. Applications call **InvokeAgent** with the alias ID on the **Agents for Amazon Bedrock Runtime endpoint**.
