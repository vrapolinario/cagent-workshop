# Building Agents with cagent - Workshop

Welcome to this hands-on workshop on building intelligent agents using cagent!
This workshop will take you from basic agent concepts to building sophisticated
multi-agent teams that can handle complex real-world tasks.

## What is cagent?

cagent is a powerful framework for building and orchestrating AI agents. Unlike
simple chatbots, cagent agents can:

- **Take Actions**: Use tools to interact with files, run commands, browse the
  web, and more
- **Work in Teams**: Coordinate with specialized sub-agents for complex projects
- **Remember Context**: Maintain persistent memory across conversations
- **Think and Plan**: Use structured reasoning to solve complex problems
- **Integrate Anywhere**: Connect to external services via the Model Context
  Protocol (MCP)

## Prerequisites

Before starting this workshop, you should have:

1. **cagent installed** - Follow the installation instructions
2. **Docker Desktop running** - Required for Step 2 (agent sharing)
3. **Docker Hub account** - For pushing and pulling shared agents
4. **Basic YAML knowledge** - Agent configurations use YAML format
5. **AI API access** - OpenAI, Anthropic, or other supported model providers

## cagent installation instructions

[Prebuilt binaries](https://github.com/docker/cagent/releases) for Windows,
macOS and Linux can be found on the releases page of the [project's GitHub
repository](https://github.com/docker/cagent/releases)

Once you've downloaded the appropriate binary for your platform, you may need to
give it executable permissions. On macOS and Linux, this is done with the
following command:

```sh
# linux amd64 build example
chmod +x /path/to/downloads/cagent-linux-amd64
```

You can then rename the binary to `cagent` and configure your `PATH` to be able
to find it (configuration varies by platform).

### Set your API keys

Based on the models you configure your agents to use, you will need to set the
corresponding provider API key accordingly, all theses keys are optional, you
will likely need at least one of these, though:

```bash
# For OpenAI models
export OPENAI_API_KEY=your_api_key_here

# For Anthropic models
export ANTHROPIC_API_KEY=your_api_key_here

# For Gemini models
export GOOGLE_API_KEY=your_api_key_here
```

## Workshop Overview

This workshop is structured as a progressive learning journey with 5 steps:

### Step 1: Introduction to cagent

- What makes agents different from chatbots
- Basic agent configuration and setup
- Your first working agent
- Understanding models and providers

### Step 2: Sharing Agents with Docker Registry

- Push and pull agents using Docker registries
- Version control and collaboration
- Agent distribution and sharing workflows
- Docker Hub integration and authentication

### Step 3: Introduction to Agents

- Advanced agent instructions and behaviors
- Personality and role definition
- Adding context with environment information
- Creating specialized agent personalities

### Step 4: Introduction to Toolsets

- Built-in tools (filesystem, shell, think, todo, memory)
- External tool integration via MCP
- Combining tools for powerful workflows
- Real-world tool usage patterns

### Step 5: Introduction to Sub-agents

- Building teams of specialized agents
- Coordination and task delegation
- Shared resources and collaboration
- Complex multi-agent workflows
