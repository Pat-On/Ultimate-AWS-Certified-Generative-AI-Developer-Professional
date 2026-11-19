# 17. Really, don't leave OpenSearch up and running for long!

A cost warning for anyone following along hands-on with the knowledge base from lecture 16.

## What to do

- The Agentic AI section builds on the knowledge base you just created. If you won't get to it soon, **delete both the knowledge base and its underlying OpenSearch Serverless collection**, as shown in the lecture 16 video.
- **Deleting a knowledge base does not delete its underlying vector store.** The collection has to be deleted separately (OpenSearch → Serverless → Dashboard).

## Why it matters

- A collection left running costs on the order of **$200 a month**, even if you don't use OpenSearch Serverless for anything.
- **"Serverless" does not mean "scales to zero"**: it keeps accruing cost while idle.
- You can recreate the knowledge base when you reach the agent lectures.
