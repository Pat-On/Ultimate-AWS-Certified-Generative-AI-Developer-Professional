# 9. Hands-On with the Bedrock Playground

The Bedrock playground is a common UI over the many foundation models. You use it to get a feel for each model's strengths and weaknesses by trying different prompts and settings. In the console it is under **Bedrock → Test → Playground**.

## Choosing a model

- Models have different capabilities, so read the **model cards**. You can also filter the list by the **input** and **output** modalities a model supports.
- The demo uses **Claude Haiku 4.5**: text and image input, text output, 200K-token input limit. It is one of the few models available in the Udemy AWS lab environment.
- Anthropic models currently prompt you for a **use-case submission** on first use. It is approved straight away, as AWS is only collecting data. See lecture 8.

## Chat mode

- Chat is the default, as in a typical AI app: earlier messages stay in the context, so you can refer back to them.
- **Files as context:** upload a document (the demo uses the astronomy club bylaws Word file from the course materials) and ask questions about it. For example, the quorum for an annual election came back as 15 members plus two board members.

## Configuration options

The settings sit behind the configuration icon, and each model has its own set.

- **System prompt:** overarching instructions that apply to the whole conversation (the demo uses "always talk like a pirate").
- **Model reasoning:** controls how deeply the model thinks. It breaks a complex request (e.g. "plan my retirement") into smaller chained steps. The trade-off is **more tokens, so higher cost**.
- **Maximum output tokens:** caps response length, keeping answers terse and **controlling cost**, since the API bills per token.
- **Stop sequences:** custom sequences that end the output, for special formatting needs.
- **Randomness and diversity**
  - **Temperature:** how random the choice of the next token is. The default is 1. Lower is more deterministic, higher gives more variance ("creativity").
  - **Top P:** only candidates within a cumulative probability threshold are considered.
  - **Top K:** only the K most likely candidates are considered.
  - Temperature and Top P were greyed out for Haiku, so support varies by model.
- **Guardrails:** filter unwanted topics or words and protect PII, using the Guardrails API (covered later).
- **Prompt caching:** if your prompts repeatedly reuse the same text (instructions, a system prompt), cache those tokens. You still pay, but at a **cheaper rate**, so it saves money.

## Single prompt mode and compare mode

- **Single prompt mode** drops the chat history. Haiku does not support it, so use something like Amazon Nova.
- **Compare mode** runs the same prompt against two models side by side.
  - Each model has its **own separate configuration**, so match the settings (e.g. the output-token limit) for a fair comparison.
  - The demo compares Haiku with AI21's Jamba 1.5 Large. Jamba does not support images, and it gave a decent answer within the token limit.

## Other modalities

- Filter the model list by output type to try image, audio or video models. At recording time the image choices were only legacy models that did not work, and audio and video were limited to Nova 2 Sonic. This will differ for you.
- **Image models** (e.g. Nova Canvas) have different settings from text models:
  - Actions: generate an image, make variations of an uploaded image, remove or replace objects, replace or remove the background, and virtual try-on.
  - **Negative prompt:** what to avoid (e.g. "no blue chickens").
  - **Image size**, which is hard to control in chat APIs.
  - **Colour palette** for branding, and a **conditioning image** to show the style you want.
  - **Prompt strength:** how strictly to follow the prompt, another creativity lever.
  - **Seed:** reuse the same seed for similar results each time.

## Prompt routers

- Besides the serverless model providers you can select a **router**, such as the Nova prompt router or the Anthropic prompt router.
- The router looks at your prompt and judges how capable a model it needs:
  - a simple request goes to a cheaper model (Nova Lite, Haiku)
  - a complex one goes to a bigger model (Nova Pro, Claude Sonnet)
- **Benefit:** it can save a lot of money.
- **Risk:** if it routes a complex prompt to a lighter model, the results suffer.
