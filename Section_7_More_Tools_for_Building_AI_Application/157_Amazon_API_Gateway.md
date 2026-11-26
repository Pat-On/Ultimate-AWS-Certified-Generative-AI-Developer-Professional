# 157. Amazon API Gateway

Clients could invoke a Lambda function directly (they would need **IAM permissions**) or through an **Application Load Balancer** (an HTTP endpoint). **API Gateway** is a serverless way to publish **REST APIs** with far more features. With Lambda behind it there is **no infrastructure to manage**.

## Features

- **WebSocket** support for real-time streaming
- **Versioning** (v1, v2) without breaking clients
- **Stages** such as dev, test and prod
- **Authentication and authorisation**
- **API keys** and **request throttling**
- Import and export **Swagger / OpenAPI 3.0**
- **Request and response transformation and validation**
- **SDK** and specification generation
- **Response caching**

## Integrations

| Integration | Use |
|---|---|
| **Lambda function** | The most common, easiest serverless REST API |
| **HTTP** | Front an on-premises API or a load balancer to add rate limiting, caching, authentication, API keys |
| **AWS service** | Expose **any AWS API**: start a Step Functions workflow, post to SQS, with authentication and rate control |

**Example:** client → API Gateway → **Kinesis Data Streams** → **Firehose** → **S3** (JSON files). Clients send data without ever holding **AWS credentials**.

## Endpoint types

| Type | For | Detail |
|---|---|---|
| **Edge-optimized** (default) | **Global** clients | Routed through **CloudFront edge locations** for lower latency; the API still lives in **one region** |
| **Regional** | Clients in the **same region** | You can add your own CloudFront distribution for more control over caching |
| **Private** | **Inside your VPC** only | Reached through an **interface VPC endpoint** (ENI); access set with a **resource policy** |

## Security

| Method | For |
|---|---|
| **IAM roles** | Internal applications, such as code on EC2 |
| **Cognito** | External users, such as web and mobile |
| **Custom authorizer** | Your own logic in a **Lambda function** |

**Custom domain with HTTPS** uses **AWS Certificate Manager (ACM)**:

- **Edge-optimized:** certificate must be in **us-east-1**.
- **Regional:** certificate must be in the **API's region**.
- Point the domain at the API with a **CNAME** or **A-alias** record in **Route 53**.

## Exam takeaways

1. Know the three **endpoint types** and the **certificate region** rule.
2. Pick the authentication method by audience: **IAM** internal, **Cognito** external, **Lambda authorizer** custom.
3. API Gateway can call **AWS services directly**, with no Lambda in between.
