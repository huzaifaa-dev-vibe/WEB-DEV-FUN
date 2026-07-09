# MCP (Model Context Protocol)

> Open standard for connecting LLMs to data and tools. From Anthropic.

---

## Purpose

Use MCP to give LLMs access to your data, files, APIs, and tools.

## Prerequisites

- [AI/](../AI/), [LLM/](../LLM/).

## Learning Outcome

You can build and use MCP servers to extend LLM capabilities.

## Dependencies

- An MCP-compatible client (Claude Desktop, Cursor, Cline, etc.).

## Related Files

- [AI/](../AI/) · [LLM/](../LLM/) · [Agentic-Coding/](../Agentic-Coding/) · [EXTERNAL_REPOSITORIES.md#mcp-servers](../EXTERNAL_REPOSITORIES.md#mcp-servers)

## AI Instructions

When using MCP:
1. **MCP server** exposes tools / resources / prompts.
2. **MCP client** (Claude, Cursor) connects to servers.
3. Server can be local (stdio) or remote (SSE/HTTP).
4. Use official SDKs (`@modelcontextprotocol/sdk`).
5. Don't expose destructive tools without confirmation.

## Human Notes

### What MCP is
- Open standard (Anthropic-led).
- Connects LLM clients to data sources + tools.
- Replaces ad-hoc integrations.
- Like "USB-C for AI".

### Architecture
```
LLM Client (Claude Desktop)
    ↕ (MCP protocol)
MCP Server (your code)
    ↕
Tools / Resources / APIs
```

### Server capabilities
- **Tools** — functions the LLM can call (e.g., `get_weather`).
- **Resources** — data the LLM can read (e.g., files, DB schemas).
- **Prompts** — pre-made prompt templates.

### Build a server (TypeScript)
```ts
import { Server } from '@modelcontextprotocol/sdk/server';
import { StdioServerTransport } from '@modelcontextprotocol/sdk/server/stdio';

const server = new Server({
  name: 'my-server',
  version: '1.0.0',
}, {
  capabilities: { tools: {} },
});

server.setRequestHandler('tools/list', async () => ({
  tools: [{
    name: 'get_weather',
    description: 'Get weather for a city',
    inputSchema: {
      type: 'object',
      properties: { city: { type: 'string' } },
      required: ['city'],
    },
  }],
}));

server.setRequestHandler('tools/call', async (req) => {
  if (req.params.name === 'get_weather') {
    const { city } = req.params.arguments;
    return { content: [{ type: 'text', text: `Weather in ${city}: sunny` }] };
  }
});

const transport = new StdioServerTransport();
await server.connect(transport);
```

### Use existing servers
Many MCP servers exist:
- Filesystem.
- GitHub.
- Postgres.
- Slack.
- Google Drive.
- Puppeteer.
- Brave Search.
- And more.

→ [EXTERNAL_REPOSITORIES.md#mcp-servers](../EXTERNAL_REPOSITORIES.md#mcp-servers)

### Configure in Claude Desktop
`~/Library/Application Support/Claude/claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/Users/me/Desktop"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": { "GITHUB_TOKEN": "..." }
    }
  }
}
```

### Use in Cursor
- `.cursor/mcp.json` similar format.

### Use in Cline
- VS Code extension configures MCP servers.

### Remote MCP servers
- HTTP/SSE transport.
- Deploy on Cloudflare Workers, etc.
- Auth via OAuth.

### Security
- **Don't expose destructive tools** (file delete, DB drop) without confirmation.
- **Audit tool calls.**
- **Rate limit.**
- **Sandbox** when possible.

### When to use MCP
- You want to give an LLM agent access to your tools/data.
- You want a standard way (vs. custom integrations).
- You want to share your tool with multiple LLM clients.

### When NOT to use
- Just calling an LLM API directly (no agent).
- Simple function calling within your app.

## Common Mistakes

- ❌ Exposing destructive tools without confirmation.
- ❌ No rate limiting.
- ❌ No auth on remote servers.
- ❌ Overly broad file system access.

## Tools

- MCP docs: https://modelcontextprotocol.io/
- MCP TypeScript SDK: https://github.com/modelcontextprotocol/typescript-sdk
- MCP Python SDK: https://github.com/modelcontextprotocol/python-sdk
- Awesome MCP Servers: https://github.com/modelcontextprotocol/servers
- MCP Inspector: https://github.com/modelcontextprotocol/inspector

## References

- MCP spec: https://spec.modelcontextprotocol.io/
- Anthropic MCP: https://www.anthropic.com/news/model-context-protocol
- Awesome MCP: https://github.com/punkpeye/awesome-mcp-servers

## Exercises

1. Build an MCP server that exposes a tool.
2. Connect it to Claude Desktop.
3. Try 3 community MCP servers.

## Projects

- Build an MCP server for your team's docs / API.

---

**Previous:** [LLM/](../LLM/) · **Next:** [Agentic-Coding/](../Agentic-Coding/) · **Related:** [AI/](../AI/)
