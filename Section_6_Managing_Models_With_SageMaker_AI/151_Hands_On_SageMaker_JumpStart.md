# 151. Hands On: SageMaker JumpStart

A tour of **SageMaker JumpStart** foundation models. **It costs real money**: the instructor recommends **watching, not following along**, because of the real risk of forgetting to shut something down and getting a bill of **thousands of dollars**.

## Steps

1. In the console, open **Amazon SageMaker AI**. Under **JumpStart** there are **Foundation models**, **Computer vision models** and **Natural language processing models**.
2. The foundation models list includes **Stable Diffusion** (image generation), **Meta Llama** models, **AI21 Jurassic-2**, **Cohere**, **Falcon** and many **Hugging Face** models (the usual repository for academic and research models). It changes as AWS adds models.
3. Selected **Falcon 40B Instruct BF16**: a **text generation** model, **40 billion parameters** (the transcript says 140, a slip), **decoder-only** like GPT, free under the **Apache 2.0** license. You could also run it in Google Colab, probably faster and cheaper, but here you pay for the **flexibility and control inside your AWS resources**.
4. **View model** shows the description, a link to the **Hugging Face model card**, notes (it may not be the best choice for further fine-tuning, and a smaller **Falcon 7B Instruct** is suggested) and sample code.
5. **Open model in Studio** needs a **SageMaker domain**: the shared environment for your account, with storage shared among users and high-level configuration. **Quick setup for a single user** (or "set up for organizations" for security settings, tool access, network security and encryption) took **about 5 minutes** and created default permissions, roles, a **default VPC and subnets**, and a **default user profile** (its name cannot be changed later). Domain details also include **space management** (shared spaces with a shared EFS directory for a team), app configurations and a **resources** tab showing what is running.
6. **Launch Studio** from the user profile, go to **Notebooks** (a read-only preview), then **open in JupyterLab**: create a **space** (it took about 5 minutes) and open the notebook.
7. The notebook code, using the **`JumpStartModel`** class: give the **model ID** (`huggingface-llm-falcon-40b-instruct-bf16`), a version (`*` for the latest), set **`accept_eula=True`**, then **`deploy()`**. This is where the money is spent.
8. **`retrieve_all_examples`** runs sample prompts (question answering, sentiment analysis and so on) and prints inputs and outputs. You can set a **random seed** for consistent results, **temperature**, **top_k**, **top_p** and a **stop token** so the model does not keep generating.
9. When finished, call **`predictor.delete_predictor()`**: the hardware is very expensive.

## It would not even run

The model's **default inference instance is an extremely large (48xlarge-class) GPU instance** that costs a huge amount, and the deployment fails with a **resource limit error**: **you must ask AWS for permission** to use hardware that expensive.

## Cleanup (important)

Even without deploying the model, the domain created resources that keep billing. To be safe, **delete the whole domain**:

1. **Resources tab**: **stop** the running JupyterLab app (it used an **ml.t3.medium** instance).
2. **Delete the shared space** created for the notebook.
3. **Delete the user profile**.
4. **Delete the domain** (under domain settings, scroll down).
5. **Refresh** the page to confirm it was deleted, since it does not update on its own.

## Exam takeaways

1. **JumpStart** gives one-click access to foundation, computer vision and NLP models from model zoos including **Hugging Face**.
2. A **SageMaker domain** holds shared storage, configuration, user profiles and spaces. Quick setup creates defaults, including a VPC and roles.
3. Deploying a JumpStart model uses the `JumpStartModel` class (`model_id`, `accept_eula`, `deploy`), and you **must delete the predictor** afterwards.
4. Large models need **expensive instance types** that may require a **quota increase request**.
5. **Clean up** by stopping apps, deleting spaces and user profiles, and finally the domain.
