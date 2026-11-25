# 140. SageMaker Deployment Safeguards

SageMaker gives you ways to deploy newly trained models in a **controlled** manner and roll back if something goes wrong.

## Deployment guardrails

- **Not the same as guardrails in generative AI**, which are usually content filters. **Deployment guardrails** are safety for the deployment itself.
- They apply to **asynchronous or real-time inference endpoints**, not batch processing.
- They control how **traffic shifts to a new model**, using **blue/green deployments** (blue = the old model, green = the new one):

| Mode | How it works |
| --- | --- |
| **All at once** | Shift **all** traffic to green, monitor, and once confident **terminate the blue fleet**. |
| **Canary** | Shift a **small portion** of traffic to green and monitor, with both running side by side. Increase the share until you are happy. A bad model affects only part of your users. |
| **Linear** | **Automates** the shift in linearly spaced steps (for example 10%, then 20%, then 30%, up to 100%). |

- **Auto-rollbacks**: if a problem is detected automatically, traffic returns to the blue deployment **without human intervention**.

## Shadow tests

- Both models run together, and **every inference request is run twice**, by the production model and by the **shadow variant** in parallel.
- Only the production model's results are returned. The shadow variant's results are used for comparison.
- If they **diverge unexpectedly**, you can decide not to roll out the new version. You **monitor the test in the SageMaker console** and decide when to **promote** it.

## Putting the tools together

- **SageMaker Studio** is the umbrella. From it you reach **SageMaker Autopilot** and **SageMaker Model Monitor**.
- **Autopilot** can automate **Notebooks, Experiments, Debugger and Automatic Model Tuning**. You can also use each of these **independently**.

## More SageMaker features

| Feature | What it does |
| --- | --- |
| **JumpStart** | **One-click** launch of a model or algorithm from a **model zoo** (like Hugging Face): the slides say over 150 open-source models for NLP, object detection, image classification and more, including large and small language models and image generation. It opens a notebook with sample code. |
| **Data Wrangler** | **Import, transform, analyze and export** data inside SageMaker Studio (an alternative to doing it in Glue or Glue Studio). |
| **Feature Store** | **Find, discover and share features** (a feature is a column of training data). It has an **online** (low latency) and an **offline** (training or batch inference) store, and features are organized into **feature groups**. A consistent view of features across pipeline stages prevents errors. |
| **Edge Manager** | A **software agent for edge devices** (models optimized with **Neo**). It collects and samples data for **monitoring, labeling and retraining**. |
| **Asynchronous inference endpoints** | Make a prediction request and **get the answer back later**, without waiting. |

## Exam takeaways

1. **Deployment guardrails** (not content filters) control traffic shifting for **real-time and asynchronous endpoints**: **all at once, canary or linear**, with **auto-rollback**.
2. **Shadow tests** run every request on both the production and the shadow model, return only production results, and let you compare before **promoting**.
3. **JumpStart** = one-click models from a model zoo. **Data Wrangler** = data prep in Studio. **Feature Store** = online and offline features in feature groups. **Edge Manager** = agent for Neo-deployed edge models.
4. **Asynchronous inference** endpoints return results later.
