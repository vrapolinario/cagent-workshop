# Step 3: Sharing Agents with Docker Registry

## From Local to Global - Sharing Your Agents

In Step 1, you learned how to create and run agents locally. Now we'll explore
one of cagent's most powerful features: the ability to share agents with others
through Docker registries. This makes agent distribution as simple as sharing
Docker images.

## Prerequisites

Before you can push and pull agents, you need:

1. **Docker Desktop running** - Make sure Docker Desktop is installed and
   running on your machine
2. **Docker Hub account** - You need to be logged into Docker Hub (or another
   Docker registry)
3. **Authentication** - You must be logged in to Docker Hub from your command
   line

### Check Your Setup

First, verify your Docker setup:

```bash
# Check if Docker is running
docker --version

# Check if you're logged in to Docker Hub
docker login --help
```

If you're not logged in to Docker Hub, do so now:

```bash
# Log in to Docker Hub (you'll be prompted for username/password)
docker login

# Or log in to a different registry
docker login registry.example.com
```

## What is Agent Sharing?

Agent sharing in cagent works similar to Docker image sharing:

- **Push**: Upload your agent configuration to a Docker registry
- **Pull**: Download someone else's agent configuration from a registry
- **Run**: Execute agents directly from registry references

Benefits of agent sharing:

- **Collaboration**: Share agents with your team or the community
- **Version control**: Tag different versions of your agents
- **Distribution**: Make agents available across different machines
- **Reusability**: Build upon existing agents created by others

## Basic Push and Pull Operations

### Creating an Agent to Share

Let's start by creating a simple agent we can share:

**shareable_assistant.yaml**

```yaml
version: "2"

models:
  helpful_model:
    provider: openai
    model: gpt-4o-mini

agents:
  root:
    model: helpful_model
    description: A helpful assistant that can be shared with others
    instruction: |
      You are a helpful assistant created to demonstrate agent sharing.
      You are knowledgeable, polite, and always try to provide useful
      information. When greeting users, mention that you were shared
      via cagent's Docker registry integration.

      Always be helpful and explain things clearly.
    add_date: true
    add_environment_info: true
```

Test this agent locally first:

```bash
cagent run shareable_assistant.yaml
```

### Pushing Your First Agent

Once you've tested your agent locally, you can share it with others:

```bash
# Push to Docker Hub (replace 'yourusername' with your Docker Hub username)
cagent push docker.io/yourusername/helpful-assistant:v1.0

# You can also use shorter tags
cagent push docker.io/yourusername/helpful-assistant:latest
```

The format is: `docker.io/username/agent-name:tag`

- **docker.io**: The registry (Docker Hub)
- **username**: Your Docker Hub username
- **agent-name**: Name for your agent
- **tag**: Version tag (like v1.0, latest, dev, etc.)

### Pulling Someone Else's Agent

You can run agents that others have shared:

```bash
# Pull an agent from Docker Hub
cagent pull docker.io/username/some-agent:latest

# Run the pulled agent directly
cagent run docker.io/username/some-agent:latest
```

You can even run agents directly without explicitly pulling:

```bash
# This will pull and run in one step
cagent run docker.io/username/some-agent:latest
```

## Exercise 1: Create and Share a Specialized Agent

Create a specialized agent and share it:

**code_reviewer.yaml**

```yaml
version: "2"

models:
  review_model:
    provider: openai
    model: gpt-4o
    temperature: 0.1 # Low temperature for consistent code reviews

agents:
  root:
    model: review_model
    description: Professional code reviewer
    instruction: |
      You are a professional code reviewer with years of experience
      in software development. When users share code with you, provide:

      1. Overall assessment of code quality
      2. Specific issues or improvements
      3. Security considerations  
      4. Performance optimization suggestions
      5. Code style and best practices feedback

      Always be constructive and educational in your feedback.
      Explain why certain changes would be beneficial.
    add_environment_info: true
```

Share this agent:

