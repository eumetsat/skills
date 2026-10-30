<p align="center"><img src="docs/assets/eumetsat-skills-icon.svg" alt="EUMETSAT Agent Skills icon" width="160"></p>
<h1 align="center">EUMETSAT Agent Skills</h1>
<p align="center">
<a href="https://skills.sh/eumetsat/skills"><img src="https://skills.sh/b/eumetsat/skills" alt="skills.sh"></a>
<a href="https://agentskills.io"><img src="https://img.shields.io/badge/Agent%20Skills-standard-blue" alt="Agent Skills"></a>
<a href="#copyright-and-license"><img src="https://img.shields.io/badge/license-CC%20BY%204.0%20AND%20MIT-green" alt="license"></a>
<a href="CHANGELOG.md"><img src="https://img.shields.io/badge/version-0.1.0-informational" alt="version"></a>
</p>

This repository gives your coding agent six skills for working with EUMETSAT tools. A skill is a `SKILL.md` file in the Agent Skills format. It holds the commands and the safety rules for one tool or service. Claude Code, Codex, OpenCode, VS Code, and any other client of the Agent Skills format can load the skills.

With the skills loaded, your agent can search and download satellite data from the EUMETSAT Data Store, run Data Tailor customisations, manage profiles, infrastructure and catalogues on the European Weather Cloud, build Firecube plugins and ingest products into datacubes, select satellite imagery around detected weather features from the Earth System Feature Database, and find the right climate data record, files and variables on the Data Store.

Installing the skills needs no account. The table below lists what each skill needs when you run its workflows.

## Available Skills

| Skill | What it does | What you need |
| --- | --- | --- |
| [eumdac](skills/eumdac/SKILL.md) | Works with the EUMETSAT Data Store and Data Tailor. Searches, lists, downloads, and orders satellite products. Checks tokens and credentials. Manages subscriptions and livefeed. | EUMDAC 3.1.1 as CLI or Python package. Data Store credentials in `~/.eumdac`. Network access to `api.eumetsat.int`. |
| [ewccli](skills/ewccli/SKILL.md) | Sets up the European Weather Cloud command line interface. Covers login profiles, OpenStack application credentials, Community Hub item discovery and deployment, infrastructure commands, and custom catalogues. | EWCCLI 0.3.1 on Python 3.11+. A European Weather Cloud account. For live commands, network access to the EWC and OpenStack endpoints. |
| [firecube](skills/firecube/SKILL.md) | Runs Firecube batch ingestion, which turns Earth Observation products into analysis-ready datacubes. Covers plugin development. | Firecube 0.1.7 on Python 3.12+. For execution, an appropriate plugin and source files. |
| [esf-satellite-data](skills/esf-satellite-data/SKILL.md) | Builds reproducible satellite imagery datasets around detected weather features from the Earth System Feature database. The imagery comes from the EUMETSAT Data Store, EUMETSAT S3 buckets, or AWS Open Data. | The internal esf MCP server 0.9.0 (`feature-db-api`), registered with your agent. Data Store or S3 access for the imagery. Access permissions, endpoint and credentials for the esf server come from your service administrator. |
| [feature-db-client](skills/feature-db-client/SKILL.md) | Fetches and saves Earth System Feature Database features as GeoDataFrames with the `feature_client` Python library. Runs spatial, temporal, and tag queries and nearest-feature search. | The feature-client package 0.1.0, a public package that needs no entitlement to install. Access permissions for the Feature Database service: an authorised endpoint and API key from your service administrator. |
| [ml-menu-cdr](skills/ml-menu-cdr/SKILL.md) | Matches a climate need to one of 38 EUMETSAT climate data records on the Data Store: clouds, radiation, albedo, precipitation, winds, atmospheric composition, sounder radiances, Meteosat imagery, scatterometer and sea ice. Gives the collection ID, the filename filter and the variable to read, and troubleshoots searches and files. Hands downloads to the eumdac skill. | Nothing to choose a record. For searches and downloads, what the eumdac skill needs. xarray to open the files. |

## Getting Started

### Prerequisites

The skills do not install runtime tools or credentials. Prepare the following:

- An agent that reads `SKILL.md` files. The one-command installs and the prompts that ask for an explanation need no EUMETSAT runtime tool and no service credentials.
- A local checkout of this repository, only for the manual install and the agent-prompt install.
- The runtime tool and the credentials of a skill, only to run that skill's tool or service operations. The table lists them.

### Installing

The repository is a plugin marketplace (`.claude-plugin/marketplace.json`) and a plain skills folder. Choose the install path for your agent. Each path installs all six skills.

#### Claude Code

```text
/plugin marketplace add eumetsat/skills
/plugin install eumetsat-skills@eumetsat
/reload-plugins
```

#### OpenAI Codex

```bash
codex plugin marketplace add eumetsat/skills
codex plugin add eumetsat-skills@eumetsat
```

#### OpenCode, VS Code and other skills-compatible agents

