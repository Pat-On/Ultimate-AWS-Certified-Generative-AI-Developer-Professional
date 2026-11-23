# 78. Amazon DynamoDB - TTL

**Time To Live (TTL)** automatically deletes DynamoDB items once an expiry timestamp attribute has passed, at no extra cost.

## How it works

- You nominate one attribute as the **TTL attribute**. When the current time passes its value, the item is expired and removed.
- The attribute must be the **Number** data type, holding a **Unix epoch timestamp** (in seconds).
- Deleting through TTL **does not consume any WCUs**, so there is no extra cost.
- Two background processes do the work:
  - An **expiration process** scans the table and marks items whose epoch time is earlier than now.
  - A **deletion process** scans and deletes those items.
- Expired items are deleted **within a few days of expiration**, not instantly.

## Behaviour to know

| Point | Detail |
| --- | --- |
| Expired but not yet deleted | Still **appear in reads, queries and scans**. Filter them out client-side if you do not want them |
| Indexes | Items are deleted from both **LSIs and GSIs** |
| DynamoDB Streams | A **delete operation for each expired item** enters the stream, which can help you recover expired items |
| Monitoring | A CloudWatch metric graphs items deleted by TTL over the last 24 hours |

## Use cases

- Reduce stored data by keeping only current items.
- Adhere to regulatory obligations.
- **Session data**, such as a table keyed by user ID and session ID with an expiry column.

## Steps

1. Create a table (`DemoTTL`) with partition key `user_id`, provisioned capacity with auto scaling off and 1 RCU and 1 WCU.
2. Add items with an `expire_on` attribute of type **Number**, using an epoch converter to turn a date and time into an epoch value (one item expiring in 5 minutes, another in 1 hour).
3. In the table's additional settings, enable **Time To Live** and enter the TTL attribute name (`expire_on`).
4. Optionally **run a preview** to simulate which items would be deleted at a chosen point. Options are an epoch value, a custom time, or the next 60 minutes, 24 hours or 7 days.
5. Once enabled, items are removed automatically after they expire.

## Exam takeaways

1. The TTL attribute must be a **Number** holding a **Unix epoch timestamp**.
2. TTL deletes are **free** (no WCUs) but are **not immediate**: expect deletion within a few days.
3. Expired items can still be returned until deleted, so **filter them out client-side**.
4. TTL deletions appear in **DynamoDB Streams** and are removed from **LSIs and GSIs**.
5. Classic use cases are session data, keeping only current data and regulatory retention.
