# 209. Principle of Least Privilege

**Grant only the permissions needed to perform a task.** Anything extra can be abused or exploited.

## In practice

- While **developing**, broader permissions are reasonable, as the needed services are not yet known.
- Once the workload's exact **services and operations** are clear, **lock it down**.
- **IAM Access Analyzer** can **generate a least-privilege policy from observed access activity**, a good starting point after testing.

## Example policy

Read only CSV files from one folder of one bucket:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ListReportsFolder",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::example-bucket",
      "Condition": { "StringLike": { "s3:prefix": "reports/*" } }
    },
    {
      "Sid": "ReadCsvReports",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/reports/*.csv"
    }
  ]
}
```

| Part | How it narrows access |
|---|---|
| `ListBucket` + `Condition` | Listing is limited to the **`reports/` prefix** of one bucket |
| `GetObject` + resource pattern | Reading is limited to **`.csv` files** under that prefix |

Note that `ListBucket` applies to the **bucket** ARN and `GetObject` to **object** ARNs.

## Exam takeaways

1. **Least privilege** = only the permissions the task requires.
2. **Generate policies from access activity** → **IAM Access Analyzer**.
3. Narrow by **action, resource and condition**.
