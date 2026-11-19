# 7. Amazon Bedrock Overview

Bedrock is AWS's main generative AI service. It is an API layer over many **foundation models**, so you build applications on the models without coding against any one of them.

## Foundation models

- Foundation models are giant pre-trained transformer models. You fine-tune them for specific tasks, or use them as components in larger (including agentic) systems.
- Well-known examples: GPT-n and DALL-E (OpenAI), Claude (Anthropic), Llama (Meta), DeepSeek, and Amazon Nova.
- **Models available in Bedrock, and what they are for**
  - **Claude (Anthropic):** conversational LLM, question answering and workflow automation. It is the popular choice, and it is what drives complex agentic tasks in tools like Claude Code.
  - **Amazon Nova:** Amazon's own LLM family (e.g. Nova Pro). **Nova Reel** generates video.
  - **Amazon Titan:** text summarisation, generation and Q&A, but mainly **embeddings**: turning text into vectors that capture its meaning, used for personalisation and search. This becomes important with RAG.
  - **Llama (Meta):** another LLM.
  - **Stable Diffusion (Stability AI):** image, art, logo and design generation.
  - **Jurassic-2 (AI21 Labs):** multilingual text generation (Spanish, French, German, Portuguese, Italian, Dutch). It is rarely seen now and matters little for this exam.
- Different models have different strengths and costs, and new, better ones keep arriving. That is the reason for the abstraction layer below.

## What Bedrock gives you

- **One unified API** to invoke chat, text and image models, so models can be swapped in and out. It is multimodal.
- Works with pre-built models, your own fine-tuned models, or your own imported models.
- **Billing:** third-party models (Anthropic, Meta and others) are billed through your AWS bill, but on **their own pricing**, via the AWS Marketplace. Check the pricing page at `aws.amazon.com/bedrock/pricing`, because prices differ a lot between models.
- Built-in support for **RAG** (Knowledge Bases, covered shortly) and for **LLM agents**.
- **Serverless:** no servers or system software to manage.
- Integrates with SageMaker (e.g. SageMaker Canvas) when you want finer control over deployment and tuning. SageMaker has its own section later.
- Usable from the console or through the API.

## The four Bedrock API endpoints

| Endpoint | Purpose | Main operations |
| --- | --- | --- |
| `bedrock` | Manage, deploy and train (fine-tune) models | n/a |
| `bedrock-runtime` | **Inference** against foundation models: run prompts, generate embeddings | `Converse`, `ConverseStream`, `InvokeModel`, `InvokeModelWithResponseStream` |
| `bedrock-agent` | Manage, deploy and train agents and knowledge bases | n/a |
| `bedrock-agent-runtime` | **Inference** against agents and knowledge bases | `InvokeAgent`, `Retrieve`, `RetrieveAndGenerate` |

- The `Stream` variants return output in real time as it is generated.
- `Converse` is the one for chat. `InvokeModel` just runs a model.
- Agents can run in parallel and are given tools: external knowledge and the ability to act on the internet or your machine.
- `Retrieve` and `RetrieveAndGenerate` hit a knowledge base's vector store directly. `Retrieve` returns just the matching knowledge-base content, while `RetrieveAndGenerate` also generates a response from it.

## The Converse API

A unified API for models that support messages (covered in more depth in lecture 10). You give it:

- a **`modelId`**
- your prompt in the **`messages`** field (or an ARN pointing to Prompt Management)
- optionally:
  - model-specific fields
  - guardrails
  - an inference config (max tokens, temperature, top-p, stop sequences)
  - prompt variables
  - tools, for agentic use

## Permissions and model access

- **Use an IAM user, never the root account.** Bedrock may seem to work with root at first, but it will not for long.
- The user needs Bedrock permissions: **`AmazonBedrockFullAccess`** for developing, or **`AmazonBedrockReadOnly`** for just using and reading.
- **Model access:** you used to have to request access to each model, accept its terms and agree to its billing. AWS is phasing this out, so you can use any model in the catalogue and are billed automatically. Lecture 8 covers this.
- Because billing is automatic, **choosing the right model for the job** (not paying for more power than you need) is a big part of optimising these systems later in the course.
