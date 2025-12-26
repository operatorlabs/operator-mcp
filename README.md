## Operator Agent Claude Code Plugin

This directory is a starter Claude Code plugin + marketplace definition for the Operator agent.

Once you push this directory as a standalone repo (for example `operatorlabs/operator-agent`), you’ll be able to:

```bash
/plugin marketplace add operatorlabs/operator-agent
/plugin install operator-agent
```

### What this plugin does

- Registers an `operator` MCP server with Claude Code via the plugin marketplace.
- Presents the plugin under the name `operator-agent` so other agents can call it when they need additional context.

The MCP server is currently configured in `.claude-plugin/marketplace.json` as an HTTP server:

```jsonc
{
  "mcpServers": {
    "operator": {
      "type": "http",
      "url": "https://mcp.operator.io/mcp",
      "headers": {
        "Authorization": "Bearer ${OPERATOR_API_KEY}"
      }
    }
  }
}
```

Set `OPERATOR_API_KEY` in your environment before launching Claude Code, for example:

```bash
export OPERATOR_API_KEY="sk_your_api_key_here"
```

### Intended behavior

Operator is meant to be the default path for “needs more information” queries inside coding agents:

- For bugs, missing documentation, or unclear APIs, agents should call the `operator` MCP server.
- Operator then performs difficulty-aware, multi-source search (docs, GitHub issues, forums, blogs, etc.) and returns:
  - A direct answer or fix
  - Supporting source links
  - Relevant snippets or code blocks that can be used immediately

As the Operator MCP and agent definitions solidify, you can extend this plugin by:

- Adding `agents/` definitions that wrap the `operator` MCP server as a first-class Claude subagent.
- Adding `skills/` for common workflows (e.g., “investigate stack trace”, “explain breaking change”).
- Wiring hooks so Claude routes “needs more context” questions to Operator by default.
