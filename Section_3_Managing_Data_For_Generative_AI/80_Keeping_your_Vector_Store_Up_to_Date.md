# 80. Keeping your Vector Store Up to Date

**Amazon EventBridge** triggers the pipelines that keep a vector store in sync with changing source data, covering incremental updates, change detection and periodic index rebuilds.

## What has to be handled

- Incremental updates.
- Real-time change detection.
- Automated synchronisation.
- Scheduled refresh pipelines.
- Source data keeps being added, deleted and changed, so the embeddings must follow.

## Keeping data in sync

- A change is signalled by an **S3 event**, a **webhook** from a third-party system, or **polling** scheduled in EventBridge.
- **EventBridge** picks up the event and starts a **Lambda function** (the connector).
- Lambda retrieves the changed data and feeds it to the **Bedrock knowledge base**, invoking **ingestion** of the new data.
- If changes are very frequent this does not scale well. Options when immediate updates are not needed:
  - Put **AWS Batch** in the middle as a buffer.
  - Use an event-driven buffer such as **SQS or Kafka** between Lambda and the data store.

## Index maintenance

- Over time **drift and fragmentation** reduce the performance of the store as the underlying data changes.
- Rebuild the index periodically:
  1. **EventBridge** schedules a periodic trigger.
  2. It calls **AWS Batch** to queue a job.
  3. The job creates new embeddings, builds a new vector database and **validates** it.
  4. **Swap the aliases** so the new store replaces the old.

## Exam takeaways

1. **EventBridge** is the trigger for both change-driven updates and scheduled rebuilds.
2. Typical sync path: event, EventBridge, **Lambda**, Bedrock knowledge base ingestion.
3. For frequent changes, buffer with **AWS Batch, SQS or Kafka**.
4. Fix **drift and fragmentation** by rebuilding the index with a scheduled **EventBridge to AWS Batch** job, validating, then swapping aliases.
