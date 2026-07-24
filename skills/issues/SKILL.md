---
name: aikido-issues
description: List, count, summarize, or triage security issues from the Aikido security feed. Use when the user asks about Aikido findings, vulnerabilities, leaked secrets, SAST/IaC/SCA results, cloud or container security issues, or EOL/license/malware alerts surfaced by Aikido.
---

When listing Aikido feed issues:

1. Use **aikido-mcp:aikido_issues_list**
2. Call it when the user wants to list, show, count, or summarize Aikido feed issues.
3. Pass scope fields only when the user (or workspace context) supplies them: `cloud_name`, `repo_name`, `repo_branch_name`, `vm_name`, `domain_name`, `container_name`, `team_name`, `workspace_name`.
4. Optional `issue_types` (array): `open_source`, `leaked_secret`, `cloud`, `sast`, `iac`, `surface_monitoring`, `malware`, `eol`, `mobile`, `docker_container`, `cloud_instance`, `scm_security`, `license`, `ai_pentest` — e.g. include `leaked_secret` for secrets. Omit when no category filter is needed.
5. SLA filters (booleans): set `out_of_sla: true` when the user wants issues that are past their SLA, or `sla_due_soon: true` for issues approaching their SLA deadline.
6. Pagination: use numeric `page` only when the user needs more than the first page of results (zero-indexed). Only 25 findings are reported per page. Report to the user if there are more findings on following pages.
7. Present each issue exactly in this form (increment `#`):
   ```
   Issue #1: <issue_title>
    - Issue type: <issue_type>
    - Severity: <issue_severity> (<issue_severity_label>)
    - Remediation: <issue_remediation>
   ```
   Add extra bullets when the field is relevant, e.g. `File: <issue_file> (line <issue_start_line>)`, `Location: <location.type> <location.name> (<location.branch_name>)`, `Issue link: <issue_link>`, `SLA due date: <issue_remediate_by_date>`.

If the Aikido MCP server is not available or fails, inform the user:

> The Aikido MCP server is required for Aikido feed issues but is not available.
> Install it following the setup guide at [reference.md](../scan/reference.md), or run `/aikido:setup`, then retry.
