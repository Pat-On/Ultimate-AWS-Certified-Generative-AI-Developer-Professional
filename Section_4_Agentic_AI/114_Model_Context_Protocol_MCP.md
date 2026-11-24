# 114. Model Context Protocol (MCP)

**MCP** is a standardized interface between agents and tools, created by Anthropic and now widely adopted. It lets an agent use external tools from third parties, or your own, through one consistent pattern.

## What it is

- Anthropic described it as a **USB-C port for AI applications**: a standard way to get context, information or capabilities from external systems and to extend agents.
- The AI application talks to the **MCP layer**, which fronts data, file systems, databases, development tools, productivity tools and more. Local or external, it all looks the same to MCP.
- Technically the **data layer is JSON-RPC 2.0**, and the **transport** is **standard I/O** for local servers or **HTTP streaming** for external ones. You are unlikely to need this for the exam.
- It standardizes **how apps provide context to LLMs**. Pretty much every agent SDK supports it, **including Strands**.

## What servers expose

- **Tools** that extend the system's capabilities.
- **Resources** that provide additional context.
- **Prompts**, for example on how to use them.

## Popular MCP servers

- **GitHub** (repositories and check-ins), **Atlassian** (Jira tickets), **PostgreSQL** (local or enterprise databases), **Slack**, **Google Maps**, and even **Udemy** (course information for a learning path).

## Deploying your own MCP server (called out in the exam guide)

- **Stateless, lightweight** access: **AWS Lambda**.
- **Complex tools** or where state matters: **Amazon ECS**, or **Fargate**.
- **AgentCore** can also deploy MCP servers.
- **API Gateway** can expose MCP endpoints.
- Use **MCP client libraries** to abstract away the protocol's complexity rather than reinventing it.

## AWS architecture guidance

- AWS's official MCP architecture guidance on its blog is more complex than what the exam guide and Skill Builder describe, but the core is the same: the **MCP server** runs on **ECS/Fargate** or **Lambda**.
- Around it are **Cognito** (authentication), **DynamoDB** (storing credentials), **CloudWatch**, **ECR** (containers), **WAF** (protecting the front end) and **CloudFront**.
- The exam focuses on the inner choice, **ECS or Lambda**, for a given problem.

## Exam takeaways

1. MCP is the standard protocol for connecting agents to external tools. Servers expose **tools, resources and prompts**.
2. **Lambda** for stateless, lightweight MCP servers. **ECS (or Fargate)** for more complex ones.
3. **API Gateway** and **AgentCore** are also ways to host or expose MCP servers, and **client libraries** are preferred over hand-written protocol code.
