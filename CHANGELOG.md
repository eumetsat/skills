# Changelog

All notable changes to EUMETSAT Agent Skills are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).
Versions follow [Semantic Versioning](https://semver.org/); the version in
`.claude-plugin/plugin.json` matches the latest tag.

## [Unreleased]

### Added

- `ml-menu-cdr`: a new skill that matches a climate need to one of the
  38 climate data records in the EUMETSAT Climate Services CDR menu (version 3)
  and gives the Data Store collection ID, the filename filter and the variable
  to read, with troubleshooting for searches and files. Downloads go through
  the `eumdac` download gate.
- `ml-menu-cdr`: eval cases `prefix-filter-before-search`,
  `download-goes-through-eumdac-gate` and `area-search-on-misplaced-footprint`.

## [0.1.0] - 2026-10-24

First tagged release.

### Added

- `eumdac`: a quick reference of verified command templates at the top of
  `SKILL.md`, and a single command that reports product count and total size
  before a download.
- `eumdac`: eval case `token-check-hides-secret`.
- `firecube`: `check_done.py` gains `--quick` (the split-batch and lifecycle
  checks run on one product of the input against a one-product reference
  store), `--quick-glob` to pick that product, and `--regridded` to skip the
  source-equivalence figures for plugins that bin or resample onto another grid.
- `firecube`: the hook order for the Zarr templates, as a table in
  `references/templates.md`.
- `firecube`: `ctx.storage.output` as the read-only route to the output target,
  including `s3://` targets, in `references/plugin-traps.md`.
- `firecube`: the rule never to return the root group from `get_batch_groups`,
  with the measured consequence, in the Zarr layout rules.
- `firecube`: the JSON-array syntax for list-typed `--option` values, in
  `references/configuration-storage.md` and `references/cli-surface.md`.
- `firecube`: the lat/lon binner's aggregation values, NaN handling, result
  dtypes and export status, in `references/plugin-development.md`.
- `firecube`: rule 17 names the installed `firecube` in the plugin's own
  environment as the authoritative source over a git checkout of core.
- `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, this changelog, and the licence split.

### Changed

- `eumdac`: `SKILL.md` cut from 11.5 KB to 6.3 KB; routine `command -v`,
  `--version` and `--help` checks only when the answer depends on them;
  read-only commands run without asking; the description says when to use the
  skill.
- `eumdac`: the download gate asks once, after stating count, size, free space
  and destination; a "go ahead" sent with the request is not authorisation.
- The repository licence is CC BY 4.0 for the skill content; the helper scripts
  under `skills/firecube/scripts/` keep the MIT licence, now in `LICENSE-MIT`.
- `firecube`: the definition of done is a list with the `check_done.py` flag
  beside each item, instead of one paragraph.
- `firecube`: `check_done.py` records the found, processed and product counts as
  evidence and checks that at least one item was processed, instead of
  asserting one file per item, which a plugin that bundles files into passes or
  days can never satisfy. A single time step now counts as an ordered
  coordinate.
- `firecube`: `check_plugin_contract.py` skips files that git ignores, so plan
  files and other local notes do not fail the referenced-files check.
- `firecube`: `check_plugin_contract.py` no longer checks the import boundary,
  which is now a ruff `banned-api` block the plugin carries in its own
  `pyproject.toml` (documented in `references/plugin-development.md`), and
  drops the `own-ordering`, `payload-hash` and `time-encoding` warnings, which
  never fired on a real plugin and are rules in `references/plugin-traps.md`.
- `firecube`: `check_done.py` drops the author, email, licence and plan-file
  checks and their flags; it reads the NetCDF group walk from
  `inspect_product.py` instead of carrying a copy.
- `firecube`: the skill, references and helper scripts target firecube 0.1.7,
  with the documented 0.1.5 differences kept in `references/troubleshooting.md`
  (2026-09-28).

### Fixed

- `eumdac`: token validity is checked with `eumdac token >/dev/null`; bare
  `eumdac token` prints the bearer token on stdout.
- `eumdac`: `Product.size` is in KB, not bytes.
- `eumdac` eval `download-needs-authorization`: the no-download grader no longer
  matches the word `download` in paths, and the judge rubric drops a clause that
  did not apply.
- The plugin licence is `CC-BY-4.0 AND MIT`; `plugin.json.ABOUT` points at
  `LICENSE-MIT`.
- Repository SBOM instructions simplified (2026-09-17); review fixes across the
  skills (2026-09-18).

[Unreleased]: https://github.com/eumetsat/skills/compare/v0.1.0...main
[0.1.0]: https://github.com/eumetsat/skills/releases/tag/v0.1.0
