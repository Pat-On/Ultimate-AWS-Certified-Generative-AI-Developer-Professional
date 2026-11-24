# 117. Amazon Q Apps

**Amazon Q Apps** are part of **Amazon Q Business** and let anyone in a company create Gen AI-powered apps **without coding**, using only natural language.

## Amazon Q Business background

- A **fully managed Gen AI assistant for your employees**, based on your company's knowledge and data.
- Answers questions, provides summaries, generates content and automates tasks.
- Performs routine actions, such as submitting time-off requests or sending meeting invites.
- Built on **Amazon Bedrock**, but you **can't choose the underlying foundation model**.
- Example questions: write a job posting for a Senior Product Marketing Manager, create a social media post under 50 words to advertise the role, or ask what was discussed in the team meetings in the week of 4/12.
- Example: https://aws.amazon.com/blogs/machine-learning/improve-productivity-when-processing-scanned-pdfs-using-amazon-q-business/

### Data sources and plugins

- **Data connectors** (fully managed RAG) connect to **40+ popular enterprise data sources**: Amazon S3, RDS, Aurora, WorkDocs, Microsoft 365, Salesforce, Google Drive, Gmail, Slack, SharePoint and more. Q Business crawls them.
- **Plugins** let you interact with **third-party services** such as Jira, ServiceNow, Zendesk and Salesforce, for example to send issues to Jira.
- **Custom plugins** connect to any third-party application using APIs.

### Security and admin controls

- Users can authenticate through **IAM Identity Center**, which can be configured with external identity providers (Google Login, Microsoft Active Directory).
- Users receive responses generated **only from the documents they have access to**.
- **Admin controls are guardrails** that control and customize responses to your organization's needs:
  - Block specific words or topics.
  - Respond **only with internal information**, instead of using external knowledge.
  - **Global controls** and **topic-level controls** (more granular rules). For example, a blocked topic "Gaming Consoles" makes a question about setting up a Nintendo Switch return "Sorry, but this is a restricted topic."

## Q Apps

- A web UI called the **Amazon Q Apps creator**: you write a prompt describing the type of app you want.
- The app is based on your **company's internal data** and can also use **plugins** (Jira, etc.).
- Q Apps generates a web application, for example one where users can upload a document and enter prompts.
- Anyone can create an app quickly **without developers**.
- Reference: https://aws.amazon.com/blogs/aws/amazon-q-business-now-generally-available-helps-boost-workforce-productivity-with-generative-ai/

## Exam takeaways

1. **Q Apps** are a **Q Business** feature for building **no-code Gen AI apps from natural language**.
2. They use your **internal company data** and can use **plugins**.
3. Q Business is built on Bedrock, but you **can't choose the foundation model**.
4. Q Business uses **data connectors** (40+) for RAG, **plugins** for third-party actions, **IAM Identity Center** for authentication and **admin controls** as guardrails.
