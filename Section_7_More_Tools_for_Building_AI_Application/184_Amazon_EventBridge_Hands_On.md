# 184. Amazon EventBridge Hands On

- **Type:** Practice lab

The console offers **rules**, **pipes** (connect event sources to targets), **schedules** and the **schema registry**.

## Rule with an event pattern

1. Create `EC2InstanceStateChangeDemo`, rule type **event pattern**.
2. Source: AWS services (partners are the other option) → **EC2** → **Instance State-change Notification**.
3. Match the states **shutting-down** and **terminated**.
4. Target: an **SNS topic** (`DemoTopic`). With an email subscription you would get a message on every matching change.

Other targets include stopping or terminating instances, starting ECS tasks, invoking Lambda and sending to SQS.

## Schedule

A schedule opens **EventBridge Scheduler**: **recurring** (for example every hour) or **one-time**, with an optional **flexible time window**. The target can be Lambda, SQS or **almost any AWS API**.

## Other features

- **Event buses:** `default`, or create your own (name, encryption) to **separate** rules and permissions.
- **Replay** events for debugging.
- **Partner event sources:** for example an Auth0 sign-up arrives with **no glue code**.
- **API destinations:** send events **outside AWS** to your own or a SaaS API.
- **Schema registry:** shows each event's JSON fields and types, with **code bindings** (Java, Python, TypeScript, Go).

## Exam takeaway

Know **rules** (react to events) and **schedules**.
