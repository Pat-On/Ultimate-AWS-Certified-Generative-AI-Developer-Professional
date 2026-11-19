# 31. Anatomy of a Prompt

Amazon describes a good prompt as having four components: the **instructions**, the **context**, the **input data** and the **output indicator**.

## The four components

| Component | What it is | Example from the lecture |
| --- | --- | --- |
| **Instructions** | The task: what you want the model to do and how | "Write a short dialogue between two friends about their favorite books." |
| **Context** | Any external information that guides the model: the setting, or data you injected, for example retrieved from an external data store | "The two friends are sitting in a cozy café on a rainy afternoon." |
| **Input data** | The input you want a response for | Friend 1 loves fantasy novels with dragons and magic. Friend 2 prefers mystery novels with clever detectives and unexpected twists. |
| **Output indicator** | The type or format of the output, and its constraints | "The dialogue should be 200 words long and should express each friend's enthusiasm for their favorite genre." |

## Notes on each

- **Context** can be information about the environment, or external data you retrieved that is relevant to the problem. For instance, if you had a database of example dialogues between friends, you could retrieve some and include them.
- **Input data** can also carry **examples** of what you want. You might give a pair of friends and a sample of their dialogue, then another pair and theirs, which tells the model the exact style you want in the output. So input data can be used in more than one way.
- The **output indicator** says how you want to receive the result and what constraints apply, such as length and style.
