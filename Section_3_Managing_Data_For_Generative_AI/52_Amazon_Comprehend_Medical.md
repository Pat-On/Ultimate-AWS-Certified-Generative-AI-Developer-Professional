# 52. Amazon Comprehend Medical

**Amazon Comprehend Medical** is a **HIPAA-eligible** variant of Comprehend for medical use. HIPAA is the US framework of rules for protecting patient privacy.

## Capabilities

- Pre-trained to extract health data from documents: prescription information, medical procedures, diagnoses, and any **protected health information (PHI)**, returned as entities.
- A separate API for PHI: call **DetectPHI** instead of DetectEntities to get only protected health information.
- Can search for specific **medical ontologies** (sets of medical terminology).
- Input: individual documents passed directly to the API, or a batch of documents in **S3**.
- Security: integrates with **VPC endpoints** and **PrivateLink**.

## Relevance to generative AI

For a medical AI application, use it to scrub PHI:

- as post-processing, to detect and redact PHI in outputs,
- on input prompts,
- on data used as context for RAG in knowledge bases.
