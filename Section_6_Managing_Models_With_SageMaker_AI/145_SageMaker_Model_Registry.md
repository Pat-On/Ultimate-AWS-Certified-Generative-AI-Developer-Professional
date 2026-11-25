# 145. SageMaker Model Registry

The **Model Registry** is a **catalog of your models**, like a fancy database table, that manages information about them.

## What it does

- **Catalogs models and manages versions.**
- **Associates metadata** with each model (whatever you want).
- **Manages approval status**: for example, hold a model for **manual approval** before it is deployed to production.
- Is a component of **deploying** to production: a pipeline can check "is this model approved and ready?". It fits into **CI/CD** systems.
- **Shares models** across applications: by **centralizing** them you build a library that the whole organization can reuse.
- **Integrates with SageMaker Model Cards**: a model card is a short web page of governance information about a model (its properties, limitations, what it was trained on), and the registry can point to it.

The slides show the basic flow: **create a model group**, **create a SageMaker Pipeline**, **register a model version from each pipeline run** into the group, and add the group to **Model Registry Collections**.

## Example: an approval and promotion workflow (from an AWS blog)

1. A training pipeline pre-processes data, trains and **creates the model**.
2. The model is **registered** in the Model Registry.
3. **EventBridge** captures the event that a new model version was registered.
4. A **Lambda** function sends a request for a **human to approve** the model.
5. The approver **approves or rejects**. The decision goes back through **API Gateway and Lambda** and **updates the approval status** in the registry's metadata.
6. An update to **Parameter Store** kicks off the **inference pipelines** that deploy the approved model through SageMaker, and notifies someone, for the **dev, test and production** stages.

## Exam takeaways

1. The **Model Registry** is a **central catalog** of model **versions, metadata and approval status**.
2. A model can be **held for manual approval** before production, and the approval status can **gate deployment** in a pipeline.
3. It supports **CI/CD** and **sharing models across applications**.
4. It links to **Model Cards** for governance information.
5. A typical approval flow combines **registry, EventBridge, Lambda, API Gateway and Parameter Store**.