```bash
# Test locally first
cagent run code_reviewer.yaml

# Push to share (replace with your username)
cagent push docker.io/yourusername/code-reviewer:v1.0
```

## Versioning Your Agents

Just like Docker images, you can version your agents:

```bash
# Push different versions
cagent push docker.io/yourusername/my-agent:v1.0
cagent push docker.io/yourusername/my-agent:v1.1
cagent push docker.io/yourusername/my-agent:latest

# Pull specific versions
cagent pull docker.io/yourusername/my-agent:v1.0
cagent run docker.io/yourusername/my-agent:v1.1
```

## Exercise 2: Create a Domain-Specific Assistant

Create an agent for a specific domain (replace with your area of expertise):

**marketing_assistant.yaml**

```yaml
version: "2"

models:
  marketing_model:
    provider: anthropic
    model: claude-3-5-sonnet-latest
    max_tokens: 32000

agents:
  root:
    model: marketing_model
    description: Digital marketing strategy assistant
    instruction: |
      You are a digital marketing expert specializing in content strategy,
      social media marketing, and brand development. You help businesses:

      - Develop content marketing strategies
      - Create engaging social media posts
      - Analyze marketing performance
      - Plan marketing campaigns
      - Write marketing copy and content

      Always provide actionable advice backed by current marketing best practices.
      Ask clarifying questions about target audience, brand, and goals when needed.

      Remember to stay current with digital marketing trends and platform changes.
    add_date: true
    add_environment_info: true
```

Version and share it:

```bash
cagent run marketing_assistant.yaml  # Test first
cagent push docker.io/yourusername/marketing-assistant:v1.0
```

## Working with Agent Catalogs

You can explore available agents using the catalog command:

```bash
# List agents from a specific organization
cagent catalog list yourusername

# List all available agents (if supported by registry)
cagent catalog list
```

## Best Practices for Sharing Agents

### 1. Clear Documentation in Instructions

Make your agents self-documenting:

```yaml
agents:
  root:
    description: Brief, clear description of what the agent does
    instruction: |
      Detailed instructions that explain:
      - The agent's primary purpose
      - What types of tasks it handles well
      - Any specific expertise or knowledge areas
      - How users should interact with it
      - Any limitations or considerations
```

### 2. Appropriate Model Selection

Choose models that match your agent's needs:

```yaml
models:
  # For analysis and reasoning tasks
  analytical_model:
    provider: anthropic
    model: claude-3-5-sonnet-latest
    temperature: 0.1

  # For creative tasks
  creative_model:
    provider: openai
    model: gpt-4o
    temperature: 0.7
```

### 3. Meaningful Names and Tags

Use descriptive names and version tags:

```bash
# Good naming
docker.io/yourusername/python-tutor:v1.0
docker.io/yourusername/data-analyst:latest
docker.io/yourusername/technical-writer:v2.1

# Avoid generic names
docker.io/yourusername/agent:latest
docker.io/yourusername/helper:v1
```

### 4. Test Before Sharing

Always test your agents locally before pushing:

```bash
# Test thoroughly before pushing
cagent run my_agent.yaml

# Try different types of conversations
# Test edge cases and error handling

# Then push when satisfied
cagent push docker.io/yourusername/my-agent:v1.0
```

## Exercise 3: Pull and Customize an Existing Agent

Try pulling and modifying someone else's agent concept:

```bash
# Pull an agent (this is a hypothetical example)
cagent pull docker.io/example/writing-assistant:latest

# Run it to understand how it works
cagent run docker.io/example/writing-assistant:latest
```

Then create your own version by modifying the concept:

**my_writing_assistant.yaml**

