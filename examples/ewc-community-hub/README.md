# EWC Community Hub Examples

These examples are sanitized prompt scenarios for the `ewc-community-hub` skill. They are not live-current claims about the catalogue contents, the schema version, or the review process. Values such as item names, repository URLs, and schema versions are observed examples.

Do not record GitHub tokens, EWC credentials, private repository URLs, or real maintainer contact details in examples. Use placeholders for anything user-specific.

## Scenarios

| File | Scenario | What it tests |
| --- | --- | --- |
| [submit-new-item.md](submit-new-item.md) | Answer an onboarding question | Fork/validate/PR path explained before asking details, no invented URLs |
| [draft-without-maintainer-contact.md](draft-without-maintainer-contact.md) | Draft an entry with missing details | Asks for maintainer contact and category, no placeholder values |
| [validate-pasted-entry.md](validate-pasted-entry.md) | Review a pasted `items.yaml` entry | Two statuses, schema validation not run, key/name mismatch, missing contact, Docker command, custom-catalogue dry-run |

## Safe Validation Boundary

Examples should prefer the local Docker validator and the custom-catalogue dry-run. Do not claim an item is accepted or published: submission ends at the pull request.
