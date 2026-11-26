# 173. AWS CodeDeploy Hands On

- **Type:** Practice lab (**terminate the EC2 instance** afterwards)

## IAM roles

1. A **CodeDeploy service role** for EC2.
2. An **instance role** with `AmazonS3ReadOnlyAccess`, so the instance can download the revision.

## Instance and agent

- Create the application `DemoApplication`, platform **EC2/on-premises**.
- Launch an Amazon Linux `t2.micro` allowing SSH and HTTP.
- Connect with EC2 Instance Connect, update, install **Ruby**, download and run the **agent installer**, then check that the agent service is running.

## Deployment group

- Tag the instance `Environment=Development`; the group **selects instances by tag**.
- Service role, **in-place**, EC2 instances, agent install by Systems Manager: never, configuration `CodeDeployDefault.AllAtOnce`, no load balancer.

## Deploy

1. Create an S3 bucket **in the same Region** and upload the application zip.
2. The zip's **`appspec.yml`** copies `index.html` to `/var/www/html` and runs **hooks**: install dependencies (Apache), start the server, stop the server.
3. Create a deployment pointing at the S3 URI.

**Lifecycle events:** ApplicationStop → DownloadBundle → BeforeInstall → Install → AfterInstall → ApplicationStart → ValidateService.

The first attempt **fails** because the **instance role was not attached**. Attach it and **retry**: the page appears at the instance's public IP.

## Exam takeaways

1. Instances are targeted by **tags** (or Auto Scaling groups).
2. A failed download usually means a missing **instance role**.
3. Know the **lifecycle event order**.
