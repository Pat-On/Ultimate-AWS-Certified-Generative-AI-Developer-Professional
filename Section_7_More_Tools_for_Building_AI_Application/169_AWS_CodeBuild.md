# 169. AWS CodeBuild

**CodeBuild** is a fully managed **continuous integration** service: it compiles code, runs tests and produces packages. No servers, no build queue, **billed per minute** of build time.

- **Sources:** CodeCommit, S3, Bitbucket, GitHub.
- **Instructions:** **`buildspec.yml` at the root of the code** (best practice and what the exam tests), or entered in the console.
- A build project can be defined in CodeBuild or from CodePipeline, and CodePipeline can invoke an existing one.
- **Environments:** prebuilt images for Java, Ruby, Python, Go, Node.js, Android, .NET Core, PHP; **extend a Docker image** for anything else.

## How it works

Source code plus `buildspec.yml` are loaded into a **container** (a prepackaged or custom **Docker image**), which runs the instructions. Optional **S3 cache** speeds later builds, logs go to **CloudWatch Logs** and S3, and **artifacts** are uploaded to S3.

## `buildspec.yml`

| Section | Content |
|---|---|
| `env` | `variables` (plain text), `parameter-store` (SSM), `secrets-manager` (secrets) |
| `phases` | `install`, `pre_build`, `build`, `post_build` |
| `artifacts` | Files to upload to S3, **encrypted with KMS** |
| `cache` | Files, usually dependencies, kept in S3 for later builds |

## Monitoring and security

CloudWatch **metrics** and **alarms**, **EventBridge** for failed builds, **IAM** permissions, **VPC** for network access, **KMS** encryption, **CloudTrail** for API logging.

## Exam takeaways

1. **`buildspec.yml` at the root.**
2. Never put secrets in plain text: use **Parameter Store** or **Secrets Manager**.
3. **EventBridge** reports failed builds.
