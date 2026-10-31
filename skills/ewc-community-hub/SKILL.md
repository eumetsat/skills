---
name: ewc-community-hub
description: Use when submitting, creating, editing, or validating an item in the EWC Community Hub catalog (ewcloud/ewc-community-hub) — drafting items.yaml metadata, annotations, values/inputSpec, opening a catalog pull request, or running the metadata schema validator.
license: CC-BY-4.0
compatibility: items.yaml schema communityhub.europeanweather.cloud/v1alpha1; local validation needs Docker; PRs need a GitHub account and EWC access.
metadata:
  author: EUMETSAT
  version: "0.1.0"
---

# EWC Community Hub

Use this skill to onboard items into the EWC Community Hub catalog: preparing
the contribution, writing the item's metadata entry in `items.yaml`, validating
it against the schema, and opening the pull request that publishes it. It does
not cover deploying or operating Hub items — hand those requests to the
`ewccli` skill (`ewc hub list/show/deploy`).

Grounded in the `ewcloud/ewc-community-hub` `main` branch and its generated
schema reference inspected on 2026-10-31. The schema is versioned
(`communityhub.europeanweather.cloud/v1alpha1`); if validation fails with
unexpected errors, re-fetch the schema reference before assuming the skill is
wrong.

## Operating Rules

1. Only EWC users can contribute. If eligibility is in question, point to the
   access page from [official-links.md](references/official-links.md) instead
   of promising acceptance.
2. Never invent metadata values: SPDX license names, categories, technologies,
   image names, flavors, URLs, or maintainer contacts. Use
   [metadata-schema.md](references/metadata-schema.md) for allowed values and
   [official-links.md](references/official-links.md) for official pages;
   otherwise ask the user.
3. The `spec.items` key must equal the item's `name`. Always check this pair
   when drafting or reviewing an entry.
4. Every maintainer entry needs at least `email` or `url`; flag the omission
   rather than fabricating a contact.
5. In `values.inputSpec`, an entry with `default` is optional and without it
   is mandatory — state which inputs the user must collect before submission.
6. Prefer `values.*` over deprecated `ewccli` attributes; only `externalIP`
   and `checkDNS` remain current under `ewccli`.
7. Never claim an item is accepted or published: submission ends at the pull
   request; maintainers review it, and outside-org PRs need manual approval
   before CI runs.
8. Recommend local Docker validation before opening a PR, and quote its exact
   output (`/tmp/items.yaml valid`) as the validation status.
9. If the item is tagged `EWCCLI-compatible`, also recommend the custom
   catalogue dry-run from [submission.md](references/submission.md) — schema
   validation alone does not exercise the `ewccli` block. Hand the actual
   `ewc hub ...` commands to the `ewccli` skill.

## Response Contract

When the answer drafts or reviews metadata or proposes submission steps,
include:

1. **Workflow type**: metadata drafting, validation, or submission.
2. **Prerequisites**: EWC access, public source repo with `LICENSE`, GitHub
   account, Docker (for local validation).
3. **Metadata or diff**: the YAML entry (or the exact fields to change),
   following [metadata-schema.md](references/metadata-schema.md).
4. **Validation status**: what was validated locally, what was not, and why.
5. **Next step**: local validator command, then the PR.

For short factual questions about fields or links, answer directly without the
template.

## Workflow

1. Capture context: item name, technology (Ansible/Terraform/other), source
   repo URL, license, maintainers, and whether the entry is new or an edit.
2. Route by intent using the table below; load only the matching reference.
3. Draft or review the `items.yaml` entry against
   [metadata-schema.md](references/metadata-schema.md).
4. Give the local validation commands from
   [submission.md](references/submission.md) — including the custom-catalogue
   dry-run when the item is `EWCCLI-compatible`.
5. Emit the Response Contract when proposing metadata or submission steps.

## Routing Table

| User wants to | Load |
| --- | --- |
| Draft or review item metadata: fields, annotations, values, inputSpec, examples | [metadata-schema.md](references/metadata-schema.md) |
| Submit an item: workflow, PR, local Docker validation, review expectations | [submission.md](references/submission.md) |
| Official links: repo, schema reference, onboarding guide, images, VM plans | [official-links.md](references/official-links.md) |
| Deploy or operate a Hub item (`ewc hub ...`) | Hand off to the `ewccli` skill |

## When To Use This Skill

Activate when:

- Creating or editing an entry in the Community Hub `items.yaml` catalog.
- Explaining item metadata fields, annotations, `values`, or `inputSpec`.
- Validating catalog metadata locally or diagnosing schema validation errors.
- Opening or debugging a pull request against `ewcloud/ewc-community-hub`.
- Answering who can contribute, support levels, or the publication process.