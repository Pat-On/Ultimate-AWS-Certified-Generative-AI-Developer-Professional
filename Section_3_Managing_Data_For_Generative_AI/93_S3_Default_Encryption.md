# 93. S3 Default Encryption

How default encryption relates to bucket policies that force a specific encryption method.

## Default encryption

- All buckets now have **SSE-S3** default encryption, applied automatically to new objects.
- You can change the default to another method, such as **SSE-KMS**.

## Forcing encryption with a bucket policy

- Optionally, use a **bucket policy** to refuse any `PutObject` call that lacks the right encryption headers (**SSE-KMS** or **SSE-C**).
- Example: **deny** `PutObject` when the header does not specify `aws:kms`.
- Example: **deny** `PutObject` when there is no customer-provided algorithm header, meaning no SSE-C.

## Exam takeaways

1. Default encryption is **SSE-S3**, and it can be changed.
2. A **bucket policy** can force the encryption method you want.
3. **Bucket policies are evaluated before default encryption.**
