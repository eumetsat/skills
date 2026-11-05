# Climate Data Records Examples

These examples are sanitized scenarios for the `ml-menu-cdr` skill. They are intended as quickstart
scenarios and regression prompts.

Do not treat dates, filenames or product counts as current results. Re-run the searches through the `eumdac` skill
when current data matters.

## Scenarios

| File | Scenario | What it tests |
| --- | --- | --- |
| [surface-albedo-sahel.md](surface-albedo-sahel.md) | Monthly surface albedo for a region and period | Record choice, product and time-step filter, variable name, eumdac hand-off |
| [antarctic-sea-ice.md](antarctic-sea-ice.md) | Daily Antarctic sea ice for one year | Choosing between two records by period, hemisphere and timeliness filter |
| [indian-ocean-albedo.md](indian-ocean-albedo.md) | Land albedo from the 63°E Meteosat record | Searching by time only where the footprint is misplaced |

## Safe Validation Boundary

The examples run no downloads. Searches are read-only and use `--limit`. Keep credentials and local paths out of
notes and logs; use placeholders in their place.
