# 124. Running Amazon Quick: Security, Pricing, and Limits

The operational side of **Amazon Quick**: security and governance, the four pricing plans, and the limits the exam likes to test.

## Security and governance

Quick runs on the identity, network and compliance controls your security team already approved. It lets you control how data is used, where it is sent and who can use it.

- **Identity**: **IAM**, **IAM Identity Center**, **SAML 2.0** federation, **Active Directory**, **MFA**, **RBAC** and **SSO**. It integrates with your own enterprise identity systems, so you are **not limited to IAM** and users need no AWS console account.
- **Network**: private **VPC** connections via elastic network interfaces, **Direct Connect** or **Site-to-Site VPN**, plus **IP and VPC access restrictions**.
- **Encryption**: **TLS 1.2 minimum** in transit. **SPICE** (the engine that accelerates analytics queries, covered with Quick Sight) uses **block-level encryption at rest**. **KMS customer-managed keys** are supported and **configured before resources are created**.
- **Data controls**: **row-level security**, **namespaces** for multi-tenancy, **domain allow-listing**, **mobile device settings**, **data sovereignty** controls.
- **Assurance**: **guardrails** and **toxicity filters**, **CloudTrail** audit logging, your existing **AWS compliance programmes**.
- **Your data is not used to train models**, so it cannot improve a model your competitors might use.

## Pricing: four plans

A **30-day trial** is available. **Free** and **Plus** need **no AWS account**: they have their own login and user base, open to anyone. **Professional** and **Enterprise** need an AWS account.

```
                                   Free             Plus             Professional  Enterprise
Price / user / month               $0               $20 (annual)     $20           $40
Sign-up                            Email or social  Email or social  AWS account   AWS account
Custom chat agents                 -                Yes              Yes           Yes
Shared spaces and knowledge bases  -                Yes              Yes           Yes
Create dashboards and datasets     -                -                -             Yes
Quick Automate                     -                -                -             Yes
Pooled index storage               ~1 GB            10 GB            25 GB         50 GB
```

- **Free**: single user, about 1 GB index storage, no published agent-hour entitlement and no way to buy more. The plan itself does not expire; the 30-day **Plus** trial does.
- Free to Plus adds bigger storage quotas, **sharing of spaces and knowledge bases** and **custom chat agents** (not system chat agents).
- **Professional** and **Enterprise** add **$250 per account per month infrastructure fee**.
- Not all you can eat: agent hours beyond **4 (Pro)** or **8 (Enterprise)** per month cost **$3 per agent hour** and **$6 per research hour**.
- **Index storage overage** costs **$5 per GB per month**.
- Watch for these extra costs at scale.

## Limits and things to watch

- **Region coverage**: **AWS GovCloud (US)** supports only classic **Quick Sight** BI, with no AI features.
- **Space structure**: spaces **cannot nest**. At most **20 resources of each type** per space.
- **Chat uploads**: regular chats are limited to **20 uploaded files**.
- **Space capacity**: **10,000 files under 10 GB**; **500 MB** per PDF, Word or PowerPoint file; **50 MB** for other types.
- **Sharing**: sharing a space **does not grant access to its linked assets**. Access is an **intersection**: the user needs access to both the space and the asset. **Deleted assets fail silently**.
- **Access control**: **per knowledge base** by default. **Document-level ACLs** are available for **S3, SharePoint, Confluence and Google Drive**.
- **Connectors**: the 50-plus list is mostly **actions only**. The **knowledge base** source list is much shorter.
- **Plan gating**: **Quick Automate**, **dashboard authoring** and **asset certification** are **Enterprise-only**. Usage beyond what the plan includes (agent hours, index overage) is **billed separately**.

## Exam takeaways

1. Quick uses **IAM, IAM Identity Center, SAML 2.0, Active Directory, MFA, SSO**, **VPC, Direct Connect, Site-to-Site VPN**, **TLS 1.2**, **KMS** keys, **CloudTrail**, and does **not train models on your data**.
2. Four plans: **Free** ($0), **Plus** ($20 annual), **Professional** ($20), **Enterprise** ($40) per user per month. Free and Plus need no AWS account.
3. Professional and Enterprise add a **$250/account/month** fee. Overage is **$3 per agent hour**, **$6 per research hour**, **$5/GB/month** index storage.
4. **Quick Automate** and dashboard and dataset creation are **Enterprise-only**.
5. Limits: **20** resources per type per space, **20** uploaded files per chat, **no nested spaces**, **500 MB** for PDF, Word and PowerPoint, **50 MB** for other files.
6. **GovCloud** has no AI features. Sharing a space does not grant access to its assets.
