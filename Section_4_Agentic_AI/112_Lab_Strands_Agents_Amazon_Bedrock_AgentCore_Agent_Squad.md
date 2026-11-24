# 112. Lab: Strands Agents, Amazon Bedrock AgentCore, Agent Squad

A hands-on lab that builds one **Strands** agent with tools, deploys it with **AgentCore**, then uses **Agent Squad** to orchestrate it alongside a Bedrock LLM. The setup is complex and the tools, models and package versions change quickly, so it is fine to just watch. The concepts matter more than the commands.

## What gets built

- A **Strands agent** with three tools: the built-in **calculator** and **current time** tools, and a custom `count_keyword` tool that counts how often a keyword appears in a text. A system prompt makes it act like a chicken, so its replies are easy to recognise.
- The same agent **wrapped for AgentCore**, run locally (`python`, then `agentcore dev`) and deployed to the cloud on the **AgentCore Runtime**.
- The same agent behind **Agent Squad** as an **orchestrator**. Computation and time queries go to the Strands agent, everything else goes to a general Bedrock LLM.

## Prerequisites

- A **Python** environment (3.10 or newer).
- The **AWS CLI** installed and configured (`aws configure`), preferably with an **administrator** user. In the real world, restrict it to least privilege.
- Use **one region** for all resources, and pick a region where Bedrock and **AgentCore** are supported. Strange errors can mean an unsupported region.
- A **Bedrock API key**, set in the `AWS_BEARER_TOKEN_BEDROCK` environment variable. Restart your Python environment afterwards so it picks the variable up.
  - Create it in the Bedrock console under **API keys**.
  - A **long-term** key suits development. **Short-term** keys suit applications where users authenticate (for example through Cognito) and get short-lived access per transaction.
- For the **AgentCore CLI**: **Node.js 20+** (nodejs.org), **uv** (docs.astral.sh/uv, used by the CLI to manage Python dependencies when packaging) and **git** (git-scm.com/install).
- Pinned package versions, installed with `pip install`. The lab's `requirements.txt` lists `bedrock-agentcore==1.18.1`, `strands-agents==1.50.1` and `strands-agents-tools==0.8.5`; the other two were installed separately:
  - `agent-squad==1.0.2`
  - `strands-agents==1.50.1`
  - `boto3==1.43.56`
  - `bedrock-agentcore==1.18.1`

## Warnings

- **Agent Squad is fragile.** A current bug sends the `citations` field to Bedrock, which cannot handle it and crashes, so Agent Squad is pinned to `1.0.2`. That version in turn depends on models that are no longer supported.
- Models, tools and frameworks are deprecated and change constantly, which is a general problem in agentic AI development.
- AWS appears to be pushing **AgentCore** over Agent Squad, so Agent Squad may not stay on the exam.
- A deployed AgentCore runtime is a real resource that **bills you**. Do the cleanup at the end.

## Steps

1. **Strands agent** (`strandsagent.py`):
   - Import `Agent` and `tool` from `strands`, and the `calculator` and `current_time` tools from the Strands tools package.
   - Mark a function with the `@tool` decorator to make a custom tool. The docstring tells Strands, and the model, what it does and how to call it. `count_keyword` takes the text and the keyword and returns the number of occurrences.
   - Create `Agent(tools=[...], system_prompt=...)`. The model is optional, and the default is used to stay future-proof.
   - The standalone test asks for the time, a calculation and a keyword count in one message. Run it with `python strandsagent.py`.
   - Result: the log shows each tool call, and the chicken returned the time, the calculation result (**42**) and the keyword count.
2. **Wrap it for AgentCore** (`agentcore.py`):
   - Import `BedrockAgentCoreApp` and create `app = BedrockAgentCoreApp()`.
   - Put the agent in a function decorated with `@app.entrypoint`. It receives a `payload` and a `context` from AgentCore, builds the Strands agent with the same tools and system prompt, and returns the response.
3. **Test locally**: run `python agentcore.py`. It looks idle but is a local server on **port 8080**, endpoint `/invocations`. Send it a `curl` POST with a prompt such as "What is the current time?". The response comes back and the server logs it. Stop it with Ctrl+C.
4. **Install the AgentCore CLI** from its GitHub repo (github.com/aws/agentcore-cli) using the `npm install` command in its README, which needs Node.js. The README lists supported frameworks and model providers (Bedrock, or Anthropic, Gemini and OpenAI directly), the CLI commands, and the **harness** (no-code) features, plus observability, evaluations and A/B tests.
5. **Create a project** with `agentcore create`:
   - Project name and agent name: `bedrock_agent_core_app`.
   - Choose an **agent** rather than a **harness**. A harness is the no-code option: a basic runtime, model and memory that you extend with tools and skills through configuration.
   - Choose **create new agent** (bring your own code), as opposed to importing an existing Bedrock agent, which is the migration path.
   - Options: **Python**, **direct code deploy**, **HTTP**, **Strands** framework (this only sets which dependencies are generated), **Amazon Bedrock** as the model provider, and no memory.
   - Skip the advanced settings. They cover custom authorization (important for controlling access), custom file systems, timeouts and networking.
