# Python template

Use this template when the user wants code. This skill supplies the collection ID, the filename filter and the
variable. The `eumdac` skill owns authentication, search and download.

Prerequisites for the snippet below: `xarray`, `netCDF4` (or `h5netcdf`) and `dask`, which `open_mfdataset` needs.

## Pick the inputs

```python
COLLECTION = "EO:EUM:DAT:0874"   # from the records table in SKILL.md
PREFIX = "SALmm"                 # product code plus time-step code; the filename filter is f"{PREFIX}*"
VARIABLE = "blue_sky_albedo_all_mean"
```

## Hand off to eumdac

Ask the `eumdac` skill to authenticate, search `COLLECTION` with the filename filter `SALmm*` and the period, and
download. Its download gate applies: product count, total size, destination, free space and the user's
authorisation. Do not write credential, search or download code here.

## Open the downloaded files

Run this only on files already present in the directory the `eumdac` skill reports.

```python
import pathlib

import xarray as xr

download_dir = pathlib.Path("<directory-reported-by-eumdac>")
ds = xr.open_mfdataset(sorted(download_dir.glob(f"{PREFIX}*.nc")), combine="by_coords")
subset = ds[VARIABLE].sel(lat=slice(-5, 20), lon=slice(-70, -20))
```

## Adapt it

- For the long IASI and MHS filenames, set `PREFIX` to a pattern such as `*METOPB+O3`; the glob appends `*`.
- If a download is a zip archive, extract the `.nc` entry before opening it.
- For SEVIRI Rapid Scan AMVs, pass `group="wind_ir108"` (or another channel group) to `open_dataset`.
- EPS native records (ASCAT, AVHRR AMVs 0151 and 0152, IASI L1C) are not netCDF: this template does not open them.
- If latitude is stored in descending order, reverse the slice bounds.
