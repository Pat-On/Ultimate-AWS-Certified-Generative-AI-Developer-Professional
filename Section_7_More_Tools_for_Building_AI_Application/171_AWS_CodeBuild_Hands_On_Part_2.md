# 171. AWS CodeBuild Hands On Part 2

- **Type:** Practice lab

## Add the buildspec

Commit a buildspec file (version `0.2`) to the repository root:

- `install`: latest Node.js runtime and an echo
- `pre_build`, `post_build`: echo messages
- `build`: the test, `grep -Fq "Congratulations" index.html` (fails the build if the text is gone)

The default file name is **`buildspec.yml`**; the lab types `buildspec.yaml`, which works only if the project is configured with that name.

The push triggers a build automatically. **Phase details** show submitted, queued, provisioning, download source, install, pre_build, build, post_build, upload artifacts, finalizing and completed. Full logs are in **CloudWatch Logs**.

## Put it in the pipeline

1. Remove the project's **webhook**, since CodePipeline will start it.
2. In the pipeline add a stage **TestCode** between source and deploy: action **CodeBuild**, input `SourceArtifact`, project `MyFirstBuild`, output `OutputOfTest`.

## Prove it

- Replace "Congratulations" with another word: the build **fails** and the pipeline **stops**, so nothing is deployed.
- Restore the word: the test passes, dev is deployed, and prod waits for manual approval.

## Exam takeaways

1. A **failing build blocks** later stages.
2. In a pipeline, **CodePipeline triggers CodeBuild**.
