# 104. Strands Agents

**Strands Agents** is Amazon's open-source Python SDK for building specialized agents and multi-agent systems. It is the agent SDK the exam focuses on.

## Overview

- Alternatives include OpenAI's Agents SDK, CrewAI, LangGraph and Google's ADK. Strands was released by Amazon but is open source and competitive with them.
- Implements the **multi-agent patterns** from lecture 102 in Python, for **complex task decomposition** and **collaborative problem solving**.
- **Tight AWS integration**: calls **Bedrock foundation models** directly and integrates with **Lambda**, **Step Functions** and more.
- **Not tied to AWS**: it also works with OpenAI and other models.
- **Multimodal**: text, speech, images and video.
- Supports the **Model Context Protocol (MCP)**, so agents can use external MCP servers for extra context or capabilities.

## Built-in tools

- **Boto3** client SDK, so an agent can do anything in AWS.
- **Bedrock knowledge bases** for RAG and data lookup.
- **Mem0** agent for **short and long-term memory** and personalization.
- Run **arbitrary Python code**.
- Call anything on the web over **HTTP** (REST or other).
- Run **shell commands** and manipulate **files** on your own computer.
- Coordinate **swarms of agents**.
- Speak output with **Amazon Polly**.
- **Custom tools**: any Python function you write.

## The Strands agent loop

1. Input plus relevant context (from a knowledge base or the prompt) enters the loop.
2. The model **selects the best-fit tool**.
3. The tool is **executed** and its result goes back to the foundation model.
4. The model decides whether it is **done** or needs more tools. If not, it loops to pick and run another tool.
5. When done, it outputs the **final response**.

## Code example (not tested on the exam)

- A custom tool is a **Python function wrapped with the `@tool` decorator**. The example counts the letters in a word, which LLMs do badly because they work on **tokens**, not characters.
- An `Agent` object is created with a **list of tools**: the custom letter counter plus built-ins such as the **calculator**, **current time** and **Python execution** tools.
- Calling the agent with a message makes it loop through the tools it needs (time, calculator, letter counter, generated Python code) before returning the final answer.

## Exam takeaways

1. Strands is **open source, Python, with tight AWS integration** (Bedrock, Lambda, Step Functions) but **not AWS-only**.
2. It supports **MCP**, **multimodal** input and **multi-agent** swarms.
3. The **agent loop** repeats select tool, execute, evaluate until the model is done.
4. Custom tools are plain Python functions with the **`@tool` decorator**.
