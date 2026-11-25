# 136. Amazon Bedrock Cross-Region Inference

**Cross-region inference** distributes inference workloads across AWS regions. Many Bedrock features require it or strongly recommend it, so it matters for efficiency and availability.

## What it does

- If a region has a **service interruption**, it **automatically switches** inference to another region.
- If a region has **quota restrictions or peak usage**, it **reroutes** inference to keep throughput going.

## The Organizations catch

- **Service control policies (SCPs)** in AWS Organizations can **block regions**. If an SCP blocks a region, cross-region inference cannot use it.
- Make sure the SCP allows every region you might be sent to, or leave the region **unspecified** in the policy.

## Inference profiles

| Profile | Behavior | Use it for |
| --- | --- | --- |
| **Geographic** | Selects the optimal region **within a specific geography** (for example within the EU). | **Data residency** requirements. Standard pricing. |
| **Global** | Selects the optimal **commercial AWS region** available. | **Maximized throughput**, with a **10% cost saving**. |

## Good to know

- It **does not work with provisioned throughput**: provisioned capacity is tied to one region.
- **Pricing is based on the region you called from**, even if Bedrock runs the request elsewhere.
- You **do not have to enable** the other regions in your account (SCPs still matter).
- Data is **encrypted in transit**, and the requests are **logged in CloudTrail**, so you can see where they went.
- Generally you want it on, unless a legal obligation restricts where your data may go.

## Exam takeaways

1. Cross-region inference routes around **outages, quota limits and peak usage** by spreading workloads across regions.
2. **SCPs that block a region** break it: allow all regions or leave the region unspecified.
3. **Geographic** profile = data residency within a geography. **Global** profile = maximum throughput and a **10% saving**.
4. It **cannot be combined with provisioned throughput**.
5. Billing follows the **calling region**, no region enabling is needed, and everything is **encrypted in transit and logged in CloudTrail**.
