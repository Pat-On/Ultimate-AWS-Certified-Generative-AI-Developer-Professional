# 32. Prompt Best Practices

Amazon's recommended best practices for prompt engineering, with the lecture's bad and good examples.

## Practices and examples

| Practice | Bad | Good |
| --- | --- | --- |
| **Be clear and concise.** The wordier the prompt, the more room for things to go wrong | "Write something about books. Talk about two people and what they like. Make it interesting." | "Write a short dialogue between two friends discussing their favorite books." |
| **Include context** | "Write a short dialogue..." | "Write a short dialogue to be used in a movie script..." |
| **Specify the desired response type.** "Short" is vague | "Write a short dialogue..." | "Write a short dialogue where each line is no more than two sentences long..." |
| **Put the desired output at the end of the prompt.** It helps the model understand and deliver what you asked | "Write a short dialogue." | "Write a short dialogue between two friends discussing their favorite books to be used in a movie script, where each line is no more than two sentences long." |
| **Phrase the input as a question.** It more easily matches questions and answers the model saw in training | "Explain the benefits of regular exercise." | "What are the benefits of regular exercise?" |
| **Provide an example response** | "Determine the sentiment of the following sentence..." | The same, "using these examples": "I had a great time at the park today" gives positive, "That restaurant had terrible service" gives negative |

- **Examples also fix the format.** Because the examples show just the word "positive" or "negative", the model knows that is the output format. This is a good trick for getting somewhat **structured data** out of a model.

## Break up complex tasks

- LLMs aren't great at reasoning yet (today), so **do the reasoning for them where you can**: split a complex task, such as writing a large system, into simpler subtasks and have the model execute each one individually.
- Keep it simple. If unsure, you can ask the model whether it understands what you are asking, though the quality of the answer usually shows you.
- You can ask the model to **think step by step**, which is **chain-of-thought prompting** (lecture 33). It can generate the subtasks itself. This is as close as LLMs get to reasoning right now.

## Experiment and be creative

- LLMs are **non-deterministic** and change often, so you won't get the same answer every time. As models evolve, keep trying different prompts and see by trial and error what works best and what each model is good or bad at.
