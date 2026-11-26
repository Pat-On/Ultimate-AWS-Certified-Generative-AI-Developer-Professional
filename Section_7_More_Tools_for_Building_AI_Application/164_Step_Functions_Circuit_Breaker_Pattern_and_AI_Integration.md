# 164. Step Functions Circuit Breaker Pattern, and AI Integration

## Circuit breaker

A **pattern**, not a built-in Step Functions feature. It stops calls to a service that is **timing out or failing**. It appears in Amazon's exam preparation material.

| Circuit | Meaning |
|---|---|
| **Closed** | The service is healthy: **calls go through** |
| **Open** | The service is broken: **calls are not attempted** |

**Flow** (Step Functions + Lambda + DynamoDB):

1. A Lambda function reads the **circuit status** from **DynamoDB**.
2. **Closed:** call the service. Success ends the workflow.
3. A timeout or failure **updates the status** to open.
4. Later requests see it is open and **fail without calling** the service.
5. Something must **detect recovery** and close the circuit again.

**Beyond the lecture:** the usual form of the pattern adds a **half-open** state, or an expiry time on the DynamoDB item, so that a trial request can test for recovery.

## Why it matters for generative AI

If the breaker tracks a foundation model's health, an open circuit can **route to a fallback model** or switch to a **degraded service mode**.

## Other generative AI uses

| Use | Detail |
|---|---|
| **ReAct (Reasoning + Acting)** | Loop: reason, take an action, **observe** the result, repeat until the answer. This can implement **chain-of-thought** style reasoning |
| **Dynamic routing** | Send each action to a **specialised model** or tool |
| **Model review and approval** | Orchestrate automated and **human** evaluation before a new model reaches production |

The lecturer notes that many models and **agent toolkits** now handle ReAct and routing better, but Step Functions can do it.

## Limits and Bedrock integration

- Data passed **between states** is limited to **256 KB**. For more, store it in **S3** or **DynamoDB** and pass a reference.
- Built-in Bedrock integration includes **`InvokeModel`** and **`CreateModelCustomizationJob`**.
- You can **chain** several model calls, and since `InvokeModel` accepts **guardrails**, chain those too.

## Exam takeaways

1. **Circuit breaker** = status in **DynamoDB**, checked by **Lambda**, orchestrated by **Step Functions**; use it for **model fallback**.
2. **256 KB** payload limit: offload to **S3 or DynamoDB**.
3. Step Functions can **chain prompts and guardrails** through Bedrock.
