---
type: tool_used
tool: Bash
input_match: "\\beumdac(?:\\s+-\\S+)*\\s+search\\b[^\\n]*EO:EUM:DAT:0302[^\\n]*--(?:bbox|geometry)|\\beumdac(?:\\s+-\\S+)*\\s+search\\b[^\\n]*--(?:bbox|geometry)[^\\n]*EO:EUM:DAT:0302"
max: 0
---

The skill must not run an area-filtered search on the collection with the misplaced footprint.
