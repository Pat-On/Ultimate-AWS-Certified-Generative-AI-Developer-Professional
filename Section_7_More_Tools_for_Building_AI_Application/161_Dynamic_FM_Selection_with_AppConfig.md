# 161. Dynamic FM Selection with AppConfig

New models appear all the time. To switch the **foundation model** without releasing code, store the choice in **AppConfig**.

- Use **feature flags** and **configuration profiles** to name the model.
- The profile can live in **S3**, which AppConfig integrates with: edit the file and deploy it through AppConfig.
- The application picks up the change **without redeployment**.

## What it enables

- **Rolling out** new models
- **A/B testing**
- **Rolling back** a model you do not like

## Alternatives

**SageMaker** and **Bedrock Evaluations** can compare and test models too. **CloudWatch Evidently** also handled A/B tests, but AWS is retiring it, so for new work look at Bedrock Evaluations.

## Exam takeaways

1. **AppConfig (with S3)** is a valid answer for **dynamic model selection**.
2. No code change, with the usual AppConfig **gradual rollout and rollback**.
