# Troubleshooting

Use this reference when a search, a file or a variable does not behave as the user expects. Find the symptom,
explain the cause to the user in one line, and take the action. When a live search disagrees with an entry here,
trust the live result.

## Searches

| Symptom | Cause | Action |
| --- | --- | --- |
| A CLARA-A3, SARAH or GIRAFE search returns many unrelated products | One collection holds every product and time step. | Add `--filename "<code><time-step>*"`, for example `"SALmm*"`. |
| A filter on a full example filename matches only part of the record | The filename tail changes between periods of the record. | Filter on the product and time-step code only. |
| An area search (`--bbox` or `--geometry`) on GSA 57°E (`EO:EUM:DAT:0301`), GSA 63°E (`EO:EUM:DAT:0302`) or AMVs 63°E (`EO:EUM:DAT:0895`) misses files | The Data Store footprint of these collections is misplaced, west of Greenwich. | Search by time only, without `--bbox` or `--geometry`, and crop after opening. |
| A CLARA-A3 search for `CMA`, `CTX`, `LWP`, `IWP`, `CPP`, `CWP` or `JCH` returns nothing | The collection metadata lists these products, but they were not found on the Data Store when the menu was compiled. | Run one `--limit 1` search to check; if still empty, tell the user. |
| An MHS Release 1 search (`EO:EUM:DAT:0305`) returns NOAA and Metop files together | The collection holds both. For Metop it is superseded by Release 2. | For Metop, use `EO:EUM:DAT:0344`; for NOAA, filter with `--filename "*NOAA18*"` or `"*NOAA19*"`. |
| An AMSR sea ice search returns files from two satellites | The record is shown as multimission, but GCOM-W and GOSAT-GW data arrive as separate products. | Filter on the platform, or combine them in the analysis. |
| An AMSR sea ice search mixes near-real-time and non-time-critical files | Both timeliness streams are in one collection. | Filter on one: `*_icdr-*` (non-time-critical) or `*_icdrft-*` (near-real time). |

## Files

| Symptom | Cause | Action |
| --- | --- | --- |
| `xr.open_dataset` fails on an ASCAT (`ASCSZFR02`, `ASCSZOR02`, `ASCSZRR02`), AVHRR AMV (`0151`, `0152`) or IASI L1C (`0590`) file | EPS native format, not netCDF. | Tell the user. Ask how they want to read it; do not guess a reader. |
| An IASI L1C download is very large | About 1.4 GB per file. | State the volume before any download. |
| The SEVIRI Rapid Scan AMV file (`1083`) opens but holds no wind variables | The variables sit in one group per channel: `wind_ir108`, `wind_wv062`, `wind_wv073`, `wind_hrvis`, `wind_vis06`. | Open a group: `xr.open_dataset(path, group="wind_ir108")`. |
| The aerosol file (`0579`) opens but holds no aerosol variables | The variables sit in netCDF groups (Data/MeasurementData/ObservationData/Aerosol). | Open the group that holds them. |
| An OCA AMV (`1082`) or 41.5°E AMV (`0896`) product holds several files | `1082` bundles three files (IR108, WV62, WV73); `0896` has separate IR and WV files. | Pick the file with `eumdac download --entry "<pattern>"` or open each file. |
| MVIRI L1.5 files (`0880`, `0881`, `0882`) have no latitude or longitude | The files carry no geolocation. | Tell the user; geolocation must come from elsewhere. |
| SEVIRI Rapid Scan imagery (`0962`) holds counts | The record stores counts with recalibration coefficients, and recalibration runs only until April 2020. | Convert counts to radiances before analysis; flag later dates. |
| AMSR sea ice files are daily or twice daily, while the OSI SAF page describes monthly composites | The Data Store and metadata give twice-daily data. | Use the Data Store files; aggregate in the analysis if needed. |

## Limitations to mention when they affect the request

- AVHRR Polar AMVs (`0152`): Metop-B data only from 2013-04-24.
- OCA (`0617`) is 15-minute and the SEVIRI Rapid Scan records (`0962`, `1083`) are 5-minute: volumes grow quickly with
  the period. Select by time of day, keep the period short, and crop each file straight after opening it.
