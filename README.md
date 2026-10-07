# Glacier Change Projections for the Karambar Basin (OGGM)

Projecting the future volume, area and meltwater runoff of glaciers in the upper Karambar / Ishkoman valley (Gilgit-Baltistan, Pakistan) under CMIP6 climate scenarios using the **Open Global Glacier Model (OGGM)**.

## Study area

- **15 glaciers** from the Randolph Glacier Inventory (RGI v6, region 14 – South Asia West), about **267 km²** of ice in total
- Includes the Karambar, Chhateboi, Chillinji, Koz Yaz and Pekhin glaciers
- Glacier attributes (ID, area, terminus type, coordinates) are in [`gdirs_data.csv`](gdirs_data.csv)
- Interactive outline map: [`glacier_map.html`](glacier_map.html)

## Method

1. **Glacier directories:** initialise OGGM with RGI outlines, DEM and historical climate for each glacier
2. **Ice thickness inversion:** estimate present-day ice thickness and bed topography
3. **Future runs:** drive the dynamical model with **5 CMIP6 GCMs** × **3 SSP scenarios**
   - GCMs: GFDL-ESM4, IPSL-CM6A-LR, MPI-ESM1-2-HR, MRI-ESM2-0, UKESM1-0-LL
   - Scenarios: SSP1-2.6, SSP3-7.0, SSP5-8.5
4. **Ensemble analysis:** merge all GCM × scenario runs into one NetCDF and compute the median, minimum and maximum across GCMs for:
   - total glacier volume
   - glacier area
   - off-glacier meltwater runoff

## Repository structure

| File | Purpose |
|---|---|
| `RGI7_karambar.ipynb`, `PROjection_5 glacier.ipynb` | Set up glacier directories and run GCM × SSP projections |
| `ice_thickness_final_*.ipynb` | Ice thickness inversion (all glaciers / Karambar / Chhateboi) |
| `Glacier_Volume.ipynb` | Volume projections and ensemble spread |
| `Glacier_area.ipynb` | Area change projections |
| `Glacier_Runoff.ipynb` | Meltwater runoff projections |
| `analysis.ipynb` | Combined analysis and figures |
| `data/run_output_*.nc` | Raw OGGM output per GCM and scenario |
| `merged_GCM_projections.nc` | Merged ensemble dataset |
| `GCM_projections_aligned.csv` | Tabular export of projections |
| `Old/` | Earlier exploratory notebooks |

## Run it yourself

```bash
conda create -n oggm_env -c oggm -c conda-forge oggm
conda activate oggm_env
pip install seaborn
jupyter lab
```

Run `RGI7_karambar.ipynb` first to generate the projections, then the volume, area and runoff notebooks.

> Some notebooks load results from a local absolute path (`/home/usman/...`). Change it to `merged_GCM_projections.nc` in the repo root before running them.

## Tools

Python · OGGM · xarray · NumPy · pandas · Matplotlib · Seaborn · NetCDF

## Author

**Muhammad Shahid Usman**, Geospatial Data Analyst & Spatial Data Scientist
[Portfolio](https://muhammadshahidusman.github.io/) · [GitHub](https://github.com/Muhammadshahidusman)
