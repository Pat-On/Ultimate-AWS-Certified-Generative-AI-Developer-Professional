# 115. OpenAPI and Tool Usage

**OpenAPI** (formerly **Swagger**, and not to be confused with OpenAI) is a specification for defining interfaces between web services. It also defines the interface between **foundation models and the tools** they use in an agentic system.

## Why it matters for GenAI

- A strict definition of a tool's interface lets the model **use the tool more reliably**.
- It **standardizes function definitions** between the foundation model or agent and the tools it calls, by defining:
  - the **input parameters** the tool expects,
  - the **expected output** and its format,
  - the **error conditions** to expect.
- The model can then call the tool, and process its result, in the correct way.

## Example

A calculator tool, from the slide. It has an `/add` path with a `GET` operation that takes two required numeric query parameters `a` and `b`, and returns a `200` JSON response with a numeric `result`.

```yaml
openapi: 3.1.0
info:
  title: Calculator Tool
  version: 1.0.0

paths:
  /add:
    get:
      operationId: add
      summary: Add two numbers
      parameters:
        - name: a
          in: query
          required: true
          schema: { type: number }
        - name: b
          in: query
          required: true
          schema: { type: number }
      responses:
        "200":
          description: Sum
          content:
            application/json:
              schema:
                type: object
                properties:
                  result:
                    type: number
```

## Use with Bedrock action groups

- OpenAPI schemas are used with **Bedrock action groups**, which is how Bedrock Agents call tools.
- Either **upload the schema to S3** and refer to it, or **paste or edit it in the Bedrock console**.
- The action group then uses the schema to **guide the agent's tool use**, keeping it reliable and consistent.

## Exam takeaways

1. **OpenAPI** = formerly **Swagger**, a spec for tool interfaces with explicit **inputs, outputs and error conditions**.
2. With **Bedrock action groups**, provide the schema from **S3** or in the **console**.
3. **AgentCore Gateway** targets can also be OpenAPI interfaces (lecture 108).
