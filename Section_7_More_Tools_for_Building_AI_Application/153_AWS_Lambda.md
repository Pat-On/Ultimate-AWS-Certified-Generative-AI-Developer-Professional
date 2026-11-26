# 153. AWS Lambda

**Lambda** runs snippets of code in the cloud **without you managing servers**. You care about what the code does; AWS handles execution and **scales automatically** with the incoming load.

- Typically small, **stateless** pieces of code.
- Often the **glue** between services that do not talk to each other directly: get triggered, reshape the data, pass it on.

## Example: serverless website

Static HTML with AJAX calls can be served from **S3**, with no servers of your own.

- **Login:** client → **API Gateway** → **Lambda** → **Cognito**, which returns a token that Lambda sends back.
- **Chat history:** client → API Gateway → Lambda → **DynamoDB** query for that user ID → back to the client.

## Example: order history app

Logs → **Kinesis Data Streams** → **Lambda** → **DynamoDB** → mobile client.

Lambda replaces a consumer application running on **EC2**. Each trigger delivers a **batch** of records; the function extracts each one and writes it to DynamoDB.

## Example: transaction rate alarm

Logs → Kinesis Data Streams → stream analytics → Kinesis Data Streams → **Lambda** → **SNS**, which sends a message to your phone when something unusual happens.

(The slide calls the analytics step **Kinesis Data Analytics**; AWS has since renamed it **Amazon Managed Service for Apache Flink**.)

## Exam takeaways

1. **Lambda** = serverless code execution with automatic scaling.
2. Its classic role is **glue** between services: reformat and forward data.
3. Common chain for a serverless API: **API Gateway → Lambda → DynamoDB** (or Cognito for authentication).
4. Anything you can code, a function can do, including calling services **outside AWS**.
