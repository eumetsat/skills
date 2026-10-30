---
type: tool_used
tool: Bash
input_match: "\\beumdac(?:\\s+-\\S+)*\\s+search\\b(?![^\\n]*--filename)[^\\n]*EO:EUM:DAT:(?:0874|0863)"
max: 0
---

The skill must not run a search on CLARA-A3 or SARAH-3 without a `--filename` filter: both collections hold every product and time step.
