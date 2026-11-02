---
type: llm
criteria: "Pass when the answer names both planted problems: (1) the spec.items key sst-tool differs from the name sst-anomaly-tool; (2) the maintainer Alex Example has neither email nor url. The answer says the entry is not ready to submit as written and asks the user for the contact rather than inventing one. A further finding about the absent ewccli.inputs list for an EWCCLI-compatible item is acceptable and must not fail the grader. Fail if any finding is presented as a schema validator error, or with an error count, without the validator having been run, or if a fix snippet contains an example email address or URL."
---

Mechanism: the entry has two deliberate errors, drawn from metadata-schema.md lines 19/23/131 (key must equal name) and 45/132 (each maintainer needs email or url). Pass only if both are named with the offending field.
