# 133. Optimizing for Specific Use Cases

Different models expose different parameters you can tune to fit a use case. To **measure the effect** of a change, use **A/B testing**, and you do not need to build it yourself:

- **Bedrock Evaluations**
- **CloudWatch Evidently**
- **SageMaker** features for this

## Common parameters

A **token** is roughly the next word the model predicts. When it picks the next token, it chooses among **candidate** tokens.

| Parameter | What it controls |
| --- | --- |
| **`maxTokens`** | The length (verbosity) of the response. |
| **`temperature`** | **How much randomness** there is in choosing among candidates. 0 gives a consistent response (other model changes can still alter it), 1 is more **creative**. Higher temperature means more randomness, not off-the-wall output, because candidates are already reasonable next choices. |
| **`top_p`** (**nucleus sampling**) | The **probability threshold**: how good a token candidate must be before it is considered at all. |
| **`top_k`** | **How many** candidates there are to sample from (a fixed number of the best options). |

- You normally specify **temperature or `top_p`, not both**.
- `top_p` and `top_k` can overlap: top_k fixes the number of candidates, top_p sets a probability threshold, and the result may be limited by top_k.

## Exam takeaways

1. **Temperature** = randomness in choosing the next token. **`top_p`** = how good a candidate must be. **`top_k`** = how many candidates. This is a frequent quiz topic.
2. Use temperature **or** `top_p`, not both.
3. Verify parameter changes with **A/B testing**: Bedrock Evaluations, CloudWatch Evidently or SageMaker.
