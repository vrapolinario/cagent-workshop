# Step 6: Extra

## Using Docker Model Runner (DMR)

Docker Model Runner (DMR) makes it easy to manage, run, and deploy AI models using Docker. Designed for developers,
Docker Model Runner streamlines the process of pulling, running, and serving large language models (LLMs) and other AI
models directly from Docker Hub or any OCI-compliant registry.

Discover curated models on [Docker Hub](https://hub.docker.com/u/ai).

Naturally, `cagent` has first-class support for DMR.

```yaml
agents:
  root:
    model: dmr/ai/smollm2
    instruction: Talk like a pirate
```

Before running this agent, make sure you have the model available locally:

```console
$ docker model pull ai/smollm2
```

**Previous:** [Step 5: Introduction to Sub-agents](step4_sharing_agents.md) | **Next:** [Step 7: Thank
You!](step7_thankyou.md)
