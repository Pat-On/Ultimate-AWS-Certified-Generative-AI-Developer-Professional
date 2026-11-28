# 206. AWS X-Ray - Hands On

## Where X-Ray lives

- The X-Ray views are now in the **CloudWatch console** (service map and traces), next to metrics, logs and alarms.
- The **older X-Ray console** still holds settings the new one lacked at recording time: **sampling, encryption, groups**.

## Deploy the demo app

1. **CloudFormation** → create a stack from the simplified **Scorekeep X-Ray** template (the lecturer's own version, as the AWS demo did not work for them).
2. Choose the **VPC** and **two subnets**; keep other defaults, acknowledge and submit.
3. The stack creates an **ECS** cluster (front end and back-end API instrumented with X-Ray) on `t2`/`t3.micro`, an Auto Scaling group, an execution role, several **DynamoDB** tables and **SNS**.
4. Open the **load balancer URL** from the stack **outputs**, create a game (tic-tac-toe) and play to generate traces.

## Service map

- Shows the **components and their dependencies**, built from the calls made: ECS container, DynamoDB tables, SNS topic.
- A node with **errors is highlighted** (in the demo, **SNS** failed 100% of the time).
- Click a node for **latency, request count, faults** and the **response time distribution**.

## Traces

- **View traces**, then run a query; **filter by node** to narrow it (21 traces down to 10 for one table).
- Response time graphs show the slow requests (most under 200 ms, one over 500 ms).
- One trace shows its **own trace map** and a **timeline of each call** (one `POST` made several DynamoDB calls).
- **Segment details:** errors, resources, **annotations** and **metadata**.
- With **CloudWatch Logs** enabled, the logs for a trace appear with it.

## Clean up

**Delete the CloudFormation stack** so nothing keeps running.

## Exam takeaways

1. **Service map** → find the failing or slow dependency.
2. **Traces** → latency and errors of one request, call by call.
