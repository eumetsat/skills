# AGENTS.md - Contributor and Agent Guide

**For end users:** see [README.md](README.md) for installation and usage.

**This file** is for contributors, maintainers, and coding agents updating this repository. `CLAUDE.md` points to this file so Claude Code reads the same guidance without a second source of truth.

## What This Is

This repository contains portable EUMETSAT agent skills, currently: `eumdac` for data access, `ewccli` for European Weather Cloud operations, `firecube` for ingestion and plugin development, `esf-satellite-data` for selecting feature-based satellite datasets, `feature-db-client` for querying and saving feature records, and `ml-menu-cdr` for choosing climate data records on the Data Store. `esf-satellite-data` and `feature-db-client` require access to separately operated services.

Think of this repo as:

- Version-controlled operational knowledge for EUMETSAT tools.
- A vendor-agnostic skill source for Codex, Claude Code, OpenCode, and compatible agents.
- A progressive-disclosure documentation set where `SKILL.md` stays concise and references/examples carry the detail.

## Repository Structure

```text
eumetsat-skills/
├── skills/{eumdac,ewccli,firecube,esf-satellite-data,feature-db-client,ml-menu-cdr}/
│   ├── SKILL.md
│   ├── agents/openai.yaml
│   └── references/
├── skills/firecube/scripts/     # Helper scripts, see their own README
├── examples/<skill>/            # Sanitized scenarios
├── docs/                        # Installation, prompts, references, validation
├── evals/<skill>/<mechanism>/   # Focused behavior cases
├── .claude-plugin/               # Claude Code plugin manifest
├── skills-bench.yaml
├── README.md
├── AUTHORS.md
├── LICENSE
├── AGENTS.md
└── CLAUDE.md -> AGENTS.md
```

## File Roles

| Path | Audience | Purpose |
| --- | --- | --- |
| `skills/*/SKILL.md` | Agents | Core activation, routing, safety rules, and concise workflow guidance |
| `skills/*/references/*.md` | Agents | Topic-specific details loaded only when needed |
| `examples/*/*.md` | Contributors and agents | Regression prompts and quickstart scenarios |
| `docs/installation.md` | End users | Agent-specific installation instructions |
| `docs/quickstart-prompts.md` | End users | Prompt examples by skill |
| `docs/validation.md` | Contributors and CI | Validation commands and new-skill shape rules |
| `docs/external-references.md` | End users and contributors | Official documentation and package links |
| `docs/skill-reference-boundaries.md` | Contributors and agents | Reference-file ownership and split guidance by skill |
| `skills-bench.yaml` | Contributors and CI | Conventions checked by `skills-bench validate` (required skills, references, CLI surfaces, budgets) |
| `evals/` | Contributors | Behaviour eval cases run by `skills-bench eval` |
| `README.md` | End users | Project overview and navigation |
| `AGENTS.md` | Contributors and agents | Maintenance rules for this repository |
| `CLAUDE.md` | Claude Code | Compatibility alias for `AGENTS.md` |

## Skill Architecture

Keep canonical skills under:

```text
skills/<skill-name>/SKILL.md
```

Markdown documentation uses the repository LICENSE and does not need a license header. Preserve license headers in code and configuration files, and keep adjacent `.ABOUT` files for headerless assets. Keep skill frontmatter first. Never expose local evidence or credentials in distributed content.

Keep local QA environments, dependency snapshots, and scanner reports ignored. The README SBOM tables must account for imports and commands in distributed scripts, with dependency name, reviewed version, license, copyright, home URL, and comments. Keep runtime and build/edit/test dependencies separate; tools used only to review this repository are not distributed-script dependencies. Document helper prerequisites alongside the scripts.

Do not duplicate skill sources into agent-specific directories inside this repository. Installation docs lead with the one-command install from the public repository (marketplace for Claude Code and Codex, the skills CLI for the rest), then give `git clone` plus symlinks as the manual path for every agent.

