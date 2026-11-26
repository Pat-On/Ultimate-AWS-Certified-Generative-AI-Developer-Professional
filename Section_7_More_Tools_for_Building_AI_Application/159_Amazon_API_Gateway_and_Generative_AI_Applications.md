# 159. Amazon API Gateway and Generative AI Applications

## Where it appears

| Role | Detail |
|---|---|
| **Feedback collection front end** | Quality is often subjective, so humans need an internet-facing API to say whether an answer was good |
| **Model front end** | External applications reach your models through it instead of calling Bedrock themselves |
| **Usage plans** | Size traffic by **model capacity** (your quotas) and client needs |
| **Throttling** | About **10 to 50 requests per second** is a reasonable start, for example against bots |
| **Burst capacity** | About **2 to 3 times** the steady rate |
| **Response filtering** | A last line of defence alongside guardrails and redaction |
| **Retry strategies** | For model timeouts |
| **Token limit management** | A **request validator** with a **JSON Schema** rejects oversized prompts |
| **Routing** | **Request transformations** can start the choice of model if the needed information is there |
| **Field validation** | Reject requests missing required inputs at the front door |

## Notes beyond the lecture

- A JSON Schema limits **characters and structure**, not exact **tokens**.
- REST APIs do not automatically retry a failed Lambda call. In practice the retry logic usually sits in the **client**, **Lambda** or **Step Functions**.
- Calling Bedrock directly needs **AWS credentials**, which is why external clients go through an API.

## Exam takeaways

1. **API Gateway fronts models and feedback endpoints.**
2. **Usage plans, throttling and burst** protect model quotas.
3. **Request validator + JSON Schema** enforces input constraints.
