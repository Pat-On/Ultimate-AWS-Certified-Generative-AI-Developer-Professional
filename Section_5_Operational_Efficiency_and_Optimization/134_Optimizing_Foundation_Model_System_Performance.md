# 134. Optimizing Foundation Model System Performance

A collection of further tips, not all closely related.

## General

- **API call profiling**: find patterns in your requests to see whether **caching, batching or RAG improvements** would help (the same questions repeatedly, requests that could be batched, queries that match poorly with the retrieved context).
- Use **structured input and output** (JSON or XML templates) where possible: it improves efficiency and accuracy.
- **Chain-of-thought** instruction patterns: make the model reason step by step for complex tasks. Many models do this on their own, so it is also a routing question: send complex reasoning tasks to a model that supports it.
- **Feedback loops**: capture user satisfaction and behavior (AWS stresses this). Fix what users dislike, and use the feedback to find and encourage prompts that work well.

## SageMaker AI specifics

- It can deploy models **up to 500 GB**. A huge model that **never starts** may just need a longer **container health check and download timeout**.
- **Third-party model parallelization** frameworks are supported: **Triton, FasterTransformer, DeepSpeed**.
- **Instance guidance**:
  - Large models: a big GPU instance such as **`ml.p4d.24xlarge`**.
  - Small models (for example named entity recognition): a **CPU** instance such as **`ml.c5.9xlarge`** can be enough if cost is the main concern.
- **UltraServers** (**Trn2**, **P6e-GB200**): connect the EC2 instances hosting your AI/ML workload with **low-latency, high-bandwidth accelerator interconnects**, which matters when a model is distributed across many instances.
- **Lambda endpoint lifecycle management**: when you run your own inference endpoints, a Lambda function can initialize them and **download model artifacts from S3 on demand** when processing is triggered.

## Exam takeaways

1. **Profile API calls** to decide whether caching, batching or RAG changes will pay off.
2. Prefer **structured input and output**, route complex reasoning to models that support **chain of thought**, and keep **feedback loops**.
3. SageMaker AI deploys models up to **500 GB**. If one never starts, raise the **download and health-check timeouts**.
4. Parallelization frameworks: **Triton, FasterTransformer, DeepSpeed**.
5. **UltraServers** give fast interconnects between instances for distributed models. **Lambda endpoint lifecycle management** pulls artifacts from S3 on demand.
