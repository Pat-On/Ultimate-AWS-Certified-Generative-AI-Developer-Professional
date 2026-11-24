# 118. Amazon Q Apps - Hands On

Creating, testing and publishing a no-code app in **Amazon Q Apps**, using a customer feedback analyzer as the example.

## Steps

1. Open **Q Apps** from the left-hand menu and choose to **create a new app**. You must give instructions describing the app.
2. Pick one of the provided examples, here **customer feedback analyzer to parse and analyze customer feedback**. It fills in instructions: create an app that provides a high-level summary of customer feedback from a given file, and, given product categories, generates an outline.
3. Click **Generate**. Behind the scenes Q Apps creates an app that fits the requirements. You can always customize it.
4. The generated app has:
   - A **customer feedback file** upload field.
   - A **product categories** text input, with your own category names.
   - A **text output** card.
5. Click **Run** to get the customer feedback summary based on the file and categories. The lab uploaded an unrelated file, so the output was poor: the app said it had no access to customer feedback in that file.
6. Customize while experimenting:
   - **Add cards**: more user inputs, more text, more file uploads and more text outputs.
   - Each card is configurable. The **text output is driven by a prompt**, which references the other cards (the file and the product categories, highlighted in the prompt). In the example the prompt is: given the customer feedback file and the product categories, generate a high-level summary that outlines highlights and lowlights.
   - You can edit the prompt freely, for example "based on the file `@Customer Feedback File` do `Product Categories`", and decide whether the app uses **only approved data sources or also LLM knowledge**.
   - The lab discarded its changes. AWS is likely to add more card types over time.
7. **Publish** the app. It then appears in your **library** of Q Apps.

## Exam takeaways

1. Q Apps are created from a **natural-language description**, then **customized with cards** (inputs and outputs) and a **prompt**.
2. Prompts reference input cards, and you can restrict the app to **approved data sources** or allow LLM knowledge.
3. **Publishing** adds the app to a **library**, so the company can build Gen AI apps on its own data very quickly.
