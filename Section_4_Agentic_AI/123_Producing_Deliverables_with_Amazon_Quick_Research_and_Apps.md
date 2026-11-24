# 123. Producing Deliverables with Amazon Quick: Research and Apps

Two more ways to produce deliverables in **Amazon Quick**: **Quick Research** for in-depth reports and **Apps** for no-code web applications.

## Quick Research

- Runs **deep, multi-source investigations** and returns a **structured, cited report** that meets your specification.
- Typical uses: **market and competitor analysis**, **literature reviews**, **regulatory research**, **customer insights**.
- Despite the name it is not instant: it takes **several minutes**, not days.
- Also available as a **step inside Quick Flows**, so you can build a flow that walks users through requesting a report and gathering the data it needs.

### Sources

- **Web search**
- **Uploaded files**
- **Spaces** and **knowledge bases**
- **Application actions** (the applications connected to Quick)
- **Third-party datasets**: Moody's, Dun & Bradstreet, HG Insights

### Running it

- Give a prompt describing the report, with as much detail as possible, then **define the objective and select the sources**.
- **More sources is not always better.** For a purpose-built dataset, restrict research to it: irrelevant data can lead the report astray, causing irrelevant results, hallucinations or citations unrelated to the goal. Constrain to **good-quality data** where you can.
- The output has **citations** for everything it drew on, with **source tracing**. You must still check that the sources support the conclusions.

## Apps in Quick

- Build a **web app with no code**: describe it in natural language and the agent **writes it live while you watch**.
- Five conversational steps: **Describe**, **Generate** (a first attempt), **Preview**, **Iterate** (give feedback as many times as needed), **Publish**.
- What an app can do:
  - **Conversational authoring**
  - **Live Quick Sight embeds**, to visualize data from Redshift, S3 or Athena
  - **Action connectors**, so every Quick connector is available to the app
  - **Built-in AI inference**, returning AI responses from the resources you give it
  - **Spaces integration** (and knowledge bases) for retrieving information
  - **Persistent data storage**, handled automatically
  - **SSO and enterprise auth**, to control who can access the app
  - **One-click publishing**
- Examples: **intake forms**, **status trackers**, **calculators**, **document viewers**.
- Share apps **internally** or **publish them as a public site**.

## Exam takeaways

1. **Quick Research** produces a **cited, structured report** in minutes from the web, files, spaces, knowledge bases, actions and third-party datasets (Moody's, Dun & Bradstreet, HG Insights), and is also a **Flows step**.
2. **Restrict research sources** to relevant, high-quality data to avoid hallucinations and off-topic citations. Verify the citations.
3. **Apps** are no-code web apps built from natural language through describe, generate, preview, iterate and publish.
4. Apps can embed **Quick Sight**, call **action connectors**, run **AI inference**, store data, use **SSO**, and be shared internally or published publicly.
