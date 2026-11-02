---
type: llm
criteria: "The response identifies BOTH planted errors specifically: (1) the spec.items key is sst-tool but the name attribute is sst-anomaly-tool, and the two must be equal; (2) the maintainer Alex Example has neither email nor url, and at least one is required. The response says the entry is not valid or not ready to submit as written, and does not invent a contact for the user (it asks for one). It must not report errors that are not there as certain (the other fields are well-formed)."
---

Mechanism: the entry has two deliberate errors, drawn from metadata-schema.md lines 19/23/131 (key must equal name) and 45/132 (each maintainer needs email or url). Pass only if both are named with the offending field.
