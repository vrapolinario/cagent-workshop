# Step 1: Introduction to cagent

In this step we will start small, we will see how to create simple agents with
cagent.

## Your First Agent

Let's create the simplest possible agent:

**basic_hello.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o-mini
    instruction: You talk like a pirate
```

## Running Your Agent

```bash
cagent run basic_hello.yaml
```

## Exercise 1: Create Your First Agent

Create a file called `my_first_agent.yaml` with:

- A model of your choice
- A simple instruction telling the agent how to behave

Test it by running: `cagent run my_first_agent.yaml`

## Model Configuration

While you can use shorthand model references like `openai/gpt-4o-mini`, you can
also define models explicitly for more control:

**basic_with_model.yaml**

```yaml
models:
  my_model:
    provider: openai
    model: gpt-4o-mini
    temperature: 0.7
    max_tokens: 1000

agents:
  root:
    model: my_model
    description: A customized greeting agent
    instruction: |
      You are a friendly assistant that greets users warmly.
      Be creative in your greetings and ask engaging questions.
```

## Exercise 2: Experiment with Model Parameters

Modify your agent to use explicit model configuration and experiment with:

- Different temperature values (0.1 for focused, 0.9 for creative)
- Different max_tokens values
- Different models (try anthropic/claude-3-haiku if you have the API key)

## Commands You've Learned

- `cagent run <config.yaml>` - Run an agent configuration
- Basic YAML structure for agents and models

## Next Steps

In Step 2, we'll dive deeper into agent configuration, add more personality, and
learn about agent properties like `add_date` and `add_environment_info`.
