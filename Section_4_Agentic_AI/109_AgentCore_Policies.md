# 109. AgentCore Policies

**AgentCore Policy** is a more recent feature giving tighter control over **what agents may do, and under which conditions**. It addresses **trust**: the Gateway lets an agent call external services, but you must trust it before letting it use your credentials and spend money.

## How it works

- Integrates with one or more **AgentCore Gateways** and controls what the agents behind them can access.
- It **intercepts every tool call**, outside the agent's code, and **evaluates it against your policies**.
- Flow: the agent requests an action through a tool call, it goes through the **Gateway**, the **policy engine** applies the **Cedar** policies to **allow or deny**, and only if allowed is the tool, API or external MCP server called.
- Policies are evaluated **outside the agent's code**, so the agent cannot hide or bypass them, which makes enforcement more reliable.
- **Very fine-grained**: who can do what under which conditions.
- Policies are tied to gateways, so you **must use a Gateway to use policies**.

## Cedar

- Policies are written in **Cedar**, an **open-source policy language**.
- Example: a refund agent may call `process refund` only if the **amount is less than $200**, so a high-value refund needs a human.
- You don't need to learn Cedar. You can also create policies from **natural language** (a model generates the Cedar) or from a **form**.

## Enforcement

- **Deny by default**: an action is denied unless explicitly permitted. An explicit **forbid** that matches a request denies it, and a request that is neither forbidden nor permitted is denied too. Aim for **least privilege**.
- **Contextual validation**: validates the full context, including **OAuth sub-claims** (identities can come from OAuth) and the **specific tool arguments**.
- **Dual modes**, like a web application firewall:
  - **Enforce mode** actively blocks disallowed actions.
  - **Log-only mode** tests and validates policies before you turn them on, so you don't accidentally deny legitimate traffic.

## Console tour

1. The console warns that policy generation may send data across regions, because it uses **cross-region inference**. Check this against any regulations you are subject to.
2. **Create a policy engine**: name, optional description and optional **KMS encryption**.
3. **Define policies** in the engine, with **Cedar examples** to start from. Choose all gateways or one specific gateway. The editor validates the Cedar.
4. Create a policy by **writing Cedar**, from a **plain-English prompt** (Generate Cedar needs the principals, actions and resources to be defined, or it fails), or with the **form**: name, description, **permit or forbid** effect, principal scope, resource scope (pick a gateway first), actions and conditions such as `input.amount < 200`. Starting from a permit rule is possible but not good practice.
5. **Associate the policy engine with a gateway** and set the **enforcement mode** (log-only or enforce).
6. **Observe with gateways** opens **CloudWatch GenAI observability** (AgentCore observability) to monitor in near real time.

The same setup can be done entirely in code with **Boto3**. The AWS getting-started documentation has a long Python example that creates a gateway and applies policies.

## Exam takeaways

1. Policy **intercepts Gateway tool calls** and evaluates them **outside the agent's code**.
2. Policies are written in **Cedar**, or generated from **natural language or a form**.
3. **Deny by default**, with **contextual validation** of OAuth claims and tool arguments.
4. **Enforce mode** blocks. **Log-only mode** is for testing. Monitor in **CloudWatch**.
