# 156. Lambda with Bedrock

| Role | What Lambda does |
|---|---|
| **Agent tools** | The glue between **Bedrock Agents** and their tools: **parameter validation**, request shaping and **error handling** |
| **Model invocation** | Calls foundation models **on demand**, with no capacity to provision, and can **hide which model** is used behind one interface |
| **Webhooks** | Receives events from enterprise or external systems, for example to start **ingesting new data into a knowledge base** |
| **API back end** | Handles the **JSON events** from **API Gateway** |
| **Custom aggregation** | Combines **several models**: voting or **weighted averaging** of answers |

Calling several models for each request raises **cost** quickly, so do it only when **quality** or **resilience** justifies it.

## Exam takeaways

1. **Lambda implements agent tools**, including validation and error handling.
2. Lambda + Bedrock = **serverless model invocation** and an abstraction over the model choice.
3. **Ensembles** (voting, weighting) are custom logic you write in Lambda, at extra cost.
