# Characterizing Bolide Signatures in GOES GLM Level-2 Data Using the NEO-Bolide Catalog

**Final Project Summary.**  
This project characterizes bolide (bright meteor) signatures in GOES Geostationary Lightning Mapper (GLM) Level-2 LCFA data using the NEO-Bolide catalog as labeled positives, extracting simple spatiotemporal and radiometric features. We compare these features against matched lightning “negative” windows and present visual case studies to highlight how bolide tracks may (or may not) differ from storm clusters.

## Team
- **Xueyicheng Xu**

---

## Background
The GOES GLM instrument continuously observes optical emissions associated with lightning activity, producing Level-2 Lightning Cluster-Filter Algorithm (LCFA) products (events, groups, flashes). Bolides (bright meteors) can also generate transient optical signatures that may appear in GLM detections but differ from typical lightning in their motion, spatial extent, and radiometric time evolution. A curated bolide catalog provides an opportunity to systematically study these signatures and build interpretable comparisons to lightning activity.

## Problem Statement / Objectives
**Goal:** Identify and characterize spatiotemporal and radiometric patterns in GLM Level-2 LCFA detections associated with cataloged bolides, and compare them against lightning activity windows.

**Key questions:**
1. Which simple, interpretable features best separate bolide windows from lightning windows?
2. How consistent are bolide signatures across events (duration, motion, spatial spread, energy accumulation/decay)?
3. In what scenarios do bolide signatures resemble storm clusters, and where do they clearly diverge?

## Datasets
1. **GOES GLM Level-2 LCFA (events / groups / flashes)**  
   - NOAA archives mirrored on Google Cloud:  
     - Example Directory: `gs://gcp-public-data-goes-16/GLM-L2-LCFA/2018/352/`  

2. **NEO-Bolide (CNEOS/JPL) catalog for positive event times/locations**  
   - https://cneos.jpl.nasa.gov/fireballs/  
   - API: https://ssd-api.jpl.nasa.gov/fireball.api

3. **References (methods + prior work)**
   - An Algorithmic Approach for Detecting Bolides with the Geostationary Lightning Mapper (Sensors, 2019)  
     https://www.mdpi.com/1424-8220/19/5/1008
   - Automated bolide detection pipeline for GOES GLM (Icarus, 2021)  
     https://www.sciencedirect.com/science/article/pii/S0019103521002451
   - GOES GLM, biased bolides, and debiased distributions (Icarus, 2023)  
     https://www.sciencedirect.com/science/article/pii/S0019103523004220

## Tools / Packages
Planned primary stack:
- **Python** + **Jupyter**
- Data + computation:
  - `numpy`, `pandas`, `scipy`
  - `xarray` (NetCDF handling), `netCDF4` (I/O)
  - `dask`
- Visualization:
  - `matplotlib`
  - `cartopy` / `pyproj`

## Planned Methodology / Approach
### 1) Build the labeled event set (positives)
- Parse NEO-Bolide catalog entries: event time (UTC), lat/lon, energy/metadata.
- For each bolide:
  - Extract GLM files overlapping a time window around the event from NEO database.
  - Download required GLM LCFA files (events/groups/flashes).

### 2) Define analysis windows
- **Positive window:** around each bolide time and (optionally) spatially centered near the catalog location.
- **Negative windows:** matched “controls” drawn from nearby times/regions with lightning activity.
  - Matching Criteria:
    - Similar local time
    - Same approximate region
    - Similar lightning rate

### 3) Extract interpretable features
Compute features for each window from LCFA products (events/groups/flashes). Example feature families:

### 4) Compare bolides vs lightning controls

### 5) Case studies (visual side-by-side)

## Expected Outcomes
- A reproducible pipeline to:
  - fetch GLM LCFA files around cataloged events,
  - generate windowed feature tables for positives and controls,
  - produce comparison plots and case-study figures.
- A feature dataset with clear documentation.
- A short final notebook summarizing results and representative examples.

## Repo Organization (planned)
- `src/` — core code (download, parsing, feature extraction)
- `notebooks/` — exploratory analysis + figures
- `docs/` — feature definitions, notes, meeting logs
- `figures/` — exported plots (tracked or generated)

## Milestones (editable)
- [ ] Week 1: Data access + event-to-file mapping + basic parsing
- [ ] Week 2: Feature extraction + first positive/negative comparisons
- [ ] Week 3: Case studies + finalized plots + write-up

## References
- Sensors (2019): https://www.mdpi.com/1424-8220/19/5/1008  
- Icarus (2021): https://www.sciencedirect.com/science/article/pii/S0019103521002451  
- Icarus (2023): https://www.sciencedirect.com/science/article/pii/S0019103523004220  
- NEO-Bolide / CNEOS: https://cneos.jpl.nasa.gov/fireballs/  
- GLM LCFA archive (example): https://console.cloud.google.com/storage/browser/gcp-public-data-goes-16/GLM-L2-LCFA/2018/352
