# 181. Amazon SQS Hands On

- **Type:** Practice lab

## Create a standard queue

- `DemoQueue` (the other type is **FIFO**).
- Settings: visibility timeout, delivery delay, wait time, retention (4 days), maximum message size.
- **Encryption:** on by default with an SQS-managed key (**SSE-SQS**), or **KMS** (choose a key; the data key reuse period limits KMS calls).
- **Access policy:** who may send and receive, as a JSON **resource policy**.
- Redrive and dead-letter queue come later.

**Note:** the lab shows a **256 KB** maximum message size, the older limit. Lecture 180 and its slide give **1,024 KB**.

## Send and receive

1. Send "hello world" (optional message attributes, out of scope for the exam).
2. **Poll for messages** and inspect ID, hash, sender, size and **receive count**.
3. Without deletion, the message **returns after 30 seconds** (the visibility timeout) and the receive count rises.
4. **Delete** it to mark it processed.

## Other options

**Edit** the queue, **Purge** all messages (development only), **Monitoring** (message count, **age of the oldest message**, another scaling signal), access policy, encryption, dead-letter redrive.

## Exam takeaway

A received message **comes back unless it is deleted** within the **visibility timeout**.
