# 144. SageMaker Model Monitor and Clarify

A model in production does not perform the same forever: the **data coming in drifts** in ways you did not expect. **SageMaker Model Monitor** watches for that.

> Per lecture 142, **Model Monitor and Clarify** are moving to **maintenance mode** (not available to new customers from July 30, 2026), but remain in exam scope for now.

## Model Monitor

- Sends **alerts through CloudWatch** on **quality deviations** in deployed models.
- **Visualizes data drift**: for example a loan model whose input population changes, or input features that start going missing.
- Detects **anomalies and outliers**, and **new features** that were not in the data before.
- **No code needed**: it works visually in SageMaker Studio.

## Clarify

- **Detects potential bias**, for example imbalances across groups, ages or income brackets. With Model Monitor you can **monitor for bias** and be alerted through CloudWatch.
- **Explains model behavior**: it shows **which features contribute most to the predictions** and where bias may come from.
- Bias metrics it supports (the slides list them for pre-training bias; you do not need the detail, but know that many exist, and **Kullback-Leibler divergence** is a popular one):

| Metric | What it measures |
| --- | --- |
| **Class Imbalance (CI)** | One group has fewer training values than another. |
| **Difference in Proportions of Labels (DPL)** | Imbalance of positive outcomes between groups. |
| **KL and Jensen-Shannon divergence** | How much the outcome distributions of groups diverge. |
| **Lp-norm, Total Variation Distance, Kolmogorov-Smirnov** | Differences between the groups' outcome distributions (P-norm, L1 norm, maximum divergence). |
| **Conditional Demographic Disparity (CDD)** | Disparity of outcomes between groups, as a whole and by subgroup. |

## How Model Monitor works

- Monitoring data is **stored in S3 and secured**.
- Monitoring jobs run on a **Monitoring Schedule**.
- Metrics are **emitted to CloudWatch**. **You** set up a **CloudWatch notification or alarm**, and then take corrective action: **retrain the model or audit the data**.
- It can show results in **SageMaker Studio**, or integrate with **TensorBoard, QuickSight and Tableau**.

## Monitoring types

| Type | What it checks |
| --- | --- |
| **Data quality drift** | Statistical properties of the features against a **baseline you define** ("quality" is up to you). |
| **Model quality drift** | The model's **accuracy** against a model quality baseline. It can use **Ground Truth labels** (human-generated) to judge what is correct. |
| **Bias drift** | Bias detected by Clarify changing over time. |
| **Feature attribution drift** | The impact of each feature on the output changing, measured with the **NDCG score** (Normalized Discounted Cumulative Gain), which compares the feature ranking of training data with live data. |

## Exam takeaways

1. **Model Monitor** alerts on **drift** (data quality, model quality, bias, feature attribution) through **CloudWatch**, with no code.
2. **Clarify** detects **bias** and **explains** which features drive predictions.
3. Data lives in **S3**, jobs run on a **Monitoring Schedule**, metrics go to **CloudWatch**, and **you** wire alarms and corrective action (**retrain or audit**).
4. **Model quality** monitoring can compare against **Ground Truth** human labels.
5. **Feature attribution drift** uses the **NDCG** score on training versus live feature rankings.
