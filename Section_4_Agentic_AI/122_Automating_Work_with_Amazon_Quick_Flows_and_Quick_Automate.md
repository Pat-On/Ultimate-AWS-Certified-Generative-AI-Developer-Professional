# 122. Automating Work with Amazon Quick Flows and Quick Automate

Quick has two sibling automation capabilities: **Quick Flows** for individual users, and **Quick Automate** for enterprise-scale processes. Automate is a separate builder, not Flows with the limits raised.

## Quick Flows

- A **flow** is a reusable sequence of steps you define once and run whenever needed, to automate routine tasks. Example: a **five whys root cause analysis** that walks users through finding the underlying reasons for a defect.
- **Three ways to build** one:
  - **Generate it from a chat conversation** you already walked through.
  - **Describe it in natural language** in the Quick Flows UI.
  - **Assemble it in the visual editor**, either from scratch or by tweaking a generated draft (reorder, open and edit steps).
- **Run** it guided step by step, or conversationally to refine outputs and ask follow-ups.
- **Publish** to an **admin-managed library** to share across the organisation.
- **No technical skills required**: aimed at any business user.

## Flow step types

Steps come from five categories. A flow uses as many or as few as it needs, in any order.

- **User input**: **text** and **files**. Gathers what the flow needs from the person running it.
- **AI responses**: six ways to have AI produce something: **chat agent**, **research**, **web search**, **general knowledge**, **UI agent** and **create image**.
- **Data insights**: **spaces and knowledge bases**, **dashboards and topics**. Pulls grounded answers from your own data.
- **Actions**: **application actions** that read or write in connected apps such as Jira or Salesforce.
- **Flow logic**: **reasoning groups**, which apply run instructions across one or more steps.

## Quick Automate

- For **enterprise-level**, **long-running, high-volume** work such as processing loan applications, processing invoices and vendor compliance checks.
- Centralised and enterprise-wide, and runs independently of any one user.
- More control: **control flow logic**, **case management**, **error handling**, **custom code** and **human-in-the-loop**.
- Aimed at power users and enterprise users, not the average business user.
- **Enterprise only**: not available on Free or Plus.

## Quick Flows vs Quick Automate

```
                  Quick Flows                              Quick Automate
Who it's for      Individual users - personal and team     Centralised and enterprise-wide; runs
                  productivity                             independently of any one user
Scope and         Shorter tasks: generating reports,       Long-running, high-volume: loan
duration          drafting content, responding to tickets  applications, invoice processing,
                                                           vendor compliance
Customisation     A simple set of no-code building blocks  Control flow logic, case management,
                                                           error handling, custom code,
                                                           human-in-the-loop
Availability      All plans                                Enterprise only - not available on
                                                           Free or Plus
```

## Exam takeaways

1. **Flows** = individual, short, repeatable tasks. **Automate** = enterprise, long-running, high-volume processes.
2. Flows can be built from **chat**, **natural language** or the **visual editor**, and shared through an **admin-managed library**.
3. Five step categories: **user input**, **AI responses**, **data insights**, **actions**, **flow logic**.
4. **Automate is Enterprise only** (not Free or Plus). Flows is on all plans.
5. Automate adds **error handling, case management, custom code and human-in-the-loop**.
