# 39. Amazon Bedrock Data Automation

**Amazon Bedrock Data Automation** (**BDA**) automatically extracts structured data from documents, images, video and audio. It is fully multi-modal and is the Bedrock take on **intelligent document processing (IDP)**. If an exam question mentions IDP, BDA is the likely answer.

## What it is used for

- Preparing data for **vector stores** and **knowledge bases** by turning unstructured files into structured output.
- Example: a photo of a driver's license is recognised as such and returned as fields (licence number, date of birth, name, address, eye colour, organ donor flag).
- Video analysis: scene summaries and scene boundaries, explicit content detection, text embedded in the video, and ad detection.

## Output and concepts

- **Standard output**: send a file and BDA picks the sensible default (JSON for documents, a text transcript for audio, and so on).
- **Custom output** (documents, audio and images; video is more limited): define exactly which fields to extract in a **blueprint**.
- **Blueprints**: there are standard ones (for example driver's license, passport) that you can extend or modify, or you can define your own.
- **Project**: stores a set of blueprints/configuration for many document types. You then send data to the project.
- Programmatic use: the **InvokeDataAutomationAsync** API call takes a project and data and processes it asynchronously.

## Console demo

- Found in the Bedrock console under Build, then Data automation (menus change often). A built-in demo lets you pick a file, review results, then create a project and blueprint.
- Input can be uploaded or imported from S3. Output goes to an auto-created bucket by default, or a custom bucket. You can supply your own **KMS key** and tags.
- **Cross-region support must be enabled** for BDA to work.
- Result options: standard output granularity, text format (**Markdown**, plain text, **HTML** or **CSV**), **bounding boxes** (image coordinates showing where each value came from), **generative fields** (a description and summary), and JSON only versus JSON plus additional files (documents only).

## Supported modalities

| Modality | Input formats | Output |
|---|---|---|
| Documents | PDF, TIFF, JPEG, PNG, DOCX | JSON, or JSON plus files (CSV for tables, full text, Markdown); HTML or CSV export. Granularity: page, **element (default)** or word. Optional bounding boxes and generative summaries |
| Images | JPEG, PNG | Image caption, **IAB (Interactive Advertising Bureau) taxonomy** category, logos, text in the image, content moderation (JSON) |
| Video | MP4, MOV, AVI, MKV, WebM | Full video summary, chapter summaries, IAB taxonomy, full transcript, on-screen text, logos, content moderation (JSON) |
| Audio | AMR, FLAC, M4A, MP3, Ogg, WAV (multiple languages) | Summary, transcript with speaker and channel labels, topic segmentation, content moderation (JSON) |

- Reformatting to HTML or Markdown is a simpler alternative to the HTML-restructuring technique from the structured data lecture.

## Blueprint details

- **Field types**: basic fields (explicit, or implicit meaning transformed rather than raw), table fields, field groups, and **custom types** (for example an address type made of street, city, state and zip).
- Blueprints can be **generated from a prompt**: a foundation model drafts the blueprint for you.
- Blueprint uses:
  - **Classification**: class and description are used to match a document to the right blueprint automatically.
  - **Extraction**: specific fields, including from tables.
  - **Normalization**: **key normalization** (street, street address and street one treated as the same key) and **value normalization** (consistent date formats and similar).
  - **Transformation**: split data, restructure fields.
  - **Validation**: check that values are in range, the expected size and so on.
