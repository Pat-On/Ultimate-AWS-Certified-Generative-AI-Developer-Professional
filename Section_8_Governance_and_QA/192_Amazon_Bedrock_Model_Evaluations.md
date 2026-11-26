# 192. Amazon Bedrock Model Evaluations

## Automatic evaluation

For the more objective tasks, with **built-in task types, datasets and metrics** (or your own datasets).

| Task | Examples of what is measured |
|---|---|
| General text generation | Real-world knowledge, **word error rate**, **toxicity** |
| Summarisation (Gigaword dataset) | **BERTScore**, toxicity |
| Question answering | Accuracy, robustness, toxicity |
| Text classification (women's e-commerce clothing reviews) | Accuracy, robustness |

## Human evaluation

For subjective judgements: people **compare two models or variants** on your prompt dataset and pick the better answer. Work team: your own (**Amazon Cognito**), **SageMaker Ground Truth** or **Amazon Augmented AI**.

## Model as a judge

A **generator** model is judged by an **evaluator** model, using your **prompt dataset**.

## RAG evaluation jobs

| Type | Measures |
|---|---|
| **Retrieve only** | Quality of retrieval: **context relevance and coverage** |
| **Retrieve and generate** | End to end: **correctness, completeness, helpfulness, logical coherence** and more |

- The prompt dataset goes in **S3** in **JSON Lines** format.
- **Custom metrics:** describe them in a prompt and the judge model scores them.

## Exam takeaways

1. Three modes: **automatic, human, LLM as judge**.
2. RAG: **retrieve only** vs **retrieve and generate**.
3. Datasets in **S3 as JSON Lines**.
