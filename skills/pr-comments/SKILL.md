---
name: aikido-mcp-comments
description: Fetches comments already posted on a GitHub/GitLab/Azure DevOps pull or merge request (e.g. CI bot results, review feedback, Aikido's own scan-result comment). Use when the user asks what CI/CD said, wants to read/check/summarize PR or MR comments, mentions "pipeline comments", or asks about "Aikido comments"/"Aikido feedback"/what Aikido said or found on a PR — this reads via the native SCM CLI (gh/glab/az), not the Aikido MCP server.
---

Reading CI/CD or Aikido comments on a pull/merge request means fetching whatever is already
posted there through the repo's own SCM CLI. Don't route this through the Aikido MCP server,
the native CLI already does it in one call.

## 1. Determine the target

- If the user names a specific repo/PR (a URL, or `org/repo#123`), use that.
- Otherwise, run `git remote get-url origin` in the current working directory and use the
  current branch's PR/MR (the CLIs below auto-detect this when no number is given).

## 2. Determine the platform

Match the remote host:
- Contains `github` → **GitHub**, use `gh`.
- Contains `gitlab` → **GitLab**, use `glab`.
- Contains `dev.azure.com` or `visualstudio.com` → **Azure DevOps**, use `az`.

If the host matches none of these (e.g. self-hosted with a custom domain, or Bitbucket), stop
and ask the user which platform it is, or tell them this skill only covers GitHub/GitLab/Azure
DevOps.

## 3. Fetch the comments

Run the command directly, don't pre-check install or auth state first. See
[reference.md](reference.md) for the exact command and flags per platform.

## 4. Recover from failure

- **Command not found**: don't install it yourself. Tell the user the CLI is missing, show the
  install command from reference.md, and ask for permission before running it. Only proceed
  once they say yes, then retry the same fetch.
- **Auth error** (401/403, or the CLI reports not logged in): print the exact login command
  for that platform, ask the user to run it (it's an interactive browser flow you can't
  complete yourself), wait for their confirmation, then retry.

## 5. Present the results

List the comments in chronological order: author, timestamp, body. Don't filter out bot
comments or try to classify which ones are "CI/CD" versus human, just show the thread as-is.

**Never:** call an Aikido MCP tool to satisfy this request, or fabricate comment content if
the fetch keeps failing, report the actual error instead.