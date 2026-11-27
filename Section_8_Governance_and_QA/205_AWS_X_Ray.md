# 205. AWS X-Ray

**Distributed tracing** with a **visual service map**. Debugging production from scattered logs is painful, especially with many microservices; X-Ray shows how requests flow and where they fail.

## Benefits

- Find **performance bottlenecks**
- Understand **dependencies** between services and pinpoint the faulty one
- See how each **request** behaves, with its **errors and exceptions**
- Check **latency SLAs**, find what **slows or throttles**, and which **users** are affected
- Graphical, so non-technical people can help troubleshoot

Works with **Lambda, Elastic Beanstalk, ECS, ELB, API Gateway, EC2** and any application server, including **on premises**.

## Tracing

| Term | Meaning |
|---|---|
| **Trace** | One request followed end to end |
| **Segments / subsegments** | What each component adds to the trace |
| **Annotations** | Extra information attached to traces |
| **Sampling** | Trace every request, a percentage, or a number per minute |

Security: **IAM** for authorisation, **KMS** for encryption at rest.

## Enabling X-Ray (exam favourite)

1. **Code:** import the SDK and the **X-Ray SDK** (Java, Python, Go, Node.js, .NET). Small code changes; it captures calls to AWS services, HTTP/HTTPS requests, database calls (MySQL, PostgreSQL, DynamoDB) and queue calls.
2. **Daemon or integration:**
   - **EC2 / on premises:** install the **X-Ray daemon** (Linux, Windows, macOS). It receives **UDP** packets and sends batches to X-Ray **every second**.
   - **Lambda and other integrated services:** AWS runs the daemon for you.
3. **IAM:** the application needs permission to write to X-Ray.

AWS has announced that the X-Ray SDKs and daemon are moving to maintenance mode in favour of **OpenTelemetry**; check the current documentation.

## Troubleshooting

| Where | Check |
|---|---|
| Works locally, **not on EC2** | The **daemon** is running on the instance, and the **IAM role** has permission |
| **Lambda** | **Execution role** with the right policy, X-Ray SDK imported in the code, **active tracing** enabled |

## Exam takeaways

1. Tracing across services → **X-Ray**.
2. EC2 needs **code changes + daemon + IAM role**.
3. Lambda needs **IAM role + SDK + active tracing**.