Keep `SKILL.md` portable. The frontmatter uses only the fields of the [Agent Skills specification](https://agentskills.io/specification), which every compliant client accepts:

```yaml
---
name: <skill-name>
description: Explain what the skill does and when agents should use it.
license: CC-BY-4.0
compatibility: Tool versions, credentials and network access the skill needs (at most 500 characters).
metadata:
  author: EUMETSAT
  version: "<release version, the same as .claude-plugin/plugin.json>"
---
```

`name` and `description` are required; the other three travel with a skill that is copied on its own. Bump every
skill's `metadata.version` together with the plugin version at release time. Do not add Claude-only, Codex-only, or
OpenCode-only fields to the canonical skill.

## Content Rules

- Keep `SKILL.md` focused on activation, routing, safety, and core workflows.
- Put detailed commands, option matrices, and Python examples in `references/`.
- Put realistic prompt scenarios and expected response shape in `examples/`.
- Prefer concise tables and concrete commands over long prose.
- Mark version-specific CLI behavior when installed tools differ from older documentation.
- Never commit real credentials, bearer tokens, subscription passwords, private account details, or local user paths.

## Reference Boundaries

Use [docs/skill-reference-boundaries.md](docs/skill-reference-boundaries.md) when adding, renaming, splitting, or reviewing reference files.

If a reference grows large or mixes concerns, split it into a new reference and link it from the relevant `SKILL.md`.

## Example Rules

Examples are sanitized regression artifacts, not live-current data claims.

When adding examples:

- Use placeholders for credentials and user-specific paths.
- Preserve the user intent, key collection IDs, command pattern, safety checks, and expected agent behavior.
- Say when dates, product IDs, counts, or file sizes are observed examples rather than current results.
- Prefer one scenario per file under `examples/<skill-name>/`.

## Validation

Run validation before handing off changes (see [docs/validation.md](docs/validation.md)):

```bash
skills-bench validate . --strict
```

The rules live in `skills-bench.yaml`: required skills, portable frontmatter (the specification's five fields),
expected reference files per skill, installed-CLI command groups (`eumdac`, `ewc`, `firecube` resolved on `PATH`,
each skipped when absent), and size budgets. Add a new skill's reference files and CLI surface there when
you add the skill.

Behaviour changes to a skill get an eval case under `evals/<skill>/<mechanism>/`. End-to-end benchmarks with a
scripted operator are not kept in this repository, which users install.

Eval discipline:

- Write at least three eval cases for a new skill or behaviour before writing the skill text, and run them without the
  skill first so the baseline failure is on record.
- Run the cases with and without the skill on a small, a mid-size and a large model (for example Haiku, Sonnet and
  Opus): a rule that holds on one model can be ignored by another.
- Include at least one case phrased the way a user would ask ("Get snow products from the Data Store"), not only cases
  that name the command.
- Show a grader failing on the bad behaviour before trusting it, and read a sample of failing runs: a grader that
  matches a word in a path, or a judge rubric with a clause that does not apply, fails correct answers.
- Report eval results (cases, models, runs, score, cost) in the merge request description, never in the README or the
  skill.

## Writing Style

- Use imperative guidance: "Run", "Check", "Do not overwrite".
- Prefer "When to use" and "Route by intent" sections for agent decision-making.
- Include safe command templates with placeholders.
- Make destructive or expensive actions explicit: overwriting credentials/profiles, deleting subscriptions or infrastructure, submitting orders, deploying cloud resources, large downloads, and long-running livefeed/subscription downloads.
- Keep agent-facing docs vendor-agnostic unless a file is explicitly about one agent.

## When To Update

Update the skill when:

- EUMDAC adds, renames, or removes CLI commands/options.
- EUMDAC releases a newer verified version than the pinned 3.1.1; update the pin once the new release is verified.
- EUMETSAT changes authentication, Data Store, Data Tailor, subscription, or livefeed workflows.
- EWCCLI adds, renames, registers, or removes CLI commands/options.
- European Weather Cloud changes login/profile, Community Hub, OpenStack credential, infrastructure, or custom catalogue workflows.
- Firecube releases a new PyPI version that adds, renames, or removes CLI commands/options, plugin templates, or hooks.
- ESF MCP or Feature Database client contracts and access requirements change.
- EUMETSAT adds, ends or renames climate data record collections, filename prefixes or variables.
- Real prompt/response tests reveal missing guidance or unsafe defaults.
- Examples expose recurring user intents that should be covered by routing or references.

Do not update for:

- Personal style preferences without a recurring agent behavior problem.
- One-off product searches that do not generalize.
- Current search results that will become stale unless they are clearly marked as examples.

## Compatibility Alias Policy

Use a single canonical contributor guide:

```bash
AGENTS.md
```

`CLAUDE.md` should remain a compatibility alias to `AGENTS.md`, not a separate maintained document. If a packaging target cannot preserve aliases, dereference at package-build time rather than committing duplicate source files.
