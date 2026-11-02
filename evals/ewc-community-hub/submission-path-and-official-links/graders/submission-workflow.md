---
type: llm
criteria: "The response describes the submission path: fork ewcloud/ewc-community-hub, create a branch, add the item under spec.items in items.yaml, and open a pull request. It tells the user to validate locally with the Docker (AJV) validator BEFORE opening the pull request. It says the submission ends at the pull request and that maintainers review it. It does NOT say or imply that the item will be accepted, approved, merged or published (for example 'it will appear in the Hub', 'you will be listed'); conditional wording such as 'once merged with published: true it appears' is acceptable only if review is stated as a prerequisite. It may mention that only EWC users can contribute, pointing to access rather than promising acceptance."
---

Mechanism: the skill's submission path is fork, branch, items.yaml entry, local Docker validation, then pull request, and rule 7 forbids promising acceptance or publication. Pass only if the order is right and no outcome is promised.
