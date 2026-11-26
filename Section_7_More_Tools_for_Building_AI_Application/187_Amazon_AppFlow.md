# 187. Amazon AppFlow

**AppFlow** is a fully managed service that moves data between **SaaS applications and AWS** without writing the integrations.

| Aspect | Detail |
|---|---|
| **Sources** | **Salesforce** (the one to remember), SAP, Zendesk, Slack, ServiceNow |
| **Destinations** | **S3**, **Redshift**, and non-AWS targets such as Snowflake and Salesforce |
| **Runs** | On a **schedule**, on **events** or **on demand** |
| **Transformation** | Filtering and validation |
| **Transport** | Encrypted over the internet, or private through **PrivateLink** |

## Exam takeaway

**Salesforce (or another SaaS) data into S3 or Redshift without custom code → AppFlow.**
