# 120. How Amazon Quick Works: Chat and Agents

**Amazon Quick** is an AI assistant for work that combines chat, research, BI, automation and no-code apps in one place, and every request flows through the same **five layers**.

## What Quick is

- Evolved from **QuickSight**, which continues as **Quick Sight** inside Quick. Existing APIs and integrations keep working.
- **Fully managed**: no infrastructure, no models to host, no ML expertise.
- **Grounded** in your systems through knowledge bases, connectors and structured data.
- **Open standards**: **MCP** and **OpenAPI** connect anything.
- Used from the web, the desktop app, or embedded in **Chrome, Slack, Teams and Microsoft 365**.

## The five layers

1. **Chat**: the front door for every request, where you type natural-language queries.
2. **Agents**: instructions, knowledge and tools. Needed when you want more than a text answer, such as using your own data or doing things.
3. **Spaces**: files, dashboards, datasets and actions, with permissions scoped to a group of people.
4. **Integrations**: knowledge bases, connectors and extensions (such as MCP servers), inside or outside the company.
5. **Features**: **Sight** (analytics), **Flows** (guided workflows), **Automate** (a more involved form of workflows), **Research** (deep research) and **Apps** (generated automatically).

## Chat

- The natural-language entry point. It looks like any chatbot, but answers from your enterprise data, generates content, runs flows, starts research and takes actions in connected apps.
- Every chat has three **scopes** for the answer:
  - **All data and apps**: every space, dashboard, dataset, topic, knowledge base and action you may access, plus the model's general knowledge.
  - **General knowledge**: the underlying model only, excluding all enterprise data.
  - **Specific data and apps**: you pick the exact resources to answer from. Tying a query to a trusted source is a good way to **reduce hallucinations**.
- In the conversation you can:
  - Pick an **agent** (agent picker).
  - **Chat with datasets**.
  - Use **web search**.
  - **Upload files**, up to **20 per chat**, in addition to files uploaded to spaces.
  - **Invoke actions** and **run flows**.
  - Get **source citations**.
  - Use **memory and personalisation**: Quick knows who you are, and automatically remembers conversations and preferences in long-term memory.

## Agents

- An **agent** is **instructions + knowledge sources + tools**.
  - **Knowledge sources**: spaces, dashboards, topics and knowledge bases.
  - **Tools**: **action connectors** it may invoke. These make the agent agentic, for example filing or closing a ticket, adding a CRM customer or updating a website.
- Quick **knowledge bases are not Bedrock knowledge bases**: same idea, different systems.
- **Preconfigured** agents stay inside their assigned resources. **Unopinionated** agents let chat decide the boundary.
- Answers are **always scoped to what the invoking user may already see**.
- Two types of chat agent:
  - **System chat agent** (**My assistant**): available to everyone. A base planner with no data of its own that resolves the user's resources at chat time.
  - **Custom chat agents**: built for a domain with a persona and toolset, then shared. **Admins control who may create them**.

## Why Quick rather than ChatGPT, Claude or Gemini on AWS

- **Identity you already run**: IAM, IAM Identity Center, SAML 2.0, MFA, RBAC and SSO.
- **Permission-aware answers**: agents return only what the user may already see.
- **Private data paths**: VPC, Direct Connect and Site-to-Site VPN to on-premises sources.
- **Native analytics** over Redshift, Athena, S3 and SPICE, not a file upload.
- Your data stays in your control and is **not used to train someone else's models**.
- One AWS agreement, bill, Region choice and compliance posture.

## Problems Quick solves

- Knowledge scattered across S3, SharePoint, Confluence, Drive, Slack, Jira and CRMs.
- Generic chatbots that cannot see enterprise data, giving confident answers with no citations.
- BI locked behind analysts, so business users wait days for a number.
- Research and synthesis done by hand across dozens of tabs.
- Insight without action: a person still has to open Jira or Salesforce to make the change.
- **Shadow AI**: staff pasting confidential data into unapproved tools.

## Exam takeaways

1. Quick request flow: **chat, agents, spaces, integrations, features**.
2. Chat scopes: **all data and apps**, **general knowledge**, or **specific data and apps** (best to limit hallucinations).
3. Agent = **instructions + knowledge sources + tools**. **Action connectors** make it agentic.
4. Answers are always **scoped to the invoking user's permissions**.
5. **System chat agent** is for everyone. **Custom chat agents** are creatable only by whoever admins allow.
6. Quick knowledge bases are **not** Bedrock knowledge bases.
7. QuickSight continues as **Quick Sight** inside Quick.
