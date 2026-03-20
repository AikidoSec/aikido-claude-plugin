# Aikido Security — Claude Code Plugin

Brings [Aikido Security](https://aikido.dev) scanning directly into Claude Code. Detects SAST vulnerabilities, exposed secrets, and IaC misconfigurations in code you write or modify, and guides Claude to fix them before they ship.

## Skills

| Skill | Command | Description |
|---|---|---|
| Scan | `/aikido:scan` | Scans modified or new files for security issues, applies fixes, and re-scans until clean |
| Setup | `/aikido:setup [api-key]` | Verifies the plugin is configured and walks through API key setup if not. Pass your API key as an argument to configure it automatically. |

## Requirements

- Node.js 18+
- An Aikido API key — get one at [app.aikido.dev](https://app.aikido.dev) → Settings → Integrations → IDE Plugins

## Installation

Install the plugin from the Claude Code marketplace (coming soon).
Or install via the Aikido plugin marketplace by running the following commands:
- `/plugin marketplace add AikidoSec/aikido-claude-plugin`
- `/plugin install aikido`
- After install, run `/reload-plugins` to activate.

Next run the setup skill with your API key:

```
/aikido:setup your-key-here
```

This saves the key to your Claude Code user settings and registers the MCP server automatically. Restart Claude Code afterwards for the changes to take effect.

Alternatively, set the key as an environment variable and restart Claude Code:

```bash
export AIKIDO_API_KEY="your-key-here"
```

Run `/aikido:setup` (without a key) at any time to verify your configuration is working.

## More information

- [Aikido MCP documentation](https://help.aikido.dev/mcp/anthropic-claude-code-mcp)
- [Aikido Security](https://aikido.dev)