```yaml
version: "2"

models:
  writing_model:
    provider: openai
    model: gpt-4o
    temperature: 0.6

agents:
  root:
    model: writing_model
    description: Technical writing assistant specialized for developers
    instruction: |
      You are a technical writing assistant focused on helping developers
      create clear, concise documentation and technical content.

      Specializations:
      - API documentation
      - README files
      - Technical tutorials  
      - Code comments and documentation
      - Architecture decision records

      Always prioritize clarity and accessibility for the target audience.
      Use examples and practical guidance when possible.
    add_environment_info: true
```

## Advanced Registry Operations

### Private Registries

You can use private registries in addition to Docker Hub:

```bash
# Login to a private registry
docker login registry.company.com

# Push to private registry
cagent push registry.company.com/team/specialized-agent:v1.0

# Pull from private registry
cagent pull registry.company.com/team/specialized-agent:v1.0
```

### Organization and Team Sharing

Organize agents by teams or purposes:

```bash
# Team-based organization
docker.io/mycompany/frontend-assistant:latest
docker.io/mycompany/backend-assistant:latest
docker.io/mycompany/devops-assistant:latest

# Project-based organization
docker.io/mycompany/project-alpha-agent:v1.0
docker.io/mycompany/project-beta-agent:v2.1
```

## Troubleshooting Agent Sharing

### Common Issues

**Authentication Problems:**

```bash
# Make sure you're logged in
docker login

# Check your login status
docker info | grep -i username
```

**Registry Connectivity:**

```bash
# Test Docker Hub connectivity
docker pull hello-world

# Verify you can push to your namespace
docker tag hello-world docker.io/yourusername/test:latest
docker push docker.io/yourusername/test:latest
```

**Agent Not Found:**

```bash
# Double-check the exact name and tag
cagent pull docker.io/username/exact-name:exact-tag

# Try listing available agents
cagent catalog list username
```

## Real-World Sharing Examples

### Development Team Agents

```bash
# Share specialized development agents
docker.io/devteam/code-reviewer:v1.0
docker.io/devteam/documentation-writer:latest
docker.io/devteam/api-designer:v2.1
docker.io/devteam/test-generator:latest
```

### Educational Agents

```bash
# Share learning-focused agents
docker.io/educators/python-tutor:v1.0
docker.io/educators/math-helper:latest
docker.io/educators/writing-coach:v1.5
```

### Industry-Specific Agents

```bash
# Domain-specific agents
docker.io/finance/risk-analyzer:v1.0
docker.io/healthcare/research-assistant:latest
docker.io/legal/contract-reviewer:v1.2
```

## Security Considerations

### What Gets Shared

When you push an agent, you're sharing:

- The agent configuration (YAML)
- Model references (but not API keys)
- Instructions and descriptions
- Tool configurations

### What Doesn't Get Shared

- Your API keys (these stay local)
- Local files referenced by tools
- Environment-specific configurations
- Personal data or credentials

### Best Practices

1. **Review configurations** before pushing
2. **Don't include sensitive information** in instructions
3. **Use environment variables** for sensitive data
4. **Consider using private registries** for internal agents
5. **Regularly update shared agents** to fix issues

## Key Takeaways

- **Docker integration makes sharing simple**: Push and pull agents like Docker
  images
- **Version control enables collaboration**: Tag different versions for
  stability
- **Test locally before sharing**: Always verify agents work correctly
- **Clear documentation helps adoption**: Write good descriptions and
  instructions
- **Security matters**: Never share sensitive information in agent
  configurations

## Integration with Team Workflows

Agent sharing integrates well with development workflows:

1. **Development**: Create agents for specific team needs
2. **Testing**: Validate agents locally and with team members
3. **Versioning**: Tag stable versions for production use
4. **Distribution**: Share via registries for easy access
5. **Updates**: Push new versions as improvements are made

## Next Steps

Now that you understand agent sharing, you're ready for Step 3, where we'll dive
deeper into creating sophisticated agents with advanced instructions and
behaviors. You'll learn how to create agents that can handle complex tasks and
interact naturally with users.

The ability to share agents transforms cagent from a personal tool to a
collaborative platform where teams and communities can build upon each other's
work!
