# 194. Principles of Responsible AI

The exam covers **best practices for ML system architecture**, including Amazon's **core dimensions of responsible AI**.

## Core dimensions

| Dimension | Question to ask |
|---|---|
| **Fairness** | Is the application biased, even unintentionally? |
| **Explainability** | Can you explain why it produced an output, and so fix a wrong one? |
| **Privacy and security** | Is private or personally identifiable data kept out of training? Could the system leak it? Are guardrails in place to remove it? |
| **Safety** | Do people feel safe using it? Can it fail in unintended ways? |
| **Controllability** | Can you steer and tune its behaviour? |
| **Veracity and robustness** | Is it truthful? Can you measure **hallucinations**, and are they within your limits? |
| **Governance** | Can you monitor it, report on it and comply with the laws of each country? |
| **Transparency** | Do you publish what the model can and cannot do, and its limitations? |

## AWS tools

| Tool | What it does for responsible AI |
|---|---|
| **Bedrock Model Evaluations** | Runs test prompts and compares responses with ideal ones, also for non-deterministic models |
| **SageMaker Clarify** | Detects **bias** in training data and output; **explainability** (which features drive a prediction); model evaluation, also continuous |
| **SageMaker data tools** | Fix bias by **rebalancing** data or adding new data |
| **SageMaker Model Monitor** | **Alerts** on inaccurate responses of a deployed model |
| **Amazon Augmented AI (A2I)** | **Humans in the loop** to review results, or to help training (for example **RLHF**: choosing the better of two responses). Use your own team or an AWS managed workforce |

Human review has an ethical side too: make sure the people doing the work are not exploited.

## SageMaker ML governance

A heading for a group of features, not a service.

| Feature | Purpose |
|---|---|
| **Role Manager** | Roles and permissions for groups of SageMaker users |
| **Model Cards** | Document a model: intended use, risks, limitations (**transparency**) |
| **Model Dashboard** | One view of all your SageMaker models, with drill-down |

## Exam takeaways

1. Know the dimensions: **fairness, explainability, privacy and security, safety, controllability, veracity and robustness, governance, transparency**.
2. **Bias and explainability** → **SageMaker Clarify**.
3. **Monitoring a deployed model** → **Model Monitor**; **human review** → **A2I**.
4. **Documentation and transparency** → **Model Cards**.
