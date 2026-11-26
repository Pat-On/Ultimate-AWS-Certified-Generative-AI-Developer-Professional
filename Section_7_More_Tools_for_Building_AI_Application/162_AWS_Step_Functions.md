# 162. AWS Step Functions

**Step Functions** designs **workflows** across AWS services, connecting steps such as data preparation and training into one system.

## Key features

- **Visual graph** of the order of execution
- **Error handling and retries outside your code**, so steps do not have to monitor themselves
- **Audit history** of past executions for troubleshooting
- **Wait** for an arbitrary time between steps
- Maximum execution time of a state machine: **1 year**

Workflows are written in the JSON-based **Amazon States Language (ASL)**. The exam does **not** ask you to read or write it.

(**Beyond the lecture:** the one-year limit is for **Standard** workflows; **Express** workflows run for up to 5 minutes.)

## Examples

| Goal | Steps |
|---|---|
| **Train a model** | Lambda generates the data set → SageMaker **XGBoost** training → save the model → **batch transform** |
| **Tune a model** | Generate data → SageMaker **hyperparameter tuning job** → extract and save the best model → batch transform |
| **Manage a batch job** | Submit the job → **notify** on success or failure |

A state machine can be very small: sometimes one monitored step with notifications is all you need.

## Exam takeaways

1. Step Functions = **orchestration** with a visual graph.
2. **Retries and error handling live in the workflow**, not the code.
3. **History/audit**, **wait** states and the **1-year** limit.
