# 166. AWS CodePipeline

**CodePipeline** is a visual workflow that **orchestrates CI/CD**.

## Building blocks

| Phase | Options |
|---|---|
| **Source** | CodeCommit, ECR, S3, Bitbucket, GitHub |
| **Build** | CodeBuild, Jenkins, CloudBees, TeamCity |
| **Test** | CodeBuild, **Device Farm** (iOS and Android apps), third-party tools |
| **Deploy** | CodeDeploy, Elastic Beanstalk, CloudFormation, ECS, S3 |
| **Invoke** | Lambda, Step Functions |

## Stages

- A pipeline is made of **stages**, each with **sequential and/or parallel actions**.
- Example: build → test → deploy to staging → load test → deploy to production.
- A **manual approval** can be added at any stage, for example to review load test results before production.

## Artifacts

Each stage can produce **artifacts**, stored in an **S3 bucket** and passed to the next stage.

1. A developer pushes code to **CodeCommit**.
2. CodePipeline packages it as an artifact in **S3**.
3. **CodeBuild** receives it from there, so it needs **no direct access to CodeCommit**.
4. The build output goes back to S3 as another artifact.
5. **CodeDeploy** takes it and deploys.

## Troubleshooting

| Need | Use |
|---|---|
| React to state changes (failed pipeline, cancelled stage), for example by email | **EventBridge** (formerly CloudWatch Events) |
| See why a stage failed (the pipeline stops) | The **console** |
| An action cannot be performed | Check the pipeline's **IAM service role** permissions |
| Audit API calls, including denied ones | **CloudTrail** |

## Exam takeaways

1. Stages exchange data through **S3 artifacts**.
2. **Manual approval** gates a stage.
3. Failures: **EventBridge** for notifications, **IAM service role** for permissions, **CloudTrail** for auditing.
