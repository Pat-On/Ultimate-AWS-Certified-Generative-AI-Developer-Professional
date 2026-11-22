# 71. Amazon DynamoDB - Hands On

Creating two **Amazon DynamoDB** tables in the console, one with only a partition key and one with a partition key plus a sort key, adding items, and seeing how the flexible attribute model and key uniqueness behave.

## Steps

1. In the DynamoDB console choose **Create table**. A serverless database already exists per region, so only tables are created.
2. Name the first table `Users` and set the partition key `user_ID` as a string. Leave the sort key empty.
3. Choose **Customize settings** instead of the quick-start defaults, set the table class, capacity mode and capacity, skip secondary indexes, keep the default encryption and create the table.
4. Open the table, choose **View items** and create an item with a user ID of John123, then add string attributes `first_name` (John) and `last_name` (Doe). Items can be entered through a form or as a JSON document.
5. Try a second item with John123 again and a different first name. It fails because the partition key must be unique when there is no sort key.
6. Create an item with user ID Alice456, first name Alice and an age of 41, with no last name. It succeeds.
7. Create a second table for user posts, with partition key user ID and a sort key holding the post timestamp, using the same provisioned settings of 2 read and 2 write units with auto scaling off.
8. Add a post item for John123 with a timestamp and a content attribute, then a second post for John123 with a later timestamp. It succeeds because the key is the combination of both values.
9. Add a post for Alice456 in the same way.

## Settings that mattered

| Setting | Choice in the demo | Notes |
| --- | --- | --- |
| Partition key | User ID, **string** | Types allowed: binary, number or string. Required |
| Sort key | None on the first table; post timestamp on the second | Optional, same type choices |
| Table class | **DynamoDB Standard** | General purpose and recommended for most use cases. **Standard-IA** suits data kept for a long time with few reads or writes, and gives cost optimisation |
| Capacity mode | **Provisioned** | Alternative is **on demand**. Provisioned is within the free tier. Both modes are covered in depth later |
| Auto scaling | Disabled for reads and writes | Gives a fixed provisioned capacity |
| Capacity units | 2 read, 2 write | The lecturer first said 2 units, then corrected to 10 as the free-tier figure, and chose 2 each. How to compute capacity comes later, along with the **capacity calculator** |
| Secondary indexes | None | Advanced topic later in the course |
| Encryption at rest | **DynamoDB-owned key** | Other key options exist |

- The console estimated **$1.32 per month** for the table. That can be ignored within the free tier; outside it, it is the monthly cost.
- The table page shows the partition key, sort key, capacity mode, replication, creation date and more. The **items** view lets you scan or query the table as well as create items.

## What the demo showed

- **No fixed schema.** Items in the same table can have different attributes. John had a first and last name, Alice a first name and an age, and the request succeeded. An RDS SQL database would complain about undefined columns or nulls.
- Only the key attribute is mandatory. Other attributes show as null when an item lacks them.
- Attributes can be added over time without affecting existing data. This is both a power and a risk.
- DynamoDB has **no way to define a not-null constraint** on an attribute.
- Tables are created at the **region** level, and as many can be created as needed without managing the underlying database.
- **Partition key only:** the key value must be unique per item.
- **Partition key plus sort key:** uniqueness applies to the **combination**, so the same user ID can have many items with different timestamps. Data is partitioned by user ID, which can be queried directly (John123 is clickable), and sorted by the sort key.

## Gotchas

- Choose a partition key with many distinct values. If one user such as John123 made all 10,000 posts, the data would be heavily skewed towards that key.
