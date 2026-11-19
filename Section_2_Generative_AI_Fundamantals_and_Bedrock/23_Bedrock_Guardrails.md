# 23. Bedrock Guardrails

Guardrails are an important Bedrock feature for AI safety, governance and security. They provide **content filtering for both prompts and responses**: for anything going into or out of a Bedrock system (a knowledge base, an agent or anything else), a guardrail checks that users aren't saying things you don't want in, and that the system isn't saying things you don't want out.

## What a guardrail can do

- **Works with text foundation models** (for example Titan or Claude). Image models are not supported at the moment.
- **Word-level and topic-level filtering:** block specific topics (religion, politics, your competitors, whatever you choose) or specific words.
- **Content filtering by category:** automatic filters for objectionable content along dimensions such as hateful or biased content. The hands-on lecture shows these.
- **Profanity filter:** switch it on and Bedrock already knows the words, so you don't type them in.
- **PII removal or masking:** choose which kinds of personally identifiable information to catch (phone numbers, Social Security numbers, driver's licence numbers, addresses and so on). You can **remove** it or **mask** it, for example replace an address with a bracketed placeholder. This is a very good feature for making sure no PII leaks out of your system in responses.

## Contextual grounding check

A newer feature, intended to **help prevent hallucination**. It measures two things, and you set a **threshold** for each, below which the result is filtered out:

- **Grounding:** how similar the response is to the contextual data that was retrieved. In a knowledge base or RAG system, if the model made things up that aren't in the documents you provided, grounding is low. If the response wasn't really based on those documents and the model "went off and made up its own thing" from its earlier training, you can filter it out.
- **Relevance:** how relevant the response is to the original query. An answer that doesn't address the question can be filtered out.

Caveats:
- These are **not perfect metrics**. They are only as good as what your vector store retrieves: if retrieval returns irrelevant information, the check works less well.
- It is a way to estimate whether the answer is relevant and correct given the data you supplied.

## Where it applies

- **Agents and knowledge bases:** attach a guardrail to either, and it is applied automatically to **all prompts and responses**.
- **Blocked message:** you can configure the message the user sees when something is filtered out.

The next lectures cover automated reasoning checks (lecture 24) and a hands-on guardrail (lecture 25).
