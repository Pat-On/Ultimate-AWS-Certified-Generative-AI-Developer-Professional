# 26. Token-Level Redaction

Guardrails (lectures 23 to 25) are fancy, and fancy can mean complicated, and complicated sometimes means it doesn't always work. **Token-level redaction** is a simpler extra layer of defence that you build **around** your system, to be safe.

## What it does

- **Filters the input before it reaches your model at all.** If a request asks for something you don't want to handle, you can say no right there and never call the model.
- **Filters the output** just before it reaches the end user, to catch anything that slipped through the model.
- These "tokens" are **not** the internal tokens of the foundation model, which you have no access to. The filtering is of the text going in and out of the system, essentially **word by word**.

## How to build it

- **Custom pre-processing and post-processing handlers** around your **inference endpoint**, which is what faces the outside world, whether it is on **Bedrock or SageMaker**. A common choice is a **Lambda function** that acts as the filter on the input side and the output side.
- What the filter does is up to you:
  - **Pattern matching:** the simple version, for example a **regular expression** with a list of words you want to remove.
  - **Named entity recognition (NER):** a more robust but more complicated way to find sensitive information. **Amazon Comprehend** can be used for this.
- Flow: input goes through the input filter (for example Comprehend) to the inference endpoint, and the output goes through the output filter (for example a regex) before the "nice and clean" response reaches the user.

## Also at ingestion

You can apply the same filters when **ingesting data**, for training or for populating vector stores, so sensitive information never gets into the system in the first place.

## Why use it

It is another layer of defence for what guardrails might miss, simple enough to reason about and test.
