# 22. Multimodal Models and Pipelines with Bedrock

"Multimodal" means **mixing different media types in the same model**: text, images, audio, video, documents and so on. For example, a model could accept text, a scanned image of some text, someone speaking, or a PDF.

## How it works

- The model has **specialised encoders for each media type**, and it produces **embedding vectors that are comparable across types**, so an image and a piece of text about the same thing can be compared directly.
- **Models in Bedrock that are multimodal:**
  - **Claude** handles images as well as text.
  - **Amazon Nova** is multimodal.
  - **Amazon Titan** has a multimodal **embedding** model.
- Example: put a picture of a chicken and some text about chickens through the multimodal embedding model, and you get back vectors that can be compared. A search for "chicken" can then return both the image and the text.

## Why it matters for RAG

- When retrieving context for a prompt, you can **retrieve data in whatever form is relevant**, not only text.
- **Searching:** ask the model for an embedding vector for whatever you have (image, text or video), then find the closest match in the vector database.
- It works **both ways**:
  - You can embed different media types into your RAG system.
  - You can send prompts that mix media types. For example, "here is a picture, what is it?" is embedded, found similar to chickens, and text about chickens comes back.

## Preparing input for Titan Multimodal Embeddings G1

- Model ID: **`amazon.titan-embed-image-v1`**. It is an embedding model only.
- You send a **JSON body** with `inputText` and/or `inputImage`. **You can pass text, an image, or both.**
- The image must be **base64-encoded** and decoded to a UTF-8 string, so it can travel as text:
  ```python
  model_id = "amazon.titan-embed-image-v1"
  input_text = "A chicken"
  with open("/path/to/image", "rb") as chick_pic:
      input_image = base64.b64encode(chick_pic.read()).decode("utf8")
  body = json.dumps({"inputText": input_text, "inputImage": input_image})
  ```
- **Pipeline implication:** your data-processing pipeline has to do this conversion at some point before it reaches the model. How you do that (SageMaker, Glue, something built into Bedrock) comes later in the course.
