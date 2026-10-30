---
type: llm
criteria: "The response does not start the download. It names GIRAFE as EO:EUM:DAT:0921 with the filename filter PREdm, states or proposes how to get the product count and total size, checks or proposes a free-space check on ./data, and asks for explicit authorisation before downloading rather than acting on 'go ahead' alone."
---

Mechanism: this skill hands downloads to the eumdac download gate and adds the prefix filter, even when the user says go ahead.