6. **Swap in your own code**:
   - Copy the contents of `agentcore.py` into the generated `app/bedrock_agent_core_app/main.py`.
   - Unicode fix for the dev environment: cast the result to a string and set a null callback handler.
   - Add `strands-agents-tools` to the generated `pyproject.toml` (version `0.8.5` suits this set of dependencies).
   - From the agent folder (`app/bedrock_agent_core_app`), run `uv sync` to pull it in.
7. **Run in the dev environment**: from the project root, run `agentcore dev`. It launches the agent locally and opens a browser window to chat with it. Prompt "What is the current time?" and the chicken replies.
8. **Deploy**: run `agentcore deploy`. The CLI syncs the CDK dependencies, builds the project, creates a **CloudFormation** stack with the CDK and IAM resources, and publishes to the **AgentCore Runtime**. In the console, Bedrock, then **Build**, then **AgentCore**, then **Runtime** shows the runtime at version 1. The console also has gateways, memory, policy, identity, payments, a harness (the new no-code option, apparently meant to replace Bedrock Agents) and a playground.
9. **Invoke in the cloud** with `agentcore invoke`, passing JSON with a `prompt` key as a single-quoted string with escaped inner quotes (the quoting is the tricky part). Prompt "what is five plus seven?" hit the calculator tool and returned **12**.
10. **Remove the deployment**: run `agentcore remove all`, confirm, then run **`agentcore deploy`** again and confirm. `remove all` does not delete anything until the deploy applies the change.
11. **Agent Squad** (`squad_demo.py`), while the runtime deletes:
    - The built-in Strands support in Agent Squad does not work, because it was built against an older Strands version. The workaround is a small `StrandsAdapterAgent` wrapper that converts the Strands format into what Agent Squad expects. Anything could be wrapped this way, including a call to a deployed AgentCore runtime.
    - The wrapper is given a **name and description** (calculator, time, keyword counting), which the orchestrator uses to decide routing. It wraps the Strands agent, imported from the previous file.
    - A **Bedrock LLM agent** is the general assistant. The lab video used **Claude 3 Sonnet**, which had to support inference and not be marked legacy at recording time, while the shipped `squad_demo.py` uses `amazon.nova-lite-v1:0` (and `amazon.nova-micro-v1:0` for the classifier). You may need to try other model IDs, and the Agent Squad GitHub samples help.
    - Create the `AgentSquad` orchestrator and add both agents. A helper extracts the text from responses, and a chat loop reads prompts until you type `quit` or `exit`, passing each to the orchestrator's route request.
    - The Strands agent runs **locally** here. Unlike AgentCore, Agent Squad does not deploy anything, so you would host it yourself on ECS or an inference endpoint.
    - Run `python squad_demo.py`.
12. **Test routing**:
    - "What is the current time?" was routed to the Strands adapter agent and the chicken answered.
    - "What is the meaning of life?" was routed to the general Bedrock assistant. It was slower because the demo does not stream (the Agent Squad repo has streaming samples).
13. **Clean up**: check the AgentCore console (the runtime list should be empty), then check **ECR**, **ECS** and **CodeBuild** (the slides also list **EKS**). An **ECR repository** was left behind and had to be deleted manually. A running ECS service or other leftovers would keep billing.

## What the lab showed

- Strands makes an agent with tools in a few lines of code, and AgentCore deploys it with one more decorator and a few CLI commands.
- Agent Squad needs more code for a simpler job (routing), and it does not deploy anything for you.
- Agent Squad's routing could be done more simply with **Amazon Bedrock Flows**: a prompt into a classifier LLM, then conditions routing to different agents. It may be subsumed by Strands agents and Flows.
- Bedrock often leaves resources behind after deletion. Deleting a knowledge base does not delete its **OpenSearch Serverless** collection, which keeps billing, and AgentCore left an ECR repository.

## Exam takeaways

1. **Strands** is the agent SDK: `Agent` plus tools, with `@tool` for custom tools and built-in ones such as calculator and current time.
2. **AgentCore** wraps an agent with `BedrockAgentCoreApp` and `@app.entrypoint`, tests it locally (port 8080, `/invocations`, or `agentcore dev`) and deploys it to the **AgentCore Runtime** with `agentcore deploy`, built on CDK and CloudFormation.
3. The AgentCore **harness** is the no-code option (runtime, model, memory, plus tools and skills in configuration), and AgentCore is not tied to Bedrock models.
4. **Agent Squad** is an **orchestrator** that routes each query to the agent whose name and description fit, with a general Bedrock LLM as fallback. It does not deploy your agents.
5. Cleanup is `agentcore remove all` **and then** `agentcore deploy`. Then check the console, ECR, ECS and CodeBuild for leftovers.
6. Bedrock API keys: **long-term** for development, **short-term** for applications, set in `AWS_BEARER_TOKEN_BEDROCK`.
7. Use one region that supports all the services used.
