# Submit A New Community Hub Item

## Prompt

I want to add an item to the EWC Community Hub, what should I do?

## Expected Agent Behavior

- Use the `ewc-community-hub` skill and load `submission.md`.
- Explain the path first: fork, branch, `items.yaml` entry, local Docker validation, pull request, maintainer review.
- State the prerequisites: EWC access, a publicly accessible versioned source, a GitHub account, Docker for local validation.
- Ask for item details only after the path is explained, and only when the user wants a draft.
- Give official links only from `official-links.md`. Do not invent repository, schema, or onboarding URLs.
- Do not promise acceptance or publication. Submission ends at the pull request.
- Hand `ewc hub list/show/deploy` requests to the `ewccli` skill.

## Expected Response Shape

- Workflow type: submission.
- Prerequisites: EWC access, public versioned source, GitHub account, Docker.
- Metadata or diff: none yet, the user has not provided item details.
- Validation status: schema validation Not run; policy review not applicable yet.
- Next step: ask whether the user wants a draft, then collect item details.
