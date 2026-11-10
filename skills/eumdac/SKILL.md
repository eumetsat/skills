---
name: eumdac
description: Use when the user mentions the `eumdac` CLI or Python package (EUMETSAT Data Access Client), the EUMETSAT Data Store or Data Tailor, collection IDs like `EO:EUM:DAT:...`, or asks to search, list, download or order satellite products (MSG/SEVIRI, MTG), check tokens or credentials, or manage subscriptions and livefeed.
license: CC-BY-4.0
compatibility: eumdac 3.1.1 (CLI or Python package), EUMETSAT Data Store credentials in ~/.eumdac, network access to api.eumetsat.int.
metadata:
  author: EUMETSAT
  version: "0.1.0"
---

# EUMDAC

Grounded in `eumdac 3.1.1` only (pinned install: [install.md](references/install.md)). Trust the templates here; run `eumdac <command> --help` only for an undocumented flag, another installed version, or a usage error. Discovery is `describe` (no `discover` command in 3.1.1).

## Quick reference

```bash
eumdac token >/dev/null    # validity only; stdout is the bearer token, never run bare or piped
timeout 120 eumdac describe [--filter "*MSG*"]
timeout 120 eumdac describe --collection "<collection-id>" [--product "<product-id>"]
timeout 120 eumdac search --collection "<collection-id>" --start "<YYYY-MM-DD[THH[:MM]]>" --end "<...>" --limit 5
timeout 120 eumdac search --collection "<collection-id>" --time-range "<start>" "<end>" --bbox W S E N --satellite "<MSG4>" --limit 5
eumdac tailor post --collection "<collection-id>" --product "<product-id>" --chain "<chain-id-or-file>"
eumdac tailor status "<customisation-id>"
eumdac tailor download "<customisation-id>" --output-dir "<dir>"
```

Times are UTC. Other filters (`--publication-*`, `--daily-window`, `--geometry`, `--product-type`, `--timeliness`, orbit/cycle, `--filename`, `--sort`): [datastore-filtering.md](references/datastore-filtering.md).

## Rules

1. Never print, commit, or log consumer keys/secrets, bearer tokens, subscription credentials, account details, or private downloaded-data paths. Never put literal secrets on a command line; use placeholders when credentials are missing.
2. Do not run `set-credentials` or `subscribe set-credentials` when a credentials file exists unless the user explicitly asks to replace it.
3. Run read-only commands directly with stored credentials; do not ask first: `describe`, `search`, `token >/dev/null`, `subscribe list`, `tailor list|status|log|quota|resources`, `local-tailor instances|show`, `order list|status`.
4. Ask for confirmation, stating what will happen, before state-changing, long-running, or expensive commands: `download`, `download-metalink`, `subscribe add|download`, `livefeed`, `tailor post|download|delete|cancel|clean`, `local-tailor set|remove`, `order resume|restart|delete|housekeep`, both `set-credentials`, and Python equivalents (bulk `product.open()` loops, `DataTailor.new_customisation(s)`).
5. Call `eumdac` from `PATH`. Run `command -v eumdac` and follow install.md only when it is not found; run `--version`/`--help` only under the conditions above. Never assume a project `.venv` or personal virtualenv path.
6. Run every live call under `timeout 120`; keep `--limit` on exploratory searches. A search combining `--sort` with `--bbox`/`--geometry` hangs on wide ranges: narrow the time range and drop `--sort`. Print one progress line before a download or long search and one result line after; never run silently. Check a shell variable is set before using it as a product ID (empty hangs).
7. `--bbox`/`--geometry` filter whole products and do not crop. Cropping or subsetting is Data Tailor (or mission `--download-coverage`).
8. Download gate. Never download because a collection was named or to be helpful. Gather count, total size, free space, and the destination the user names (never invent one), then ask once stating all four and download only after explicit authorisation given after the user has seen them (a "go ahead" sent with the request is not authorisation), under `timeout`, then report the destination directory (back to a calling skill if any).
   - Space: `df -h <destination>`. Download options and `--yes`: [datastore-download.md](references/datastore-download.md).
   - Count and size in one call, no separate count search (`Product.size` is KB; a hint, not the archive size; prints only count and GB; the shebang finds the Python with eumdac for tool installs):

```bash
timeout 120 "$(head -1 "$(command -v eumdac)" | cut -c3-)" -I - "<collection-id>" "<start>" "<end>" <<'PY'
import sys, eumdac
from datetime import datetime
from eumdac.config import get_credentials_path
col, t0, t1 = sys.argv[1:4]
store = eumdac.DataStore(eumdac.AccessToken(get_credentials_path().read_text().strip().split(",")))
res = store.get_collection(col).search(dtstart=datetime.fromisoformat(t0), dtend=datetime.fromisoformat(t1))
print(f"{res.total_results} products, {sum(p.size for p in res) / 1024**2:.2f} GB")
PY
```
9. If the user has no files and asks where their data is, ask; do not search their disks. Apply rules without lecturing; state only what is needed in one line.

## Response contract

When proposing commands or code: state CLI vs Python, prerequisites (install, credentials, network, IDs), placeholders for secrets, and validation status (what was run, what was not, why; claim live validation only after real service calls). Answer short factual questions and your own read-only runs directly. Do not guess product IDs.

## Route by intent

Read only the reference needed. Out of scope: science interpretation, generic packaging, post-download analysis, web UIs.

| Intent | Reference |
| --- | --- |
| Climate data record (CDR) or long climate time series: which collection, filename filter, variable | If the `ml-menu` skill is installed, load it first for the collection, filename filter and variable; then return here for search and download |
| Install, missing CLI, wrong Python | [install.md](references/install.md) |
| Credentials, token, 401/403 | [auth.md](references/auth.md) |
| List/describe collections or products | [datastore-discovery.md](references/datastore-discovery.md) |
| Search filters beyond the quick reference | [datastore-filtering.md](references/datastore-filtering.md) |
| Download options (entries, integrity, coverage, threads, layout); another skill needing files on disk | [datastore-download.md](references/datastore-download.md) |
| Metalink carts | [datastore-metalink.md](references/datastore-metalink.md) |
| Python API (`AccessToken`, `DataStore`, `DataTailor`) | [python-api.md](references/python-api.md) |
| Data Tailor, local-tailor, orders | [tailor-orders.md](references/tailor-orders.md) |
| Subscriptions, livefeed | [subscriptions-livefeed.md](references/subscriptions-livefeed.md) |
| Errors, debug/trace, stuck jobs | [troubleshooting.md](references/troubleshooting.md) |
