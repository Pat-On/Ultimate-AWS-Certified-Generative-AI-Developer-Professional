# 199. CloudWatch RUM

**Real User Monitoring**: in the exam guide, though not specific to generative AI.

## What it does

- Measures performance from **real user sessions**, not synthetic ones.
- The lecture presents it for **mobile apps** (**iOS** and **Android**): add a code snippet to the app. (RUM also covers **web applications**.)
- Shows **page load times, errors, app launch times** and **responsiveness**.
- Integrates with **CloudWatch Application Signals**, with results viewable through **X-Ray traces**.

Relevant to generative AI when your application has such a front end and you want its **end-to-end performance**.

## Exam takeaways

1. **Real users** → **RUM**; **simulated users** → **Synthetics (canaries)**.
