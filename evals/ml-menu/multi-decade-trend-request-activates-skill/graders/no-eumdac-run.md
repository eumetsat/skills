---
type: tool_used
tool: Bash
input_match: '(?<![\w./~-])eumdac\b(?!(?:[^\n]|\\\n)*--help)'
max: 0
---

The first step is choosing the record, which needs no `eumdac` command. `--help` does not count. A backslash-newline continuation does not hide the flag.
