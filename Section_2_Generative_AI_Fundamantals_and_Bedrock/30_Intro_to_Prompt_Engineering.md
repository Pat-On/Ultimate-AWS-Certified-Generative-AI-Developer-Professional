# 30. Intro to Prompt Engineering

**Prompt engineering** is the art and science of asking a generative AI system the right way. How you ask matters a lot: the more detailed you are, the better, and the way you phrase a request can strongly influence the result.

## Benefits of effective prompting

The AWS training material lists four.

1. **Boost the model's abilities and improve safety.**
   - Asking the right way gets better results, and can get the model to do things you didn't think it could.
   - It can also improve safety: you can tell it not to leak sensitive information or to avoid wrong or harmful advice, simply by specifying that in the prompt.

2. **Augment the model with domain knowledge and external tools, without changing the model's parameters or fine-tuning it.**
   - The lecture says this is a grey area for "prompt engineering". It means techniques covered later in the course in the context of AWS services: **retrieval-augmented generation (RAG)** and **LLM agents**.
   - **Domain knowledge (RAG):** store your own documents and data in a form friendly to generative AI, retrieve what is relevant to the question, and include it in the prompt before it goes to the model. In a way it is "cheating": the original prompt is combined with information looked up from an external store.
   - **External tools:** the system can also be given functions it may call. For example, tell it that if it needs the current weather in a city it can use a given piece of code, or that it can call a function to fetch internal information in real time. The model can go back and forth, use the tool, and combine the results into a final response.

3. **Interact with language models to grasp their full capabilities.** Sometimes you have to play with a model to learn what it is good and not so good at.

4. **Achieve better quality outputs through better quality inputs.** Garbage in, garbage out, and the converse: a good prompt makes a good answer much more likely.
