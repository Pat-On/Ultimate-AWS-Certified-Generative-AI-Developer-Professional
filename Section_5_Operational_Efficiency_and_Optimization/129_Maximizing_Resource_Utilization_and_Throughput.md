# 129. Maximizing Resource Utilization and Throughput

Another lever is making sure you are not paying for capacity that sits idle.

## Batching

- **Batch embeddings** for vector stores: submit chunks together in large batches, not one at a time. It is faster and cheaper.
- **Bedrock batch inference**: when you do not need real-time answers, put many prompts in an **S3 bucket**, and Bedrock processes them and writes all responses back to **S3**.

## Capacity planning

- Start from your desired **tokens per minute (TPM)** and **requests per minute (RPM)** to work out the capacity you need and whether you are being throttled or hitting quotas.
- The **AWS Service Quotas** tool has a **Bedrock** section to estimate capacity and to **request a quota increase** (there is a form). **CloudFormation** templates can also help with capacity planning.
- **Tensor parallelism**: sharding a large model's **weights across many GPUs** (a large model does not fit on one), giving **better memory utilization per container**. It happens under the hood, so you only need to know the term.

## Provisioned throughput

- For **dedicated capacity and deterministic performance**, provision by **tokens** or by **model units (MUs)**, an opaque unit that corresponds roughly to token throughput.
- **Required for customized models.** Also the answer when a scenario needs consistent performance under high volume and a model is not keeping up.
- You provision **for a given model**, not for Bedrock overall. At inference time you must pass the **ARN of the provisioned model** as the model ID, **not** the generic model ID.

## Monitoring and scaling

- **CloudWatch**, including built-in dashboards (you do not have to use QuickSight), tracks utilization.
- **AWS Cost Explorer** attributes model cost to a **business function, application or department**.
- **Auto-scaling**: use serverless services such as **Lambda, Bedrock, OpenSearch Serverless and AgentCore** so scaling and utilization are handled for you.

## Exam takeaways

1. **Batch** embedding requests, and use **Bedrock batch inference** (S3 in, S3 out) when real time is not needed.
2. Plan capacity from **TPM and RPM**, use **Service Quotas** to check or raise limits, and use **provisioned throughput** for dedicated capacity.
3. **Customized models require provisioned throughput.** Calls must use the **provisioned model ARN**.
4. **Cost Explorer** attributes cost to business functions. **CloudWatch** dashboards monitor utilization.
5. **Tensor parallelism** shards model weights across GPUs for better memory use.
