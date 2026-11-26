# 163. Step Function States

The workflow is a **state machine**, and each step in it is a **state**. Expect several exam questions on this.

## State types

| State | What it does |
|---|---|
| **Task** | Does real work: Lambda, another AWS service or a **third-party API** |
| **Choice** | **Conditional logic** through choice rules (comparisons), such as special handling for large data or PII |
| **Wait** | Delays the workflow for a set time |
| **Parallel** | Runs **separate branches** at the same time |
| **Map** | Runs the **same steps for each item** of a data set, in parallel (JSON, S3 objects, CSV files) |
| **Pass** | Passes its input on; mainly for debugging |
| **Succeed / Fail** | Ends the execution successfully or with failure |

## Parallel vs Map

- **Parallel:** different branches doing **different things**.
- **Map:** the **same set of steps** applied to **every item**, parallel by itself (no Parallel state needed in front), much like a distributed data engine. This makes it the key state for **data engineering**.

## Exam takeaways

1. Know every **state type** and its purpose.
2. **Map = per item of a data set. Parallel = distinct branches.**
