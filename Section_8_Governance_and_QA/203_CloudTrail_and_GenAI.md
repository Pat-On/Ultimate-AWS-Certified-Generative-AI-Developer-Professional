# 203. CloudTrail and GenAI

**CloudTrail** records **API calls** in the account, including calls to **Amazon Bedrock**, which makes it an **audit trail** for governance and compliance.

## What the audit trail answers

- **Who** made a call
- **When** it was made
- **Which** Bedrock activity it was, including use of prompt resources

As a developer you need a way to track and log this, because many regulations require it.

**Important:** CloudTrail does **not** log the text of the prompts. See lecture 204.

## Exam takeaways

1. **Audit of Bedrock API usage** → **CloudTrail**.
