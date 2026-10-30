# Skill Reference Boundaries

Use this file when adding, renaming, splitting, or reviewing skill reference files.

## EUMDAC

- `install.md`: installation methods and version checks.
- `auth.md`: credential setup and credential overwrite safety.
- `datastore-discovery.md`: collections, products, and metadata discovery.
- `datastore-filtering.md`: search filters, area filters, temporal filters, and advanced filtering.
- `datastore-download.md`: direct downloads and large-download safety.
- `datastore-metalink.md`: cart/metalink downloads.
- `python-api.md`: Python API patterns.
- `tailor-orders.md`: Data Tailor and order workflows.
- `subscriptions-livefeed.md`: subscriptions and livefeed workflows.
- `troubleshooting.md`: triage and common failure modes.

Split large or mixed sections into new references and link them from `SKILL.md`.

## EWCCLI

- `install.md`: installation methods, Python requirement, PATH, and version checks.
- `auth-profiles.md`: `ewc login`, profile storage, OpenStack application credentials, SSH key safety, and config precedence.
- `hub.md`: EWC Community Hub list/show/deploy workflows, item inputs, dry-run, and deployment safety.
- `infra.md`: direct `ewc infra` create/show/list/delete workflows and resource safety.
- `vm-images.md`: official EWC Virtual Image names, short `ewccli` image selectors, and image-name safety.
- `vm-plans.md`: federee-specific VM plan/flavour names, defaults, GPU/HPC notes, and official links.
- `custom-catalogues.md`: `--path-to-catalog`, item metadata, local unpublished items, and validation flow.
- `troubleshooting.md`: triage and common failure modes.
- `official-links.md`: verified official EWC links and link-use policy.

If EWCCLI registers new command groups such as Kubernetes, S3, or DNS, add or split references and update `SKILL.md`.

Do not invent EWC service URLs, Confluence links, Horizon routes, OpenStack command alternatives, or support processes. Add only verified official links, or ask the user for the official article or permission to look it up.

## Firecube

- `install.md`: PyPI install with uv/pip, Python 3.12+ requirement, optional extras, verification, shell completion, and upgrade/uninstall.
- `cli-surface.md`: registered command tree of the grounded release, read-only/mutating/destructive classification, shared options, and renamed-flag hints.
- `configuration-storage.md`: config file, environment, and flag precedence; target/product URI rules; storage type/driver coherence; S3 access setup.
- `ingestion.md`: `firecube ingest` workflow, user-supplied source data rule, plugin options, output-format choice, execution shapes, and re-run behavior; parallelism and write safety point to `parallelism.md`.
- `plugin-development.md`: known public plugins table (no index page exists yet; keep it current), plugin lifecycle, evidence and cube design procedure, template choice, scaffolding, source discovery, config options, telemetry, local testing, install/uninstall, and packaging contract.
- `plugin-traps.md`: public hook contract (MUST/SHOULD/CAN/DO NOT), public-API-only rule and core handoffs, resume/rerun/extension contract, Zarr layout rules, GenericZarr versus DirectZarr, plugin performance rules in short, authoring traps table, and a pointer to the 0.1.5 differences in `troubleshooting.md`.
- `templates.md`: one section per template (append Zarr, Parquet, direct Zarr, base, Tensogram): fit, contract, hook matrix, batch lifecycle, runtime behaviour, skeleton, context and exception tables.
- `parallelism.md`: the five parallelism models and their write domains, what the engine runs in worker threads and under the write lock, plugin state rules, staged versus direct write modes, slot-range procedure, verification of parallel runs.
- `benchmarks.md`: reproducible measurement: what to hold constant and record, what each template can gain from which knob, workflow, protocol for long runs (caps, process groups, parent versus worker CPU, stage timings with waits), equivalence checks, reporting.
- `zarr-parquet-archive.md`: Zarr, Parquet, and Tensogram archive commands with safety labels, index inspection, and store comparison.
- `chunks-catalog.md`: chunk control-plane inspection, recovery order, delete/reingest, snapshots, and Intake catalog generation.
- `performance.md`: `advise` commands, tuning knobs, CPU work in plugins (GIL, worker processes, discovery cost, diagnosis), bottleneck-to-action, memory, observability for measurement, and production checklist; benchmarking procedure points to `benchmarks.md`.
- `troubleshooting.md`: symptom/cause/fix triage, first checks, debug output, public bug reporting, and the list of differences for plugins still on 0.1.5.

Keep `firecube` aimed at users and plugin developers. Firecube contributor workflows (repository CI, release process, core internals) belong in the upstream repository, not here. Source data is always user-supplied; suggest an `eumdac` search only as advice when the user has a relevant EUMETSAT collection but no files.

## ESF Satellite Data

- `workflow.md`: the end-to-end selection procedure, feature-type confirmation, classification, deduplication, coverage, sizing, and download.
- `mcp-tools.md`: the `esf` MCP server tools, their inputs, and row budgets.
- `data-sources.md`: EUMETSAT Data Store, EUMETSAT S3 buckets, GeoRing, AWS Open Data, and anonymous access.
- `destinations-and-credentials.md`: destination checks and credential files referenced by name only.
- `download-script-template.md`: the generated download script, parallel fetch, extraction, manifest.
- `parameters-to-iterate.md`: which inputs to ask about versus default, matching a request to a feature type, and feasibility caveats to raise unprompted.
- `error-cases.md`: refusals, shortfalls, and mismatches.
- `streaming-and-stac.md`: streaming access and STAC manifests.
- `zarr-store-template.md`: store inspection and event-based subsets.

Keep service-specific values configurable and document the supported MCP contract. This repository owns its distributed skill copy.

## Feature DB Client

- `querying.md`: reference-data reads, feature queries, nearest-feature search, `get_features` signature.
- `saving-features.md`: required metadata, multi-index reference columns, minimal and comprehensive `save_features` examples.
- `reference-data-and-errors.md`: per-type `get_*`/`create_*`/`update_*` table and exception classes.

Keep the environment write policy and secret hygiene in `SKILL.md`; they gate every reference.

## Climate Data Records

- `records.md`: one entry per record in the CDR menu: Data Store title and ID, sensor and platform, period, coverage, resolution, time step, contents, variables, example filename, packaging and notes. Generated from the menu; regenerate it when the menu changes.
- `troubleshooting.md`: symptom, cause and action for searches that return too much or nothing, area searches that miss files, and files that will not open or hold no variables; limitations to mention when they affect a request.
- `python-template.md`: the Python search, filtered download and open template and how to adapt it.

Keep the records table, the filter rule, the answer-first rule and the hand-off to the `eumdac` skill in `SKILL.md`. Download commands, credentials and the download gate belong to `eumdac`; do not copy them here. Record facts come from the CDR menu; phrase its discrepancy notes as help for a symptom, not as a permanent fact.
