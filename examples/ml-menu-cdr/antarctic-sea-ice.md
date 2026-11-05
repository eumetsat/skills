# Antarctic Sea Ice Concentration

## Prompt

Get me daily Antarctic sea ice concentration for 2023 from EUMETSAT.

## Expected Agent Behavior

- Use the `ml-menu-cdr` skill and answer from its records table.
- Recommend the AMSR record (`EO:EUM:DAT:1064`), which covers all of 2023. The DMSP record (`EO:EUM:DAT:0645`)
  starts on 2023-09-03, so it covers only part of the year.
- Filter on the southern hemisphere and one timeliness: `ice_conc_sh_*_icdr-*`. Variable `ice_conc`.
- Hand the search to the `eumdac` skill; apply its download gate before any download.

## Command Pattern

```bash
timeout 120 eumdac search --collection "EO:EUM:DAT:1064" --filename "ice_conc_sh_*_icdr-*" --start "2023-01-01" --end "2024-01-01" --limit 5
```

## Expected Response Shape

- Record: AMSR sea ice concentration, `EO:EUM:DAT:1064`.
- Filter: `ice_conc_sh_*_icdr-*`; variable `ice_conc`.
- Validation status: read-only search run or proposed; no download.
