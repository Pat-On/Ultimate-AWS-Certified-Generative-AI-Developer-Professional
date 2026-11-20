# 49. Amazon Comprehend

**Amazon Comprehend** is a fully managed, serverless **natural language processing (NLP)** service that uses machine learning to find insights and relationships in text.

## Built-in capabilities

- Detects the language of the text.
- Extracts key phrases, places, people, brands and events.
- Determines how positive or negative the text is (**sentiment**).
- Tokenization and part-of-speech analysis.
- Organises a collection of documents by **topics** that it discovers itself.
- Use cases: analyse customer emails to find what drives positive or negative experiences, and group articles by topic.

## Named entity recognition (NER)

- Out of the box, extracts predefined general-purpose entities (people, places, organizations, dates and other standard categories) from text.

## Custom models

- **Custom classification**: you define the categories (for example support request, billing request, complaint). Supply training data in **S3**; Comprehend builds and trains a custom classifier. Supports text, PDF, Word and images as documents. Works in real time (single document) or asynchronously (batches and large jobs).
- **Custom entity recognition**: for business-specific terms and noun phrases (for example policy numbers or phrases signalling customer escalation). Train with a list of entities and documents containing them. Real-time or asynchronous analysis.
