# 113. Lab: Amazon Bedrock AgentCore Harnesses

Using **AgentCore** with **no command line and no code**, entirely from the AWS console, by building a **harness**.

## What a harness is

- A harness is AgentCore's way of making agentic AI applications **without writing code**.
- You tie it to existing building blocks written by someone else: **MCP servers**, **skills**, built-in tools and gateways.

## Steps

1. In the AgentCore console, go to **Build > Harness** and **create a harness** with **quick create**. Name it, for example `Bedrock Expert Agent`. It is ready in under a minute and comes with a **default endpoint**. You then configure it in the **harness playground**, and can watch it with **observability** once deployed.
2. **Choose the model**. Providers include **Bedrock**, a model hosted on **Bedrock Mantle**, **LiteLLM**, **OpenAI** and **Gemini** directly. With Bedrock, pick a model that your account can access **and that supports reasoning**. The lab used **Claude Sonnet 4.6** (Opus is too expensive). Access to Anthropic models on Bedrock is often limited, so you may need an alternative reasoning model that is still supported.
3. Write the **system prompt**. The lab made it a helpful assistant that always talks like a chicken.
4. Optionally add **tools**:
   - The built-in **browser** and **code interpreter** tools.
   - An **AgentCore Gateway**, if you have one.
   - **Remote MCP servers**, which is what most people will use: enter the server's endpoint URL and the agent gains whatever capabilities it exposes.
5. Add a **skill**. Choose an AWS-provided skill from GitHub, or give a link to your own through **Git or S3**. The lab used the Amazon Bedrock skill, with the path `core-skills/Amazon-Bedrock`. The console UI is unclear on the path format, and you can enable one specific skill instead of all of them.
6. **Apply**, then **test in the playground**. The prompt "Tell me what data sources can connect to Bedrock knowledge bases" got a correct answer, in chicken style, listing Salesforce, Confluent, SharePoint, web crawlers, S3 and custom data sources. The **trace** shows the model chose to consult the Amazon Bedrock skill.
7. **Delete the harness** when done: **Build > Harness**, select it and delete. This cleanly removes its resources. Deletion takes a few minutes.

## What is a skill

- A **skill** is a large **`SKILL.md` markdown file** with guidance for the model on how to answer certain kinds of questions.
- It holds background information, **links to further reference pages** (such as the knowledge base setup page for a RAG question), **rules and constraints** on how to respond, and **few-shot examples**.
- The model decides **which skill to use** for a prompt.

## Exam takeaways

1. A **harness** is the **no-code** way to build an AgentCore agent, configured with a **model, system prompt, tools (browser, code interpreter, Gateway, remote MCP servers) and skills**.
2. A **skill** is a markdown guidance file (`SKILL.md`) loaded from AWS, Git or S3.
3. The model must support **reasoning** and be accessible to your account.
4. It costs money, so **delete the harness** afterwards.
