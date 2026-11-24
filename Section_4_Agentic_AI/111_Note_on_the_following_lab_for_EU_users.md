# 111. Note on the following lab for EU users

- Reports from users in EU regions, such as **eu-west-2**, say the **default Claude Sonnet model** used by **Strands Agents** (currently `eu.anthropic.claude-sonnet-4-20250514-v1:0`) is **not recognized as a valid model ID**.
- This seems to be a **bug in Strands**, which is supposed to default to an appropriate model for any given region. It might be some sort of regulatory thing.
- **Fix 1**: pass a current, EU-supported model identifier explicitly to the `Agent` constructor, for example `model="amazon.nova-lite-v1:0"`.
- **Fix 2** (easier): run the lab from **us-east-1**.
- **Fix 3**: just watch the video without following along.
