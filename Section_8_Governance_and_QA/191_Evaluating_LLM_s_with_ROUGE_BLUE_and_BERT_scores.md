# 191. Evaluating LLMs with ROUGE, BLEU, and BERT Scores

All three compare model output with an **ideal (ground truth) answer**.

## ROUGE

For **summarisation** and **machine translation**: counts **overlapping units** (words, n-grams, sentence fragments).

| Variant | Compares |
|---|---|
| **ROUGE-1** | Unigrams (single words) |
| **ROUGE-2** | Bigrams (word pairs) |
| **ROUGE-N** | N words at a time |
| **ROUGE-L** | **Longest common subsequence**: good for **coherence and word order** |

**Example:** reference "Certified AI Practitioner", output "Certified ML Practitioner".

- ROUGE-1 = **2/3** (Certified, Practitioner match)
- ROUGE-2 = **0** (no shared word pair)

## BLEU

Mostly for **machine translation**, against a human translation.

- Measures **precision** of n-grams (ROUGE is about **recall**).
- Works sentence by sentence.
- **Brevity penalty** for overly short output.
- Limited at judging **fluency and grammar**.

**Clarification:** the lecture's wording is muddled. **Precision** = how much of the **output** appears in the reference. **Recall** = how much of the **reference** appears in the output.

## BERTScore

Compares **embedding vectors** from **BERT** (a language model that predates GPT), so it measures **semantic similarity**.

- **Less sensitive to synonyms and paraphrasing**.
- Judges meaning rather than exact wording.

## Exam takeaways

| Metric | Remember |
|---|---|
| **ROUGE** | Overlap, **recall**, summaries |
| **BLEU** | **Precision**, translation, brevity penalty |
| **BERTScore** | **Meaning** through embeddings |
