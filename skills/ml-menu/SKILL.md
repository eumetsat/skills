---
name: ml-menu
description: "Works with the EUMETSAT Data Store and eumdac to find climate data records (CDRs) for long time series: ML model training, trend analysis and anomaly detection. Picks one of the 38 CDR menu records and gives its collection ID, filename filter and variable, and flags what breaks a long series (interim extensions, satellite changes, sampling changes). Covers clouds, albedo, radiation, precipitation, winds, aerosol, ozone, trace gases, sounder radiances, scatterometer, Meteosat imagery and sea ice. Hands downloads to eumdac."
license: CC-BY-4.0
compatibility: Record selection needs no tool. Searches and downloads use the eumdac skill (eumdac 3.1.1, Data Store credentials in ~/.eumdac, network access to api.eumetsat.int). Opening files needs xarray with netCDF4 or h5netcdf.
metadata:
  author: EUMETSAT
  version: "0.1.0"
---

# EUMETSAT climate data records

Grounded in the EUMETSAT Climate Services CDR menu (version 3), which covers 38 climate data records on the Data
Store.

## Rules

1. Answer from the table below without running `eumdac`. Run a live search only when the user asks for one, at
   most two, with `--limit`.
2. The Data Store wins. When a value here disagrees with a live `eumdac describe` or `eumdac search`, use the live
   value and tell the user in one line.
3. Do not download from this skill. When the user wants the files, end the answer by listing what must be settled
   before the `eumdac` skill downloads: product count, total size, destination directory, free space there, and the
   user's explicit go-ahead. State these as required, not optional. Then hand the collection ID, time range and filter
   to the `eumdac` skill; its download gate applies unchanged.
4. CLARA-A3, SARAH and GIRAFE hold every product and time step in one collection. Always filter on the product code
   plus the time-step code, for example `--filename "SALmm*"`. Never search or download them without that filter.
5. Give a variable name only when the table or [records.md](references/records.md) lists it. Otherwise tell the user
   to inspect one file (`ncdump -h <file>`) before writing analysis code.
6. Some records are EPS native format, not netCDF (marked "EPS native" below). Say so before proposing xarray code.
7. Never write credentials into code. Python reads `~/.eumdac`, as the `eumdac` skill does.

## Records

Period ends are from the menu; "present" means the record is still extended.

