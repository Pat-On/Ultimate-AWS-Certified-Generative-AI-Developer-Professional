# 138. Intro to Amazon SageMaker AI

**Bedrock is not the only way to manage and deploy models.** SageMaker predates Bedrock and has been rebranded **SageMaker AI**. It handles the broader **machine learning** workflow, not just generative AI, and gives you **lower-level access and more flexibility** than Bedrock.

## The lifecycle it covers

SageMaker has tools for every step of the ML cycle:

1. **Fetch, clean and prepare** data for training.
2. **Train** the model, spinning up the resources the training needs, then **evaluate** it.
3. **Deploy** the model.
4. After deployment, **evaluate its results and monitor for drift**. A deployment can produce more data that feeds back into training.

**The exam does not cover the training part** (out of scope), but it helps to see how the pieces fit.

## How training and deployment fit together

| Stage | Pieces |
| --- | --- |
| **Training** | **Training data in S3**, a **training code image in ECR**, and **training instances** that run the code on the data. SageMaker can orchestrate it from a notebook. For generative AI this might be a pre-trained model from Hugging Face or a fine-tune. |
| **Model artifacts** | The trained model's artifacts (for example weights) are written to **S3**. |
| **Deployment and hosting** | An **inference code image** (the code that queries the model) plus the artifacts, hosted on an **endpoint that SageMaker manages**. The **client application talks to that endpoint**. |

## Ways to drive it

- **SageMaker Notebooks**: a Jupyter Lab environment. You spin up a **notebook instance on EC2** from the console, with access to S3 data, the usual Python data tools (scikit-learn, Spark, TensorFlow) and a wide variety of **built-in models**. From the notebook you can launch training instances and deploy models.
- **The SageMaker AI console**: it covers pretty much everything, so you can work visually or in code.

## Exam takeaways

1. **SageMaker AI** covers the whole **ML lifecycle** (data prep, training, evaluation, deployment, monitoring), not just generative AI, and gives more control than Bedrock.
2. **Training is out of scope** for this exam.
3. Training uses **S3 data and an ECR code image**. Trained **artifacts go to S3**. Inference runs from an **inference image on a SageMaker-managed endpoint** that clients call.
4. **Notebook instances** (on EC2) and the **console** are two ways to drive it.
