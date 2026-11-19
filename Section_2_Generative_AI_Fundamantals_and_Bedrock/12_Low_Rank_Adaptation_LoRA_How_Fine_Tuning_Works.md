# 12. Low-Rank Adaptation (LoRA) - How Fine-Tuning Works

**LoRA (low-rank adaptation)** is a popular, long-established way to fine-tune a foundation model without retraining the whole model from the ground up. It adds a small amount of trainable information alongside the model instead.

## How it works

- Rather than updating the entire model, you add **low-rank matrices** to the model, usually to the **attention weights**, and train only those.
  - Self-attention is the layer, introduced in Google's paper "Attention Is All You Need", that lets an LLM understand how the words in a phrase relate to each other. It is the heart of how LLMs work, so a little extra training there goes a long way.
  - Other parts of the model can be targeted too, but the attention weights are the most interesting.
  - **"Low rank"** just refers to the simplicity of these extra matrices. The exam does not expect the maths.
- **At inference time**, the fine-tuned weights are **added into the base model's pre-trained weights** before output is generated.
- The **base model itself stays unchanged**. The fine-tuned weights are a small separate set that is combined with it at inference.

## Why it is efficient

- You pay only for training the extra bits, not for rebuilding a huge model.
- It is very efficient for **storage, training and inference**.

## LoRA versus an adapter layer

- LoRA puts the extra weights **alongside** the model's layers (to the **side**).
- An **adapter layer** instead adds a new layer **on top** of the model, so the fine-tuned information is embedded after everything else, as an afterthought.
- Both work, but LoRA tends to work better.
