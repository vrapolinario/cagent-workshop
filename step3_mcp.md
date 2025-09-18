# Step n: MCP (Model Context Protocol)

[MCP](https://modelcontextprotocol.io/) is an open-source standard for connecting AI applications to external systems.

MCP is a standardised protocol clients can use to give an agent access to different MCP servers that contain tools (and much more, we encourage you to go and read the specification).

![MCP Toolkit](mcp.png)

```diff
version: "2"

agents:
  root:
    model: openai/gpt-4o
    instruction: You are an amazing developer
    add_environment_info: true
    add_date: true
    toolsets:
      - type: todo
      - type: shell
      - type: filesystem
      - type: mcp
        ref: docker:duckduckgo
```
