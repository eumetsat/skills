---
type: tool_used
tool: Bash
input_match: '\beumdac(?:\s+-\S+)*\s+search\b(?:[^\n;&|]|\\\n)*(?:EO:EUM:DAT:0302(?:[^\n;&|]|\\\n)*--(?:bbox|geometry)|--(?:bbox|geometry)(?:[^\n;&|]|\\\n)*EO:EUM:DAT:0302)'
max: 0
---

The skill must not run an area-filtered search on the collection with the misplaced footprint. A backslash-newline continuation stays part of the same command. The proposed command is graded by the `explains-footprint` and `no-area-filter-in-answer` graders.