| Record | Data Store ID | Period | Coverage | Time step | Filter → variable |
| --- | --- | --- | --- | --- | --- |
| **Clouds, radiation, albedo, precipitation** | | | | | |
| CLARA-A3 (AVHRR): CFC, CPH, CTO, OLR, RSF, SAL, SDL, SIS, SNL, SNS, SRB | `EO:EUM:DAT:0874` | 1979-01-01 to present | Global | `dm` daily, `mm` monthly, `pm` 5-day (SAL) | `SALmm*` → `blue_sky_albedo_all_mean`; other products: inspect a file |
| SARAH-3 surface radiation: CAL, DAL, DNI, PAR, SDU, SID, SIS | `EO:EUM:DAT:0863` | 1983-01-01 to present | Meteosat 0° disk | `in` 30-min, `dm` daily, `mm` monthly (SDU: `ds`, `ms`) | `SISmm*` → `SIS` (+ clear-sky `SISC`); variable = product code |
| GIRAFE precipitation | `EO:EUM:DAT:0921` | 2002-01-01 to present | Global, 1° | Daily, monthly | `PREdm*`, `PREmm*` → `precipitation` |
| OCA cloud analysis (SEVIRI) | `EO:EUM:DAT:0617` | 2004-01-19 to 2019-08-31 | MSG 0° disk | 15-minute | `cloud_top_pressure`, `cloud_probability`, `cloud_particle_effective_radius`, `scene_classification` |
| GSA land surface albedo, MFG and MSG 0° | `EO:EUM:DAT:0300` | 1982-02-10 to 2017-12-31 | Meteosat 0° disk | 10-day | `DHR30` (black-sky), `BHRiso` (white-sky) |
| GSA land surface albedo, 57°E | `EO:EUM:DAT:0301` | 2006-12-07 to 2017-03-30 | Meteosat 57°E disk | 10-day | `DHR30`, `BHRiso`; no `--bbox` (footprint misplaced) |
| GSA land surface albedo, 63°E | `EO:EUM:DAT:0302` | 1998-07-10 to 2007-04-10 | Meteosat 63°E disk | 10-day | `DHR30`, `BHRiso`; no `--bbox` (footprint misplaced) |
| **Winds (atmospheric motion vectors)** | | | | | |
| AMVs, MFG and MSG 0° | `EO:EUM:DAT:0405` | 1981-09-03 to 2019-09-01 | Meteosat 0° disk | 2-hourly MFG, hourly MSG | `speed`, `dir`, `u`, `v`, `height` |
| AMVs, MFG 57°E | `EO:EUM:DAT:0894` | 2006-11-28 to 2017-04-01 | Meteosat 57°E disk | 2-hourly | `speed`, `dir`, `u`, `v`, `height` |
| AMVs, MFG 63°E | `EO:EUM:DAT:0895` | 1998-07-01 to 2007-04-16 | Meteosat 63°E disk | 2-hourly | `speed`, `dir`, `u`, `v`, `height`; no `--bbox` (footprint misplaced) |
| AMVs, MSG 41.5°E | `EO:EUM:DAT:0896` | 2017-02-01 to 2019-09-01 | Meteosat 41.5°E disk | Hourly | `speed`, `dir`, `u`, `v`, `height`; IR and WV in separate files |
| OCA AMVs (SEVIRI) | `EO:EUM:DAT:1082` | 2004-01-19 to 2019-08-31 | MSG 0° disk | Hourly | `speed`, `dir`, `height`, `u`, `v`; 3 files per product (IR108, WV62, WV73) |
| SEVIRI Rapid Scan AMVs | `EO:EUM:DAT:1083` | 2008-05-06 to 2020-04-03 | Europe and North Africa | 5-minute | `wind_speed`, `wind_from_direction`, `air_pressure`, `u`, `v` in group `wind_ir108` (one group per channel) |
| AVHRR GAC polar AMVs | `EO:EUM:DAT:0558` | 1979-01-01 to 2019-09-01 | Polar | Per orbit | `wind_speed`, `wind_from_direction`, `eastward_wind`, `northward_wind`, `wind_pressure` |
| AVHRR global AMVs, Metop-A/B tandem | `EO:EUM:DAT:0151` | 2013-04-24 to 2017-12-31 | Global | Daily | EPS native |
| AVHRR polar AMVs, Metop-A and -B | `EO:EUM:DAT:0152` | 2007-03-01 to 2017-12-31 | Poleward of 45° | Per orbit | EPS native |
| **Atmospheric composition and profiles (IASI, GOME-2)** | | | | | |
| IASI temperature and humidity profiles | `EO:EUM:DAT:0576` | 2007-07-10 to 2023-12-31 | Global | Twice daily | `*+PW3+IASI*` → `T`, `W`, `pressure_levels`, `Ts`, `Ps` |
| IASI ozone | `EO:EUM:DAT:1027` | 2007-07-10 to 2023-12-31 | Global | Twice daily | `*+O3+IASI*` → `o3_x_o3`, `o3_cp_o3_a` |
| IASI SO2 | `EO:EUM:DAT:0960` | 2007-07-10 to 2023-12-31 | Global | Twice daily | `*+SO2+IASI*` → `so2_col` |
| IASI CO (FORLI-CO) | `EO:EUM:DAT:0959` | 2007-07-10 to 2023-12-31 | Global | Twice daily | `*+CO+IASI*` → `co_x_co`, `co_cp_co_a` |
| Multi-sensor aerosol optical properties | `EO:EUM:DAT:0579` | 2007-07-10 to 2019-08-31 | Global | Per orbit | `aerosol_optical_depth`, `aerosol_class` (in netCDF groups) |
| **Radiances and brightness temperatures** | | | | | |
| IASI L1C spectra | `EO:EUM:DAT:0590` | 2007-07-10 to 2019-10-01 | Global | Per orbit | EPS native, `GS1cSpect`; about 1.4 GB per file |
| MHS Release 2, Metop-A and -B | `EO:EUM:DAT:0344` | 2006-10-31 to 2018-12-31 | Global | Per orbit | `btemps` |
| MHS Release 1, NOAA and Metop | `EO:EUM:DAT:0305` | 2005-08-30 to 2018-01-01 | Global | Per orbit | `FIDUCEO_FCDR_L1C_MHS_*` → `Ch1_BT` to `Ch5_BT`; for Metop use 0344 |
| AMSU-B, NOAA-15 to -17 | `EO:EUM:DAT:0303` | 1999-01-01 to 2014-06-06 | Global | Per orbit | `Ch16_BT` to `Ch20_BT` |
| SSM/T-2, DMSP | `EO:EUM:DAT:0343` | 1994-07-05 to 2005-01-10 | Global | Per orbit | `tb`, `cloud_flag` |
| ATMS, Suomi-NPP | `EO:EUM:DAT:0345` | 2011-12-10 to 2018-12-31 | Global | Per orbit | `btemps` |
| MWHS-1, FY-3A and -3B | `EO:EUM:DAT:0348` | 2008-07-01 to 2018-12-31 | Global | Per orbit | `btemps` |
| MWHS-2, FY-3C | `EO:EUM:DAT:0349` | 2013-09-30 to 2018-12-31 | Global | Per orbit | `btemps` |
| **Imagery** | | | | | |
| MVIRI L1.5, 0° | `EO:EUM:DAT:0880` | 1982-08-11 to 2006-07-19 | Meteosat 0° disk | 30-minute | `toa_bidirectional_reflectance_vis`, `count_ir`, `count_wv`; no lat/lon in files |
| MVIRI L1.5, 57°E | `EO:EUM:DAT:0881` | 2006-11-01 to 2017-04-04 | Meteosat 57°E disk | 30-minute | as 0880 |
| MVIRI L1.5, 63°E | `EO:EUM:DAT:0882` | 1998-07-01 to 2006-10-31 | Meteosat 63°E disk | 30-minute | as 0880 |
| SEVIRI Rapid Scan L1.5 | `EO:EUM:DAT:0962` | 2008-05-06 to 2021-09-22 | Europe and North Africa | 5-minute | `counts_vis006` to `counts_ir134`, `counts_hrv` (counts, not radiances) |
| **Scatterometer (ASCAT, Metop-A)** | | | | | |
| ASCAT L1B full resolution (SZF) | `EO:EUM:CM:METOP:ASCSZFR02` | 2007-01-01 to 2014-04-01 | Global | Per orbit | EPS native: `SIGMA0_FULL`, `INC_ANGLE_FULL`, `AZI_ANGLE_FULL` |
| ASCAT L1B 25 km (SZO) | `EO:EUM:CM:METOP:ASCSZOR02` | 2007-01-01 to 2014-04-01 | Global | Per orbit | EPS native: `SIGMA0_TRIP`, `KP`, `INC_ANGLE_TRIP`, `AZI_ANGLE_TRIP` |
| ASCAT L1B 12.5 km (SZR) | `EO:EUM:CM:METOP:ASCSZRR02` | 2007-01-01 to 2014-04-01 | Global | Per orbit | EPS native: as SZO |
| **Sea ice** | | | | | |
| AMSR sea ice concentration | `EO:EUM:DAT:1064` | 2021-01-01 to present | Each hemisphere, 25 km | Daily (unconfirmed) | `ice_conc_nh_*_icdr-*` (`sh` south, `icdrft` near-real time, FTP/THREDDS only per collection metadata) → `ice_conc` |
| DMSP sea ice concentration | `EO:EUM:DAT:0645` | 2023-09-03 to present | Each hemisphere, 26 × 25 km | Daily | `ice_conc_nh_*` (`sh` south) → `ice_conc` |

