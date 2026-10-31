# Item Metadata Schema (`items.yaml`)

Use this reference when drafting or reviewing an item entry for the EWC
Community Hub catalog. The catalog is a single file, `items.yaml`, in
[`ewcloud/ewc-community-hub`](https://github.com/ewcloud/ewc-community-hub).

Authoritative field reference (generated from the JSON schema):
<https://github.com/ewcloud/ewc-community-hub/blob/main/docs/schema-reference/items/v1alpha1.md>

## Document envelope

All three top-level keys are required; values are fixed constants:

```yaml
apiVersion: communityhub.europeanweather.cloud/v1alpha1
kind: CommunityHubCatalog
spec:
  items:
    my-item:        # key MUST equal the item's `name` attribute
      ...
```

> ⛔ The map key under `spec.items` **must always equal** the item's `name`
> attribute — this enforces entry uniqueness.

The schema forbids additional properties anywhere: unknown or misspelled fields
fail validation.

## Item fields

**Required:**

| Field | Notes |
| --- | --- |
| `name` | Unique id, must equal the `spec.items` key (e.g. `my-item`). |
| `displayName` | Human-friendly name; may contain spaces/capital letters. |
| `description` | Full multi-line description for the detail page. |
| `summary` | One-line summary shown on the catalog card. |
| `version` | `MAJOR.MINOR` or `MAJOR.MINOR.PATCH` (e.g. `"0.0.1"`). |
| `published` | `true` to make it visible in the Hub. |
| `home` | HTTPS URL of the item's home page (usually the repo). |
| `license` | HTTPS URL to the license file in the repo. |
| `icon` | HTTPS URL to an image used as the Hub icon. |
| `sources` | List of Git repo URLs; first entry is the primary source, extra entries are mirrors. |
| `maintainers` | List of `{name, email?, url?}`. **At least one of `email` or `url` must be set** per maintainer. |
| `annotations` | Object, see below. |

**`annotations` (classification):**

| Field | Required | Values / notes |
| --- | --- | --- |
| `category` | ✅ | Catalog category for browsing/filtering, e.g. `Compute`, `Dataset`. |
| `technology` | ✅ | Deployment technology, e.g. `Ansible Playbook`, `Terraform Module`. |
| `licenseType` | ✅ | SPDX **full name**, e.g. `Apache License 2.0`, `MIT License`. |
| `supportLevel` | ✅ | `EWC` (supported by the EWC team) or `Community` (best-effort by maintainers). |
| `others` | optional | Comma-separated free-form tags, e.g. `Deployable,EWCCLI-compatible`. |

**`values` (deployment config — optional object; supersedes deprecated
`ewccli` sub-attributes):**

| Field | Notes |
| --- | --- |
| `inputSpec` | Inputs users can set at deploy time. Each entry: `name` (✅), `description` (✅), `type` (✅, short type name like `str`), `default` (optional — **presence makes the input optional, absence makes it mandatory**). |
| `outputSpec` | Outputs produced after deploy: `name`, `description`, `type`. |
| `pathToMainFile` | Path (relative to sources root) of the main file to run, e.g. `playbooks/my_item.yml`. If unset, EWCCLI asks the user. |
| `pathToRequirementsFile` | Path of the dependency file to install first, e.g. `requirements.yml`. |
| `osImageName` | OpenStack image, e.g. `Ubuntu-24.04-20260519071420`. See [official-links.md](official-links.md) for the EWC Images page. |
| `osFlavorName` | OpenStack flavor (VM size), e.g. `eo1.medium`. See [official-links.md](official-links.md) for the EWC VM plans page. |
| `osSecurityGroups` | List of OpenStack security group names attached to the server. |
| `ansibleUser` | OS default user Ansible impersonates over SSH, e.g. `ubuntu`. |
| `ansibleVersion` | Ansible version required, e.g. `11.0.0`. |
| `pythonVersion` | Python version required by the deployment tooling, e.g. `3.12`. |

**`ewccli` (optional object):**

- `externalIP` (bool) — assign a public IP to the server.
- `checkDNS` (bool) — EWCCLI checks the server's DNS record around deploy.
- ⛔️ **Deprecated** (use `values.*` instead): `pathToMainFile`,
  `pathToRequirementsFile`, `defaultImageName`, `defaultSecurityGroups`,
  `inputs`.

## Minimal complete example

```yaml
apiVersion: communityhub.europeanweather.cloud/v1alpha1
kind: CommunityHubCatalog
spec:
  items:
    my-item:
      name: "my-item"                 # MUST match the key above
      displayName: My Item
      summary: My 1st EWC Community Hub Item
      description: |
        My first ever Item contributed to
        the EWC Community Hub.
      version: "0.0.1"
      published: true
      home: https://my-public-git-server.com/my-repo
      license: https://my-public-git-server.com/my-repo/blob/main/LICENSE
      icon: https://raw.my-public-git-server.com/my-repo/refs/heads/main/icon.png
      sources:
        - https://my-public-git-server.com/my-repo.git
      maintainers:
        - name: my name or my organization
          email: name@organization.com
          url: https://my-public-git-server.com/my-repo/issues
      annotations:
        category: "Compute"
        technology: "Ansible Playbook"
        licenseType: "MIT License"
        supportLevel: "Community"
        others: "Deployable,EWCCLI-compatible"
      ewccli:
        externalIP: false
      values:
        inputSpec:
          - name: my_required_input
            description: "My required input."
            type: str
          - name: my_optional_input
            description: "Optional because it has a default."
            type: str
            default: "my default value"
        osImageName: Ubuntu-24.04-20260519071420
        pathToRequirementsFile: requirements.yml
        pathToMainFile: playbooks/my_item.yml
```

## Common pitfalls

- **Key ≠ `name`**: `spec.items.my-item` key and `name: my-item` must match.
- **Missing maintainer contact**: each maintainer needs `email` or `url`.
- **Wrong `supportLevel`**: only `EWC` or `Community`.
- **`licenseType` must be the SPDX full name**, not a short identifier or URL.
- **`home`/`icon`/`license`/`sources` must be HTTPS** and match
  `^https://[\w\-\./:#?=&%]+$`.
- **Required vs optional inputs**: in `values.inputSpec`, an entry with
  `default` is optional; without `default` it is mandatory — EWCCLI refuses to
  deploy when a mandatory input is missing.
- **Deprecated `ewccli` attributes**: prefer `values.*`; only `externalIP` and
  `checkDNS` are current under `ewccli`.
- **Version format**: `MAJOR.MINOR` or `MAJOR.MINOR.PATCH` only.
- **No additional properties**: typos fail validation.