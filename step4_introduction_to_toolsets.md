# Step 4: Introduction to Toolsets

## From Conversation to Action

In the previous steps, we created agents that could have conversations. Now
we'll give them superpowers by adding toolsets - the ability to take actions in
the real world.

## What are Toolsets?

Toolsets are collections of tools that agents can use to:

- Read and write files
- Execute shell commands
- Search the web
- Manage databases
- Browse websites
- And much more

## Built-in Tools

cagent comes with several built-in tools that don't require external
dependencies:

### 1. Filesystem Tool

Gives agents the ability to read and write files:

**filesystem_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: File management assistant
    instruction: |
      You are a file management assistant. You can read, write, and organize files.
      When users ask you to work with files, use your filesystem tools to help them.
      Always confirm what you're about to do before making changes.
    toolsets:
      - type: filesystem
```

### 2. Shell Tool

Allows agents to execute system commands:

**shell_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: System administration assistant
    instruction: |
      You are a system administration assistant. You can run commands to help
      users manage their system, check status, and perform tasks.
      Always explain what commands you're running and why.
      Be cautious with destructive operations - ask for confirmation first.
    toolsets:
      - type: shell
```

### 3. Think Tool

Enables structured reasoning and problem-solving:

**thinking_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Problem-solving assistant
    instruction: |
      You are a careful problem solver. Use your think tool to work through
      complex problems step by step. Break down problems, analyze options,
      and reason through solutions before providing answers.
    toolsets:
      - type: think
```

### 4. Todo Tool

Manages task lists and project organization:

**todo_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Task management assistant
    instruction: |
      You are a task management assistant. Help users organize their work
      by creating and managing todo lists. Break down complex projects
      into manageable tasks.
    toolsets:
      - type: todo
```

### 5. Memory Tool

Provides persistent storage across conversations:

**memory_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Assistant with persistent memory
    instruction: |
      You are an assistant with long-term memory. You can remember
      information across conversations and recall relevant details
      when needed. Use your memory to provide personalized assistance.
    toolsets:
      - type: memory
        path: "./agent_memory.db"
```

## Exercise 1: Create a File Assistant

Create an agent that can help with file operations:

```yaml
agents:
  root:
    model: openai/gpt-4o-mini
    description: Personal file organizer
    instruction: |
      You are a personal file organizer. Help users:
      - Find files they're looking for
      - Organize files into logical structures
      - Read and summarize file contents
      - Create new files with specific content
      - Clean up cluttered directories

      Always ask for permission before moving or deleting files.
    toolsets:
      - type: filesystem
    add_environment_info: true
```

Test this agent by asking it to:

- List files in the current directory
- Read a text file and summarize it
- Create a new file with some content

## Combining Multiple Built-in Tools

You can give agents multiple tools for more sophisticated capabilities:

**multi_tool_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Development assistant
    instruction: |
      You are a development assistant that can help with coding tasks.
      You can read and write code files, run tests and commands, manage
      todos for project planning, and think through complex problems.

      Workflow for helping with development:
      1. Use think tool to understand the requirements
      2. Read existing code to understand the context
      3. Create or update todos to plan the work
      4. Write or modify code files as needed
      5. Run tests or commands to verify the changes
    toolsets:
      - type: filesystem
      - type: shell
      - type: think
      - type: todo
    add_environment_info: true
```

## Exercise 2: Create a System Monitor

Create an agent that combines shell and thinking tools:

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: System monitoring assistant
    instruction: |
      You are a system monitoring assistant. Help users understand
      and optimize their system performance.

      Use your tools to:
      - Check system resources (CPU, memory, disk)
      - Identify running processes
      - Monitor system logs
      - Suggest optimizations

      Always think through what you're checking and explain your findings.
    toolsets:
      - type: shell
      - type: think
    add_environment_info: true
```

Test this agent by asking it to check system performance or running processes.

## MCP (Model Context Protocol) Tools

MCP tools extend your agent's capabilities by connecting to external services.
These require the external tool to be installed.

### Filesystem MCP Tool (Alternative)

Instead of the built-in filesystem tool, you can use the MCP version:

```yaml
toolsets:
  - type: mcp
    command: rust-mcp-filesystem
    args: ["--allow-write", "."]
    tools: ["read_file", "write_file"]
```

### Web Search via Docker MCP

Using Docker MCP Toolkit for web search:

```yaml
toolsets:
  - type: mcp
    ref: docker:duckduckgo
