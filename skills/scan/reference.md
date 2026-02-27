# Aikido MCP Setup

To install and configure the Aikido MCP, use the **setup skill** (`aikido:setup`). It configures your API key and verifies the MCP server. You can pass your API key as an argument for automatic configuration:

- **With API key:** `/aikido:setup <your-api-key>`
- **Without API key:** `/aikido:setup` (you’ll be guided to get your key from https://app.aikido.dev → Settings → Integrations → IDE Plugins)

After setting the key, restart Claude Code so the MCP server picks it up.

For manual steps, see: https://help.aikido.dev/mcp/anthropic-claude-code-mcp