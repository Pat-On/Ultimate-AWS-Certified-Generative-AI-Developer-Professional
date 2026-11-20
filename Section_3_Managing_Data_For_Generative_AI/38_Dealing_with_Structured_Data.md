# 38. Dealing with Structured Data

A set of specific structured-data topics called out in the exam guide and Skill Builder materials: formatting requests for models, recovering structure from unstructured text, chunking, and chat formatting.

## Request and response formats

- **Amazon Bedrock** expects **JSON**. Your application builds the JSON request (for example an input text plus a text generation config with parameters), dumps it to a string and sends it to the **InvokeModel** endpoint.
- The exact JSON format differs per model.
- **SageMaker AI** endpoints also expect a model-specific input and output format. For LLMs this is usually JSON (messages, optional max tokens, optional system prompt, chat history as a list of messages). Classical ML algorithms may use CSV, protobuf and similar formats.
- Key takeaway: neither service formats data for you. Your app or endpoint code is responsible for building the input JSON and for formatting the output.

## Extracting structure from unstructured data

- Problem: OCR'd documents or raw text lose headings, sections, metadata and especially **tables**. This applies to context placed in a prompt and to data retrieved from a **knowledge base** (RAG).
- Technique called out by Amazon: **reformat as HTML**. Most models understand HTML well, and it preserves tables and organisation.
- Tools: **Pandoc** (third party), **Amazon Textract** and **Amazon Comprehend**, within an ingestion pipeline. Amazon's prep materials suggest **AWS Glue**. **Bedrock Data Automation** is a newer and easier option.

## Chunking for RAG

- Chunking happens before embeddings are created for a vector store.
- One approach is to insert **divider strings** that mark where chunks should be split.
- On the fly: attach a **Lambda pre-processor** to a **Bedrock knowledge base**. Example: convert HTML header tags into section-break and subsection-break divider strings so the knowledge base chunks more intelligently.
- As a pre-processing step instead: **Glue ETL** in a larger pipeline.

## Formatting conversations for the Converse API

- The **Converse API** needs chat history as a `messages` array. Each message carries a **role** (`user` or `assistant`) and **content** (for example a text block).
- Messages alternate to record who is speaking, so the history is preserved across turns.
