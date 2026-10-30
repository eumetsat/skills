---
type: tool_used
tool: Bash
input_match: "\\beumdac(?:\\s+-\\S+)*\\s+download\\b(?![^\\n]*--help)|\\.open\\(\\)"
max: 0
---

The skill must not run `eumdac download` or a Python `product.open()` loop before the count, size, free space and destination are stated and the user authorises. `--help` does not count.
