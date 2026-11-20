# 51. Using Comprehend, Lambda, and Bedrock together

An exam-guide pattern: use **AWS Lambda** to call **Amazon Comprehend** to enforce data quality before data enters a **Bedrock** system.

## Pattern

- Data arrives from **Bedrock Data Automation**, **S3** or another source and triggers a Lambda function.
- Lambda calls Comprehend to filter or transform the data, then passes it on to Bedrock.
- Comprehend tasks in this role: redact **PII**, extract entities, detect language, classify content.

## Example uses

- Cleaning transcripts before they go into a **Bedrock knowledge base**.
- Pre-screening user-generated content (for example a file uploaded with a prompt) before it reaches an agent, by filtering and classifying it.
