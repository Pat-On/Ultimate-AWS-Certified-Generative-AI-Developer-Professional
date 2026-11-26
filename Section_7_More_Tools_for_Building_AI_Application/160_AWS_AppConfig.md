# 160. AWS AppConfig

Configuration often ships with the application or sits in **environment variables**. **AppConfig** keeps it **outside**, and lets you **configure, validate and deploy dynamic configuration** with **no code deployment and no restart**.

## Typical uses

- **Feature flags:** ship a feature switched off, then turn it on when ready.
- **Performance tuning.**
- **Allow and block lists**, such as IP addresses.

It works with applications on **EC2, Lambda, ECS, EKS** and more.

## How it works

1. **Configuration sources:** **Parameter Store**, **SSM documents**, an **S3 bucket** and others.
2. The application **polls** for changes.
3. Changes roll out **gradually** instead of to every instance at once.
4. A **CloudWatch alarm** that fires during the rollout triggers a **rollback**.

## Validation before deployment

| Validator | Checks |
|---|---|
| **JSON Schema** | **Syntax:** the shape and types |
| **Lambda function** | **Semantics:** your own, more complex checks in code |

## Exam takeaways

1. **Dynamic configuration without redeploying** = AppConfig.
2. **Gradual rollout with automatic rollback** through CloudWatch alarms.
3. **JSON Schema** is syntactic validation, **Lambda** is semantic validation.
