# 148. SageMaker on the Edge (Neo)

"The edge" means deploying your **trained SageMaker models to edge devices**: an embedded computer in a self-driving car, a smart camera such as an **AWS DeepLens**, and so on.

## SageMaker Neo

- **Train once, run anywhere.** Neo **compiles and optimizes** your model for specific edge devices.
- Supports **ARM, Intel and Nvidia** processors.
- Takes models written in **TensorFlow, MXNet, PyTorch, ONNX and XGBoost** (the slides also list **DarkNet and Keras**) and optimizes them for the target device.
- Neo has a **compiler** (which produces the code the edge processor expects) and a **runtime library** (which runs on the device to use the compiled model).
- **Why run at the edge:** you do not need to go over the internet to a cloud endpoint. For **latency-sensitive** uses, such as a self-driving car deciding whether to brake, the model must run **locally** on the device.
- Memory aid: Neo is a character in *The Matrix*, where everything is code surrounding you, so Neo puts your model's code on the devices around you.

## Neo and AWS IoT Greengrass

- A Neo-compiled model can be deployed to an **HTTPS endpoint**, hosted on **C5, M5, M4, P3 or P2** instances, and it must be the **same instance type used for the compilation**. That defeats much of the point of Neo.
- The interesting pairing is **IoT Greengrass**: it is **how you get the model onto an actual edge device**, giving **inference at the edge with local data, using a model trained in the cloud**. Greengrass uses **Lambda** functions for inference applications.
- The full picture: **train on SageMaker in the cloud, compile with Neo, deploy to devices with IoT Greengrass**, with Lambda for inference.

## Exam takeaways

1. **Neo** = compile a trained model for **specific edge hardware** (ARM, Intel, Nvidia), from TensorFlow, MXNet, PyTorch, ONNX or XGBoost. It has a **compiler and a runtime**.
2. **IoT Greengrass** deploys the Neo-compiled model to the device, with **Lambda** for inference.
3. A Neo model on an HTTPS endpoint must use the **same instance type** as the compilation.
4. Edge inference suits **low-latency or offline** uses.
