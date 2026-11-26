# 172. AWS CodeDeploy

**CodeDeploy** automates upgrading an application from version 1 to version 2, with **gradual rollout** and **automatic rollback** on failure or a **CloudWatch alarm**. The file **`appspec.yml`** defines how a deployment runs.

**Targets:** EC2 and on-premises servers, Lambda functions, ECS services.

## EC2 and on-premises

- Needs the **CodeDeploy agent** on each instance (install by hand or with **Systems Manager**).
- Instances need **IAM permission to read S3**, where the application revision is stored.
- **In-place** or **blue/green** deployments.

| Speed | Effect |
|---|---|
| **AllAtOnce** | Fastest, most downtime |
| **HalfAtATime** | Capacity reduced by half |
| **OneAtATime** | Slowest, least impact |
| **Custom** | Your own percentage |

**In-place** stops and upgrades the same instances in batches. **Blue/green** creates a **new Auto Scaling group** with v2, moves the **load balancer** to it, then removes the old one.

## Lambda

Shifts traffic between two versions behind an **alias** (integrated with **SAM**).

## ECS

Deploys a new **task definition**, **blue/green only**, moving the load balancer between two **target groups**.

## Traffic shifting (Lambda and ECS)

| Strategy | Meaning | Lambda example (ECS uses the `ECS` prefix) |
|---|---|---|
| **Linear** | Add a share every N minutes | `LambdaLinear10PercentEvery3Minutes`, `...Every10Minutes` |
| **Canary** | Small share first, then all | `LambdaCanary10Percent5Minutes`, `...30Minutes` |
| **AllAtOnce** | Immediate | |

## Exam takeaways

1. **`appspec.yml`** (CodeDeploy) vs **`buildspec.yml`** (CodeBuild).
2. EC2 needs the **agent** and **S3 permissions**.
3. **ECS = blue/green only.** Know **linear vs canary**.
