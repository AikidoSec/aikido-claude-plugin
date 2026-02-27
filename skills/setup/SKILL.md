---
name: aikido-setup
description: Configures the Aikido plugin by setting up the API key and verifying the MCP server. Use when the user wants to set up or verify the Aikido plugin, after installing it, or when aikido_full_scan fails or is unavailable.
---

When helping the user configure the Aikido security plugin:

1. Check whether the Aikido MCP server is currently available by calling **aikido-mcp:aikido_full_scan** with a minimal test payload: one file with path `test.js` and content `// test`.
2. If it responds successfully, confirm to the user that the Aikido plugin is already configured and ready to use.
3. If it fails or is unavailable, guide the user through the setup:
   a. Tell the user to get their API key from **https://app.aikido.dev** → Settings → Integrations → IDE Plugins.
   b. Provide the exact shell command to set it for their current shell, and offer persistent options:

      **Temporary (current session only):**
      ```
      export AIKIDO_API_KEY="<my-key>"
      ```

      **Persistent — add to shell profile:**
      - Bash: `~/.bashrc` or `~/.bash_profile`
      - Zsh: `~/.zshrc`
      - Fish: run `set -Ux AIKIDO_API_KEY "<my-key>"`

   c. Remind the user to restart Claude Code after setting the key so the MCP server picks it up.
   d. Offer to verify the setup after they have set the key by running the test scan again.