```

### Custom MCP Server

You can also connect to remote MCP servers:

```yaml
toolsets:
  - type: mcp
    remote:
      url: "https://mcp-server.example.com"
      transport_type: "sse"
      headers:
        Authorization: "Bearer your-token-here"
    tools: ["search_web", "fetch_url"]
```

## Exercise 3: Web-Enabled Research Assistant

Create an agent that can search the web (requires Docker MCP setup):

**research_agent.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Web research assistant
    instruction: |
      You are a research assistant with web search capabilities.
      When users ask questions that require current information,
      search the web to find accurate, up-to-date answers.

      Research process:
      1. Think about what information is needed
      2. Search for relevant information
      3. Analyze and synthesize the results
      4. Provide a clear, well-sourced answer
      5. Store important findings in memory for future reference
    toolsets:
      - type: think
      - type: memory
        path: "./research_memory.db"
      - type: mcp
        ref: docker:duckduckgo
    add_date: true
```

## Advanced Tool Configuration

### Memory with Custom Database

```yaml
toolsets:
  - type: memory
    path: "./specialized_memory.db"
```

### Shared Todo Lists

Multiple agents can share the same todo list:

```yaml
toolsets:
  - type: todo
    shared: true
```

### Selective MCP Tools

You can limit which tools from an MCP server your agent can use:

```yaml
toolsets:
  - type: mcp
    command: some-mcp-server
    tools: ["specific_tool_1", "specific_tool_2"] # Only these tools
    env:
      - "SOME_CONFIG=value"
```

## Real-World Agent Examples

### Code Review Assistant

**code_reviewer.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Automated code reviewer
    instruction: |
      You are a senior code reviewer. When users share code or ask you
      to review files, provide thorough, constructive feedback on:

      - Code quality and best practices
      - Potential bugs and issues
      - Performance optimization opportunities
      - Security considerations
      - Documentation and readability

      Always read the code files first, then provide specific,
      actionable feedback with examples.
    toolsets:
      - type: filesystem
      - type: think
      - type: todo
    add_environment_info: true
```

### Project Manager Assistant

**project_manager.yaml**

```yaml
agents:
  root:
    model: anthropic/claude-3-sonnet
    description: Project management assistant
    instruction: |
      You are a project management assistant. Help users plan,
      organize, and track their projects.

      Capabilities:
      - Break down large projects into manageable tasks
      - Create and manage todo lists
      - Track project progress
      - Identify dependencies and blockers
      - Generate status reports
      - Remember project details across sessions
    toolsets:
      - type: todo
      - type: memory
        path: "./project_memory.db"
      - type: think
      - type: filesystem
    add_date: true
    add_environment_info: true
```

## Exercise 4: Design Your Own Multi-Tool Agent

Create an agent for a specific use case that combines multiple tools:

Ideas:

- **Data Analyst**: filesystem + shell + think (for analyzing data files)
- **Documentation Assistant**: filesystem + memory + think (for maintaining
  docs)
- **DevOps Helper**: shell + todo + memory (for deployment and monitoring)
- **Content Manager**: filesystem + memory + todo (for managing blog/content)

## Tool Interaction Patterns

Agents with tools often follow these patterns:

1. **Think First**: Use the think tool to plan approach
2. **Gather Information**: Read files or run commands to understand context
3. **Take Action**: Make changes or generate output
4. **Verify**: Check that actions were successful
5. **Remember**: Store important information for future use

## Best Practices

1. **Be Specific in Instructions**: Tell agents how to use their tools
   effectively
2. **Combine Complementary Tools**: Think + filesystem, shell + todo, etc.
3. **Consider Security**: Be careful with shell access and file permissions
4. **Test Thoroughly**: Verify agents behave safely with their tools
5. **Start Simple**: Begin with one tool, then add more as needed

## Troubleshooting Tools

If tools aren't working:

- Check that external MCP tools are installed correctly
- Verify file permissions for filesystem operations
- Test MCP tools independently before integrating
- Check debug logs for tool execution errors

## Key Takeaways

- **Tools transform agents from chatbots to actors**: They can now manipulate
  the real world
- **Built-in tools are easy to start with**: filesystem, shell, think, todo,
  memory
- **MCP tools provide unlimited extensibility**: Connect to any service or API
- **Combination is powerful**: Multiple tools working together create
  sophisticated workflows
- **Instructions matter more with tools**: Agents need guidance on when and how
  to use tools

## Next Steps

In Step 4, we'll learn about sub-agents - how to create teams of specialized
agents that can work together on complex tasks. This is where cagent's
multi-agent orchestration really shines!
