# 116. Humans in the Loop

Injecting **human judgment** into agentic AI systems, for when you can't fully trust the AI or the task is complicated.

## Patterns

- **Human augmentation**: the AI prepares drafts and **humans refine** them. Refining a document a chatbot drafted already makes you a human in the loop. This can be low-tech.
- **Escalation criteria**: the system routes **complex or uncertain cases** to a human expert.
  - Example: a customer-service agent that isn't resolving the problem recognises it and escalates, for instance by filing a ticket for a human.
  - The decision uses **confidence scores or risk assessments**: if confidence is below a threshold, a human gets involved.
  - **MCP integrations** can fire off the ticket, for example a **Jira** ticket in an external ticketing system.
- **Human feedback for improvement**: preferences collected from people tune and refine the system, such as a chatbot offering two responses to choose between. It can go wrong, as with a period when ChatGPT became overly sycophantic.

## Collecting feedback on AWS

The architecture on the slide: the AI application asks the user to rate the response, and the feedback flows through:

1. **Amazon API Gateway**, fronting the feedback collection.
2. **AWS Lambda**.
3. **Amazon DynamoDB**, storing the feedback with **indexing** so it can be analysed later.

Use it to measure **which foundation model, variant or fine-tuned model** pleases human users most.

## Exam takeaways

1. Human in the loop covers **augmentation** (humans refine AI drafts), **escalation** on low confidence or high risk, and **feedback** for continuous improvement.
2. Feedback collection: **API Gateway, then Lambda, then DynamoDB** (indexed for analysis).
3. Compare models or variants by the **human preference** data collected.
