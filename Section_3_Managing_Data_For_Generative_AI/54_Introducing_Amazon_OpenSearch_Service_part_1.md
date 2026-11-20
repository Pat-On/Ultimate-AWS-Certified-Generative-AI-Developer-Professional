# 54. Introducing Amazon OpenSearch Service (part 1)

**Amazon OpenSearch Service** (formerly **Amazon Elasticsearch Service**) is a petabyte-scale search, analysis and reporting engine. It began as a search engine but is now used mostly for analysis and reporting, and for suitable queries can beat tools such as Apache Spark.

## Background

- **OpenSearch** is Amazon's fork of **Elasticsearch** and **Kibana**, created in **September 2021** after Elastic changed Elasticsearch's license. Exam material may still say "Amazon Elasticsearch Service".
- The Elastic Stack comprised Elasticsearch, **Kibana** (visualization) and **Beats** (ingestion). OpenSearch's equivalent of Kibana is **OpenSearch Dashboards**.
- At its core it is a scalable, fast search engine built on **Apache Lucene**, distributed horizontally across nodes. You send JSON requests to index documents and to search them (keywords, attributes, fuzzy matching).
- **Dashboards**: visualize and query data in OpenSearch interactively, like a self-hosted analytics dashboard, without curl commands. A good alternative where data is too large or too sensitive for Google Analytics.
- **Ingestion**: expect **Kinesis** integration on the exam rather than Beats and Logstash (the older Elastic-world tools).

## Use cases and examples

| Use case | Example |
|---|---|
| Full-text search | Mirror Web indexed 1.4 billion documents for the UK government web archive for $337, at 146 million documents per hour (14 times faster than before) |
| Log analytics | Adobe, peaking at over 200,000 API calls per second, with reduced operational overhead |
| Real-time application monitoring | Expedia: Docker logs, root cause analysis, price optimization |
| Security analytics | Centralize and analyze events organisation-wide in real time |
| Clickstream analytics | Hearst: OpenSearch with **Kinesis Data Streams** and **Kinesis Data Firehose**, 30 TB per day from 300+ websites, available to editors within minutes |

## Main concepts

- **Document**: the unit of storage and retrieval; text or structured JSON, with a unique document ID.
- **Type**: defines schema and mapping for a kind of document. Types are being phased out: **one type per index** now, and the type field is greyed out in the new UI. Think in terms of documents and indices. (Elasticsearch 6 questions may still mention types.)
- **Index**: a collection of related documents. It contains an **inverted index** that lets you search everything in it at once.
- **Shards**: an index is split into shards (horizontal scaling). Each document is hashed to a shard, and shards can live on different nodes. Each shard is a self-contained **Lucene index**.
- **Redundancy**: **primary** and **replica** shards (example: two primaries, each with two replicas). Writes go to the primary and are replicated. Reads can be served by primaries or replicas, so the application should spread reads (round robin) across them to increase read throughput.
