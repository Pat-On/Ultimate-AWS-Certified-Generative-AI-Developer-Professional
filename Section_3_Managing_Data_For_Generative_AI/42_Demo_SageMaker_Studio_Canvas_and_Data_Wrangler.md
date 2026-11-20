# 42. Demo: SageMaker Studio, Canvas, and Data Wrangler

A watch-only demo of preparing data and building a model with **SageMaker Canvas** and **Data Wrangler** inside **SageMaker Studio**. The instructor advises not following along: it costs real money if something is left running, and the UI changes constantly. For the exam, the concepts matter, not the UI.

## Setup and Studio overview

- Using Studio requires a **domain**. For a single user it just sets up permissions and network access; for organisations you define roles and responsibilities with the **Role Manager**.
- **SageMaker Studio** is an integrated development environment for ML. Applications include **JupyterLab** (Python), **RStudio** (R) and **Canvas** (no code).
- Other Studio features: AutoML, experiments, training and evaluation job management, **Pipelines** for ML workflow automation, a model registry view, and **SageMaker JumpStart** for pre-trained foundation models.

## Steps in the demo

1. Open Canvas ("Run in Canvas", about one minute to spin up). Data prep can be done in plain language using generative AI ("chat for data prep").
2. **Import** a CSV from S3 by pasting its S3 URI. The dataset was the UCI employee absenteeism data (about 700 rows); the goal was to predict absenteeism. Random sampling is available for large datasets and was unnecessary here.
3. **Data insights** report: runs an analysis on an ML instance (ml.m5.4xlarge, set to one instance to save money; took about 10 minutes). Settings: problem type **regression**, target column absenteeism time in hours. It reports missing data, duplicates, outliers, anomalous samples, a **quick model** result and **feature importance** ordered by prediction power.
   - Findings: no missing data, but about a third of rows were duplicates (suspicious), some outliers that looked plausible, a quick model with poor accuracy, and workload average per day and transportation expense as the strongest predictors.
   - Lesson: for a dataset this small, local Python would have been free and faster; do not use expensive cloud instances unnecessarily.
4. **Transform** using chat. Prompts such as "transform workload average from string to long type, accounting for commas" and "remove duplicate rows" generated pandas code that was reviewed (always check generated code) and added as flow steps. A library of built-in transforms can be used instead.
5. **Export** options: to S3, to a Jupyter notebook, or "create model" directly in Canvas.
6. **Create model**: problem types offered include predictive analysis (tabular), image analysis, text analysis and **fine-tuning a foundation model**. Canvas recommended a category prediction (classification) model rather than regression. Build modes: **quick build** (about 2 to 15 minutes) or **standard build** (slower, more accurate and costly). The model reached the same conclusions on column impact.
7. **Predict**: batch or single predictions. The prediction dataset must have the same feature columns as the training data. Results can be sent to **QuickSight**, downloaded, linked in S3 or previewed, and include a confidence probability.
8. Deployment to real-time **inference endpoints** is possible but gets expensive quickly; it can also be managed under MLOps.

## Other Canvas capabilities

- Ready-to-use models built on higher-level AI services: object detection (**Amazon Rekognition**), sentiment analysis, language detection, text detection and entity detection (**Comprehend**, **Textract**). Both single and batch predictions are supported.
- A **gen AI chat** interface where you choose the foundation model.

## Cost warning

- Log out of Canvas when finished: instances tied to the workspace keep billing. Also make sure any endpoints you created are shut down.
