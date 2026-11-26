# 165. Lab: Prompt Chaining with Step Functions and Bedrock

- **Type:** Practice lab (watch it as a demo: it depends on specific models, and Bedrock models come and go)

**Goal:** chain prompts into a conversation around a model that only supports **`InvokeModel`** (plain text in, no chat history), so each answer builds on the earlier ones.

## Start from the template

Step Functions console → **templates** → Bedrock → **prompt chaining**.

- The built-in demo is **broken**: it targets a **Cohere Command Text** model that no longer exists, and demo mode is **read-only**.
- Choose **Use template** (build on it) so it can be edited.
- The template's instruction to **enable model access** is out of date: the lecture says it is no longer needed.
- Check that **Bedrock and the model are available in your Region**.

## How the state machine works

1. The input is a **list of prompts**.
2. A **Choice** state asks whether any prompts remain.
3. If so, **invoke the model** with the **earlier conversation plus the next prompt**, then loop.
4. When none remain, the execution **succeeds**.

## Adapting it to another model

The replacement is **Amazon Titan Text G1 - Lite**. Take the model ID and formats from the **model catalog** (inference parameters and response).

| What | Template (Cohere) | Titan |
|---|---|---|
| **Model ID** | Command Text | Titan Text Lite (also drives the **IAM permissions**) |
| **Prompt field** | `prompt` | `inputText` |
| **Max tokens** | top level | `textGenerationConfig.maxTokenCount` (250) |
| **Output path** | `generations[0].text` | `results[0].outputText` |

Temperature and top P stay at their defaults.

## Run and clean up

- Creating the state machine also creates an **IAM role** allowing `InvokeModel` on that model (and **X-Ray** tracing).
- The sample input (`prompt chaining` JSON in the course materials) has three prompts: name a real city and country, describe it in 2 to 3 sentences, then write about its **cuisine**.
- The execution succeeded (it chose Cleveland); check **execution input and output**.
- **Delete the state machine** afterwards.

## Lesson

Applications that depend on a particular model are **fragile**. Model retirements change **IDs and request and response formats**, so design for that.

## Exam takeaways

1. **Prompt chaining** = a loop with a **Choice** state that feeds earlier output into the next call.
2. With `InvokeModel`, the **request and response format depends on the model**.
