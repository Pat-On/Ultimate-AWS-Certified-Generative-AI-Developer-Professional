# 103. Short and Long-Term Agent Memory

Agents have **short-term** and **long-term memory**, much like the human mind.

## Short-term memory

- Refers to the **current session or conversation**. It is what makes a conversation possible, for example referring back with "do that again".
- It keeps the **conversation history**, which becomes part of one big prompt that includes the prior context.
- It can also hold **events within the session**, such as tools called or files uploaded.
- It can simply live **in memory**, or in a distributed cache such as **ElastiCache** or **MemoryDB**, or in **DynamoDB**.

## Long-term memory

- Persists **across sessions**, for example picking a conversation back up a year later.
- Beyond storing conversations verbatim, you can store **summaries of past conversations**.
- It can hold **learned facts about the user**, such as coding style, favorite tools, interests and job, which are folded into future responses.
- It can hold **explicit facts** the user asks it to remember.
- Conceptually it is a **unified memory record**, but different memory types (user preferences, semantic facts, session summaries) can use **different strategies**.

## Where to store it

- **DynamoDB**, which suits both short and long-term storage.
- **SQLite**, the default in OpenAI's SDK, for small to medium solutions.
- **RDS or Aurora**.
- **Amazon AgentCore Memory**, a highly scalable managed feature you attach to your agents, so you don't reinvent it.
- **Mem0**, which the **Strands SDK** integrates with.
- **Knowledge bases** are arguably long-term memory, but of **contextual information from outside the system**, not the user's past interactions with the agent.

## Exam takeaways

1. **Short-term** = the current session's history. **Long-term** = insights from past interactions, kept across sessions.
2. **DynamoDB** fits both. **AgentCore Memory** and **Mem0** are the ready-made options.
3. A **knowledge base** holds external context, not past user interactions.
