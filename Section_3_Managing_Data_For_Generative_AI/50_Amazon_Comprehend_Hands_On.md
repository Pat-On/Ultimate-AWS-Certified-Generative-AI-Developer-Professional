# 50. Amazon Comprehend - Hands On

A console demo of **Amazon Comprehend** analysing a sample message (a financial company telling a customer a minimum payment is due).

## Real-time analysis results

- **Entities**: people, organization, quantities, dates, and an "other" category for unrecognised items. This turns unstructured text into structured data.
- **Key phrases**: the most important phrases in the text.
- **Language**: detected with a confidence score (99% English).
- **PII**: detected person names, credit card account number, bank account number, routing number and a due date. Useful when processing data in batch.
- **Sentiment**: neutral at 99% confidence for this informational text. Useful, for example, for judging the quality of support agent and customer interactions.
- **Targeted sentiment**: how sentiment is built up around specific entities.
- **Syntax**: grammatical analysis (nouns, proper nouns, punctuation).
- **Analysis jobs** process large amounts of data from **S3**.

## Custom classification

- You create custom categories (for example billing, product support, feature request, account problem) and Comprehend classifies incoming text accordingly.
- Training data is a **CSV file** of example texts and their labels, stored in S3. At least **10 documents per class** are needed; more is better.
- Train the classifier, then purchase a **custom endpoint** to run real-time classification requests.
