# 177. AWS Outposts and GenAI

| Reason | Detail |
|---|---|
| **Compliance** | AI and data laws differ between jurisdictions |
| **Privacy** | Sensitive or classified data that must not leave your organisation |
| **On-premises data** | Run AI next to the data |

**Considerations:** provision enough **compute and storage** for foundation model inference, based on your data volume and needs; use **local caching** to limit data movement, including what is sent to external models.

## Exam takeaway

**Data that may not leave the premises + generative AI → Outposts**, sized for inference.
