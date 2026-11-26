# 170. AWS CodeBuild Hands On Part 1

- **Type:** Practice lab

**Goal:** a build that tests whether "Congratulations" still appears on the web page.

## Project settings

| Setting | Choice |
|---|---|
| Name | `MyFirstBuild` |
| Source | **GitHub** through OAuth, the Node.js app repository |
| Trigger | Webhook: build on **push** (pull requests and releases are also possible) |
| Environment | Managed image, **Ubuntu**, standard runtime, `standard:7.0` |
| Service role | New |
| Timeout | Default **1 hour**, adjustable |
| VPC | Optional, needed to reach private resources such as databases |
| Compute | 3 GB memory, 2 vCPU |
| Buildspec | Use a buildspec file |
| Artifacts | None |
| Logs | CloudWatch Logs or S3 |

The first build **fails as expected**: the repository has no buildspec file yet.

## Exam takeaways

1. A CodeBuild project can be triggered directly by a **repository webhook**.
2. A **missing buildspec** fails the build.
