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

## Workshop Overview

This workshop is structured as a progressive learning journey with 5 core steps:

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

## Prerequisites

Before starting this workshop, you should have:

1. **cagent installed** - Follow the installation instructions in the main
   README
2. **Docker Desktop running** - Required for Step 2 (agent sharing)
3. **Docker Hub account** - For pushing and pulling shared agents
4. **Basic YAML knowledge** - Agent configurations use YAML format
5. **AI API access** - OpenAI, Anthropic, or other supported model providers
6. **Command line familiarity** - You'll run cagent from the terminal

## Workshop Structure

Each step is designed as a standalone learning module that builds upon previous
knowledge:

- **Theory and Concepts**: Understanding the "why" behind each feature
- **Practical Examples**: Complete, working agent configurations
- **Hands-on Exercises**: Build your own agents to reinforce learning
- **Real-world Applications**: See how concepts apply to actual use cases

## How to Use This Workshop

### For Self-Study

1. Work through each step in order
2. Try all the example configurations
3. Complete the exercises before moving on
4. Experiment with variations and modifications

### For Instructors

- Each step is designed for ~15 minutes of instruction
- Include time for hands-on practice with each concept
- Encourage experimentation and questions
- Use the exercises to assess understanding

### For Teams

- Work through steps together
- Discuss real-world applications for your specific use cases
- Share interesting agent configurations you create
- Plan how to integrate agents into your workflows

## Getting Started

### 1. Verify Your Setup

```bash
# Check that cagent is installed
cagent --version

# Test with a simple agent
cagent run step1_introduction_to_cagent.md
```

### 2. Follow the Learning Path

Start with Step 1 and work through each step sequentially. Each step builds on
concepts from previous steps.

### 3. Practice and Experiment

Don't just read - create and test your own agent configurations. Learning by
doing is most effective.

## Key Learning Outcomes

By the end of this workshop, you will be able to:

### Technical Skills

- Configure agents with appropriate models and instructions
- Integrate tools to give agents real-world capabilities
- Design multi-agent teams for complex projects
- Use shared resources for agent collaboration
- Debug and troubleshoot agent behaviors

### Design Skills

- Identify tasks suitable for agent automation
- Break down complex workflows into agent-manageable steps
- Design effective agent personalities and instructions
- Plan tool requirements for specific use cases
- Architect multi-agent systems for scalability

### Practical Applications

- Automate repetitive development tasks
- Create intelligent content creation workflows
- Build research and analysis assistants
- Design customer service and support agents
- Implement code review and quality assurance systems

## Workshop Files

This directory contains:

- **step1_introduction_to_cagent.md** - Basic concepts and first agents
- **step2_sharing_agents.md** - Agent distribution with Docker registries
- **step3_introduction_to_agents.md** - Advanced agent configuration
- **step4_introduction_to_toolsets.md** - Tools and capabilities
- **step5_introduction_to_sub_agents.md** - Multi-agent teams
- **README.md** - This introduction (you are here)

## Common Workshop Patterns

Throughout this workshop, you'll see these recurring patterns:

### Progressive Complexity

Each step starts simple and adds complexity gradually. Don't skip ahead - the
foundation matters.

### Example-Driven Learning

Every concept is illustrated with complete, working examples you can run
immediately.

### Hands-on Exercises

Theory is reinforced with practical exercises. Complete these to solidify your
understanding.

### Real-world Applications

Learn not just how to build agents, but when and why to use different
approaches.

## Tips for Success

### Start Simple

- Begin with basic agents before building complex teams
- Test each configuration before adding more features
- Understand one concept fully before moving to the next

### Experiment Freely

- Modify example configurations to see what happens
- Try different models and see how they behave differently
- Create agents for your own use cases and interests

### Think About Real Applications

- Consider how each concept applies to your actual work
- Identify processes in your workflow that could benefit from agents
- Design agents that solve real problems you face

### Ask Questions

- If something doesn't work as expected, investigate why
- Experiment with different instructions and configurations
- Don't be afraid to break things - that's how you learn

## Beyond This Workshop

After completing this workshop, you'll have a solid foundation in cagent. Next
steps include:

### Explore Advanced Features

- Custom MCP tool development
- Advanced model configurations
- Production deployment considerations
- Performance optimization techniques

### Build Real Systems

- Identify automation opportunities in your work
- Start with small, focused agent implementations
- Gradually expand to more complex multi-agent systems
- Share your successes with the community

### Stay Current

- Follow cagent development and new features
- Engage with the community for tips and best practices
- Contribute back with your own examples and tools

## Getting Help

If you encounter issues during the workshop:

1. **Check the Examples**: Make sure you're following the provided
   configurations exactly
2. **Review Previous Steps**: Later concepts build on earlier ones - make sure
   you understand the foundations
3. **Read Error Messages**: cagent provides helpful error messages when things
   go wrong
4. **Consult Documentation**: The main project documentation has detailed
   reference information
5. **Ask the Community**: The cagent community is helpful for troubleshooting
   and advice

## Workshop Goals

This workshop aims to:

- **Demystify AI Agents**: Show that building agents is accessible and practical
- **Provide Practical Skills**: Give you tools you can use immediately
- **Inspire Innovation**: Help you see new possibilities for automation and
  assistance
- **Build Confidence**: Empower you to create sophisticated agent systems

## Ready to Begin?

Time to start building! Open [Step 1: Introduction to
cagent](step1_introduction_to_cagent.md) and begin your journey into the world
of AI agents.

Remember: the best way to learn cagent is by building and experimenting. Don't
just read about these concepts - create agents, test them, break them, and learn
from the experience.

Happy agent building!

---

## Workshop Feedback

We'd love to hear about your experience with this workshop:

- What concepts were most challenging?
- Which examples were most helpful?
- What real-world applications are you planning?
- How can we improve the workshop content?

Your feedback helps make this workshop better for future participants.
