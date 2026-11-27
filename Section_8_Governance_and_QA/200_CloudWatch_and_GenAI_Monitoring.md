# 200. CloudWatch and GenAI Monitoring

**CloudWatch Logs** holding **prompt inputs** and **model responses** is the basis for monitoring and troubleshooting generative AI.

## Uses

- **Prompt regression testing**: how do prompts and responses change over time?
- Measuring is the first step to testing.

## AI-specific indicators

| Indicator | Question |
|---|---|
| **Prompt effectiveness** | Do prompts achieve the wanted result? |
| **Response quality** | Is the output good? |
| **Latency** (end to end) and **error rates** | Is the system healthy? |
| **Hallucination rate** | Checked against ground-truth and prompt datasets, with anomaly detection |
| **Response drift** | Are responses becoming less similar over time? |
| **Token bursts** | Unexpected traffic spikes? |
| **Business impact** | Is it earning money or driving sales? |
| **Cost anomalies** | Is cost shooting up, and why? |

Also useful (in CloudWatch or elsewhere):

- **Foundation model interaction traces**, including agent traces
- **Bedrock model invocation logs**

## A/B testing

**CloudWatch Evidently** appears in some preparation material but is **deprecated**; do not expect it as an answer. Use, for example, the A/B testing built into **SageMaker deployments**.

## Exam takeaways

1. Prompts and responses go to **CloudWatch Logs** (**model invocation logging**).
2. Track **latency, errors, quality, hallucinations, drift, tokens and cost**.
3. **Evidently is deprecated.**
