# 10. More Depth on the Bedrock Converse API

The **Converse API** comes up a lot. You only need to know that it is the Swiss Army knife for message-based interactions with foundation models in Bedrock. It gives you one consistent API across models, so you can switch models in your application more easily.

## What you pass in

- **At a minimum:** a **prompt** and a **`modelId`**.
  - The prompt goes in the `messages` field, or can be a reference to a stored prompt in Bedrock Prompt Management (covered later).
- **Optionally:**
  - **`toolConfig`:** for agentic AI, the parameters for the set of tools the model may use.
  - **`guardrailConfig`:** guardrail settings. Guardrails filter out objectionable inputs and outputs (covered later).
  - **Model-specific information** and **configuration settings**.
- The details change quickly, so check the latest documentation for specifics and examples. The exam will never expect you to write code, but it is useful to understand how the API works.

## Request structure

This is the current structure of a Converse request:

```http
POST /model/modelId/converse HTTP/1.1
Content-type: application/json

{
   "additionalModelRequestFields": JSON value,
   "additionalModelResponseFieldPaths": [ "string" ],
   "guardrailConfig": {
      "guardrailIdentifier": "string",
      "guardrailVersion": "string",
      "trace": "string"
   },
   "inferenceConfig": {
      "maxTokens": number,
      "stopSequences": [ "string" ],
      "temperature": number,
      "topP": number
   },
   "messages": [
      {
         "content": [
            { ... }
         ],
         "role": "string"
      }
   ],
   "outputConfig": {
      "textFormat": {
         "structure": { ... },
         "type": "string"
      }
   },
   "performanceConfig": {
      "latency": "string"
   },
   "promptVariables": {
      "string" : { ... }
   },
   "requestMetadata": {
      "string" : "string"
   },
   "serviceTier": {
      "type": "string"
   },
   "system": [
      { ... }
   ],
   "toolConfig": {
      "toolChoice": { ... },
      "tools": [
         { ... }
      ]
   }
}
```

## Key fields

| Field | Purpose |
| --- | --- |
| `modelId` (in the URL path) | Which foundation model to use |
| `messages` | The conversation, each with a `role` and `content`. This is where your prompt goes |
| `system` | System prompt: overarching instructions for the whole conversation |
| `inferenceConfig` | `maxTokens`, `stopSequences`, `temperature` and `topP`, the same settings as in the playground (lecture 9) |
| `guardrailConfig` | Which guardrail (identifier and version) to apply, and whether to return a `trace` |
| `toolConfig` | The `tools` available to the model and a `toolChoice`, for agentic use |
| `promptVariables` | Values for a prompt stored in Prompt Management |
| `additionalModelRequestFields` | Model-specific request fields |

The remaining fields (`outputConfig`, `performanceConfig`, `requestMetadata`, `serviceTier` and `additionalModelResponseFieldPaths`) are in the structure but the lecture doesn't go into them. See the documentation.
