# Draft An Entry Without A Maintainer Contact

## Prompt

Draft the items.yaml entry for my Ansible item `<repo-URL>`. It is called `<item-name>` and it `<one-line purpose>`.

## Expected Agent Behavior

- Use the `ewc-community-hub` skill and load `metadata-schema.md`.
- Notice that no maintainer contact and no category were given.
- Ask the user for a maintainer `email` or `url`, and for the category. Do not guess either.
- Do not draft a placeholder contact such as `maintainer@example.com`, and do not leave a made-up category in the entry.
- Use the item name as both the `spec.items` key and the `name` value.
- Take allowed values (technology, license type, support level) from `metadata-schema.md`, or ask.
- State which `values.inputSpec` inputs are mandatory (no `default`) once inputs are known.

## Expected Response Shape

- Workflow type: metadata drafting.
- Prerequisites: public versioned source with a `LICENSE`, EWC access, GitHub account, Docker.
- Metadata or diff: the fields that can be filled from the user's details, with the contact and category left out and asked for.
- Validation status: schema validation Not run; policy review lists the missing maintainer contact.
- Next step: answer the questions, then run the local validator and open the pull request.
