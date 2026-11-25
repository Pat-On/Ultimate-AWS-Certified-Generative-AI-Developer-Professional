# 150. SageMaker Pipelines

**SageMaker Pipelines** orchestrates ML and AI workflows as a **directed acyclic graph (DAG)**: processes connected in a graph, with no loops.

- Define it **visually in the pipeline designer**, or in **JSON** (the harder way).
- Integrated with **SageMaker Unified Studio** and **SageMaker AI**.

## Example workflow

1. **Process data**: the incoming training data is prepared.
2. **Train model.**
3. **Process data again to evaluate** the model's output.
4. A **condition** step decides whether the evaluation meets your expectations:
   - **No:** the pipeline **fails** and stops.
   - **Yes:** it **registers the model in the Model Registry** and **creates the model** at the same time, then **deploys** it with **batch inference** enabled.

So the whole path from training to evaluating, registering, creating and deploying is **automated**. You start it with whatever training data you have and end with either a **new deployed model** or a **failure** if it did not pass.

## Exam takeaways

1. **Pipelines** = a **DAG** for ML workflows, built in the **visual designer** or as **JSON**.
2. A **condition step** can gate registration and deployment on the evaluation result.
3. It ties together **processing, training, evaluation, the Model Registry and deployment**.
