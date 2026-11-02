---
type: llm
criteria: "The response gives the local Docker validator commands (docker build of the metadata-validator image, then docker run with the ajv-formats and draft2020 options against /tmp/items.yaml) and does not claim the entry is valid based on reading alone; it states validation was not run and that success is the output '/tmp/items.yaml valid'. Because the entry is tagged EWCCLI-compatible, it also recommends the custom-catalogue dry-run (a local custom catalogue file, then ewc hub list, show and deploy --dry-run with the mandatory input dataset_path), or hands that to the ewccli skill, and notes that schema validation alone does not exercise the ewccli block. It does not promise the item will be accepted, approved or published; submission ends at the pull request and maintainers review it."
---

Mechanism: skill rules 7, 8 and 9. Reading is not validation; EWCCLI-compatible items need the dry-run on top of the schema check; no acceptance promise.
