# 96. S3 Access Points

**S3 Access Points** simplify security management for buckets holding data accessed by many users or groups, by moving access rules out of one large bucket policy.

## The problem

- A bucket holds **finance** and **sales** data, and different users and groups need different access.
- One bucket policy covering everyone grows with every new user and dataset, and becomes unmanageable.

## Access points

- Each access point has its own **access point policy**, which looks like a bucket policy, and its own **DNS name**.
- Example:
  - **Finance access point**: policy grants read/write to the `/finance` prefix.
  - **Sales access point**: policy grants read/write to the `/sales` prefix.
  - **Analytics access point**: policy grants **read-only** access to the entire bucket (finance and sales).
- With the proper **IAM permissions**, each user group connects only through its own access point.
- Security management moves from the bucket policy into the access points, so the **bucket policy stays simple** and access scales.

## Network origin

- Each access point is created with either an **Internet origin** or a **VPC origin**.
- A **VPC origin** makes the access point reachable only from within the VPC, so for example an EC2 instance reaches the bucket privately, without going through the internet.
- To reach a VPC-origin access point you must create a **VPC endpoint** (**Gateway** or **Interface** endpoint).
- The **VPC endpoint policy** must allow access to both the **target bucket** and the **access point**.
- Security is then layered: **VPC endpoint policy**, **access point policy** and **S3 bucket policy**.

## Exam takeaways

1. Access points **simplify security management at scale**, with one policy per access point and a simple bucket policy.
2. Each access point has its **own DNS name** and **own access point policy**.
3. For private access, use a **VPC origin** with a **VPC endpoint** whose policy allows both the bucket and the access point.
