# Monthly Surface Albedo Over The Sahel

## Prompt

I need monthly surface albedo over the Sahel for 2000 to 2020 from EUMETSAT. Which dataset and which files?

## Expected Agent Behavior

- Use the `ml-menu-cdr` skill and answer from its records table.
- Recommend CLARA-A3 (`EO:EUM:DAT:0874`), global from 1979, with the filter `SALmm*` and the variable
  `blue_sky_albedo_all_mean`. GSA (`EO:EUM:DAT:0300`, 10-day, to 2017) is an alternative only if 10-day land albedo
  to 2017 is enough.
- State that the collection holds every CLARA-A3 product, so the search must filter on `SALmm*`.
- Hand the search to the `eumdac` skill. Do not download without the `eumdac` download gate.

## Command Pattern

```bash
timeout 120 eumdac search --collection "EO:EUM:DAT:0874" --filename "SALmm*" --start "2000-01-01" --end "2021-01-01" --limit 5
```

## Expected Response Shape

- Record: CLARA-A3, `EO:EUM:DAT:0874`.
- Filter: `SALmm*`; variable `blue_sky_albedo_all_mean`.
- Validation status: read-only search run or proposed; no download.
