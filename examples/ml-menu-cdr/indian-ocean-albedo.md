# Land Surface Albedo Over Pakistan From The 63°E Meteosat Record

## Prompt

Give me the eumdac search for land surface albedo over Pakistan for 2003 from the Meteosat 63°E record. Don't run it.

## Expected Agent Behavior

- Use the `ml-menu-cdr` skill and answer from its records table.
- Use GSA 63°E (`EO:EUM:DAT:0302`), 10-day, variables `DHR30` (black-sky) and `BHRiso` (white-sky).
- Search by time only. The Data Store footprint of this collection is misplaced, so a `--bbox` or `--geometry`
  search may miss files; crop to Pakistan after opening.

## Command Pattern

```bash
timeout 120 eumdac search --collection "EO:EUM:DAT:0302" --start "2003-01-01" --end "2004-01-01" --limit 5
```

## Expected Response Shape

- Record: GSA 63°E, `EO:EUM:DAT:0302`; variables `DHR30`, `BHRiso`.
- No area filter, with the reason; crop after opening.
- Validation status: command proposed only.
