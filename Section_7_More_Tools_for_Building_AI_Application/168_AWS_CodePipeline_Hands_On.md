# 168. AWS CodePipeline Hands On

- **Type:** Practice lab

**Goal:** deploy code from GitHub to Elastic Beanstalk automatically.

## Create the pipeline

- Custom pipeline `MyFirstPipeline`, execution mode **Queued**, new **service role** (it grants what the pipeline may do), default artifact store and encryption.
- **Source:** **GitHub (version 2)**, recommended. It needs a **connection** and an installed GitHub app. Pick the repository and the `main` branch, with a trigger on **push to main**.
- **Build:** skipped for now (CodeBuild or Jenkins).
- **Deploy:** Elastic Beanstalk, the first (dev) environment.
- If the deploy lacks permission, attach the **Elastic Beanstalk administrator policy** to the pipeline's service role (acceptable for a demo only).

## Add production with approval

1. Edit the pipeline and add a stage **DeployToProd**.
2. First action group: **manual approval** (optional SNS topic, review URL and comments).
3. Second action group: deploy the **source artifact** to the **prod** environment.

A stage can hold **several action groups**, here two in sequence.

## Run it

- Committing a change to `main` (the background colour) **starts the pipeline**.
- Dev deploys first. Prod waits until someone **reviews and approves**.
- The **history** lists each run with its duration, result and commit.

**Note:** the lecture calls **CodeCommit** discontinued. AWS closed it to new customers in 2024; check its current status before relying on that.

## Exam takeaways

1. A source change **triggers** the pipeline.
2. **Stages** contain **action groups**; add **manual approval** before production.
3. Permission failures mean checking the **service role**.
