# 146. SageMaker Lineage Tracking

**SageMaker ML lineage tracking** matters for **governance** of ML models. It **creates and stores a record of your ML workflow** (MLOps), visualizing the pipeline and keeping a **running history of your models and how they are put together**, as it changes over time.

- Useful for **auditing and compliance**.
- Tracking entities can be created **automatically or manually**, so you choose what to track.
- It integrates with **AWS Resource Access Manager** for **cross-account** lineage (next lecture).

## What a lineage graph shows

Following a typical ML job end to end: input **dataset artifacts** (and streamed input) go into a **processing job** (a trial component), which produces **processed dataset artifacts**. Those feed the **training job** trial component, which produces **model artifacts**. The model is then packaged and deployed through an **endpoint**, which is captured too.

## Entities (concepts, not for memorizing)

| Entity | What it is |
| --- | --- |
| **Trial component** | A processing, training or transform job. |
| **Trial** | A model composed of trial components. |
| **Experiment** | A group of trials for a given use case. |
| **Context** | A logical grouping of entities. |
| **Action** | A workflow step or a model deployment. |
| **Artifact** | An object or data, such as an S3 bucket or an ECR image. |
| **Association** | Connects entities, with an optional type: **ContributedTo, AssociatedWith, DerivedFrom, Produced, SameAs**. |

## Querying lineage

- Use the **LineageQuery API** from Python, part of the **Amazon SageMaker SDK for Python**. For example, **find all models or endpoints that use a given artifact**, so you know who is affected before you change it.
- You can also produce a visualization, using an external **Visualizer helper class** in a notebook.

## Exam takeaways

1. Lineage tracking = a **record of how data, jobs, models and endpoints connect**, for **auditing, compliance and governance**.
2. It can be **automatic or manual**, and it is queried with the **LineageQuery API** in the SageMaker Python SDK.
3. **Cross-account** lineage works with **AWS Resource Access Manager** and the AddAssociation API.
