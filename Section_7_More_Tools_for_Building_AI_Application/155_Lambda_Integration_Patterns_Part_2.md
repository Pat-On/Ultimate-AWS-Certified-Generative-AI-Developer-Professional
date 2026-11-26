# 155. Lambda Integration Patterns, Part 2

## S3 → Lambda → OpenSearch

**Amazon OpenSearch Service** (which branched from Elasticsearch) is a search engine that also works for analytics and visualisation, such as a home-grown web analytics tool over server logs.

An S3 data lake **cannot be connected to it directly**. New data in S3 triggers Lambda, which transforms it into the shape OpenSearch expects and loads it in **near real time**.

## S3 → Lambda → Data Pipeline

Data Pipeline normally runs on a **schedule** (with a precondition checking for new data in S3). If data arrives at **unpredictable times**, let S3 trigger Lambda and have Lambda **start the pipeline on demand**.

(AWS has since put **Data Pipeline** into maintenance and closed it to new customers; it can still appear in course material.)

## S3 → Lambda → Redshift

- Best practice for loading Redshift is the **`COPY`** command.
- Use Lambda when new data can **arrive at any time** and should load automatically.
- Lambda is **stateless**, so keep track of **what has been loaded** in **DynamoDB** (which files, when, into which table). Lambda batches the new files and loads them with `COPY`.

## Kinesis → Lambda: the pitfalls

The function receives an event with a **batch** of stream records.

| Fact | Consequence |
|---|---|
| **Batch size** is set on the trigger, up to **10,000 records** | Too large a batch can cause **timeouts** |
| Maximum run time is **900 seconds** | A slow batch fails and the stream **backs up** |
| **Payload limit of 6 MB** | Larger batches are **split** |
| A failed batch is **retried until it succeeds or the data expires** | Unhandled errors **stall the shard** |
| Each shard is processed **synchronously** | The batch must be finished quickly |

**Mitigation:** handle errors properly, and use **more shards** so one failure does not hold up everything.

**Correction:** the lecture says the default timeout is 900 seconds. 900 seconds is the **maximum**; the default is **3 seconds**.

**Beyond the lecture:** the trigger also offers splitting a failed batch, limits on retries and record age, a destination for failed records, and a parallelisation factor per shard.

## Exam takeaways

1. S3 to OpenSearch needs **glue**, and Lambda is it.
2. Lambda has **no state**: track progress in **DynamoDB**.
3. Kinesis: know **10,000 records**, **6 MB**, **15 minutes**, retry until expiry and the **stalled shard**.
