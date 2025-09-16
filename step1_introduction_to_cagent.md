# Step 1: Introduction to cagent

## What is cagent?

cagent is a powerful, customizable multi-agent system that orchestrates AI
agents with specialized capabilities and tools. Think of it as allowing you to
quickly build, share and run a team of virtual experts that collaborate to solve
complex problems.

## Key Features

- **Multi-agent architecture**: Create specialized agents for different domains
- **Rich tool ecosystem**: Agents can use external tools and APIs via the MCP
  protocol
- **Smart delegation**: Agents can automatically route tasks to the most
  suitable specialist
- **YAML configuration**: Declarative model and agent configuration
- **Advanced reasoning**: Built-in "think", "todo" and "memory" tools for
  complex problem-solving
- **Multiple AI providers**: Support for OpenAI, Anthropic, Gemini and Docker
  Model Runner

## Installation and Setup

1. Download the appropriate binary for your platform from the releases page
2. Make it executable: `chmod +x cagent`
3. Move to your PATH or create a symlink
4. Set your API keys:
   ```bash
   export OPENAI_API_KEY=your_api_key_here
   export ANTHROPIC_API_KEY=your_api_key_here
   export GOOGLE_API_KEY=your_api_key_here
   ```

## Your First Agent

Let's create the simplest possible agent:

**basic_hello.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o-mini
    description: A simple greeting agent
    instruction: |
      You are a friendly assistant that greets users warmly.
      Always introduce yourself and ask how you can help.
```

## Running Your Agent

```bash
cagent run basic_hello.yaml
```

## Exercise 1: Create Your First Agent

Create a file called `my_first_agent.yaml` with:

- A model of your choice (openai/gpt-4o-mini is recommended for beginners)
- A description of what your agent does
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

## Key Concepts

1. **Agent**: The basic unit in cagent - has a model, description, and
   instruction
2. **Model**: Defines which AI provider and model to use, plus configuration
3. **Root agent**: The entry point - this is the agent that handles user
   interaction initially
4. **YAML configuration**: All agents and models are defined in YAML files

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
