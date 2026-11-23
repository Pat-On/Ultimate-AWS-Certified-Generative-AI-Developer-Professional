# 84. Amazon S3 - Lifecycle Rules

How objects move between storage classes, **lifecycle rules** that automate it, example design scenarios and **S3 Analytics** for choosing transition times.

## Moving between classes

- Objects can transition between classes, for example Standard to Standard-IA, Intelligent-Tiering or One Zone-IA, and onward to Glacier Flexible Retrieval or Deep Archive.
- Move infrequently accessed objects to **Standard-IA**. Move archive objects you do not need quickly to **Glacier** or **Glacier Deep Archive**.
- This can be done manually or automated with **lifecycle rules**.

## Lifecycle rules

- **Transition actions** move objects to another class, for example to Standard-IA 60 days after creation, or to Glacier after 6 months.
- **Expiration actions** delete objects after some time, for example:
  - Access log files after 365 days.
  - Old versions of files, if versioning is enabled.
  - Incomplete multi-part uploads, for example those more than two weeks old.
- Rules can apply to a whole bucket, a **prefix** (for example `s3://mybucket/mp3/*`) or object **tags** (for example `Department: Finance`).

## Scenarios

| Scenario | Design |
| --- | --- |
| Thumbnails of profile photos are easily recreated and kept for 60 days. Source images need immediate retrieval for 60 days, then the user can wait up to 6 hours | Source images in **Standard**, with a lifecycle transition to **Glacier** after 60 days. Thumbnails in **One Zone-IA**, with an expiration after 60 days. Use a prefix to separate them |
| Deleted objects must be recoverable immediately for 30 days, then within 48 hours up to 365 days | Enable **versioning**, so deletes are hidden by a **delete marker**. Transition **noncurrent versions** to **Standard-IA**, then to **Glacier Deep Archive** |

## S3 Analytics - storage class analysis

- Recommends the right time to transition objects, for **Standard and Standard-IA only**. It does **not work for One Zone-IA or Glacier**.
- Produces a **.csv report**, updated **daily**, which takes **24 to 48 hours** to start showing data.
- A good first step to build or improve lifecycle rules.

## Exam takeaways

1. Lifecycle rules have **transition actions** and **expiration actions**, scoped by prefix or tags.
2. Expiration can clean up **old versions** and **incomplete multi-part uploads**.
3. For recoverable deletes, combine **versioning** with transitions of **noncurrent versions**.
4. **S3 Analytics** supports only Standard and Standard-IA, with a daily CSV report.
