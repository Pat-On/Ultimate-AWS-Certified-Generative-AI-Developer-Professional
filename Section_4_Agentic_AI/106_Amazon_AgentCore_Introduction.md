# 106. Amazon AgentCore Introduction

**Amazon Bedrock AgentCore** is AWS's latest way to build and deploy agentic AI, and the one it is steering developers toward as it deprecates the console-based Bedrock Agents. For a strictly **no-code** option, use **Amazon Quick** instead.

## Value proposition

- It solves the problems of **deploying agents at scale**: a fleet of inference endpoints, **memory at scale**, and **authentication with external systems**. A demo agent is easy, production is the hard part.
- **Fully serverless**: no Docker, **ECR** or **ECS** to manage.
- **Framework-agnostic**: it works with OpenAI Agents SDK, LangGraph, LangChain, Google ADK, CrewAI, Strands and more. It is a wrapper or toolkit around your own code, and does not even require agentic code.
- **Not tied to Bedrock Agents, Bedrock models or Strands**, although it has built-in support for **Bedrock Knowledge Bases** and other AWS features. **Strands** gets somewhat tighter integration.
- Integrates with **Bedrock Knowledge Bases**, so you don't rebuild vector stores or lookups.

## AgentCore CLI

- Packages existing agent code and deploys it at scale.
- Can also **create agents from scratch** (for example on Strands or another framework), and **add tools and capabilities with no code**. It generates a **harness** and the code for it.
- You can alternatively **bring your own code**, as shown in the lab.

## Capabilities

- **Agent**: your code, which orchestrates what the agent does, which tools it calls and which systems it talks to.
- **Identity**: authenticate users and control access to the agent, so it isn't open to everyone.
- **Built-in tools**: such as web search.
- **Memory**: built-in short-term and long-term memory, which can be added in one CLI line.
- **Gateway**: manages communication with external systems, through **MCP** or otherwise.
- **Runtime**: manages the interactions between user, agent and capabilities. It runs **locally for development** and deploys to the cloud.
- **Observability**: monitoring in real time via **CloudWatch**, underlying everything.
- **Evaluations**: newer, tracks how the agent is doing and visualizes it in CloudWatch.
- **Policies**: work with Gateways for **fine-grained control** over which external systems can be used.
- A **micropayment** system for charging for access, and **Insights** (preview/beta), which guides on what is going right or wrong.

## AgentCore Runtime

- Provides **serverless endpoints** and deploys your agent to them automatically, enhanced with the AgentCore capabilities.
- Deployment goes through **ECR**. Via the CLI, **CodeBuild** builds and pushes the container for you.
- You can instead **build your own Docker container** for more control.
- You can have **multiple endpoints** and scale as far as you will pay for.
- The observability dashboard tracks **usage and performance** over time. You must tick a **GenAI observability** checkbox in CloudWatch to enable it.

## Exam takeaways

1. AgentCore is the **replacement for Bedrock Agents Classic**, for developers. **Amazon Quick** is the no-code route.
2. It is **serverless, framework-agnostic and model-agnostic**.
3. Core building blocks: **Runtime, Identity, Memory, Gateway, built-in tools, Observability**, plus **Evaluations** and **Policies**.
4. Runtime deploys through **ECR** and can run locally for development.
5. Enable **GenAI observability** in CloudWatch to see the dashboard.
