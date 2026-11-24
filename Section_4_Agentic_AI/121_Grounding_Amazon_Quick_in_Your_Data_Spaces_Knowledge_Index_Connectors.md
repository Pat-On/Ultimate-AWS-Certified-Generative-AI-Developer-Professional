# 121. Grounding Amazon Quick in Your Data (Spaces, Knowledge, Index, Connectors)

Quick is grounded in enterprise data through **spaces**, **knowledge bases** on a shared **Quick Index**, and **connectors** to about 50 applications.

## Spaces

- A **space** is a shared context: a collection of data, Quick resources and actions scoped to a team or domain, with controlled access. Agents and chats answer only from the context they can access, which follows **least privilege**.
- **Owners** share, link and unlink resources. **Viewers** ask questions and download files.
- **Sharing a space does not by itself grant access to the underlying assets**. You need access to both the space and the assets in it.
- What goes into a space: **uploaded files**, **dashboards**, **topics and datasets**, **knowledge bases** and **application actions**.
- What draws on a space: **chat agents**, **apps** in Quick, and **flows and research**. The space scopes what they can do and access.

## Knowledge and the Quick Index

- The **Quick Index** is an indexed collection of content from your data sources, optimised for AI retrieval, semantic search and cited answers. It is kept in sync over time.
- **Many knowledge bases share one Quick Index** (one per Quick account). **Access control sits at the knowledge base level**.
- Data sources for knowledge bases: **Amazon S3**, **Microsoft SharePoint Online**, **Microsoft OneDrive**, **Google Drive**, **Confluence Cloud** and a **web crawler**.
- Example knowledge bases: policy documents, customer feedback, product documentation. They are used by spaces, agents, research and flows.
- **Pooled storage limits**: **25 GB** on Professional, **50 GB** on Enterprise.
- **Bring your own index**:
  - **Amazon Q Business** is deprecated, and Quick is the recommended migration path. Bring your own index ingests a Q Business index into a Quick Index.
  - You can also bring a **Bedrock knowledge base** into Quick. They are not the same thing as Quick knowledge bases.

## Connectors and integrations

- About **50 supported applications**, in three integration types. Most support **actions only**, and the knowledge base list is much shorter.
  - **Action connectors**: real-time calls into external services to read data, update records or trigger processes. Examples: Slack, Teams, Jira, Salesforce, ServiceNow, GitHub, Notion, HubSpot, QuickBooks, Box, Asana. For instance, create a Notion page, read Salesforce data, or open or close a Jira ticket.
  - **Data access integrations**: connect to an external application to reach its data. They are the foundation for knowledge bases and are not used directly for analysis.
  - **Knowledge bases**: selected content indexed for AI retrieval and question answering, from S3, SharePoint Online, OneDrive, Google Drive, Confluence Cloud and web crawler.
- **Build your own** with **MCP servers**, **OpenAPI specifications** or **REST APIs** for systems not on the official list.
- **Extensions** embed Quick in **Chrome, Slack, Teams and Microsoft 365**.

## Exam takeaways

1. A **space** scopes data, resources and actions to a team. **Space access does not grant access to the underlying assets**.
2. All knowledge bases share **one Quick Index**, with access control at the **knowledge base** level.
3. Index storage: **25 GB Professional**, **50 GB Enterprise**.
4. **Q Business is deprecated**: migrate with **bring your own index**. **Bedrock knowledge bases** can also be brought in.
5. Three integration types: **action connectors**, **data access integrations**, **knowledge bases**. Knowledge base sources are only S3, SharePoint Online, OneDrive, Google Drive, Confluence Cloud and web crawler.
6. Custom integrations use **MCP**, **OpenAPI** or **REST APIs**.
