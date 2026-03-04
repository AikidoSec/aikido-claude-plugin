---
name: setup
description: Configures the Aikido plugin by setting up the API key and verifying the MCP server. Accepts an optional API key argument to configure automatically. Use when the user wants to set up or verify the Aikido plugin, after installing it, or when aikido_full_scan fails or is unavailable.
arguments:
  - name: aikido-api-key
    description: Your Aikido API key from https://app.aikido.dev → Settings → Integrations → IDE Plugins. When provided, the key is configured automatically in Claude Code's MCP settings.
    required: false
---

When helping the user configure the Aikido security plugin:

## If the user provided an API key as an argument:

1. Read `~/.claude/settings.json` (create it as `{}` if it doesn't exist).
2. Merge `AIKIDO_API_KEY` into the `env` object, preserving all other existing settings. The result should look like:
   ```json
   {
     "env": {
       "AIKIDO_API_KEY": "<key>"
     }
   }
   ```
3. Write the updated JSON back to `~/.claude/settings.json`.
4. Confirm to the user that the API key has been saved to their Claude Code user settings and will apply to all projects.
5. Inform the user that they need to restart Claude Code for the MCP server to pick up the new key.
6. Offer to verify the setup after restart by running **aikido-mcp:aikido_full_scan** with a test payload.

## If no API key was provided:

1. Check whether the Aikido MCP server is currently available by calling **aikido-mcp:aikido_full_scan** with a minimal test payload: one file with path `test.js` and content `// test`.
2. If it responds successfully, confirm to the user that the Aikido plugin is already configured and ready to use.
3. If it fails or is unavailable, guide the user through the setup:
   a. Tell the user to get their API key from **https://app.aikido.dev** → Settings → Integrations → IDE Plugins.
   b. Suggest running the skill with the key directly:
      ```
      /aikido:setup <my-key>
      ```
   c. Remind the user to restart Claude Code after setting the key so the MCP server picks it up.
   d. Offer to verify the setup after they have set the key by running the test scan again.
