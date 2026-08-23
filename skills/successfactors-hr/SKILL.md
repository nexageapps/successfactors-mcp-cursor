---
name: successfactors-hr
description: >
  Query SAP SuccessFactors Employee Central through SuccessFactors MCP.
  Use when the user asks about employees, org charts, managers, job info,
  time off, who they are in SuccessFactors, or the DEMOCO demo tenant.
---

# SuccessFactors HR in Cursor

This plugin talks to SuccessFactors MCP over Streamable HTTP. The public
demo is company **DEMOCO** (synthetic people). It is not a live customer
tenant.

## How to ask

Type the question, not the tool name. On DEMOCO, `100045` (Jane Smith) and
`100020` (Alex Kim) exist.

- "Who is Jane Smith's manager?"
- "Search employees named Alex. What is their title and department?"
- "Call test_connection. Which tenant is active?"
- "Tell me about myself" (only after a signed-in MCP identity; do not search
  for the Cursor account name)

## Tool selection

| User asks | Call |
| --------- | ---- |
| Who am I / tell me about myself | `who_am_i` with no arguments |
| Find people by name | `search_employee` |
| One employee record | `get_employee` (`user_id` or omit for the signed-in caller) |
| Manager / reports / org | `get_manager`, `get_direct_reports`, `get_organization_hierarchy` |
| Job / employment | `get_job_information`, `get_employment_information` |
| Time off | `get_leave_balance`, `get_time_off_requests` |
| Which tenant is this? | `test_connection` |

All tools are READ. Do not invent writes. Do not put Hub keys, passwords, or
`sfmcp_…` values in tool arguments.

Anonymous `/mcp` on the public demo stays on DEMOCO even if someone saved a
Hub sandbox on `/connect`. A sandbox session needs `Authorization: Bearer
sfmcp_…` in the MCP config, not in chat.
