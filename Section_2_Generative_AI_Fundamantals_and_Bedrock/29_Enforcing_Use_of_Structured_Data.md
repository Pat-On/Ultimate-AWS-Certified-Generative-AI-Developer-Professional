# 29. Enforcing Use of Structured Data

Sometimes you don't want raw text back but **structured data**, usually **JSON**, that you can operate on further. There are two main ways to get it.

## 1. Ask for it in the prompt

- Just say you need structured output. Today's models usually comply, although it takes "a little leap of faith" that they follow English instructions.
- **Be specific.** Specific, **numbered instructions** make the model more likely to follow them precisely.
- **Give an example** of the output you want.
- **Attach a JSON schema** to the prompt as a reference.
- **Say what to do on failure:** for example return missing fields as `null`, or return an error response if the task can't be done.
- Example from the lecture: a prompt to analyse customer reviews, with the data inside specific tags, instructions to return JSON matching the provided schema, an example of a valid response (a sentiment and a summary), `null` for missing fields, and an error response when it doesn't work.

## 2. Use tool calling

- Modern models connect to **external tools** (agentic AI: external APIs, MCP servers, custom functions), and calling a tool needs **structured data** passed to it.
- With **tool use in the Bedrock Converse API** you can specify an external tool that expects a given **schema**, and the model fills in that structured data. The "tool" doesn't have to do anything real: it can simply output the data somewhere you can collect it, and that is still a tool.
- **In practice it works neither better nor worse** than putting the schema in the prompt, because under the hood it may be doing that anyway. With older, smaller models it made a difference, but with modern models there is no measurable difference.
- If you are already building an agentic system with tools, use tool calling. If you only need structured data back, either approach is fine.

## For the exam

- You can get **structured JSON output from a prompt**.
- Giving the model a specific schema that the response must follow may be called a **response format template**.
