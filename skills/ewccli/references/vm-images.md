# EWC Virtual Images

Use this reference when users ask which image name to use with `ewc infra create --image-name`, or when explaining EWC virtual images in a getting-started answer.

Official page: https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Virtual+Images+Available

This snapshot is based on the official page last modified on 2025-12-09 and checked on 2026-04-29.

## Response Rules

1. Do not invent image names.
2. Distinguish the table columns:
   - Layout names such as `rocky-9-generic` are not the official EWC Virtual Image name.
   - Use the `EWC Virtual Image name` column when giving exact image names.
3. Distinguish exact official image names from `ewccli` short selectors. `ewccli 0.10.0` can normalize short selectors such as `Rocky-9`, `Ubuntu-22.04`, `Ubuntu-24.04`, and some GPU selectors to the latest matching OpenStack image, but these short selectors are not the dated official image names in the KB table.
4. In getting-started answers, avoid hard-coding a dated image name unless the user asks for a concrete current example. Link to the official page and say to use a current value from the `EWC Virtual Image name` column.
5. Recheck the official page before treating image names as current; image names are time-versioned and can change.

## Current Official EWC Virtual Image Names

From the latest table, "Latest version - December 2025":

| Instance type | Layout | EWC Virtual Image name |
| --- | --- | --- |
| Rocky 8.10 | `rocky-8-generic` / `rocky-8-ecmwf-data` | `Rocky-8.10-20251107135124` |
| Rocky 9.6 | `rocky-9-generic` / `rocky-9-ecmwf-data` | `Rocky-9.6-20251107141503` |
| Rocky GPU 9.6 | `rocky-9-gpu` | `Rocky-9.6-GPU-20251107150148` |
| Ubuntu 22.04 | `ubuntu-22.04-generic` / `ubuntu-22.04-ecmwf-data` | `Ubuntu-22.04-20251007115800` |
| Ubuntu GPU | `ubuntu-22.04-eumetsat-gpu` | `Ubuntu 22.04 NVIDIA_AI` |
| Ubuntu 24.04 | `ubuntu-24.04-generic` / `ubuntu-24.04-ecmwf-data` | `Ubuntu-24.04-20251007115108` |

## EWCCLI Image Selectors

The inspected `ewccli 0.10.0` source uses `Rocky-9` as the default CPU image selector. This is an `ewccli` selector/prefix, not the official dated image name in the KB table.

When users need exact OpenStack image names, send them to the official image page or use values from the `EWC Virtual Image name` column. When users need an `ewccli` command and accept automatic latest-image resolution, explain that `ewccli` can use a supported selector.

Safe command pattern with a placeholder:

```bash
ewc infra --profile <profile-name> create <server-name> \
  --image-name <ewc-virtual-image-name-or-supported-ewccli-selector> \
  --flavour-name <flavour-name>
```

Safe wording:

```text
Use the official EWC Virtual Images page and copy from the `EWC Virtual Image name` column. Do not use the layout label as the image name. `Rocky-9` is an ewccli short selector/default, not a dated official EWC Virtual Image name.
```
