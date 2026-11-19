# 25. Hands-On with Bedrock Guardrails

A walk-through of creating a guardrail in the console and testing it. The UI changes often, so things may not be where the video shows them. Guardrails are under **Build**.

## Basics

- Give the guardrail a **name** and optionally a description.
- **Blocked message:** the default message returned when something is blocked (for example "Sorry, the model cannot answer this question"). You can use the same message for everything, or customise it per kind of block.
- **Cross-region inference:** off by default. It helps reliability and throughput because you are not limited to one region's resources. Newer features often **require** it, and there is little reason not to use it these days.
- **KMS key:** optional, if you want to use your own.

## Filters

- **Harmful content categories** (hate speech, insults and so on):
  - Set a **threshold** for each category. Keeping them high blocks more.
  - It can also check **images as well as text**, if your application accepts or produces images.
- **Prompt attacks:** catches attempts to override your instructions ("ignore all previous instructions and ...").
  - Choose to **block** or just **detect**, and set a threshold (the demo uses medium).
  - It is off by default because it can produce **false positives**.
- **Content filter tier:** **Classic** (older model, English, French and Spanish only) or **Standard** (newer, more languages, but it **requires cross-region inference**).
- **Denied topics:**
  - Add a topic with a **definition** and a few **example phrases**, and choose block or detect separately for **input** and **output**.
  - Demo: "No politics", with examples like "Should I vote Democrat or Republican?" and "Tell me about the Supreme Court decision yesterday", which is deliberately not obviously political.
- **Word filters:** a built-in **profanity** list, plus your own **custom words** (the demo blocks "potato"). Each can apply to input and/or output.
- **Sensitive information (PII):**
  - Choose which types to handle (the demo selects all except name) and, for each, to **mask** or **block**. The demo masks.
  - You can also add **custom patterns** (regular expressions) for your own kinds of sensitive data.
- **Contextual grounding check:**
  - **Grounding:** whether a response built from knowledge base content is actually based on it.
  - **Relevance:** whether the response is relevant to the original prompt.
  - Each has a threshold and block or detect. False positives are possible, so it needs tuning, which is why it is not on by default.
- **Automated reasoning checks:** checks the **reasoning** of a reasoning model, in the manner of an LLM as a judge. **Currently only in detect mode**, so it reports and does not block. Not used in the demo.

## Testing

- Pick a model to converse with (the demo uses an Anthropic model) and run prompts.
- "I really like a potato right now" was **blocked** with the configured message. Viewing the **trace** shows the **word filter** for "potato" triggered it.
- A political prompt was also blocked, and the trace shows the **"no politics" denied topic** tripped it.

## Cost and cleanup

- Guardrails don't cost much to leave running, and a guardrail is used in an agent example later in the course.
- If you will be away from the course for a while, delete it and recreate it later.
