# Step 2: Introduction to Agents

## Building on Step 1

In Step 1, you created a basic agent. Now we'll explore how to make agents more
sophisticated and useful by understanding all the agent properties and
capabilities.

## Agent Properties Deep Dive

### Required Properties

Every agent needs these essential properties:

```yaml
agents:
  root:
    model: string # Which model to use
    description: string # What the agent does
    instruction: string # How the agent should behave
```

### Optional Properties

These properties enhance your agent's capabilities:

```yaml
agents:
  root:
    model: openai/gpt-4o-mini
    description: Enhanced assistant
    instruction: |
      You are a helpful assistant with enhanced capabilities.
    add_date: true # Adds current date to context
    add_environment_info: true # Adds working directory, OS, git info
    toolsets: [] # Tools the agent can use (covered in Step 3)
    sub_agents: [] # Other agents this one can delegate to (covered in Step 4)
```

## Enhanced Agent Example

Let's create a more sophisticated agent:

**enhanced_assistant.yaml**

```yaml
models:
  smart_model:
    provider: openai
    model: gpt-4o
    temperature: 0.3
    max_tokens: 2000

agents:
  root:
    model: smart_model
    description: |
      A context-aware assistant that helps with daily tasks and provides 
      information about the current environment and date.
    instruction: |
      You are an intelligent assistant with awareness of the current date and 
      environment. Use this information to provide contextually relevant help.

      Key behaviors:
      - Always greet users appropriately based on the time of day
      - Reference the current date when relevant to questions
      - Be aware of the user's working directory and operating system
      - Provide helpful, accurate information
      - Be proactive in offering assistance
    add_date: true
    add_environment_info: true
```

## Exercise 1: Create a Specialized Agent

Create a specialized agent for a specific role. Choose one:

**Option A: Code Review Agent**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: |
      Expert code reviewer that analyzes code for bugs, performance issues,
      and adherence to best practices.
    instruction: |
      You are a senior software engineer specializing in code review.
      When users share code, analyze it for:
      - Potential bugs and errors
      - Performance optimizations
      - Code style and best practices
      - Security vulnerabilities
      - Readability and maintainability

      Provide constructive feedback with specific suggestions for improvement.
    add_environment_info: true
```

**Option B: Writing Coach Agent**

```yaml
agents:
  root:
    model: anthropic/claude-3-sonnet
    description: |
      Professional writing coach that helps improve writing style, 
      clarity, and effectiveness.
    instruction: |
      You are an experienced writing coach and editor. Help users improve
      their writing by:
      - Identifying areas for clarity and conciseness
      - Suggesting better word choices and sentence structure
      - Checking for grammar and style consistency
      - Providing constructive feedback on tone and voice
      - Helping with organization and flow

      Always explain your suggestions and provide examples when helpful.
    add_date: true
```

## Understanding Context Enhancement

### add_date: true

When enabled, the agent receives the current date and time, allowing it to:

- Give time-appropriate greetings
- Reference current events contextually
- Help with date-based calculations
- Provide seasonally relevant advice

### add_environment_info: true

When enabled, the agent receives information about:

- Current working directory
- Operating system
- Git repository status (if applicable)
- Platform details

This helps the agent provide more relevant technical assistance.

## Advanced Instructions

Your instruction field can be quite sophisticated:

**advanced_instruction_example.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Advanced project assistant
    instruction: |
      You are a project management assistant with the following capabilities:

      PRIMARY ROLE:
      - Help users organize and track their work
      - Provide project planning and execution guidance
      - Break down complex tasks into manageable steps

      COMMUNICATION STYLE:
      - Be professional but approachable
      - Ask clarifying questions when tasks are unclear
      - Provide step-by-step guidance for complex processes
      - Summarize key points at the end of longer responses

      WHEN HELPING WITH TASKS:
      1. First, understand the full scope of what's needed
      2. Break large tasks into smaller, actionable items
      3. Suggest realistic timelines when appropriate
      4. Identify potential blockers or dependencies
      5. Recommend tools or resources that might help

      CONSTRAINTS:
      - Always ask for clarification rather than making assumptions
      - Prioritize actionable advice over theoretical discussion
      - Be honest about limitations and suggest alternatives when needed
    add_date: true
    add_environment_info: true
```

## Exercise 2: Create an Advanced Agent

Create an agent with:

1. A detailed, multi-paragraph instruction with specific behavioral guidelines
2. Both `add_date` and `add_environment_info` enabled
3. A custom model configuration with specific temperature and max_tokens
4. Test it by asking questions that would benefit from date/environment context

## Agent Naming and Organization

While we've been using "root" as our agent name, you can organize more complex
configurations:

```yaml
agents:
  researcher:
    model: claude
    description: Research specialist
    instruction: |
      You specialize in finding and analyzing information.

  writer:
    model: gpt4
    description: Content creation specialist
    instruction: |
      You specialize in creating clear, engaging content.

models:
  claude:
    provider: anthropic
    model: claude-3-sonnet

  gpt4:
    provider: openai
    model: gpt-4o
```

To run a specific agent: `cagent run config.yaml -a researcher`

## Exercise 3: Multiple Agent Definitions

Create a configuration file with 2-3 different agents, each specialized for
different tasks:

- Give them descriptive names (not just "root")
- Make each agent's instruction reflect their specialty
- Test running different agents with the `-a` flag

## Common Patterns

### The Thinking Agent

```yaml
agents:
  analyst:
    model: openai/gpt-4o
    description: Analytical thinker
    instruction: |
      You are a careful analytical thinker. Before responding to any question:
      1. Break down what's being asked
      2. Consider multiple perspectives
      3. Identify what information you need
      4. Reason through the problem step by step
      5. Provide a clear, well-reasoned answer
```

### The Domain Expert

```yaml
agents:
  security_expert:
    model: openai/gpt-4o
    description: Cybersecurity specialist
    instruction: |
      You are a cybersecurity expert with deep knowledge of:
      - Threat assessment and risk management
      - Secure coding practices
      - Network security
      - Incident response

      Always consider security implications in your responses and 
      provide specific, actionable security guidance.
```

## Key Takeaways

1. **Instructions are crucial**: They define your agent's personality and
   behavior
2. **Context matters**: Use `add_date` and `add_environment_info` when relevant
3. **Specialization works**: Focused agents often perform better than
   generalists
4. **Model selection impacts behavior**: Choose models appropriate for your use
   case
5. **Testing is important**: Always test your agents with realistic scenarios

## Next Steps

In Step 3, we'll enhance our agents with toolsets - giving them the ability to
interact with files, run commands, search the web, and much more. This is where
agents become truly powerful!
