# 40. SageMaker Data Wrangler

**SageMaker Data Wrangler** is the most directly applicable SageMaker tool for data engineering: an ETL pipeline built into **SageMaker Studio**, much like **AWS Glue**'s visual tooling but tailored to machine learning data preparation.

## Capabilities

- **Import** data from many sources: **S3**, **Lake Formation**, **Athena**, **SageMaker Feature Store**, **Redshift**, and anything reachable over **JDBC** (SaaS apps such as Salesforce, external systems such as Databricks).
- **Visualize** data to check distributions and spot outliers before training.
- **Transform** with more than 300 built-in transformations, or custom code in **pandas**, **PySpark** or **PySpark SQL**.
- **Quick Model**: train a model on a subset of the transformed data and measure results quickly, to compare different transformations.

## How it works

- Data Wrangler does not run your pipeline. It is a **code generation tool**: the data flow is exported as a **Jupyter notebook** or Python code that you reuse in your own pipeline.
- Export destinations include **SageMaker Processing** (for example to train a model), **SageMaker Pipelines**, and back into **SageMaker Feature Store** so other models can use the transformed features.

## Example walkthrough

- Import a CSV from an S3 bucket (Titanic passenger data); a preview appears and column data types are inferred. You can correct the types and rename columns.
- Visualize distributions (for example age) as a sanity check.
- Transform: **Encode categorical** applies **one-hot encoding**, turning a class column (1, 2, 3) into three binary features. Transformation choices such as encoding, normalization and which data to include or hold back strongly affect model quality.
- Run Quick Model to test how the transformation choices affect the model, then export the flow as code.

## Troubleshooting

- The Studio user needs the appropriate **IAM roles** for Data Wrangler, and data sources must allow access (the **AmazonSageMakerFullAccess** policy is mentioned).
- Error "the following instance type is not available" usually means a **quota** problem, not a lack of capacity. Request an increase in **Service Quotas**, under Amazon SageMaker, **Studio Kernel Gateway apps** (for example ml.m5.4xlarge instances).
