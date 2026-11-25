# 130. Intelligent Caching Systems for GenAI

Caching avoids redoing expensive work for repeated requests. With generative AI the difficulty is that the same question can be worded in countless ways, so there are three kinds of cache to know.

## Semantic caching

Cache the **meaning** of the prompt, not its text.

1. When a prompt arrives, create an **embedding vector** for it.
2. Look for a matching or **close** embedding in the cache. On a **hit**, return the cached response and **skip the foundation model**. On a **miss**, call the model and cache the result.

- **Where to store it**: **ElastiCache for Valkey** or **MemoryDB** (in-memory vector stores). **OpenSearch** also works.
- **AWS reference architecture**: **API Gateway** receives the prompt, a **Lambda** function creates the embedding and checks the cache (ElastiCache), and the model is called only on a miss.
- **Risks**:
  - **Tune the similarity threshold** carefully. Embeddings are not perfect, and a wrong match gives an irrelevant answer, which is a bad user experience.
  - The **overhead** (cache, embeddings) must not outweigh the benefit. With few hits the extra infrastructure is not worth it.
- It can **dramatically improve latency** when users ask the same things repeatedly.

## Prompt caching

Built into **Bedrock** for most newer supported models. You cache a **prompt prefix**.

- Put the **static** parts first: system instructions, **few-shot examples**, attached documents. Put the **dynamic** content (what the user typed) at the end. A **cache checkpoint** separates the two.
- The cached prefix is not tokenized again each time, and cached tokens are **discounted per token**. Repeatedly queried **uploaded documents** can sit in the prefix instead of being embedded again.
- **Trade-off**: cache **writes cost more**, reads cost less. With too few hits it can cost more than it saves. Measure it.
- **CloudWatch** records cache reads and writes. It can also be enabled in **Bedrock Prompt Management**.

## Edge caching

Use **CloudFront** (normally in front of S3 or website content, with edge locations worldwide) for GenAI applications to cut latency and back-end requests.

- Prompts are dynamic, so **fingerprint** them: a deterministic **hash of the request** goes in a **GET** request (for example `GET /ask?fingerprint=<hash>`), so CloudFront can cache the response. This suits an application that picks from a menu of known prompts.
- Results can be fingerprinted too, to encode when a result is valid for a given set of model configuration values.
- It is a poor fit for **personalized output**. Set an appropriate **TTL** if responses change.
- Cache **images and other static content** on the edge as well.

## Exam takeaways

1. **Semantic caching** = cache by embedding similarity, stored in **ElastiCache for Valkey, MemoryDB or OpenSearch**. Tune the similarity threshold and check the overhead is worth it.
2. **Prompt caching** = cache a **static prefix** up to a **cache checkpoint**, with dynamic content last. Reads are discounted but writes cost extra.
3. **Edge caching** = **CloudFront** with a **request fingerprint** in a GET, a good TTL, and no personalized responses.
