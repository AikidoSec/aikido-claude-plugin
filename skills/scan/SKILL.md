---
name: scan
description: Runs an Aikido security scan on generated, added, or modified code files to detect SAST vulnerabilities and exposed secrets. Use when the user wants to scan code for security issues, after writing or modifying code, or when they mention Aikido, security scan, or SAST.
---

When scanning the user's code for security vulnerabilities using the Aikido MCP server:

1. Identify all files that were generated, added, or modified in this session (or that the user has mentioned).
2. For each file, read its full content.
3. Run **aikido-mcp:aikido_full_scan** with all files and their full content. Stay within the 50-file limit per request — batch into multiple calls if needed.
4. If any security issues are found:
   - Explain each issue clearly: title, description, severity, file location, and line numbers.
   - Apply fixes guided by the remediation provided by Aikido.
   - After applying all fixes, run **aikido-mcp:aikido_full_scan** again to verify that the issues were resolved and no new issues were introduced.
   - **Stopping the loop:** If you can explain why the applied fix is safe (e.g. the fix correctly addresses the finding and the remaining scan output is a false positive or acceptable), you may stop and report to the user. Otherwise, repeat the fix-and-rescan cycle up to 3 attempts; if issues remain after that, report them to the user instead of continuing.
5. Report the final scan result to the user — confirm all clear or list any unresolved issues with explanation.

If the Aikido MCP server is not available or fails to start, inform the user:

> The Aikido MCP server is required for security scanning but is not available.
> Install it following the setup guide at [reference.md](reference.md).