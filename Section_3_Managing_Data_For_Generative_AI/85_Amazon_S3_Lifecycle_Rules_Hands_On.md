# 85. Amazon S3 - Lifecycle Rules - Hands On

Creating a **lifecycle rule** in the console and looking at its five rule actions.

## Steps

1. Under the bucket's **Management** tab, create a lifecycle rule (`demo rule`) applied to all objects, and acknowledge the warning.
2. Choose the rule actions you need, then add transitions or expirations.
3. Review the **timeline** summary, which shows what happens to current and noncurrent versions, then create the rule.

## Rule actions

| Action | Example in the demo |
| --- | --- |
| Move **current versions** between storage classes | Standard-IA at 30 days, Intelligent-Tiering at 60, Glacier Instant Retrieval at 90, Glacier Flexible Retrieval at 180, Deep Archive at 365 |
| Move **noncurrent versions** between storage classes | Glacier Flexible Retrieval after 90 days |
| **Expire current versions** | After 700 days |
| **Permanently delete noncurrent versions** | After 700 days |
| Delete **expired object delete markers** or **incomplete multi-part uploads** | Not configured in the demo |

- The **current version** is the most recent one, shown to the user. A **noncurrent version** has been overwritten by a newer one.
- You can add as many transitions as you like.

## Exam takeaways

1. Lifecycle rules offer **five actions**: transition current, transition noncurrent, expire current, permanently delete noncurrent, and clean up delete markers or incomplete multi-part uploads.
2. Current and noncurrent versions are handled separately, so versioning matters.
