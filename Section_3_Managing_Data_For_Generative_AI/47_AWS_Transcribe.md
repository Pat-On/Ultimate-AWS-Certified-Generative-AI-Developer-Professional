# 47. AWS Transcribe

**Amazon Transcribe** automatically converts speech to text using a deep learning process called **ASR (automatic speech recognition)**.

## Features

- **PII redaction**: automatically removes personally identifiable information such as names, ages and social security numbers.
- **Automatic language identification** for multilingual audio (for example French, English and Spanish in one recording).
- Use cases: transcribing customer service calls, automated closed captioning and subtitling, and generating metadata for media assets to build a searchable archive.

## Improving accuracy

- **Custom vocabulary**: add specific words, phrases, brand names, acronyms and domain terms, optionally with hints such as pronunciation. It teaches new **words**.
- **Custom language model**: train on your own domain-specific text so Transcribe learns **context** (for example, in IT "microservice" is one word, rather than "my crow service"). It does not teach new words.
- Use **both together** for the highest transcription accuracy.

## Toxicity detection

- ML-based, works directly on voice samples. It combines **speech cues** (tone and pitch) with **text cues** (profanity, hate speech); the combination of audio and text drives the result.
- Categories: sexual harassment, hate speech, threats, abuse, profanity, insult and graphic.
- The instructor flags this as something that can come up on the exam.
