# 154. Lambda Integration Patterns, Part 1

## Why not just run a server?

- **No server management:** AWS handles patching, monitoring and hardware failures.
- Single servers are cheap, but a **fleet sized for peak** load pays for a lot of idle time. With Lambda you **pay only for the processing time you use**.
- It eases splitting work between **front-end** and **back-end** teams.

## Main uses

| Use | Example |
|---|---|
| **Real-time file processing** | A new object in S3 triggers processing |
| **Real-time stream processing** | Consume Kinesis streams or Firehose |
| **ETL** | Extract, transform and load incoming data |
| **Cron replacement** | Run on a **schedule** (every minute, hour, day), for example to start batch jobs |
| **AWS events** | React to events from many AWS services |

**Languages:** Node.js, Python, Java, C#, Go, PowerShell, Ruby.

## Triggers

Many services can invoke Lambda (Alexa among them), and you can also invoke it manually.

| Trigger | Behaviour |
|---|---|
| **S3** | An object event (for example, creation) invokes the function, which might load the data into Redshift |
| **DynamoDB** | Table changes invoke it for event-driven processing |
| **Kinesis Data Streams** | Lambda **polls** the stream and reads records in **batches**. The stream does **not push** |
| **Firehose** | Lambda **transforms** records before delivery to S3, Redshift, OpenSearch and others |
| **IoT** | Device data invokes the function |
| **SNS, SQS** | Also common sources |

Downstream there is no limit: every AWS service has an API your code can call.

## Exam takeaways

1. **Pay per use** and no servers are the reasons to choose Lambda.
2. It can replace **cron**.
3. With **Kinesis**, Lambda **polls** the stream, even though diagrams suggest a push.
