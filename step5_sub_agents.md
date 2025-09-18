# Step 5: Introduction to Sub-agents

## From Single Agent to Team of Specialists

In the previous steps, we created individual agents with various tools. Now
we'll learn about cagent's most powerful feature: sub-agents. This allows you to
create teams of specialized agents that work together on complex tasks.

## What are Sub-agents?

Sub-agents are specialized agents that work under a root coordinator agent.
Think of it like a company structure:

- **Root agent**: The project manager who understands the big picture
- **Sub-agents**: Specialized team members (designer, developer, tester, writer,
  etc.)

Benefits of sub-agents:

- **Specialization**: Each agent excels at specific tasks
- **Parallel processing**: Multiple agents can work simultaneously
- **Modular design**: Easy to add, remove, or modify team members
- **Clear responsibilities**: Each agent has a focused role

## Basic Sub-agent Structure

Here's the fundamental pattern for sub-agents:

**basic_team.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Team coordinator
    instruction: |
      You are a team coordinator managing specialized sub-agents.
      Delegate tasks to the appropriate team members based on their expertise.
    sub_agents: [specialist1, specialist2]

  specialist1:
    model: openai/gpt-4o-mini
    description: Specialist for task type A
    instruction: You specialize in task type A. Focus on doing this well.

  specialist2:
    model: openai/gpt-4o-mini
    description: Specialist for task type B
    instruction: You specialize in task type B. Focus on doing this well.
```

## Exercise 1: Simple Two-Agent Team

Let's start with a basic writing team:

**writing_team.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Writing project manager
    instruction: |
      You are a writing project manager who coordinates between a researcher
      and a writer to create well-researched articles.

      Workflow:
      1. When given a topic, first ask the researcher to gather information
      2. Once research is complete, ask the writer to create the article
      3. Review the final output and suggest improvements if needed

      Always use the transfer_task tool to delegate work to your team members.
    sub_agents: [researcher, writer]

  researcher:
    model: openai/gpt-4o-mini
    description: Content researcher
    instruction: |
      You are a thorough researcher. When given a topic, research and gather
      relevant information, facts, and insights. Present your findings in a
      clear, organized manner that will help a writer create great content.

      Always be accurate and cite your sources when possible.

  writer:
    model: openai/gpt-4o-mini
    description: Content writer
    instruction: |
      You are a skilled content writer. Use research provided to you to create
      engaging, well-structured articles. Focus on clarity, flow, and making
      complex topics accessible to readers.
```

Test this by asking the root agent to create an article about a topic of your
choice.

## Sub-agents with Different Tools

One of the most powerful patterns is giving different sub-agents different
toolsets:

**dev_team.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Development project manager
    instruction: |
      You are managing a development team. You have a frontend developer
      who handles UI/UX and user-facing code, and a backend developer
      who handles server logic, databases, and APIs.

      When users request development work:
      1. Analyze the requirements 
      2. Determine what frontend and backend work is needed
      3. Delegate tasks to the appropriate specialists
      4. Coordinate their work to ensure integration
    sub_agents: [frontend_dev, backend_dev]
    toolsets:
      - type: think
      - type: todo

  frontend_dev:
    model: openai/gpt-4o
    description: Frontend developer
    instruction: |
      You are a frontend developer specializing in user interfaces,
      user experience, and client-side functionality. You work with
      HTML, CSS, JavaScript, React, and other frontend technologies.

      Focus on creating intuitive, responsive, and visually appealing
      user interfaces.
    toolsets:
      - type: filesystem
      - type: shell
      - type: think

  backend_dev:
    model: openai/gpt-4o
    description: Backend developer
    instruction: |
      You are a backend developer specializing in server logic, 
      databases, APIs, and system architecture. You work with
      various backend technologies and focus on performance,
      security, and scalability.

      Focus on creating robust, efficient backend systems.
    toolsets:
      - type: filesystem
      - type: shell
      - type: think
