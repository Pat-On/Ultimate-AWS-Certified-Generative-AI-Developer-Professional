# 28. Bedrock Prompt Flows

A saved prompt (lecture 27) can be used inside a **Bedrock flow**. Flows used to be called **prompt flows**, and some documentation still says so, but the feature has been absorbed into the more general **Flows** feature.

## What a flow is

- A mechanism for **chaining prompts and models together**, and for other things too. It is a visual way to build larger applications with multiple prompts and tools, which edges into **agentic AI** (a later section), though it doesn't have to be complicated.
- A flow is **nodes and connections** between them. The simplest example: a **flow input** node connected to a **knowledge base** lookup node, connected to the **flow output**. The input is used for the lookup and the result goes to the output.
- **Connections can be conditional**, so you can branch: depending on the input, route to different paths to perform different tasks in the same system.
- Build flows **visually** with the **Flow Builder** in the console, which lets you make agentic applications **without writing code**, or define them in **JSON through the API** and build your own tooling around them.

## Flows with saved prompts

- Stored prompts (versioned, with variants) can be **flow components**.
- Example: the flow input supplies a `genre` and a `number`, a **prompt node** uses the saved music playlist prompt with those values to call a foundation model, and the model's completion goes to the flow output.
- The input **need not be raw text**: it can be **structured data**. Flow Builder recognises the prompt's variables and lets you pass each one in explicitly.
- Because inputs and outputs have structure, flows can **enforce pre- and post-processing** on them.

## A conditional flow

1. The flow input is raw text from a user.
2. A **saved prompt categorises** the input (for example "asking for documentation" or something else).
3. A **condition node** routes on that category:
   - **documentation:** go to a **knowledge base** node, look it up and return the answer;
   - **anything else:** go to a second, more general **saved prompt** that answers professionally, whose output is the final output.

This one flow uses one prompt to classify, a condition to route, and then either a knowledge base lookup or a plain foundation model call.
