# Validate A Pasted Entry

## Prompt

Is this items.yaml entry valid and can I submit it?

```yaml
apiVersion: communityhub.europeanweather.cloud/v1alpha1
kind: CommunityHubCatalog
spec:
  items:
    <item-key>:
      name: "<different-item-name>"
      maintainers:
        - name: <maintainer-name>
      annotations:
        others: "Deployable,EWCCLI-compatible"
      # remaining fields omitted in this example
```

## Expected Agent Behavior

- Use the `ewc-community-hub` skill and load `metadata-schema.md` and `submission.md`.
- Report two statuses and keep them apart.
  - Schema validation: `Not run`. Do not certify validity by reading, and do not quote validator output that was not produced.
  - Policy review: the `spec.items` key does not equal `name`, and the maintainer has neither `email` nor `url`.
- Do not present the policy findings as schema errors, and do not invent an error count.
- Return only the fields to change. Do not return a complete corrected file with filled-in unknowns, and ask the user for the maintainer contact.
- Propose the Docker validator command from `submission.md`.
- Because the item is tagged `EWCCLI-compatible`, also propose the custom-catalogue dry-run, and hand the `ewc hub` commands to the `ewccli` skill.
- Do not say the item is accepted or published.

## Expected Response Shape

- Workflow type: validation.
- Prerequisites: Docker for the validator, EWC access and a GitHub account for the pull request.
- Metadata or diff: the key/name pair to align and the maintainer contact to add.
- Validation status: schema validation Not run; policy review with the two findings.
- Next step: run the Docker validator, run the custom-catalogue dry-run, then open the pull request.
