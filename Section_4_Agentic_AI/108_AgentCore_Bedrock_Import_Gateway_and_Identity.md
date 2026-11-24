# 108. AgentCore Bedrock Import, Gateway, and Identity

Three more **AgentCore** capabilities: importing existing Bedrock agents, the **Gateway** for external tools, and **Identity** for the agent itself.

## Bedrock agent import

- Lets you take an **existing Bedrock agent**, build on it and deploy a more extensive system through AgentCore.
- Run the CLI command **`agentcore import-agent`** and specify the Bedrock agent.
- It converts the agent into **code** using the **Strands SDK**, or optionally **LangChain and LangGraph**, written to the output directory you choose.
- From there it is like any other AgentCore agent: develop on it, test it and deploy it.

## AgentCore Gateway

- Addresses using **external tools at scale**. Frameworks can already call tools, including external ones through **MCP**, but the Gateway does it in a more scalable way.
- It makes everything look like an **MCP tool**: external APIs, **Lambda functions** and other services. It tracks the **gateway endpoints** your agent code refers to.
- Targets can be anything exposing **OpenAPI** interfaces, **Smithy models** (an AWS format) or **Lambda functions**.
- It **manages authorization and credentials** centrally, keeping them secure in the cloud.
- It offers **semantic tool selection**, helping choose the right tool for the job and not only connecting to it.

## AgentCore Identity

- This is the identity of the **agent itself** when it connects to external services and tools. It is **not** how users log in to your agent, which you would handle with something like **Amazon Cognito**.
- Gives agents their own identities, treated somewhat like people, and lets them access **external tools and AWS services** securely.
- A **central repository of agent identities**, like a Cognito user pool but for agents.
- **Secure credential storage** for the external tools.
- **OAuth 2.0 support**, with built-in support for **Google, GitHub, Slack, Salesforce and Atlassian**.
- It is a deep topic that the exam is not expected to need in depth.

## Exam takeaways

1. **`agentcore import-agent`** converts a Bedrock agent into **Strands** (or LangChain/LangGraph) code that you can extend and deploy.
2. **Gateway** exposes APIs, Lambda functions and Smithy/OpenAPI targets as **MCP tools**, with central credentials and **semantic tool selection**.
3. **Identity** is for the **agent's** access to external services (OAuth 2.0, credential storage). **Cognito** is for **user** login.