```

## Exercise 2: Documentation Team

Create a team that specializes in creating and maintaining documentation:

**docs_team.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Documentation team lead
    instruction: |
      You lead a documentation team consisting of a technical analyst
      who understands complex systems, and a technical writer who
      creates clear, user-friendly documentation.

      Process for documentation tasks:
      1. Have the analyst examine and understand the subject matter
      2. Have the writer create clear, well-structured documentation
      3. Review and ensure quality and completeness
    sub_agents: [analyst, tech_writer]
    toolsets:
      - type: filesystem
      - type: think

  analyst:
    model: openai/gpt-4o
    description: Technical analyst
    instruction: |
      You are a technical analyst who excels at understanding complex
      systems, code, and processes. When given something to analyze,
      break it down into its key components, understand how it works,
      and identify what needs to be documented.

      Provide clear analysis that a technical writer can use to
      create excellent documentation.
    toolsets:
      - type: filesystem
      - type: shell
      - type: think

  tech_writer:
    model: openai/gpt-4o-mini
    description: Technical writer
    instruction: |
      You are a technical writer who creates clear, accessible
      documentation. Use analysis provided to you to write docs that
      are well-organized, easy to follow, and helpful for users.

      Focus on structure, clarity, and providing practical examples.
    toolsets:
      - type: filesystem
      - type: think
```

## Advanced Pattern: Hierarchical Sub-agents

Sub-agents can have their own sub-agents, creating hierarchical teams:

**company_structure.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: CEO - Overall project coordinator
    instruction: |
      You are the CEO coordinating major projects. You work with
      department heads who manage their own specialized teams.
    sub_agents: [engineering_manager, marketing_manager]

  engineering_manager:
    model: openai/gpt-4o
    description: Engineering department head
    instruction: |
      You manage the engineering department, coordinating between
      frontend and backend development teams.
    sub_agents: [frontend_team, backend_team]

  frontend_team:
    model: openai/gpt-4o-mini
    description: Frontend development team
    instruction: You handle all user interface and user experience work.
    toolsets:
      - type: filesystem
      - type: shell

  backend_team:
    model: openai/gpt-4o-mini
    description: Backend development team
    instruction: You handle server logic, databases, and APIs.
    toolsets:
      - type: filesystem
      - type: shell

  marketing_manager:
    model: openai/gpt-4o
    description: Marketing department head
    instruction: |
      You manage marketing initiatives and coordinate content creation.
    sub_agents: [content_creator, social_media_manager]

  content_creator:
    model: openai/gpt-4o-mini
    description: Content creation specialist
    instruction: You create marketing content, blog posts, and materials.

  social_media_manager:
    model: openai/gpt-4o-mini
    description: Social media specialist
    instruction: You manage social media presence and engagement.
```

## Shared Resources Between Sub-agents

Sub-agents can share resources like memory and todo lists:

**collaborative_team.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Project coordinator with shared resources
    instruction: |
      You coordinate a team that shares todo lists and memory.
      This enables better collaboration and information sharing.
    sub_agents: [planner, executor]
    toolsets:
      - type: todo
        shared: true
      - type: memory
        path: "./shared_memory.db"

  planner:
    model: openai/gpt-4o-mini
    description: Task planner
    instruction: |
      You create detailed project plans and task lists. Use the shared
      todo system so the executor can see what needs to be done.
    toolsets:
      - type: todo
        shared: true
      - type: memory
        path: "./shared_memory.db"
      - type: think

  executor:
    model: openai/gpt-4o-mini
    description: Task executor
    instruction: |
      You execute tasks from the shared todo list. Update task status
      and store results in shared memory for the team.
    toolsets:
      - type: todo
        shared: true
      - type: memory
        path: "./shared_memory.db"
      - type: filesystem
      - type: shell
```

## Exercise 3: Quality Assurance Team

Create a team that includes a QA specialist:

**qa_team.yaml**

