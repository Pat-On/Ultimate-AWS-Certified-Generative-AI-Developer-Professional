# 147. Cross-Account Lineage Tracking

The exam guide explicitly calls out **cross-account lineage tracking** in SageMaker: tracing data lineage **across organizational boundaries** is possible.

- Use the SageMaker **`AddAssociation` API** to connect entities across accounts (the lecture audio says "AD Association"; the slide shows `AddAssociation`).
- You also need the **required IAM roles and permissions** to allow the cross-account access.
- Lecture 146 adds that this integrates with **AWS Resource Access Manager**.

## Exam takeaway

**Cross-account lineage tracking = the `AddAssociation` API plus the appropriate IAM roles and permissions.**