The IASI and MHS R1 filters cover every satellite in the record. Adding `METOPA` or `METOPB` (IASI), or `NOAA18` or
`NOAA19` (MHS R1), selects one satellite and shortens the series.

## Long time series

For ML training, trend or anomaly work, check these against the requested period. Facts come from the records
reference and troubleshooting; the menu documents nothing further.

- Interim records: AMSR (`1064`) and DMSP (`0645`) sea ice are interim CDRs (`icdr` in filenames); "present" means the record is extended.
- Satellite changes inside a record: IASI (`0576`, `1027`, `0960`, `0959`) and AVHRR polar AMVs (`0152`) span Metop-A and -B, and Metop-B data start 2013-04-24 in `0152`. MHS R1 (`0305`) is superseded by R2 (`0344`) for Metop. `0558` spans TIROS-N, NOAA-6 to -19 and Metop-A/B; `0305` spans NOAA-18, NOAA-19 and Metop-A/B.
- Sampling changes: `0405` is 2-hourly for MFG and hourly for MSG.
- Orbital positions are separate records, not one series: 0°, 57°E, 63°E and 41.5°E (for example `0300`, `0301`, `0302`, `0896`).
- Calibration limits: SEVIRI Rapid Scan (`0962`) recalibration runs only until 04/2020; MVIRI (`0880`, `0881`, `0882`) files carry no geolocation; `0962` holds counts, not radiances.
- Quality flags: IASI profiles (`0576`) list Q flags; SSM/T-2 (`0343`) lists `cloud_flag`.

The menu does not document homogeneity or breakpoints beyond these. Tell the user so; do not infer any.

## Workflow

1. Pin down the variable, region, period and time step the user needs.
2. Pick candidate records from the table. Check that period and coverage fit; say so when none does.
3. Give the collection ID, filter and variable. Mention a limitation only when it affects the request.
4. For a search or download, hand off to the `eumdac` skill with the filter:

```bash
timeout 120 eumdac search --collection "EO:EUM:DAT:0874" --filename "SALmm*" --start "2020-01-01" --end "2021-01-01" --limit 5
```

5. For Python, adapt [python-template.md](references/python-template.md).

## Route by intent

| Intent | Reference |
| --- | --- |
| Sensor, satellites, resolution, full variable list, example filename, packaging for one record | [records.md](references/records.md) |
| Search returns too much or nothing, area search misses files, file will not open or has no variables | [troubleshooting.md](references/troubleshooting.md) |
| Python search, filtered download and opening | [python-template.md](references/python-template.md) |

## Response contract

Give the record name and collection ID, the filter, the variable, and any limitation that affects the request. State
what you checked live and what comes from this skill. For ML or trend use, name the items from "Long time series"
that touch the requested period. When the user will fetch files, list the five download prerequisites from Rule 3.
