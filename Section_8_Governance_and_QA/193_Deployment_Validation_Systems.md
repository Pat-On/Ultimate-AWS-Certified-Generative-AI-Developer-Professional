# 193. Deployment Validation Systems

CI/CD needs a way to tell whether a deployment is **safe to roll out** or must be **rolled back**. Generative AI is **non-deterministic** and models change, so **unit tests with expected outputs are not enough**.

## Synthetic user workflows

Simulate real use **end to end**, **before and after** deployment and **continuously**.

| Job | Tool |
|---|---|
| Simulated user checks | **CloudWatch Synthetics (canaries)** |
| Orchestrate the flow | **Step Functions** |
| Start it | **EventBridge** |
| Step logic | **Lambda** |
| Store, query, visualise results | **S3**, **Athena**, **QuickSight** |

## AI-specific output checks

- Measure **hallucination rate** (against ground truth), **semantic drift**, **faithfulness** and **compliance**.
- Use **Bedrock Model Evaluations**, or build your own with **Lambda and Step Functions**.

## Response consistency

Exact answers cannot be expected. Run a **test prompt dataset** and check that responses stay **semantically similar** and consistent in style (a **judge model** can help), within an **accepted range**. Tune the threshold to avoid false alarms.

## Exam takeaways

1. **Synthetic workflows / canaries** validate generative AI deployments.
2. Validate **hallucination, drift, faithfulness, compliance**.
3. Test for **variability within thresholds**, not exact matches.
