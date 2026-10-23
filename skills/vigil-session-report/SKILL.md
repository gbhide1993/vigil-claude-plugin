---
description: Generate a Vigil session audit report. Use when the user asks to download a session report, generate a PDF, get the audit report, or review what the agent did this session.
---

# Vigil Session Report

Use the `vigil` MCP server to summarize the current session and point the user to the PDF audit report.

## Steps

1. Call `get_current_session` (no parameters) to get the current session.
   - If the Vigil tools are unavailable, tell the user: "Vigil backend is not reachable. Vigil must be running at http://127.0.0.1:7422."
   - If `session_id` is null (`status` is `"none"`), tell the user: "No Vigil session found. Vigil must be running and monitoring an agent session."

2. Tell the user, from the result:
   - Session ID (first 8 characters)
   - `agent` name
   - `start_time` (local timezone), `status` (`active`, `idle` or `completed`) and `duration_min`
   - Summary counts: `files_touched`, `red_lines`, `friction_signals`
   - Network connections are not monitored, and file reads are not recorded, so do not report either as zero

3. Provide the PDF download URL:
   ```
   http://127.0.0.1:7422/api/sessions/{session_id}/report
   ```
   Tell the user they can open this URL in their browser to download the PDF, or use the **Download Session Report (PDF)** button in the Vigil VS Code sidebar.

4. If `red_lines` is greater than 0, call `get_red_line_events` with `since_hours` set to the hours since `start_time`, rounded up (minimum 1). Keep only events whose `session_id` matches the current session and list them in full (type, severity, description, timestamp, process, filepath).

5. If the user asks about friction (retry loops, rapid reverts), call `get_friction_findings` with `session_id`. If they ask about a specific file, call `get_file_history` with `filepath`.

## Notes

- The PDF is generated independently of agent self-reporting. It reflects what Vigil observed at OS level; file reads are not recorded and short-lived processes between checks can be missed, so absence of an entry is not proof something did not happen
- Network connections are not monitored
- Red lines are high-risk events such as credential file changes, out-of-scope writes and dangerous commands
- Friction findings are inferred patterns, each with a confidence level, not proof of a problem
- The Vigil backend must be running at `http://127.0.0.1:7422` for this to work
