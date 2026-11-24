# 107. AgentCore Memory and Tools

Beyond the Runtime, **AgentCore** offers a managed **memory system** and **built-in tools**. It is likely to play a larger role in the exam over time.

## Short-term memory

- The **chat history within the current session**, which makes conversation possible ("do that thing again").
- The API is built around **session objects** and the **events** within a session.

## Long-term memory

- More than reloading and resuming past sessions. It stores **extracted insights**.
- **Session summaries** instead of verbatim conversations, which saves **storage** and **tokens** when reused in a new conversation.
- **User preferences** learned over time, such as coding style and favorite tools.
- **Facts** the user explicitly asks it to remember.
- The API uses **memory records**: structured information derived from agent interactions, organised by **strategies**.
- Built-in strategies: **user preferences**, **semantic facts** and **session summaries**.

## Why use AgentCore Memory

- Building memory from scratch is painful, and AgentCore provides it out of the box.
- **Easy integration with the Strands SDK**.
- Other SDKs' memory implementations, such as the OpenAI Agents SDK's **SQLite**, don't scale well. AgentCore Memory is **serverless and scales**, which is its focus: production, not toy applications.

## Built-in tools

- **Browser tool**: lets the agent take control of a browser and interact with the web.
- **Code interpreter tool**: runs code in a **safe, isolated container**, in **Python, JavaScript or TypeScript**.
- These may duplicate tools in the framework you wrap. Choose between them yourself. AgentCore's focus is scale.

## Exam takeaways

1. **Short-term** = session history (sessions and events). **Long-term** = memory records with strategies for **user preferences, semantic facts and session summaries**.
2. AgentCore Memory is **serverless and scalable**, and integrates easily with **Strands**.
3. Built-in tools are **Browser** and **Code Interpreter** (Python, JavaScript, TypeScript, isolated container).
