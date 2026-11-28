# 211. IAM Introduction: Users, Groups, Policies

**IAM** (Identity and Access Management) is a **global** service.

## Root user

Created by default with the account. Use it only to **set the account up**; do not use it afterwards or **share** it.

## Users and groups

- A **user** is one person in the organisation.
- A **group** gathers users (for example *Developers*, *Operations*, *Audit team*).

| Rule | |
|---|---|
| Groups contain **only users**, never other groups | Required |
| A user can belong to **several groups** | Allowed |
| A user can belong to **no group** | Allowed, but not best practice |

## Policies

**JSON documents** assigned to users or groups that say what they may do. Not programming: a description of permissions.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "elasticloadbalancing:Describe*",
        "cloudwatch:Describe*",
        "cloudwatch:ListMetrics",
        "cloudwatch:GetMetricStatistics"
      ],
      "Resource": "*"
    }
  ]
}
```

This allows looking at EC2, load balancers and CloudWatch, without changing anything.

**Least privilege:** give no more permissions than the user needs. Otherwise a new user could launch costly services or create security problems.

## Exam takeaways

1. IAM is **global**.
2. **Groups hold users only**; users can be in many groups or none.
3. Permissions come from **JSON policies**; apply **least privilege**.
