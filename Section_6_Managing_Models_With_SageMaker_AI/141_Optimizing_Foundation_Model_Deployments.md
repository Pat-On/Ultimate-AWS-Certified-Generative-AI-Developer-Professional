# 141. Optimizing Foundation Model Deployments

Specific advice for deploying foundation models on SageMaker AI, on top of the general deployment safeguards from the previous lecture.

## Endpoints and hosting

| Topic | Details |
| --- | --- |
| **Single and multi-model endpoints** | An endpoint can serve **more than one model at a time**, so you can reuse the same fleet for several models and avoid paying for capacity you do not need. |
| **Multi-container endpoints** | More generally, an endpoint can hold several **containers**, and they need not be foundation models. Each endpoint supports its own **deployment guardrails, VPC and network isolation**. |
| **Inference components** | Each model gets **its own scaling policy**, so models scale independently for different workloads. |
| **Train in SageMaker AI, deploy through Bedrock** | You can train or fine-tune a model in SageMaker AI (for example starting from a Hugging Face model) and then host it through **Bedrock Custom Model Import**. Inference becomes **serverless**, with none of the SageMaker complexity. |
| **Cross-region inference profiles** | For endpoints on **Bedrock**: if a region goes down or is overloaded, Bedrock redistributes traffic to other regions. Restrict it to a **geography** or choose **global**, which gives the **highest throughput** (details in a later lecture). |
| **EC2 Auto Scaling groups** | Can sit in front of SageMaker AI endpoints for **load balancing and auto scaling**. |

## Model servers on SageMaker AI

| Server | Notes |
| --- | --- |
| **TorchServe** | For PyTorch models. |
| **DJL Serving** | **Deep Java Library**, a Java-based deep learning library **created by Amazon**, so it is **more likely to appear on the exam**. You build deep learning containers and deploy them with DJL Serving. |
| **Deep Learning Containers** | The prebuilt containers used with these servers. |
| **Triton Inference Server** | Also supported. |

## Cost and efficiency

- **Asynchronous inference** when latency does not matter: SageMaker AI **async endpoints** take a request and return the result later. You can also build your own queue with **SNS or SQS** to control the rate of requests.
- **Model compression** makes a model smaller to deploy, which saves money and is a little faster:
  - **Quantization**: reduce the bit depth of the weights (32-bit to 16 or even 8) with little loss of quality.
  - **Pruning**: remove parts of the model that are not needed.
  - **Knowledge distillation**: train a **smaller model from a larger one**, passing the useful knowledge down.
- **Do not optimize prematurely.** Measure your real performance, costs and resource utilization first (monitoring and **CloudWatch**), and work back from problems that actually exist.

## Exam takeaways

1. An endpoint can serve **multiple models or containers**. **Inference components** give each model its **own scaling policy**.
2. A model trained or tuned in SageMaker AI can be hosted **serverlessly through Bedrock Custom Model Import**.
3. Model servers to know: **TorchServe, DJL Serving (Amazon's Deep Java Library, likelier on the exam), Deep Learning Containers, Triton**.
4. Use **asynchronous inference** (async endpoints, or SNS and SQS) when latency is not critical.
5. Shrink models with **quantization, pruning and knowledge distillation**.
6. **Measure before optimizing.**
