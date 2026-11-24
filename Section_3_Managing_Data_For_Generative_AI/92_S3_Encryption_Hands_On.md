# 92. S3 Encryption - Hands On

Setting default encryption on a bucket, overriding it per object, and seeing which encryption options the console supports.

## Steps

1. Create a bucket with **versioning enabled**. Default encryption must be chosen, so select **SSE-S3**.
2. Upload `coffee.jpg`. In the object details, under server-side encryption, it shows **SSE-S3** (Amazon S3 managed keys).
3. Edit the object's server-side encryption, overriding the bucket default for this one object. Choose **SSE-KMS** (or **DSSE-KMS**, which is two levels of KMS encryption).
4. For the KMS key, enter a **key ARN** or pick from your own KMS keys. With no custom key, only the **`aws/s3`** key is listed. It is the default KMS key for S3 and **costs nothing**. A custom KMS key **costs money every month**.
5. Save. Editing the encryption **creates a new version** of the object, so the object now has two versions, and the current one uses SSE-KMS with the `aws/s3` key.
6. The override can also be set at upload time, under **Properties**, **Server-side encryption**. Use the bucket default or override with SSE-S3, SSE-KMS or DSSE-KMS.
7. To change the bucket default, edit **Default encryption** in the bucket properties and choose SSE-S3, SSE-KMS or DSSE-KMS.
8. With SSE-KMS, the **bucket key** option is shown. It reduces cost by making fewer API calls to KMS, and is **enabled by default**. It does not apply to SSE-S3.

## What the demo showed

- The console only offers **SSE-S3, SSE-KMS and DSSE-KMS**.
- **SSE-C** cannot be enabled from the console, only from the **CLI**.
- **Client-side encryption** needs no S3 setting. You encrypt before upload and decrypt after download, and S3 is not told the data is encrypted.

## Exam takeaways

1. Changing an object's encryption creates a **new version** when versioning is on.
2. **Bucket keys** reduce KMS API calls and cost, and only apply to **SSE-KMS**.
3. **SSE-C** is CLI/API only. **Client-side** encryption is invisible to S3.
