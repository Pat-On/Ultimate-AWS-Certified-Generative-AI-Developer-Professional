# 75. Amazon DynamoDB - Basic APIs - Hands On

Using the DynamoDB console to see which API call each action triggers: scan, put, update, get, batch delete and query.

## Steps

1. On the `UserPosts` table, open the items view, which starts on **Scan**. Choose the table and **Run** to scan the whole table and return many items.
2. **Create item** with user ID Alice456, a post timestamp and a content attribute. Because the key is new, this is a **PutItem**.
3. Select the item and choose **Actions**, then **Edit**. Change one attribute (the content) and save. Behind the scenes this is an **UpdateItem**.
4. Click a row and open the **item editor**. Retrieving that one item is a **GetItem**.
5. Select items and choose **Actions**, then **Delete items**. This is a batch of deletes (**BatchWriteItem**).
6. Switch from **Scan** to **Query**. Enter a partition key of John123 and run it to get all of that user's items.
7. Add a condition on the sort key (the post timestamp). The options are equal, less than or equal, greater than, between and begins with. Posts after 2021-11 returned one item, and a later boundary of 2021-09 returned two.

## What the demo showed

- Console actions map directly to the API calls: create is **PutItem**, edit is **UpdateItem**, opening an item is **GetItem**, multi-delete is a batch write, and the items view is **Scan** or **Query**.
- **Scan** returns everything, and the filter in the console is applied **client side** in the browser, not in DynamoDB.
- **Query** works only on the **partition key and sort key**. You cannot query on content, and filtering on content would again happen afterwards on the client.
- To delete everything, scanning and batch deleting works but is inefficient. Dropping the table is the efficient way.

## Exam takeaways

1. Query needs the partition key and can narrow with a sort key condition, which is why key design matters.
2. Searching on non-key attributes means a scan with a filter, which is expensive.
3. To empty a table, drop it rather than scan and delete.
