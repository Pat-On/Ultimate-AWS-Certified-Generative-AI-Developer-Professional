# 139. Data Processing, Training, and Deployment with SageMaker

More detail on how to prepare data, train a model and deploy it in SageMaker. Everything is **container-based**: one container for processing, one for training code, all in **ECR**.

## Data preparation

| Topic | Details |
| --- | --- |
| **Sources** | Usually **S3**. **FSx for Lustre** is an option at larger scale. Also **Athena**, **EMR**, **Redshift** and **Amazon Keyspaces**. |
| **Format** | The ideal format depends on the algorithm. Each built-in algorithm has its own recommendation, often **RecordIO or protobuf** or a columnar store. |
| **Tools** | **Apache Spark** integrates with SageMaker. **scikit-learn, NumPy and pandas** are available in notebooks. |

## SageMaker Processing

1. Copy data from **S3**.
2. Spin up a **processing container**: your own code, or a **built-in processing container**.
3. Write the processed output to **another S3 bucket**, which is then passed to training.

## Training

- Create a **training job**. Inputs: the **S3 URL of the processed training data**, the **compute resources** (training can need heavy hardware and get expensive, and algorithms differ in whether they scale on one machine or many, with their own instance recommendations), an **S3 output bucket** for the model artifacts, and the **ECR path of the training code**.
- Algorithm options: **built-in algorithms**, **Spark MLlib**, your own **Python, TensorFlow, PyTorch or MXNet** code, **scikit-learn**, **RL estimator** (reinforcement learning), **XGBoost**, **Hugging Face** (including many open-source generative AI models, large and small), **Chainer**, **your own Docker image**, or algorithms bought from the **AWS Marketplace**.

## Deployment

The trained model sits in S3. Options:

| Option | Use it for |
| --- | --- |
| **Persistent real-time endpoint** | Making individual predictions on demand, scaled as needed. |
| **Batch transform** | Predictions for a **whole dataset at once**, with **no runtime endpoint**. |

More deployment features:

- **Inference pipelines** for more complex processing.
- **SageMaker Neo** to deploy models to **edge devices**, for places without reliable connectivity or where cloud latency is not tolerable.
- **Elastic Inference** to accelerate deployed (deep learning) models.
- **Automatic scaling**: adds endpoints when traffic grows.
- **Shadow testing**: compares a new model against the deployed one to catch errors. Controlled deployment and quick rollback are covered in the next lecture.

## Exam takeaways

1. Data usually comes from **S3** (also Athena, EMR, Redshift, Keyspaces, FSx for Lustre). A **processing job** copies from S3, runs a built-in or custom container and writes to S3.
2. A **training job** needs the processed data's S3 URL, compute, an S3 output location and an **ECR training image**.
3. **Real-time endpoint** = on-demand predictions. **Batch transform** = whole dataset, no endpoint.
4. **Neo** = edge deployment. **Elastic Inference** = acceleration. **Automatic scaling** = more endpoints under load. **Shadow testing** = compare new against current.
