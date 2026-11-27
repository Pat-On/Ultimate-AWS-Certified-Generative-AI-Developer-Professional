# 202. AWS CloudTrail - Hands On

## Event history

The console's **Event history** shows the **management events** of the **last 90 days**: every such API call in the account.

## Demo: who terminated the instance?

1. In the EC2 console, **terminate** a demo instance.
2. **Wait about 5 minutes** for the event to arrive.
3. Refresh Event history and open **`TerminateInstances`**.
4. The event shows the **event source** (EC2), the **access key** used, the **region** and more; the **full event record** can be viewed.

## Exam takeaways

1. **Event history** answers who did what without any setup, for 90 days of management events.
2. Events appear **with a delay** of a few minutes.
