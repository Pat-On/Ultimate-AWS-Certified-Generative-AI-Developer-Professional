# 45. Glue Data Quality

**AWS Glue Data Quality** is a step you can add to a Glue job (in Glue Studio) that evaluates incoming data against rules, and either fails the job or logs the result to **CloudWatch**. It is a recent feature and fair game for the exam from 2024 onward.

## How it works

- Rules can be written manually or **recommended automatically**: point it at source data you know is good and it infers rules (expected ranges, standard deviation of typical values and so on). Recommended rules can be edited.
- It is integrated into a Glue job like any other transform stage.
- Rules are written in **DQDL** (Data Quality Definition Language).
- On a rule failure you can:
  - **fail the whole job** (a threshold that is too tight causes false positives), or
  - **report the results to CloudWatch** and act on them as you see fit.

## Example rule types

- Row count within a range (too few rows suggests a problem).
- Column completeness (no missing values).
- Column value length within a range.
- Standard deviation of a column within expected bounds.
- In the demo, a rule set failed because the standard deviation and values of a date column were not as expected: either a too-tight threshold or real bad data or outliers.
