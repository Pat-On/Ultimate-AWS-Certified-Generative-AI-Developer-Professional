# 83. Amazon S3 - Storage Classes - Hands On

Uploading an object, choosing and changing its **storage class**, then automating transitions with a **lifecycle rule**.

## Steps

1. Create a bucket (any region) and upload an object.
2. Under the upload options, open the object's **properties**. The **storage class** list shows each class with its AZ count, minimum storage duration, minimum billable object size and monitoring and auto-tiering fees.
3. Upload with **Standard-IA** and check the object shows that class.
4. Edit the storage class under the object's properties to change it, for example to **One Zone-IA**, **Glacier Instant Retrieval** or **Intelligent-Tiering**.
5. Under the bucket's **Management** tab, create a lifecycle rule (`DemoRule`) applied to all objects, with transitions of current versions such as Standard-IA after 30 days, Intelligent-Tiering after 60 days and Glacier Flexible Retrieval after 180 days.
6. Review the transitions in the rule summary.

## Notes

- The list also showed **Reduced Redundancy**, a **deprecated** class that is not covered in the course.
- Storage class can be changed manually per object, or automated with lifecycle rules.

## Exam takeaways

1. Storage class is set at upload and can be **edited afterwards** on the object.
2. **Lifecycle rules** under Management automate moves between classes after a number of days.
3. **Reduced Redundancy** is deprecated.