```yaml
agents:
  root:
    model: openai/gpt-4o
    description: Quality-focused project manager
    instruction: |
      You manage projects with a focus on quality. Your team includes
      a developer who creates solutions and a QA specialist who tests
      and validates the work.

      Always have QA review work before considering tasks complete.
    sub_agents: [developer, qa_specialist]
    toolsets:
      - type: todo

  developer:
    model: openai/gpt-4o
    description: Solution developer
    instruction: |
      You develop solutions to user requirements. Focus on creating
      working, functional implementations.
    toolsets:
      - type: filesystem
      - type: shell
      - type: think

  qa_specialist:
    model: openai/gpt-4o-mini
    description: Quality assurance specialist
    instruction: |
      You test and validate work done by the development team.
      Check for correctness, completeness, and quality. Provide
      detailed feedback and identify any issues that need fixing.
    toolsets:
      - type: filesystem
      - type: shell
      - type: think
```

## Real-World Example: Complete Development Team

Here's a comprehensive example inspired by the dev-team.yaml:

**complete_dev_team.yaml**

```yaml
agents:
  root:
    model: anthropic/claude-sonnet-4-0
    description: Product Manager
    instruction: |
      You are a Product Manager leading a complete development team.
      Your team includes a UI/UX designer, a frontend engineer,
      a backend engineer, and a QA tester.

      For each project:
      1. Break requirements into small, manageable iterations
      2. Coordinate work between team members
      3. Ensure each iteration delivers complete, testable features
      4. Maintain project documentation and track progress

      Always start with the most basic functionality and build iteratively.
    sub_agents: [designer, frontend_engineer, backend_engineer, qa_tester]
    toolsets:
      - type: filesystem
      - type: think
      - type: todo
      - type: memory
        path: "./project_memory.db"

  designer:
    model: openai/gpt-4o
    description: UI/UX Designer
    instruction: |
      You create user interface designs and wireframes. Focus on
      user experience, accessibility, and visual design.

      For each feature:
      1. Create wireframes and mockups
      2. Define user interactions
      3. Specify design details for implementation
      4. Consider responsive design for different screen sizes
    toolsets:
      - type: filesystem
      - type: think
      - type: memory
        path: "./project_memory.db"

  frontend_engineer:
    model: openai/gpt-4o
    description: Frontend Engineer
    instruction: |
      You implement user interfaces based on designs. Create
      responsive, interactive web applications.

      Technologies: HTML, CSS, JavaScript, React, TypeScript
      Focus on code quality, performance, and user experience.
    toolsets:
      - type: filesystem
      - type: shell
      - type: think
      - type: memory
        path: "./project_memory.db"

  backend_engineer:
    model: openai/gpt-4o
    description: Backend Engineer
    instruction: |
      You build backend systems, APIs, and databases. Focus on
      performance, security, and scalability.

      Responsibilities:
      - Design and implement APIs
      - Set up databases and data models
      - Handle authentication and authorization
      - Integrate with frontend systems
    toolsets:
      - type: filesystem
      - type: shell
      - type: think
      - type: memory
        path: "./project_memory.db"

  qa_tester:
    model: openai/gpt-4o
    description: QA Tester
    instruction: |
      You test applications for functionality, usability, and quality.
      Create test plans, execute tests, and report issues.

      Testing approach:
      - Functional testing of features
      - User experience testing
      - Integration testing
      - Bug reporting with reproduction steps
    toolsets:
      - type: filesystem
      - type: shell
      - type: think
      - type: memory
        path: "./project_memory.db"
```

## Communication Patterns Between Sub-agents

### 1. Direct Delegation

The root agent directly assigns tasks to specific sub-agents.

### 2. Workflow Handoffs

Work flows from one sub-agent to another in sequence.

### 3. Parallel Processing

Multiple sub-agents work on different parts of the same project simultaneously.

### 4. Review and Feedback Loops

Sub-agents review each other's work and provide feedback.

## Exercise 4: Design Your Own Team

Create a sub-agent team for one of these scenarios:

### Content Marketing Team

- **Root**: Content marketing manager
- **Sub-agents**: Content strategist, copywriter, SEO specialist, social media
  manager

