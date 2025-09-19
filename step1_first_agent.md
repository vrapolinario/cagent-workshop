# Step 1: Introduction to cagent

In this step we will start small, we will see how to create simple agents with
cagent.

## Your First Agent

Let's create the simplest possible agent:

**basic_hello.yaml**

```yaml
version: "2"

agents:
  root:
    model: openai/gpt-4o
    instruction: You talk like a pirate
```

Let's run this amazing agent now.

```bash
cagent run basic_hello.yaml
```

If everything is setup correctly, you should see the TUI and be able to ask a
question to your agent and it should answer in pirate speak.

If you don't have access to OpenAI, go to [models.dev](https://models.dev) and
look for the models that exist for `openai`, `anthropic` or `google` provider
IDs.

`cagent` supports these providers:

- `openai`
- `anthropic`
- `google`
- `dmr`: Use any local Docker Model Runner model that you alrady have pulled
  locally.

## Model Configuration

While you can use shorthand model references like `openai/gpt-4o-mini`, you can
also define models explicitly for more control:

**basic_with_model.yaml**

```yaml
version: "2"

models:
  my_model:
    provider: openai
    model: gpt-4o-mini
    temperature: 0.7
    max_tokens: 1000

agents:
  root:
    model: my_model # References the model defined above
    instruction: You talk like a pirate
```

## Next Steps

In Step 2, we'll dive deeper into agent configuration, add more personality, and
learn about agent properties like `add_date` and `add_environment_info`.

---

**Previous:** [README](README.md) | **Next:** [Step 2: Builtin tools](step2_builtin_tools.md)
