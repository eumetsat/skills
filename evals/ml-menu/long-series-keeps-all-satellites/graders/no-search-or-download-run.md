---
type: tool_used
tool: Bash
input_match: '(?<![\w./~-])eumdac\b(?!(?:[^\n]|\\\n)*--help)'
max: 0
---

The skill must answer from its table without running any `eumdac` command. `--help` does not count. A backslash-newline continuation does not hide the flag.
