# 11. Fine-Tuning Foundation Models in Bedrock

Fine-tuning extends the training of a foundation model (a large language model or an image model) on your own data, so the knowledge is **baked into the model** instead of being added on top of it. How the training works under the hood is covered in lecture 12 (LoRA).

## Why fine-tune

- It **replaces prompt engineering**: you don't have to build up a big conversation or stuff examples of your data into every prompt to get the output you want.
- It **saves tokens in the long run**, because the information is in the model and not re-sent in each prompt. That can make it cheaper than prompt engineering or RAG over time.
- The fine-tuned model is used **like any other model**: same API, with a new model identifier in place of the base model's.
- You can **fine-tune a fine-tuned model** again as new information arrives, making it smarter over time.

## Typical applications

- A chatbot with a certain **personality, style or objective**, such as customer support or writing ads in your brand's voice. Training on your past ads or messages makes output sound less obviously AI-generated.
- Training on **data newer than the model's cutoff date**, which is usually at least a few months old.
- Training on **proprietary data**, such as your past emails and messages, or customer support transcripts.
- **Specific tasks** like classification or judging whether a statement is true, using examples of the answers you want, even for something the model wasn't designed to do.

## Custom models (fine-tuning in Bedrock)

In Bedrock a fine-tuned model is called a **custom model**.

- **Supported models:** Titan, Cohere and Meta models (others may follow). Not every model can be fine-tuned, so check the model card first.
- **Text models:** provide **labelled** training pairs of a `prompt` and a `completion`, as JSON lines (e.g. `{"prompt": "...", "completion": "..."}`). They can be questions and answers.
  - The pairs are examples of the style and type of answer you want. The model is not limited to those questions, and generalises to new ones.
- **Image models:** provide pairs of an **S3 path to an image** and its **description (the prompt)**. This works for text-to-image and image-to-embedding models.
- **Workflow:** upload the training data to **S3**, then tell Bedrock to create a custom model from a chosen foundation model and that data.
- **Security:** to train on sensitive or proprietary data, use a **VPC with PrivateLink**. This is likely to show up in the exam.
- **Cost and time:** fine-tuning a large model is **expensive and slow** up front, even though it can pay off later. That is why many people prefer simpler approaches, which the next lectures cover.

## Continued pre-training

- It is the same as a custom model, except the data is **unlabelled**: raw text records (`{"input": "..."}`), with no prompt/completion pairs.
- Typical data is your own business documents. It bakes the extra data into the model, so you don't have to include it in prompts.
- It is also costly and time-consuming.

| | Custom model (fine-tuning) | Continued pre-training |
| --- | --- | --- |
| Training data | **Labelled**: prompt and completion pairs (text), or image and description pairs | **Unlabelled**: raw text |
| Data location | S3 | S3 |
| Result | A new model, used like any other | A new model, used like any other |
