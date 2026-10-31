# EWC Community Hub Official Links

Use this reference when an answer needs official links for the EWC Community
Hub or its supporting documentation. Only use links listed here or links
verified from an official EWC/GitHub source for the current task. Do not
construct Confluence, portal, or repository URLs from memory or guessed page
titles.

These links are a lookup aid, not proof a page still exists. Quote a listed
link as is; do not fetch it unless the user asks. If a needed page is not
listed here, give the Knowledge Base root
(<https://confluence.ecmwf.int/display/EWCLOUDKB>) and tell the user to search
there. Do not construct new URLs.

## Core links

| Topic | Official link | Use when |
| --- | --- | --- |
| EWC Community Hub catalog repository | https://github.com/ewcloud/ewc-community-hub | Editing `items.yaml`, schemas, CI workflows |
| Community Hub on the EWC website | https://europeanweather.cloud/community-hub | Showing the published catalog |
| Item metadata schema reference | https://github.com/ewcloud/ewc-community-hub/blob/main/docs/schema-reference/items/v1alpha1.md | Exact field requirements, types, defaults |
| Onboarding / contribution guide | https://confluence.ecmwf.int/x/wyLOIQ | Collaboration workflow, conventions, recommendations |
| Get EWC access | https://europeanweather.cloud/get-access | Checking whether the user can contribute |
| EWC Support Portal | https://support.europeanweather.cloud | Alternative contribution channel (tickets) |
| EWC Knowledge Base root | https://confluence.ecmwf.int/display/EWCLOUDKB | Any official page not listed above |
| EWC Virtual Images Available | https://confluence.ecmwf.int/spaces/EWCLOUDKB/pages/414272933/EWC+Virtual+Images+Available | Source of truth for `values.osImageName` and `values.ansibleUser` — copy image names and default users from the `EWC Virtual Image name` and user columns |
| EWC VM plans | https://confluence.ecmwf.int/x/evWHEw | Choosing `values.osFlavorName` |

## Quick topic routing

| User asks about | Start with |
| --- | --- |
| Drafting or reviewing item metadata / `items.yaml` | [metadata-schema.md](metadata-schema.md) |
| Submission workflow, PRs, local validation | [submission.md](submission.md) |
| Image names, `ansibleUser` | EWC Virtual Images Available |
| Flavors / VM sizes, `osFlavorName` | EWC VM plans |
| Access, eligibility to contribute | Get EWC access |
| Support, contribution tickets | EWC Support Portal |
| Anything else official | EWC Knowledge Base root, then search |

## Boundary

This skill covers **catalog metadata and submission only**. It does not cover
deploying or operating Hub items — that is the `ewccli` skill (`ewc hub
list/show/deploy`). Do not give `ewc` command guidance from this skill beyond
noting the hand-off.