# 190. Evaluation Techniques for Foundation Models

Judging a model that answers open questions in plain language is **hard**: there is no single number for "accurate". **Never test on training data.**

## 1. Human evaluation

People are often the best source of feedback:

- **User experience:** how it feels to use
- **Contextual relevancy and sensitivity:** did it answer what was asked?
- **Creativity and flexibility**
- **Unexpected or complex problems:** does it invent, admit it does not know, or build a useful answer?

**Weakness:** models sound authoritative while being **wrong**, and people can be fooled.

## 2. Benchmark datasets

**Test prompts** with ideal answers written by **subject matter experts**. Your model answers, an **evaluator** compares, and **scores** come out. They may target an application or a skill such as **reasoning**.

| Measure | Question |
|---|---|
| **Accuracy** | How close to the ideal answer? |
| **Speed / efficiency** | How fast? |
| **Scalability** | How does it hold up with more data, users, longer prompts, more context? |
| **Context retrieval** | Is retrieved data (RAG) relevant? |

Useful as **early, offline metrics** before human feedback, and common in model **leaderboards**.

**Weaknesses:** only as good as the test data, and often **contaminated**: if the questions and answers reached the training data, the model has an **open-book exam** (for example coding puzzles).

## 3. A model as judge

A **trusted model** scores your model's responses, using the prompts and evaluation data (answers or retrieved context), on **relevancy, comprehensiveness, accuracy** and more.

- Assumes the judge is **better**; shared flaws pass unnoticed.
- Suits testing **small, efficient models** that aim to approximate a larger one.

## 4. Hybrid

Combine **human** and **benchmark** evaluation. **Disagreement** between them exposes the limits of one or both and shows where to investigate.

## Exam takeaways

1. Know the four approaches: **human, benchmark, LLM judge, hybrid**.
2. **Data contamination** invalidates benchmarks.
3. A judge model must be **trusted**, ideally stronger than the model tested.
