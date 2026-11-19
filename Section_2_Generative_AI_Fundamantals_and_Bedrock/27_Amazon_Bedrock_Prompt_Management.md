# 27. Amazon Bedrock Prompt Management

Bedrock has built-in **prompt management**, so you don't keep reinventing prompts. It is more than version control: it is a way of building prompts into larger applications.

## What it provides

- **Reusable prompts:** store a specialised prompt once and share it across applications.
- **Versioning:** keep a history of how a prompt was refined, and roll back if you need to.
- **Variables:** placeholders for values, written in **double curly braces**. For example: "Make me a music playlist for `{{genre}}` music with `{{number}}` songs". In an application you collect the genre and number from the user, pass them into the prompt, and send it to the foundation model. This is a good way to pass structured user input into an application.
- **Prompt variants:** versions of a prompt tuned for different foundation models, inference configurations or other differences.
- **Prompt Builder** in the Bedrock console, to play with and test prompts.
- **Tools and caching:** you can associate tools and caching strategies with a prompt.
- **Deployment:** once tested, a prompt is deployed (as a version) and can be used within a **flow** (lecture 28), which ties prompts together into larger applications.

## Demo: creating a prompt

1. In the console go to **Build, Prompt management**, then create a prompt.
2. **Name** it using only letters, hyphens and underscores, with no spaces (the demo uses `music-playlist-prompt`). Add a description if you want. You can supply your own KMS key, or let Amazon manage it.
3. Write the prompt, optionally with a **system prompt** to guide the model further. Use `{{genre}}` and `{{number}}` for the variables.
4. Associate it with a **model** (the demo uses an Anthropic Sonnet model) or with a larger agentic system.
5. Adjust the **settings**: maximum output tokens, custom stop sequences and temperature.
6. Enter **test values** (the demo uses "vocal jazz" and 10) and run it in the prompt window to check the output.
7. Save it as a **draft**. You can also create a variant here.
8. From the level above, **create a version**. The demo publishes **version 1**, which can now be used in applications, for example in a flow.
