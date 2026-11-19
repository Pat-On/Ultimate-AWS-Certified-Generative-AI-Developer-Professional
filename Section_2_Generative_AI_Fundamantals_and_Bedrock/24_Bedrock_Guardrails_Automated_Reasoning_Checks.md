# 24. Bedrock Guardrails Automated Reasoning Checks

Automated reasoning checks are another guardrail feature. "Reasoning" here is more than chain-of-thought prompting: the aim is to **enforce complex policies** about how your application works, at the guardrail stage.

## What it is for

- Policies that really must be enforced, such as **mortgage approval** or **medical information**.
- It can help **detect hallucinations in complex scenarios** like these.

## How it works

- You give Bedrock your policy as plain text in a **PDF**, and it breaks the policy down into **structured rules and logic** that the guardrail then applies.
- **Example policy:** "Full-time employees who have worked for at least 1 year are eligible for parental leave."
  - Bedrock extracts a boolean variable, **IsFullTime**.
  - If true, it checks **YearsOfService >= 1**, using the years of service taken from the employee's records.
  - If either check fails, **EligibleForParentalLeave = false**. If both pass, it is **true**.
  - That output variable is created automatically along the way.
- **API:** `CreateAutomatedReasoningPolicy`, where you give the policy a name and attach the PDF. That is all there is to it.

## Advice

- The PDF should be **clear, well organised and well structured**, so Bedrock can interpret it as well as possible.
- AWS recommends **starting simple and working up in complexity**. Things can go wrong if the document is interpreted incorrectly, so check that the guardrail behaves as you intended at each step.
