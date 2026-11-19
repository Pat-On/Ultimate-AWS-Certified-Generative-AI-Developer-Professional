# 8. A quick note on model access

Practical notes before the hands-on activities in the following lectures.

## Using Anthropic models

- Access to all Bedrock foundation models is now supposed to be enabled by default. **Anthropic models are, for now, an exception.**
- The first time you use one (e.g. Claude Haiku or Opus) you must **submit a use case and request access**. You are prompted for it when you select a Claude model.
  - A use case such as "educational use with an online course" is reasonable.
- Alternatively, choose a foundation model that is not from Anthropic.

## Models change frequently

- The models offered through Bedrock change constantly as new ones are added and older ones removed.
- Don't expect the models you see in Bedrock to match the screenshots or videos in this course.

## No free tier

- Bedrock, and many of the newer services in this course, are **not covered by the AWS free tier**.
- To follow along hands-on you need a **paid account**, and it will cost a few dollars.
- Set up a **billing alarm** to be safe (lecture 5). You can also just watch the videos.

## Quota limits

- Some students find their **on-demand quotas for Bedrock set to zero**.
- A sign of this is an error like "Throttling Exception: Too many tokens per day, please wait before trying again".
- The fix is to **contact AWS support** and ask for the quota limit to be raised to a non-zero value.
- Keep billing alarms set and monitor your usage to keep costs under control.
