# EWCCLI Official Links

Use this reference when an EWCCLI or EWC answer needs official links. Only use links listed here or links verified from an official EWC source for the current task. Do not construct Confluence, portal, Horizon, OpenStack, or service URLs from memory or guessed page titles.

These links are a lookup aid, not proof a page still exists. Quote a listed link as is; do not fetch it unless the user asks. If a needed page is not listed here, give the Knowledge Base root (https://confluence.ecmwf.int/display/EWCLOUDKB) and tell the user to search there. Do not construct new URLs.

## Link Policy

When the user asks about an EWC service outside the validated `ewccli` command surface:

1. If a relevant official link is listed below, provide the link and clearly separate it from `ewccli` command guidance.
2. If no relevant official link is listed, ask the user for the official article or ask whether to look up current official EWC documentation.
3. Do not invent commands, UI paths, service endpoints, dashboard routes, or support processes.
4. If a listed page is outside the validated `ewc` command surface, say so explicitly before linking it.

## Core Links

| Topic | Official link | Use when |
| --- | --- | --- |
| European Weather Cloud website | https://www.europeanweather.cloud/ | General EWC entry point |
| European Weather Cloud Knowledge Base | https://confluence.ecmwf.int/display/EWCLOUDKB | Knowledge Base root |
| EWC Support Portal | https://support.europeanweather.cloud/ | Use only when the workflow is grounded in official docs or the user asks for support |
| OpenStack application credentials | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+OpenStack+API+access+-+How+to+request+Openstack+Application+Credentials | Requesting OpenStack application credentials for EWCCLI authentication |
| EWC Virtual Images Available | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Virtual+Images+Available | Choosing exact values from the `EWC Virtual Image name` table column |
| EWC DNS | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+DNS | DNS naming behavior for EWC machines, DNS records, or DNS questions outside `ewccli` |

## Quick Topic Routing

| User asks about | Start with |
| --- | --- |
| Access, onboarding, login, IAM, roles, permissions | EWC Getting Access, EWC Services Login, or EWC Identity and Access Management (IAM) Service |
| Application credentials, OpenStack CLI, Terraform/OpenTofu | EWC OpenStack API access pages |
| VM images, image names, OpenStack images | EWC Virtual Images Available |
| VM plans, flavours, flavors, instance sizes, GPU plans, HPC plans | EWC VM plans plus the ECMWF/EUMETSAT federee-specific VM plans pages |
| VMs, plans/flavors, GPUs, DNS, security, SSH, Morpheus legacy UI | EWC Cloud Management pages |
| Community Hub items, ewccli deployment, contributions | EWC Community Hub pages |
| MARS, CDS/ADS, EUMETCast, EUMETSAT buckets, Data Tailor | EWC Data access pages |
| Object storage, S3 buckets, NFS/shared storage | EWC Storage pages |
| Managed Kubernetes | EWC K8S pages, choosing ECMWF or EUMETSAT side as appropriate |
| Tenancy administration | EWC Tenancy management pages |
| Unsupported `ewc` command request | Say it is outside validated `ewccli` support, then link the relevant official article if listed |

## Unsupported Command Boundary

`ewccli 0.10.0` registers only `login`, `version`, `hub`, and `infra`. If the user asks for DNS, S3, Kubernetes, IAM, Morpheus, or another EWC workflow that is not exposed by the validated `ewc` command surface, provide the relevant official KB link from this file, or ask to look up current official documentation if no link is listed. Do not expose internal anti-hallucination policy wording in the answer.

## Section Root Pages

Use these as starting points for deeper topics. Do not construct subpages under them from memory; browse from the root or ask the user for the specific article.

| Section | Official link |
| --- | --- |
| European Weather Cloud Knowledge Base | https://confluence.ecmwf.int/display/EWCLOUDKB/European+Weather+Cloud+Knowledge+Base |
| EWC Getting Started | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Getting+Started |
| EWC Getting Access | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Getting+Access |
| EWC Services Login | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Services+Login |
| EWC Identity and Access Management (IAM) Service | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Identity+and+Access+Management+%28IAM%29+Service |
| EWC Cloud Management | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Cloud+Management |
| EWC Community Hub | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Community+Hub |
| EWC Data access | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Data+access |
| EWC Storage | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Storage |
| EWC K8S | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+K8S |
| EWC VM plans | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+VM+plans |
| ECMWF - VM plans and flavors | https://confluence.ecmwf.int/display/EWCLOUDKB/ECMWF+-+VM+plans+and+flavors |
| EUMETSAT - VM plans and flavors | https://confluence.ecmwf.int/display/EWCLOUDKB/EUMETSAT+-+VM+plans+and+flavors |
| EWC Tenancy management | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Tenancy+management |
| EWC Service Status page | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Service+Status+page |
| EWC Service Definition | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Service+Definition |
| EWC Publications | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Publications |
| EWC Acknowledgement and Reference | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Acknowledgement+and+Reference |
| EWC Discussion Platform | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Discussion+Platform |
| EWC Training and Tutorials | https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+Training+and+Tutorials |
| How-to articles | https://confluence.ecmwf.int/display/EWCLOUDKB/How-to+articles |
| Troubleshooting articles | https://confluence.ecmwf.int/display/EWCLOUDKB/Troubleshooting+articles |
| Terms and Conditions for the Use of European Weather Cloud Operational Service | https://confluence.ecmwf.int/display/EWCLOUDKB/Terms+and+Conditions+for+the+Use+of+European+Weather+Cloud+Operational+Service |
