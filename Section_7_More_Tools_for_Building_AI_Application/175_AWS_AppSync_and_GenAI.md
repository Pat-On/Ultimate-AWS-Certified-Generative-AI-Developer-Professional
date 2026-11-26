# 175. AWS AppSync and GenAI

**AppSync** is a **serverless** service for **GraphQL** (and pub/sub) APIs. GraphQL, developed at Facebook, queries **several data sources** and returns the result as a **graph** (nodes and connections).

- Custom business logic lives in **resolvers** between the schema and the data source, in **JavaScript or TypeScript**.
- It translates requests to the data source with **VTL** (Apache Velocity Template Language) mapping templates.

## Generative AI use

A resolver calls a **Lambda** function that invokes a **foundation model** for **real-time inference**, so model output can be served through GraphQL.

## Exam takeaway

**GraphQL on AWS = AppSync**, with **Lambda resolvers** for model inference.
