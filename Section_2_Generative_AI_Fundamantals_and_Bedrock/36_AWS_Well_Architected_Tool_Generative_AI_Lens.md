# 36. AWS Well-Architected Tool: Generative AI Lens

The **Well-Architected Generative AI Lens** is called out specifically in the exam guide. It is not a service but a set of **best practices**: an overview of generative AI and how to use it in an enterprise setting, in the same way there is a Well-Architected machine learning lens.

## Homework

- Read it at some point before the exam, at least at a high level. It is a set of web pages: https://docs.aws.amazon.com/wellarchitected/latest/generative-ai-lens/generative-ai-lens.html
- Every topic in it is covered by this course, so you won't miss anything by skipping it, but it is a useful review and the exam may refer to it explicitly.

## The six pillars

The Well-Architected framework maps different domains, such as generative AI, to best practices across the same six pillars:

1. Operational excellence
2. Security
3. Reliability
4. Performance efficiency
5. Cost optimisation
6. Sustainability

## The generative AI lifecycle

The lens structures things around this lifecycle, which is worth knowing **in order**. A newer exam question type gives you several steps and asks you to **put them in the right order**.

1. **Scoping:** define what you actually want to accomplish.
2. **Model selection:** choose the model appropriate for the task.
3. **Model customisation:** customise, fine-tune or augment the model if it doesn't do what you need off the shelf.
4. **Development and integration:** build on top of the customised model.
5. **Deployment.**
6. **Continuous improvement:** measure the results, keep improving, and loop back to scoping to build more on top of the application.
