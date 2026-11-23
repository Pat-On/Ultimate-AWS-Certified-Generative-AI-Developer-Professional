# 90. S3 Encryption

The ways to encrypt objects in **Amazon S3**, which are **SSE-S3**, **SSE-KMS**, **DSSE-KMS**, **SSE-C** and **client-side encryption**, plus **encryption in transit** and how to enforce it. You need to know which method fits which situation.

## SSE-S3

- Uses a key **handled, managed and owned by AWS**. You never have access to it.
- The object is encrypted **server-side** with **AES-256**.
- Request it with the header `x-amz-server-side-encryption: AES256`.
- **Enabled by default** for new buckets and new objects.

## SSE-KMS

- The key is managed in **AWS KMS**. Advantages are **user control** over the keys and **auditing of key usage in CloudTrail**.
- Request it with the header `x-amz-server-side-encryption: aws:kms`, and specify the KMS key to use.
- To read an object you need access to the object **and** to the underlying KMS key, which is an extra layer of security.

### KMS limitation

- Uploading calls the **GenerateDataKey** KMS API and downloading calls the **Decrypt** KMS API.
- These calls count towards the **KMS quota per second**, which is **5,500, 10,000 or 30,000 requests per second** depending on the region.
- You can request an increase in the **Service Quotas console**.
- A very high-throughput bucket encrypted with KMS keys can be **throttled**. The exam may test this.

## DSSE-KMS

- **Dual-layer server-side encryption**. The object is encrypted twice, first with a **KMS** key and then with **S3-managed** keys.
- It is the right answer when the exam requires **multilayer encryption**.
- Sent with a header naming the KMS-DSSE value (see lecture 91).

## SSE-C

- **Server-side** encryption with keys **fully managed by the customer outside AWS**.
- The key is sent to S3 with each request. S3 **never stores** it and discards it after use.
- **HTTPS is mandatory**, and the key must be passed in the **HTTP headers of every request**, uploads and reads alike.

## Client-side encryption

- The client **encrypts data before upload** and **decrypts it after download**, so S3 only ever holds ciphertext.
- Easiest with a client library such as the **Amazon S3 Client-Side Encryption Library**.
- The customer **fully manages the keys and the encryption cycle**.

## Comparison

| | Key held by | Encryption happens | Header or protocol | Notes |
| --- | --- | --- | --- | --- |
| **SSE-S3** | AWS (S3-owned) | Server | `x-amz-server-side-encryption: AES256` | AES-256, default |
| **SSE-KMS** | AWS KMS, under your control | Server | `x-amz-server-side-encryption: aws:kms` | CloudTrail audit, KMS API quotas of 5,500 to 30,000 req/s |
| **DSSE-KMS** | KMS plus S3-managed | Server, twice | KMS-DSSE header | Multilayer encryption |
| **SSE-C** | Customer, outside AWS | Server | **HTTPS only**, key in headers on every request | S3 discards the key |
| **Client-side** | Customer | Client | HTTP or HTTPS | S3 never sees plaintext |

## Encryption in transit

- Also called **SSL/TLS** or encryption in flight.
- S3 exposes two endpoints, **HTTP** (not encrypted) and **HTTPS** (encrypted in flight).
- HTTPS is recommended and is **mandatory for SSE-C**. Most clients use it by default.
- To **force it**, attach a **bucket policy** that **denies** `s3:GetObject` when the condition `aws:SecureTransport` is **false**. HTTP requests are blocked and HTTPS requests can be allowed.

## Default encryption versus bucket policies

- **SSE-S3** is applied automatically to new objects.
- You can optionally **force encryption** with a bucket policy that refuses any `PutObject` call without encryption headers (SSE-KMS or SSE-C).
- **Bucket policies are evaluated before default encryption.**

## Exam takeaways

1. Know the header values, `AES256` for SSE-S3 and `aws:kms` for SSE-KMS, and that **SSE-S3 is the default**.
2. **SSE-KMS** gives control and CloudTrail auditing, but heavy traffic can hit **KMS API quotas** (throttling).
3. **SSE-C** requires **HTTPS** and the key in the headers of every request. **Client-side** encryption keeps keys and crypto entirely with the client.
4. Choose **DSSE-KMS** when multilayer encryption is required.
5. Force HTTPS with a bucket policy that denies requests where **`aws:SecureTransport` is false**.
