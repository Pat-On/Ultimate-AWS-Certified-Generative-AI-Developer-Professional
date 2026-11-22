# 74. Amazon DynamoDB - Basic APIs

The DynamoDB API calls the exam refers to by name: writing, reading, deleting, batching, and using SQL through **PartiQL**.

## Writing data

| API | Behaviour |
| --- | --- |
| **PutItem** | Creates a new item or **fully replaces** the item with the same primary key. Consumes WCU |
| **UpdateItem** | Edits **only some attributes** of an existing item, or adds the item if it does not exist. Works with **atomic counters** |
| **Conditional writes** | Accept a write, update or delete **only if a condition is met**. They help with concurrent access to items |

## Reading data

- **GetItem** reads one item by its primary key, either hash or hash plus range. It can be eventually consistent (default) or **strongly consistent**, which costs more RCU and a little more latency. A **ProjectionExpression** returns only some attributes.
- **Query** returns items for a **KeyConditionExpression**:
  - The partition key must use **equality** (for example John123).
  - An optional sort key can use equal, less than, greater than, begins with, between and so on.
  - A **FilterExpression** filters after the query but before results are returned, and only works on **non-key attributes**.
  - Results are limited by the **limit** parameter or **1 MB** of data, and **pagination** fetches more.
  - It can run against a table, a **Local Secondary Index** or a **Global Secondary Index**.
- **Scan** reads the **entire table**:
  - It returns up to **1 MB** per page, so you paginate.
  - Filtering happens on the client side, which is inefficient. Scan is really for exporting a whole table.
  - It consumes a lot of RCU. Use a **limit** or smaller result sizes with pauses to protect normal traffic.
  - A **parallel scan** uses several workers on different data segments for speed, which raises throughput and RCU consumed. Limits can still reduce its impact.
  - It accepts ProjectionExpression and FilterExpression.

## Deleting data

- **DeleteItem** removes one item, optionally with a condition (delete only if money equals zero).
- **DeleteTable** removes the whole table and all its items. It is much faster than scanning and deleting each item. The exam can ask this, so to delete everything do **not** scan, use DeleteTable.

## Batch operations

Batching saves latency and API calls, and DynamoDB applies the operations in **parallel**. Part of a batch can fail, in which case the failed items are returned and only those are retried.

| API | Limits | Failure handling |
| --- | --- | --- |
| **BatchWriteItem** | Up to **25** PutItem and/or DeleteItem calls, up to **16 MB** written, **400 KB** per item. **No UpdateItem** | Returns **UnprocessedItems**, usually from missing write capacity |
| **BatchGetItem** | Up to **100** items and **16 MB**, from one or more tables, read in parallel | Returns **UnprocessedKeys**, usually from missing read capacity |

Two ways to handle the unprocessed ones: retry with **exponential backoff**, or, if it keeps happening, **add WCU or RCU**.

## PartiQL

- A **SQL-compatible query language** for DynamoDB. It supports **select, insert, update and delete** across multiple tables, but **no joins**.
- It runs from the Management Console, **NoSQL Workbench**, the DynamoDB APIs, the CLI or the SDK.
- It adds **no new capabilities**. It is just SQL syntax for the same operations.

## Exam takeaways

1. **PutItem** replaces the whole item, **UpdateItem** changes only some attributes.
2. **Query** needs a partition key with equality. **FilterExpression** works only on non-key attributes and does not save RCU. **Scan** reads everything.
3. To empty a table, use **DeleteTable**, not scan plus delete.
4. **BatchWriteItem** does up to 25 puts and deletes, never updates. Retry **UnprocessedItems** and **UnprocessedKeys** with exponential backoff or add capacity.
5. **PartiQL** is SQL over DynamoDB with no joins.
