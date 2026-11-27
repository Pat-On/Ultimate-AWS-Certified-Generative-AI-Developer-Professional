# 204. Clarification on CloudTrail + Bedrock

| Need | Service |
|---|---|
| **Usage** of Bedrock and prompt resources (audit trail) | **CloudTrail** |
| The **actual prompts** and responses | **CloudWatch Logs** (Bedrock model invocation logging) |

- CloudTrail **does not log the prompts themselves**; it tracks the use of prompt resources.
- AWS Skill Builder material refers to CloudTrail for **audit trails of prompt usage**, which is why it appears in this context.
- Reference: [Logging Amazon Bedrock API calls using CloudTrail](https://docs.aws.amazon.com/bedrock/latest/userguide/logging-using-cloudtrail.html)

## Exam takeaways

1. **Who used what** → CloudTrail; **what was said** → CloudWatch Logs.