With the [skills CLI](https://skills.sh):

```bash
npx skills add eumetsat/skills -g -a opencode --skill '*' -y   # all projects
npx skills add eumetsat/skills -a opencode --skill '*' -y      # this project only
```

Replace `-a opencode` with your agent. To target several agents, pass `-a` once for each, for example `-a claude-code -a codex -a opencode`. To install one skill, pass `--skill eumdac`. To install by hand, run:

```bash
git clone https://github.com/eumetsat/skills.git eumetsat-skills
mkdir -p ~/.agents/skills
ln -s "$PWD"/eumetsat-skills/skills/* ~/.agents/skills/
```

Use the skills directory that your client documents. <https://agentskills.io/clients> and [installation](docs/installation.md) list the path for each agent. For a prompt-based install, open a checkout and give your agent this prompt:

```text
Install every skill under skills/ from this checkout for my current agent using docs/installation.md.
Keep any existing skill installation unless I authorize replacing it.
Verify that each installed skill resolves to skills/<name>/SKILL.md.
```

## Quickstart

After the install, give your agent this prompt:

```text
Use the eumdac skill to explain how I can search an EUMETSAT Data Store collection.
Do not install tools, configure credentials, or download data yet.
```

The agent names the collection and the search filters it needs. Then it explains the search procedure. The prompt asks for an explanation only, so this step needs no installed tools and no credentials. See [more prompts](docs/quickstart-prompts.md) and [worked examples](examples/).

## Development

Keep skill sources in `skills/<name>/SKILL.md`. Read [AGENTS.md](AGENTS.md) for the contribution rules. Read [reference boundaries](docs/skill-reference-boundaries.md) before you move guidance.

[Validation](docs/validation.md) covers tool access, CLI checks, and behavior cases. [External references](docs/external-references.md) lists the official product and agent documentation.

## Software Bill Of Materials

Generate the source inventory in SPDX JSON format at `.reports/source-sbom.spdx.json`:

```bash
mkdir -p .reports
trivy fs --include-dev-deps --skip-dirs .venv,.venvs,venv,env,.reports \
  --format spdx-json --output .reports/source-sbom.spdx.json .
```

The source scan does not resolve standalone Python imports. The tables below record the versions and licenses reviewed for the [Firecube helpers](skills/firecube/scripts/README.md).

### Included Components

No third-party components are vendored.

### Direct Runtime Dependencies

These dependencies are needed when running the corresponding helper scripts.

| dependency | version | license | copyright | home_url | comments |
| --- | --- | --- | --- | --- | --- |
| firecube | 0.1.7 | Apache-2.0 | | https://github.com/eumetsat/firecube | Ingestion checks; optional API inspection in the contract checker. |
| numpy | 2.5.2 | BSD-3-Clause | | https://numpy.org | Product inspection and store comparison. |
| xarray | 2026.7.0 | Apache-2.0 | | https://xarray.dev | Product inspection and store comparison. |
| zarr | 3.3.0 | MIT | | https://github.com/zarr-developers/zarr-python | Zarr store checks. |
| netCDF4 | 1.7.4 | MIT | | https://github.com/Unidata/netcdf4-python | NetCDF backend; alternative to h5netcdf for supported inputs. |
| h5netcdf | 1.8.1 | BSD-3-Clause | | https://h5netcdf.org | Alternative backend for NetCDF4/HDF5 inputs. |
| h5py | 3.16.0 | BSD-3-Clause | | https://www.h5py.org | Fallback group walk in product inspection and store comparison when netCDF4 is absent. |

### Direct Build, Edit, And Test Dependencies

| dependency | version | sw type | license | copyright | home_url | comments |
| --- | --- | --- | --- | --- | --- | --- |
| uv | 0.12.13 | Development tools | MIT OR Apache-2.0 | | https://github.com/astral-sh/uv | Runs plugin tests and lint checks from check_done.py. |
| pytest | 9.0.3 | Development tools | MIT | | https://github.com/pytest-dev/pytest | Plugin tests invoked by check_done.py. |
| ruff | 0.15.6 | Development tools | MIT | | https://github.com/astral-sh/ruff | Plugin lint checks invoked by check_done.py. |

## Copyright and License

Copyright (c) 2026 EUMETSAT.

The skills, their references, examples, evaluation cases and documentation are
licensed under the Creative Commons Attribution 4.0 International licence
([LICENSE](LICENSE), CC BY 4.0): use, share and adapt them, including
commercially, with attribution to EUMETSAT and an indication of what you
changed.

The three helper scripts under `skills/firecube/scripts/` are small conveniences
that accompany the firecube skill. They carry the MIT licence in their headers
and in [LICENSE-MIT](LICENSE-MIT), so they can be copied into a plugin project
under the usual software terms. Configuration and metadata files (`plugin.json`,
`agents/openai.yaml`, `skills-bench.yaml`, `ruff.toml`) are MIT as well, stated in
their headers or adjacent `.ABOUT` files. The plugin as a whole is therefore
`CC-BY-4.0 AND MIT`.

See [AUTHORS.md](AUTHORS.md) for authors and maintainers and
[CONTRIBUTING.md](CONTRIBUTING.md) for how to contribute.
