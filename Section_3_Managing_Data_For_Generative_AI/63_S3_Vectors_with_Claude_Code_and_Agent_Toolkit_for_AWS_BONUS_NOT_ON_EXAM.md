# 63. S3 Vectors with Claude Code and Agent Toolkit for AWS [BONUS - NOT ON EXAM]

A bonus lecture, not on the exam, showing how the AWS agent toolkit lets **Claude Code** build an **Amazon S3 Vectors** store from a prompt, and where human review is still needed.

## Agent toolkit for AWS

- AWS publishes an **agent toolkit** (GitHub repo with documentation) for doing agentic development, data analysis and data engineering from the command line inside **Claude Code**, **Codex**, **Kiro** or another framework.
- An **MCP server** is also available for integrating it into other tools.
- It builds on the **AWS CLI**, which must already be installed.
- It blurs the lines between software engineering, data engineering and data analysis, and removes the need for much of the AWS console.

| Plugin | Capabilities |
|---|---|
| **AWS Core** | General-purpose: **CloudFormation**, serverless setup, **S3**, SDK usage, deployment |
| **AWS Agents** | **Bedrock** and **AgentCore**; builds agents using Bedrock (AgentCore must already be set up) |
| **AWS Data Analytics** | **S3 Tables**, **S3 Vectors**, data lakes, analytics jobs, **Glue**, **Athena** |

- **AWS Data Analytics** skills: create managed **Iceberg** tables on **S3 Tables** (the preferred way to store structured data in S3), ingest data (from S3, JDBC, Snowflake, DynamoDB, Glue), query the data lake, find assets, explore the data catalog, discover data across **Redshift**, S3 Tables and remote Iceberg tables, use S3 Vectors, and connect to external databases (Oracle, SQL Server, Snowflake, BigQuery, RDS).
- Skills do not need to be called by name; the agent selects them.

## Installation

1. Start Claude Code in a project directory.
2. Install each plugin from the official Claude plugin marketplace with `/plugin install`: **AWS Core** (spoken in full as `/plugin install aws-core@claude-plugins-official`), **AWS Agents** and **AWS Data Analytics**. The transcript gives the exact install names only for AWS Core.
3. Choose **user scope** for the install.
4. Do **not** enable automatic acceptance of changes: AWS costs real money, so review every action.

## Workflow: building a vector store

The example data is a JSON Lines file of prompt/completion pairs (empty prompts) holding every line of dialogue spoken by the android Data in Star Trek: The Next Generation, 6,276 lines, previously used for fine-tuning and already stored in S3. The goal is a vector store from which an AI system could imitate how Data speaks.

1. **List the bucket.** Asking what is in the S3 bucket returned the directory listing plus insights into what each dataset is (old MovieLens data, fine-tuning data).
2. **Ask for the design first.** The prompt asked for an S3 vector store of embeddings for the dialogue, but told Claude to ask which embedding model and chunking strategy suit the data before building.
3. **Environment hint.** Claude was told to use the Anaconda `python` command rather than the Windows `python3` command (not needed on Linux).
4. **Data analysis.** Claude downloaded the file, sampled lines, computed statistics and recommended:
   - **One line per chunk**, because short dialogue lines are semantically coherent and should not be split.
   - **Amazon Titan Text Embeddings V2** at **256 dimensions** instead of 1024; more would be overkill and 256 is cost effective. This was more useful than the instructor's instinct to choose 1024.
5. **Region.** Claude looked up the region (us-east-1).
6. **Create the bucket and index.** Claude proposed a name (shown in the console as "Sundog Dialogue Vectors") in us-east-1 with default encryption and 256 dimensions, created the **S3 vector bucket**, then an **index** with a matching dimension count (a vector bucket needs an associated index).
7. **Review the generated script.** Claude wrote a Python script that downloads the data from S3, generates embeddings with the chosen model and loads them in **batches of 100**, with some exception handling. Bucket and index names can be edited before running it.
8. **Run and verify.** The run succeeded. The console showed the new vector bucket containing an index for the TNG dialogue. Claude also wrote and ran a test query for dialogue about friendship and service, which returned a relevant line ("a reminder of friendship and service"). Its summary listed the bucket, index, dimensions, number of vectors and the **cosine** distance metric.
9. **Next step (left as an exercise)**: build an agent on top of the store.

## Cost and review warnings

- Everything on AWS costs money, so keep manual approval of changes and read the generated code before running it.
- The script made **one embedding API call per line** instead of batching requests, so it took about **20 minutes** and cost slightly more than necessary, though embeddings are cheap. The review should have caught this.
- Names such as the bucket name are chosen by the agent unless specified; change them before the run if they matter.

## Takeaways

- Claude Code with the AWS skills and MCP server makes data analytics and AI agent work on AWS much easier, including chunking and embedding model recommendations.
- Understanding the fundamentals and how to optimise these systems is still necessary, to review the agent's code and check that its decisions are optimal.
