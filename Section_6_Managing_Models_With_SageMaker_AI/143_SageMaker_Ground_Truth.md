# 143. SageMaker Ground Truth

**SageMaker Ground Truth** uses **humans to label your data**. It sits under feature engineering because it deals with **missing data**, most often missing **labels**, but also missing features: anything a human can infer easily.

> Per the deprecation note in lecture 142, Ground Truth is moving to **maintenance mode** (not available to new customers from July 30, 2026) and **Ground Truth Plus** has reached end of support. Both remain in scope for the exam for now.

## What it does

- The classic example is **image classification**: someone must tag training images with what is in them (basketball or soccer game, where the birds are) before a model can be trained. Ground Truth **manages the fleet of humans** who do the labeling.
- **It also builds its own model while labels arrive.** The model learns from the human labels, and over time **only the ambiguous items it is unsure about are sent to human labelers**. This can **cut labeling cost by up to 70%**.

## Who labels

| Workforce | Notes |
| --- | --- |
| **Amazon Mechanical Turk** | A large worldwide workforce doing simple tasks for very little money. |
| **Your own internal team** | A good fit for sensitive data. |
| **Professional labeling companies** | Specialized, and more expensive. |

## Other ways to generate labels or features

- **Amazon Rekognition**: image recognition with a pre-trained model for common objects, to classify images or to produce a feature such as "what is in this image".
- **Amazon Comprehend**: text analysis and topic modeling, to generate **topics or sentiment** for a document, as labels or as extra features.
- Any **pre-trained model or unsupervised technique** can help create new labels or features.

## Ground Truth Plus

A **turnkey** option: AWS experts set up and manage the workflow and the labelers for you.

1. You fill out an **intake form** (who you are, what you are trying to do).
2. AWS contacts you to work out the details and the pricing (not published).
3. You **track progress in the Ground Truth Plus Project Portal**, with charts of progress and results.
4. You **get the labeled data back in S3**.

## Exam takeaways

1. **Ground Truth** = humans (Mechanical Turk, your own team, or labeling vendors) labeling training data, managed for you.
2. It **learns as labels come in** and sends only **ambiguous items** to humans, which can **cut cost by up to 70%**.
3. **Ground Truth Plus** is the turnkey version: intake form, AWS-managed workflow, progress in the project portal, results in S3.
4. **Rekognition** (images) and **Comprehend** (text) can generate labels or features automatically.
5. Ground Truth is in **maintenance mode** and Ground Truth Plus has ended support, but both stay in the exam scope for now.
