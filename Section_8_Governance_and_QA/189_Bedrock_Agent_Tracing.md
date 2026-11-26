# 189. Bedrock Agent Tracing

**Governance** means keeping track of everything the system does, for **audit and compliance**. The same records help **QA and troubleshooting**, which is why the section combines them.

An agent can behave like a black box. **Tracing** returns a structured **JSON `trace` object** showing its **reasoning**:

- Which **action groups** (tools) it called, how, and what came back
- Which **knowledge bases** it queried and what they returned
- **Error details**

**Example:** if an answer contains the wrong time, the orchestration trace leads back to the action group call that fetched it.

## Trace types

| Type | Shows |
|---|---|
| **PreProcessing** | How the user input was categorised |
| **Orchestration** | Action group and knowledge base calls; usually the **most useful** |
| **PostProcessing** | How the final response was assembled |
| **CustomOrchestration** | How the order of actions was decided |
| **RoutingClassifier** | How the request was classified and routed |
| **Failure** | Why a step failed |
| **Guardrail** | What guardrails did to input or output |

## Notes beyond the lecture

- The lecture says the trace is included unless disabled. With the `InvokeAgent` API you have to **ask for it** (`enableTrace`), which is off by default.
- The slide calls this feature **Bedrock Agents Classic** tracing.

## Exam takeaways

1. **Debug an agent with its trace**, mostly the orchestration trace.
2. Know the **trace types** and what each explains.
