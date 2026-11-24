# 100. Hands On: Amazon Bedrock Agents Classic

Building an agent in **Amazon Bedrock Agents (Classic)** that combines the self-employment **knowledge base**, a **guardrail**, a **foundation model** and a custom **action group** backed by Lambda.

## Heads-up

- Bedrock Agents was deprecated effective **July 30, 2026** and is closed to new users. AWS points people to **Amazon AgentCore** instead.
- The exam has not caught up, so you may still see questions on **Bedrock Agents (now Bedrock Agents Classic)**.
- You may not be able to follow along, so watch and understand it. Later you will integrate the same pieces with AgentCore.

## Building blocks from earlier

- A **knowledge base** about a self-employment book.
- A **guardrail** that filters politics, profanity, personal information and the word "potato".

## Steps

1. In the Bedrock console, go to **Build > Agents** and **create an agent**. Give it a name and a **description**. Fill in descriptions, because Bedrock may use them to **route requests** to the right agent in a multi-agent system.
2. Create a **new service role** (or reuse one) and pick the **foundation model** (the default was Claude 3.5).
3. Write the **agent instructions**, which work like a system prompt. State what the agent does (answer self-employment questions from the knowledge base, weather questions from the weather action group) and optionally a tone or style. The agent **cannot be prepared with empty instructions**: you get "Agent instruction cannot be null".
4. Review the **additional settings**:
   - **Code interpreter** can be enabled to write, run and test code. It is not needed here.
   - **User input** can be enabled so the agent asks follow-up questions, for example for a missing city.
   - **Custom KMS encryption** and an **idle session timeout**. The default is 10 minutes, which is more than needed.
5. **Add an action group** named `get weather`. Describe it as retrieving the current weather for a given city in Celsius or Fahrenheit.
   - Define it with **function details**. You could instead use the schema of an existing Lambda or API Gateway setup.
   - Choose **create a new Lambda function**. Creating the action group generates an **empty boilerplate Lambda**.
   - Name the function `get weather` and describe it. More detail about the expected input helps.
   - **Confirmation before running** the action group is optional and was left off.
   - Parameter `city`: string, **required**, described as the name of the city for which weather is requested.
   - Parameter `units`: string, **not required**, described as the desired temperature units, Celsius or Fahrenheit.
6. **Write the Lambda code.** The boilerplate extracts the **action group, function name, message version and parameters** from each request. The handler:
   - Defaults `city` to none and `units` to Fahrenheit, then overrides them with any values supplied.
   - Logs the values for debugging.
   - Returns a **structured response** whose body says the weather is 75 degrees and sunny. A real agent would call an external weather API.
   - Deploy the function.
7. Back in the agent builder, review **memory**. It is needed to keep context across a conversation or recall past actions. It was left off for this one-shot test (covered later).
8. **Add the knowledge base** and give it instructions, for example "use this knowledge base for questions about self-employment". The instructions let the agent route those queries to it.
9. **Attach the guardrail**.
10. Leave **orchestration strategy** at the default. Custom prompts could change it. Multi-agent collaboration features also exist.
11. **Save and Prepare** the agent. Prepare is greyed out until you save.
12. **Test** it and use **Show trace** to inspect the **pre-processing, routing, orchestration and post-processing** steps.

## Test results

- **Knowledge base query** (health insurance when self-employed): returned relevant information with a **citation**. The orchestration trace showed the underlying system prompt and the model deciding to search the knowledge base.
- **Weather in Orlando** with the guardrail on: "Orlando" was **masked**, because the guardrail treats **addresses as PII** and anonymizes them. The pre-processing trace showed the intervention. The guardrail was cleared from the agent (then Save, Prepare again) rather than edited.
- **Weather without the guardrail**: the answer was **75 degrees Celsius**. The trace showed the model **supplied its own default of Celsius** even though `units` was optional, so models can be too clever. Fixes are to make the parameter required or to put a **default (Fahrenheit) in the tool instructions**.
- **Weather in Fahrenheit**: worked, and the model even converted the result to Celsius.

## Deploying

- To use the agent from a real application, select the agent, **create an alias** (name and description). This creates a **versioned alias deployment** used as the production endpoint. It was not done here to avoid production costs.

## Cleanup

Deleting the agent does **not** delete its associated resources, which must each be removed separately. These keep costing money, especially the **OpenSearch** vector store.

1. Delete the **agent** (type "delete" to confirm).
2. Delete the **knowledge base**. This does not delete the underlying vector store, only the data in it.
3. Delete the **guardrail**.
4. In **OpenSearch Serverless**, delete the **collection**. It keeps accruing charges even when unused.
5. Delete the **Lambda function** (the weather function).
6. The data in **S3** also remains and needs cleanup.

## Exam takeaways

1. The agent combines a **foundation model, action group (Lambda), knowledge base and guardrail**.
2. Agent **instructions are mandatory** to prepare the agent. **Descriptions** help routing between agents.
3. **Show trace** exposes pre-processing, routing, orchestration and post-processing, and shows guardrail interventions and knowledge base use.
4. An **alias** gives a versioned production endpoint.
5. Deleting an agent does **not** delete its Lambda, knowledge base, vector store or S3 data.
