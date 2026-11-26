# 183. Amazon EventBridge

Formerly **CloudWatch Events**.

## Two triggers

- **Schedule:** cron-style, for example run a Lambda function every hour.
- **Event pattern:** react to what a service does, such as a **root user sign-in** (notify through SNS).

## Flow

**Source** → optional **filter** (for example one S3 bucket) → a **JSON event** with details → **destination**.

| Sources | Destinations |
|---|---|
| EC2 state changes, failed CodeBuild builds, S3 events, Trusted Advisor findings, **any API call through CloudTrail**, schedules | Lambda, Batch, ECS task, SQS, SNS, Kinesis Data Streams, Step Functions, CodePipeline, CodeBuild, SSM, EC2 actions |

## Event buses

| Bus | Receives |
|---|---|
| **Default** | Events from AWS services |
| **Partner** | Events from SaaS partners (Zendesk, Datadog, Auth0) |
| **Custom** | Events from your own applications |

## More features

- **Archive** events (all or filtered, forever or for a period) and **replay** them, useful after fixing a bug.
- **Schema Registry:** infers event schemas, **versions** them and **generates code**.
- **Resource-based policy** per bus: allow or deny other accounts and Regions, for example a **central bus** that collects an organisation's events with `PutEvents`.

## Exam takeaways

1. **Schedules and event-driven rules** = EventBridge.
2. API call reactions = **EventBridge + CloudTrail**.
3. Know **bus types**, **archive/replay**, **Schema Registry**, **cross-account policies**.
