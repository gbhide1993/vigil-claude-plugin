---
description: Generate a Vigil audit report for the current Claude Code session
---
# Vigil Session Report

Generate a Vigil audit report for the current Claude Code session using the `vigil` MCP server.

1. Call `get_current_session` (no parameters). If the Vigil tools are unavailable, tell the user the Vigil backend is not running. If `session_id` is null (`status` is `"none"`), tell the user no Vigil session has been observed.
2. Display from the result: session ID (first 8 chars), `agent`, `start_time`, `status`, `duration_min`, `files_touched`, `red_lines`, `friction_signals`. Network connections are not monitored, and file reads are not recorded; do not report either as zero.
3. Provide the PDF download link: http://127.0.0.1:7422/api/sessions/{session_id}/report
4. If `red_lines` is greater than 0, call `get_red_line_events` with `since_hours` set to the hours since `start_time`, rounded up (minimum 1). Keep only events whose `session_id` matches, and list them in full.
