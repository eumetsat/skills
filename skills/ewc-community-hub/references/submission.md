# Submitting an Item to the EWC Community Hub

Use this reference for the end-to-end onboarding workflow: preparing sources,
editing `items.yaml`, validating, and opening the pull request.

## Prerequisites

- **Only EWC users can contribute items.** Access check:
  <https://europeanweather.cloud/get-access>
- A **public** source repository for the item (Git URL reachable without
  credentials) containing a `LICENSE` file and, optionally, an icon.
- Contributions go through a **GitHub pull request** or an EWC Support Portal
  ticket: <https://support.europeanweather.cloud>

## Workflow

1. Fork [`ewcloud/ewc-community-hub`](https://github.com/ewcloud/ewc-community-hub)
   and create a branch.
2. Edit `items.yaml` — add your item under `spec.items`. Field-by-field
   guidance: [metadata-schema.md](metadata-schema.md).
3. Validate locally with the Docker validator (recommended, see below). If the
   item is `EWCCLI-compatible`, also dry-run it through a custom catalogue
   (see below).
4. Open a pull request. The `validate.yml` GitHub Action runs the same schema
   check automatically.
   - ⚠️ PRs from contributors **outside the `ewcloud` org** need manual
     approval by an org member before the Action starts.
5. Respond to maintainer review feedback. Once merged with `published: true`,
   the item appears at <https://europeanweather.cloud/community-hub>.

Official onboarding guide (collaboration workflow, conventions,
recommendations): <https://confluence.ecmwf.int/x/wyLOIQ>

## Validation

CI validates every PR via
[`.github/workflows/validate.yml`](https://github.com/ewcloud/ewc-community-hub/blob/main/.github/workflows/validate.yml)
— AJV, JSON Schema draft 2020-12, against `schemas/items/v1alpha1.json`.

Run the **same check locally** (requires Docker; one-time image build):

```bash
# from the root of your ewc-community-hub clone
docker build --tag ewc-community-hub/metadata-validator .

docker run --rm --volume .:/tmp:ro \
  ewc-community-hub/metadata-validator \
  -s tmp/schemas/items/v1alpha1.json \
  -d /tmp/items.yaml \
  -c ajv-formats \
  --spec draft2020 \
  --errors text
```

Success output:

```
/tmp/items.yaml valid
```

## Testing with a custom catalogue (EWCCLI-compatible items)

Schema validation only proves the metadata is well-formed. If the item is
tagged `EWCCLI-compatible` in `annotations.others`, the `ewccli` block
(entrypoint, `inputSpec`, `values`) is exercised only by an actual CLI run —
test it before opening the PR.

Put the item entry (same content as in `items.yaml`) in a local custom
catalogue file:

```yaml
apiVersion: communityhub.europeanweather.cloud/v1alpha1
kind: CommunityHubCatalog
spec:
  items:
    my-item:   # must equal the entry's `name`
      ...      # identical to your items.yaml entry
```

Then run the `ewccli` validation sequence:

```bash
ewc hub --path-to-catalog custom-catalogue.yaml list
ewc hub --path-to-catalog custom-catalogue.yaml show my-item
ewc hub --path-to-catalog custom-catalogue.yaml deploy my-item --dry-run \
  --item-inputs <mandatory-input>=<value>   # one per input without `default`
```

- `list` / `show` confirm the entry parses and the `ewccli` block is readable.
- `deploy --dry-run` with **every mandatory input** (each `inputSpec` entry
  without `default`) confirms the entrypoint resolves and inputs validate,
  without creating any resource.
- The custom catalogue is a local test artifact — do **not** commit it to the
  hub repository; the PR only touches `items.yaml`.

Command details and catalogue shape: `ewccli` skill,
`references/custom-catalogues.md`.

## Review expectations

- Maintainers review metadata correctness (schema, URLs, contact info) and
  item quality (sources reachable, license present, description clear).
- Keep the PR scoped to your item entry; unrelated `items.yaml` churn slows
  review.
- Bump your item's `version` on every change to its metadata or sources.