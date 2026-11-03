---
name: ewccli
description: Use when working with ewccli, the European Weather Cloud command line interface, for EWC setup, login profiles, OpenStack application credentials, Community Hub item discovery/deployment, infrastructure commands, custom catalogues, or CLI troubleshooting.
license: CC-BY-4.0
compatibility: ewccli 0.10.0 on Python 3.10-3.14 and a European Weather Cloud account; live commands need network access to the EWC and OpenStack endpoints.
metadata:
  author: EUMETSAT
  version: "0.1.0"
---

# EWCCLI

Use this skill for European Weather Cloud (EWC) CLI workflows: installing `ewccli`, validating the `ewc` command, preparing login profiles, handling OpenStack application credentials safely, listing/showing/deploying Community Hub items, using infrastructure commands, testing custom catalogues, or troubleshooting `ewc` errors.

This skill is grounded in `ewccli 0.10.0` (released 2026-10-22) and the upstream `ewcloud/ewccli` source inspected on 2026-11-03. Install that exact version (`ewccli==0.10.0`); a newer release may change the registered command surface, so revalidate this skill before recommending one. Prefer installed `ewc --help` output and official EWC upstream docs when exact flags, item metadata, or service behavior matter.

## Operating Rules

1. Never print, commit, or log OpenStack application credential IDs, application credential secrets, private SSH keys, encoded SSH key material, tokens, cloud account details, or private profile files.
2. Read-only commands (`ewc version`, `ewc --help`, `ewc hub list`, `ewc hub show`, `ewc infra list`, `ewc infra show`) are safe to run without confirmation when the user asks for a check. They still need a working profile or catalogue source.
3. State-changing commands (`ewc login`, `ewc hub deploy`, `ewc infra create`, `ewc infra delete`) require explicit user confirmation before execution. Confirm target federee, profile, tenant, item/server name, and dry-run expectations first, and prefer `--dry-run` where supported.
4. Do not overwrite or delete profiles in `$HOME/.ewccli/profiles`, SSH keys under `$HOME/.ewccli/.ssh`, OpenStack `clouds.yaml`, or generated deployment outputs unless the user explicitly requests it.
5. Never invent EWC-specific values: tenant names, portal or Horizon URLs, OpenStack CLI alternatives, DNS commands, service paths, or support processes. Use [official-links.md](references/official-links.md) for links and [auth-profiles.md](references/auth-profiles.md) for the tenant-name convention and the credential-request process; otherwise ask the user.
6. `ewc login` consumes an existing credential source (`clouds.yaml`, sourced `openrc`, environment variables, or its interactive prompt) and writes only the `ewccli` profile. It does not create or configure `clouds.yaml` or `openrc`. See [auth-profiles.md](references/auth-profiles.md).
7. If credentials are missing, provide commands with placeholders or explain the interactive prompt path instead of inventing values.
8. For exact command flags, run `ewc --help` or `ewc <group> --help` locally before finalizing examples. Some `ewc infra <command> --help` calls initialize profile/OpenStack configuration, so treat them as configured-environment checks.
9. Locate the CLI with `command -v ewc` before anything else. Never assume a project `.venv`, a personal virtualenv directory, or a repository-specific path; install per [install.md](references/install.md) into standard user-tool locations or an environment the user names.
10. For `ewc infra`, place `--profile <profile-name>` immediately after `infra`, before the subcommand.
11. Since `0.10.0`, every server boots from a volume (default root volume 50 GB, sized with `--root-volume`). Treat the root volume as part of the server's configuration when comparing or redeploying.

## Response Contract

When the answer proposes commands, configuration, or execution, include:

1. **Workflow type**: install, login/profile, Hub, infrastructure, custom catalogue, or troubleshooting.
2. **Prerequisites**: Python version, `ewccli` install status, credentials/profile status, network access, and whether live EWC/OpenStack services are required.
3. **Credential safety**: placeholders for secrets and no profile/key/credential echoing.
4. **Command or config**: minimal examples verified against installed help/source, or clearly marked as illustrative.
5. **Validation status**: what was run locally, what was not run, and why.

For short factual questions, answer directly without the template.

## Workflow

1. Capture execution context: operating system, shell, Python version, `ewccli` version, install method, profile name, federee, tenant, and target service.
2. Route by user intent using the table below, not by the first matching keyword. Load only the matching references; if the first one is too narrow, return to the table.
3. Inspect local help before giving exact flags or environment variable names.
4. Propose the minimal safe command/config using placeholders for credentials and user-specific names.
5. Validate with read-only checks when possible. Do not claim live validation unless EWC/OpenStack calls were actually run.
6. Emit the Response Contract when commands or configuration are proposed.

## When To Use This Skill

Activate when:

- Installing or verifying the pinned release of `ewccli` or the `ewc` command.
- Running or explaining `ewc login`, profiles, federees, tenant names, SSH keys, OpenStack application credentials, or `clouds.yaml` precedence.
- Listing, showing, or deploying EWC Community Hub items with `ewc hub`.
- Creating, listing, showing, or deleting EWC/OpenStack servers with `ewc infra`.
- Choosing EWC virtual images for infrastructure, distinguishing `ewccli` short selectors from official EWC Virtual Image names.
- Answering VM plan/flavour questions for EWC infrastructure, using federee-specific official KB pages rather than generic size categories.
- Creating or testing custom EWC Hub catalogues with `--path-to-catalog`.
- Troubleshooting `ewccli` errors, profile lookup, credential precedence, SSH key checks, item inputs, custom catalogue validation, or deployment failures.

Do not use for:

- EUMETSAT Data Store/Data Tailor workflows; use the `eumdac` skill instead.
- General OpenStack administration unless the user is using `ewccli` commands or EWC profiles.
- Kubernetes, S3, or DNS workflows unless they become registered `ewc` commands in the installed version.
- Scientific interpretation or analysis after infrastructure is deployed, unless the task needs EWC CLI behavior.

## Reasoning Traps

| Observed | Tempting conclusion | Check first |
| --- | --- | --- |
| User asks for their tenant name | Offer a plausible example, or read it from `openrc` or `clouds.yaml` | Give only the `<memberstate>-<organization>-<projectname>` convention and EWC Support |
| `ewc login` succeeded | It configured `clouds.yaml` or `openrc` | It reads credential sources and writes only the `ewccli` profile |
| `ewc hub list` works | Credentials are valid | Catalogue discovery works unauthenticated; `ewc infra --profile <name> list` is the live check |
| Request outside `login`, `version`, `hub`, `infra` | Suggest a Horizon URL, OpenStack command, or support process | State the boundary; link only what official-links.md lists |
| Image name needed | Use `Rocky-9` as the official name | That is an `ewccli` short selector; official names come from the EWC Virtual Images page |
| A rule applies | Explain the rule to the user | Apply it; state only what is needed in one line |

## Route By Intent

| Intent or symptom | Read this reference | First checks |
| --- | --- | --- |
| Install or verify EWCCLI: `ewc` missing, Python too old, PATH warning | [install.md](references/install.md) | Python 3.10-3.14, package manager, `ewc --help` |
| Request or configure credential sources, then login: profiles, application credentials, SSH keys, precedence | [auth-profiles.md](references/auth-profiles.md) | Official credential request, received `openrc` or `clouds.yaml`, profile name, federee, tenant, SSH key paths |
| Use Community Hub items: list/show/deploy, item inputs, dry-run, force | [hub.md](references/hub.md) | Profile, catalogue source, item name, required item inputs |
| Use infrastructure commands: create/show/list/delete servers | [infra.md](references/infra.md) | Profile, server name, image/flavour/network/security settings |
| Choose or explain VM images: official names, short selectors, defaults | [vm-images.md](references/vm-images.md) | Official image table date, EWC Virtual Image name, short selector vs exact name |
| Choose or list VM plans/flavours: defaults, federee differences, GPU/HPC | [vm-plans.md](references/vm-plans.md) | Federee, default flavour, official KB modification date |
| Test custom catalogue entries: `--path-to-catalog`, item metadata, unpublished items | [custom-catalogues.md](references/custom-catalogues.md) | Catalogue file, item metadata, source path/repo, required inputs |
| Debug EWCCLI errors: sanitized errors, version drift, missing profiles, deployment failures | [troubleshooting.md](references/troubleshooting.md) | Exact command, sanitized output, installed version, profile state |
| Provide official EWC links: website, KB, support, DNS, credential requests | [official-links.md](references/official-links.md) | Confirm the link is listed or verify it from an official EWC source |

## Unsupported EWC CLI Capabilities

In `ewccli 0.10.0`, the registered commands are only `login`, `version`, `hub`, and `infra`. Check the routing table first; VM images, VM plans, login/profile, Hub, custom catalogue, troubleshooting, and official-link requests all have a route.

For requests outside those routes, use workflow type "official EWC link / unsupported ewccli workflow": state that `ewccli 0.10.0` does not provide the workflow, name the registered commands, explain the nearest validated boundary if there is one, and give the official link from [official-links.md](references/official-links.md) if one is listed. Otherwise ask the user for the official article or whether to look up current official EWC documentation. Present only the boundary and the link in the answer.

## Core CLI Surface

`ewccli 0.10.0` installs the `ewc` command and registers only `login`, `version`, `hub`, and `infra`. For exact commands, flags, and profile-option placement, see [hub.md](references/hub.md) and [infra.md](references/infra.md). Always inspect local help before using advanced options:

```bash
ewc --help
ewc version
```