### Research Team

- **Root**: Research project leader
- **Sub-agents**: Data collector, data analyst, report writer

### Customer Support Team

- **Root**: Support team lead
- **Sub-agents**: Technical support, billing specialist, escalation handler

### Educational Team

- **Root**: Course coordinator
- **Sub-agents**: Subject matter expert, instructional designer, content creator

## Best Practices for Sub-agents

### 1. Clear Role Definition

Each agent should have a well-defined, specific role and responsibility.

### 2. Appropriate Model Selection

- Use more capable models for coordinators and complex reasoning
- Use efficient models for specialized, focused tasks

### 3. Tool Distribution

Give each agent only the tools they need for their specific role.

### 4. Communication Protocols

Establish clear patterns for how agents coordinate and share information.

### 5. Shared Resources

Use shared memory and todos when agents need to collaborate closely.

### 6. Error Handling

Plan for what happens when sub-agents encounter problems or conflicts.

## Common Anti-patterns to Avoid

### 1. Over-complexity

Don't create sub-agents for simple tasks that a single agent can handle well.

### 2. Role Overlap

Avoid giving multiple agents the same responsibilities without clear
coordination.

### 3. Tool Duplication

Don't give every agent every tool - be intentional about tool distribution.

### 4. Poor Coordination

Ensure the root agent knows how to effectively coordinate sub-agents.

## Advanced Sub-agent Techniques

### Dynamic Task Routing

The root agent can choose which sub-agent to use based on the specific task:

```yaml
instruction: |
  Analyze each request and route to the most appropriate specialist:
  - Code-related tasks → developer
  - Design tasks → designer  
  - Testing tasks → qa_specialist
  - Writing tasks → technical_writer
```

### Multi-stage Workflows

Create workflows where work passes through multiple agents:

```yaml
instruction: |
  For each project:
  1. Designer creates mockups
  2. Developer implements the design
  3. QA tests the implementation
  4. Technical writer documents the feature
  5. Project manager reviews and approves
```

### Feedback Loops

Implement review and revision cycles between agents.

### Specialized Models

Use different AI models for different sub-agents based on their strengths.

## Monitoring and Debugging Sub-agent Teams

### Questions to Ask:

- Are tasks being routed to the right specialists?
- Are agents completing their assigned work?
- Is coordination between agents working smoothly?
- Are shared resources being used effectively?

### Common Issues:

- **Coordination problems**: Root agent doesn't delegate effectively
- **Resource conflicts**: Agents interfering with each other's work
- **Communication gaps**: Information not shared between agents
- **Role confusion**: Agents unclear about their responsibilities

## Key Takeaways

- **Sub-agents enable specialization**: Create expert agents for specific
  domains
- **Coordination is crucial**: The root agent must effectively manage the team
- **Tool distribution matters**: Give agents the right tools for their roles
- **Shared resources enable collaboration**: Memory and todos can be shared
- **Start simple**: Begin with 2-3 agents before creating complex hierarchies
- **Clear roles prevent conflicts**: Each agent should have distinct
  responsibilities

## Integration with Previous Steps

Sub-agents combine everything from previous steps:

- **Step 1**: Individual agent capabilities
- **Step 2**: Advanced agent instructions and behaviors
- **Step 3**: Toolsets for different specializations
- **Step 4**: Team coordination and collaboration

## Next Steps for Your Workshop

After mastering sub-agents, participants should be able to:

- Design multi-agent teams for complex projects
- Create specialized agents with focused roles
- Implement effective coordination between agents
- Use shared resources for collaboration
- Build real-world agent systems for their specific needs

## Production Considerations

When deploying sub-agent systems:

- **Performance**: More agents mean more API calls and costs
- **Complexity**: Debug and maintain systems with multiple agents
- **Reliability**: Handle failures in sub-agent communications
- **Security**: Ensure proper access controls across the agent team

This completes your foundation in cagent! You now understand how to build
sophisticated multi-agent systems that can handle complex, real-world tasks
through specialized collaboration.
