# 2. Course Overview

Instructor: Frank Kane. The course covers the official exam guide plus the AWS training materials and Skill Builder, but it is **not organised by exam domain**. The domains overlap a lot, so the material is arranged to build up from fundamentals with less repetition.

## What the course covers

- **Generative AI fundamentals and Amazon Bedrock (Section 2)**
  - Foundation models (Amazon Nova, Titan, Claude and others).
  - Fine-tuning and how the training data is formatted.
  - Retrieval-augmented generation (RAG): Bedrock Knowledge Bases backed by vector stores, which hold embeddings that capture the meaning of text chunks. RAG injects ground-truth data to customise a system and reduce hallucination.
  - Guardrails, prompt management and optimisation, Bedrock Flows (chaining prompts and systems), and enterprise integration.
- **Managing data for GenAI (Section 3)**
  - Getting data into the vector store: transforming and structuring it with Bedrock data analysis (extracts structured data from unstructured data), SageMaker Data Wrangler, Transcribe, Comprehend and AWS Glue (ETL), monitored with CloudWatch.
  - A deep dive into **OpenSearch**, the main RAG and knowledge-base store for this exam, including tuning it for GenAI workloads.
  - Alternative vector stores (RDS, Aurora), connecting DynamoDB to OpenSearch, and S3 lifecycle management. S3 basics are assumed.
- **Agentic AI (Section 4)**
  - Agents in Bedrock and multi-agent workflows.
  - Strands Agents (a Python SDK).
  - **AgentCore**, Amazon's newest service for deploying agents to production at scale, with built-in memory and tools.
  - Human-in-the-loop patterns and the Amazon Q family of agentic developer tools.
- **Operational efficiency and optimisation (Section 5)**, a big exam topic
  - Context management and token efficiency.
  - Picking the right model per workload, so smaller models handle simpler prompts at runtime.
  - Resource utilisation and throughput, caching, and responsive, resilient design.
  - Foundation-model performance tuning and resource allocation.
  - Bedrock cross-region inference, which spreads load and is essential for some applications.
- **Managing models with SageMaker AI (Section 6)**, an alternative to Bedrock that gives more control and can deploy any ML model
  - Processing, training and deploying models.
  - Safe rollout and rollback of deployments.
  - Ground Truth (labelled data), Model Monitor (drift), Clarify (explainability), Model Registry, lineage tracking, Neo (edge) and Pipelines.
- **More tools for building AI applications (Section 7)**
  - Lambda, API Gateway (the front door), AppConfig (change behaviour on the fly), Step Functions (e.g. circuit breakers for failure cases) and EventBridge (event triggers).
  - CodeBuild, CodeDeploy and CodePipeline, AppSync, Outposts and Wavelength (enterprise integration), an event-driven buffer between incoming data and the app, and Amplify for the front end.
- **Governance and QA (Section 8)**
  - Bedrock prompt management, agent tracing, evaluating GenAI and agent applications, and responsible AI.
  - CloudWatch, CloudTrail (audit trail), X-Ray and Lake Formation (data access control).
- **Security, identity and compliance (Section 9)**
  - IAM, KMS, Macie (sensitive data), Secrets Manager and Cognito (user login).
  - VPC and PrivateLink. Much of this will be familiar from other certifications, here applied to GenAI.
- **Other services you should know (Sections 10-18)**, the appendices
  - Analytics, compute, containers, customer engagement, database, developer tools, machine learning, management and governance, networking and content delivery, and storage.
  - Not GenAI services themselves, but they are explicitly in scope and do show up in practice exams and Skill Builder.
  - Skip any you already know well. Some content is reused from other courses by the same instructor.

## About the exam

- It **replaces the Machine Learning Specialty exam**, which is being phased out in early 2026. That exam was mostly classical ML.
- It is **professional level**: complex real-world scenarios with detailed requirements, where you pick the best solution. These are not simple "what does this service do?" questions, so you need to understand how the pieces fit together.
- Helpful background:
  - **Machine Learning Engineer Associate** is the closest certification.
  - AI Practitioner helps with the business focus.
  - Data engineering knowledge is explicitly out of scope but still helps in understanding how systems come together.
  - There is little overlap with the instructor's other prep courses, apart from the appendices.

## Who it is for

- **Target candidate (per AWS):** 2+ years of AWS and ML/AI experience and 1+ year of hands-on experience implementing GenAI solutions.
- **Not a first certification.** The AWS basics (S3, IAM, storage, security) are assumed. If they are new to you, take Cloud Practitioner first.
- **Not required:**
  - Model development and training. You only need to know how to *use* foundation models.
  - Classical ML.
  - A data or feature engineering background, though data pipelines and data manipulation do appear in the exam.
