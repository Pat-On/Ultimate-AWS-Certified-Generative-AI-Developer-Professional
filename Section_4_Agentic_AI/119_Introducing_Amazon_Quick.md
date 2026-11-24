# 119. Introducing Amazon Quick

**Amazon Quick** is an **agentic AI system aimed at business users, not developers**: an AI assistant for work (chat, research, BI, automation and no-code apps in one place), deeply integrated with your enterprise and its data sources.

## What it is

- Looks like ChatGPT, Gemini or Claude, but is integrated with your enterprise data. Example: a space with proprietary documents tied to a chatbot in a few clicks in the UI gives advice grounded in those documents.
- **Evolved from QuickSight**, which continues as **Quick Sight** inside Quick. Existing APIs and integrations keep working.
- **Amazon Quick is not QuickSight**:
  - QuickSight is AWS's long-standing **business analytics** application, also for business users.
  - Quick is about **agentic AI**: building applications and chatbots on top of your data.
  - Neither needs an **AWS console account**. Quick has its own separate account.
  - Branding is confusing: the console entry "Amazon Quick" takes you to QuickSight, while the Amazon Quick site takes you to Quick.
- **Fully managed**: no infrastructure, no models to host, no inference to serve, no ML or AI experience needed. You don't worry about which model is used.
- **Grounded in your systems** through knowledge bases, connectors and structured data.
  - A Quick **knowledge base** is not a Bedrock knowledge base: it is a collection of documents organized into a space with specific permissions.
  - It can connect to other systems in your organization and to **structured data sources**, in AWS or elsewhere.
- **Open standards**: **MCP** and **OpenAPI** connect anything, so MCP servers (internal or external) extend Quick.
- **Entry points**: web, desktop app, or embedded in **Chrome, Slack, Microsoft Teams and Microsoft 365**.

## Problems it solves

- **Knowledge scattered** across S3, SharePoint, Confluence, Drive, Slack, Jira and CRMs (Salesforce, etc.). Quick pulls it together so you can query it in one place.
- **Generic chatbots can't see enterprise data**: confident answers with no citations, unless you upload data explicitly. Quick grounds and cites answers in your data.
- **BI locked behind analysts**: business users wait days for a number. With the right data sources wired up, they can just ask the chatbot.
- **Manual research** across dozens of tabs: Quick has a **research mode** for deep research that consolidates web data and the data sources you explicitly allow or exclude.
- **Insight without action**: Quick has **agentic capabilities**, so it can open or close a Jira ticket or make changes in Salesforce, not only answer.
- **Shadow AI**: staff pasting confidential data into unapproved tools. With Quick the data stays internal and more secure.

## Why Quick vs. ChatGPT, Claude or Gemini on AWS

- **Identity you already run**: IAM, IAM Identity Center, SAML 2.0, MFA, RBAC and SSO.
- **Permission-aware answers**: agents return only what the user may already see. Information is organized into **spaces** accessible only to certain people or groups.
- **Private data paths**: VPC, Direct Connect and Site-to-Site VPN to on-premises sources, rather than uploading a file over the open internet.
- **Native analytics** over Redshift, Athena, S3 and **SPICE** (the engine on top of QuickSight that accelerates queries), not just a file upload.
- **Your data stays in your control** and is not used to train someone else's models, with no need to rely on a vendor's promise.
- **One AWS agreement, bill, Region choice and compliance posture**: no new vendor to onboard, which cuts red tape for legal departments.

## How Quick works: the building blocks

Every request flows through five layers: **chat** interprets it, an **agent** plans it, a **space** supplies the context, **integrations** reach your systems, and a **feature** does the work. All are delivered through the web app, desktop app, Chrome, Slack, Teams and Microsoft 365.

| Layer | Role |
|---|---|
| Chat | The front door for every request |
| Agents | Instructions, knowledge, tools |
| Spaces | Files, dashboards, datasets, actions |
| Integrations | Knowledge bases, connectors, extensions |
| Features | Sight, Flows, Automate, Research, Apps |

### Chat

- The primary interface: one natural-language front door to answer from data, generate content, run a flow, start research or take an action in a connected app.
- **Scope the answer** to: **all data and apps** (spaces, dashboards, datasets, topics, knowledge bases, actions and model knowledge), **general knowledge** (the underlying model only, no enterprise resources) or **specific data and apps** (the exact resources you choose).
- In the conversation: agent picker, chat with datasets, web search, **upload files (20 per chat)**, invoke actions, run flows, source citations, memory and personalisation.

### Chat agents

- An **agent = instructions + knowledge sources + tools**. Knowledge sources are spaces, dashboards, topics and knowledge bases. Tools are action connectors it may invoke.
- Preconfigured agents stay inside their assigned resources. Unopinionated ones let chat decide the boundary.
- Answers are **always scoped to what the invoking user may already see**.
- **System chat agent ("My assistant")**: available to everyone, a base planner with no data of its own that resolves the user's resources at chat time.
- **Custom chat agents**: built for a domain with a persona and toolset, then shared. Admins control who may create them.

### Spaces

- A **space** is a collection of data and Quick resources scoped to a team or domain, so agents answer only from that context.
- Contents: uploaded files, dashboards, topics and datasets, knowledge bases, application actions. Used by chat agents, apps in Quick, and flows and research.
- **Owner / Viewer permissions**: owners share, link and unlink resources. Viewers ask questions and download files.
- **Sharing a space does not by itself grant access to the underlying assets.**

### Knowledge and the Quick Index

- The **Quick Index** is an indexed collection of content from your data sources, optimised for AI retrieval, semantic search and cited answers. Content is indexed and kept in sync.
- Data sources: Amazon S3, Microsoft SharePoint Online, Microsoft OneDrive, Google Drive, Confluence Cloud, web crawler.
- **Many knowledge bases share one Quick Index**, and **access control sits at the knowledge base level**. Examples: policy documents, customer feedback, product documentation. They are used by spaces, agents, research and flows.
- You can bring your own **Q Business index** or **Bedrock knowledge base**.
- **Pooled storage: 25 GB Professional, 50 GB Enterprise.**

### Connectors and integrations

- **Around 50 supported applications**, in three integration types. Most support actions only, and the knowledge base list is much shorter.
  - **Action connectors**: real-time calls into external services to read data, update records or trigger processes. Examples: Slack, Teams, Jira, Salesforce, ServiceNow, GitHub, Notion, HubSpot, QuickBooks, Box, Asana.
  - **Data access integrations**: connect to an external application to reach its data. They are the foundation for knowledge bases and are not used directly for analysis.
  - **Knowledge bases**: selected content indexed for AI retrieval and question answering (S3, SharePoint Online, OneDrive, Google Drive, Confluence Cloud, web crawler).
- Build your own with **MCP servers, OpenAPI specifications or REST APIs**.
- **Extensions** embed Quick in Chrome, Slack, Teams and Microsoft 365.

## Exam takeaways

1. **Quick** is a fully managed **agentic AI assistant for business users**. It evolved from QuickSight, which continues as Quick Sight inside Quick. Don't confuse the two.
2. It is grounded in your data through **knowledge bases, connectors and structured data**, and it extends through **MCP and OpenAPI**.
3. A Quick **knowledge base** is **not** a Bedrock knowledge base. It is organized into **spaces** with permissions, and answers only show what the user may already see.
4. Security: IAM, IAM Identity Center, SAML, MFA, RBAC and SSO, private paths (**VPC, Direct Connect, Site-to-Site VPN**), and data not used to train others' models.
5. It can **take actions** (Jira, Salesforce) and run **research**, not just answer questions.
