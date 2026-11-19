# 33. Types of Prompts

Three prompt types you should know. They are widely recognised, not just an Amazon thing.

## Zero-shot

- **No examples given.** It relies on a model large enough to already know what you are asking for.
- Example: "Determine the sentiment of the following sentence..." with no examples. The model's training is enough to classify it as positive or negative.

## Few-shot

- The opposite: you **provide some examples** of the desired responses to given prompts.
- Example: "Determine the sentiment of the following sentence, using these examples: 'I had a great time at the park today' => positive; 'That restaurant had terrible service' => negative."
- Give as many as you like: the more examples, the more you steer the system.
- The examples teach **both** what counts as positive or negative **and the output format** you want, here just the word positive or negative.

## Chain of thought (CoT)

- Tell the model to **"think step by step"**, so it breaks a large problem into subtasks instead of tackling it all at once. This often gives a better result and one that is more **explainable**.
- Example: "Describe how to solve a quadratic equation using the quadratic formula. Think step by step, starting with the standard form of a quadratic equation, identifying the coefficients, and then applying the quadratic formula. Make sure to include an example equation and solve it."
- Here the prompt does two things: it says to think step by step, and it gives **explicit guidance on the steps** (standard form, coefficients, apply the formula), so you don't rely on the model to work out the breakdown. The model may even write code (for example Python) for some steps.
- Without "think step by step" the model might find the problem harder.
