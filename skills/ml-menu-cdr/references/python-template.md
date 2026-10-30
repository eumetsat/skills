# Python template

Use this template when the user wants code. It needs `eumdac` 3.1.1, `xarray`, and `netCDF4` or `h5netcdf`, plus
Data Store credentials in `~/.eumdac` (set up through the `eumdac` skill, never in the script).

The download loop is a bulk download. Before running it, follow the `eumdac` skill's download gate: report the
product count, total size, free space and destination, and wait for the user's authorisation.

```python
import datetime as dt
import pathlib

import eumdac
import xarray as xr
from eumdac.config import get_credentials_path

COLLECTION = "EO:EUM:DAT:0874"   # from the records table in SKILL.md
PREFIX = "SALmm"                 # product code plus time-step code
VARIABLE = "blue_sky_albedo_all_mean"
START, END = dt.datetime(2020, 6, 1), dt.datetime(2020, 7, 1)
OUT = pathlib.Path("<destination-dir>")

token = eumdac.AccessToken(get_credentials_path().read_text().strip().split(","))
collection = eumdac.DataStore(token).get_collection(COLLECTION)
products = collection.search(dtstart=START, dtend=END, title=f"{PREFIX}*")
print(f"{products.total_results} products, {sum(p.size for p in products) / 1024**2:.2f} GB")

# Run the part below only after the user authorises the download.
OUT.mkdir(parents=True, exist_ok=True)
for product in products:
    with product.open() as src, open(OUT / src.name, "wb") as dst:
        dst.write(src.read())

ds = xr.open_mfdataset(sorted(OUT.glob(f"{PREFIX}*.nc")), combine="by_coords")
subset = ds[VARIABLE].sel(lat=slice(-5, 20), lon=slice(-70, -20))
```

## Adapt it

- Replace `COLLECTION`, `PREFIX` and `VARIABLE` from the records table in `SKILL.md` or [records.md](records.md). For
  the long IASI and MHS filenames, set `PREFIX` to a pattern such as `*METOPB+O3`; the search and the file glob append `*`.
- `title` is the Python name of the CLI's `--filename` filter. If the collection rejects it, print
  `collection.search_options` and filter the results on `str(product)` instead.
- If a download is a zip archive, extract the `.nc` entry before opening it.
- For SEVIRI Rapid Scan AMVs, pass `group="wind_ir108"` (or another channel group) to `open_dataset`.
- EPS native records (ASCAT, AVHRR AMVs 0151 and 0152, IASI L1C) are not netCDF: this template does not open them.
- If latitude is stored in descending order, reverse the slice bounds.
- For long periods, search and download one month at a time, retry failed products, and write the subset to Zarr
  (`subset.to_zarr(...)`) so later analyses open one store instead of thousands of files.
