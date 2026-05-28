# Pacific–Antarctic Ridge Meander Analysis

Code and supporting figures for:

> Liu, X., Yang, C., and Chen, Y. (2026).
> *Standing Meanders of the Antarctic Circumpolar Current: Evidence for
> Ridge-Controlled Eddy Saturation.*
> *Journal of Geophysical Research: Oceans.*
> https://doi.org/10.1029/2025JC023527

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![DOI](https://img.shields.io/badge/DOI-10.1029%2F2025JC023527-1f7ab7.svg)](https://doi.org/10.1029/2025JC023527)
[![Made with MATLAB](https://img.shields.io/badge/Made%20with-MATLAB-orange.svg?logo=mathworks&logoColor=white)](https://www.mathworks.com/products/matlab.html)

This repository provides the datasets, MATLAB functions, and figures used in
the analysis of standing meanders of the Antarctic Circumpolar Current over
the Pacific–Antarctic Ridge (PAR). The analyses combine satellite altimetry,
the Roemmich–Gilson Argo climatology, and CMEMS surface geostrophic
velocities to document meander position, width, and intensity together with
the associated eddy kinetic energy (EKE) over 1993–2023.

---

## Repository structure

```
southern-ocean-pacific-antarctic-ridge-meander-trends/
├── meander_loc_mon_1993_2023_mean_199303_202303/        Monthly mean meander
│                                                        positions, 1993–2023
├── meander_monthly_locations_north_south_boundaries/    North/south latitude
│                                                        boundaries of the meander
├── 01-PAR-Argo-Temperature-2004-2023-Build-4D-Cube.m
├── 02-CMEMS-Gyre-ADT-TimeSeries-Trend-1993-2023.m
├── 03-Mann_Kendall_Trend_Test.m
├── 04-PAR-CMEMS-EKE-Trend-Analysis-1993-2023.m
├── 05-Meander-Width-Speed-Trend-Decomposition.m
├── 06-Modified-Mann-Kendall-Trend-Test.m
├── 07-Plot-TimeSeries-With-Trend.m
├── 08-Theil-Sen-Slope.m
├── .gitignore
├── CITATION.cff                                          Machine-readable citation
├── LICENSE                                               MIT Licence
└── README.md                                             This file
```

---

## Scientific overview

Standing meanders of the Antarctic Circumpolar Current are persistent
zonal deviations of the jet that are anchored to bottom topography. The
Pacific–Antarctic Ridge meander is one of the largest of these features.
This study uses three decades of satellite altimetry, the Roemmich–Gilson
Argo climatology, and CMEMS surface geostrophic currents to document
1993–2023 trends in the meander's position, width, and along-jet speed,
and examines whether observed widening of the meander is consistent with
along-jet speed strengthening — a signature consistent with
ridge-controlled eddy saturation of the regional flow.

The repository is organised so that the data folders (described below)
hold the analysis inputs, and the numbered MATLAB scripts at the
repository root take those inputs through to the trend diagnostics and
figures that appear in the manuscript.

---

## Data folders

| Folder | Contents |
|---|---|
| `meander_loc_mon_1993_2023_mean_199303_202303/` | Monthly mean meander positions for 1993–2023 derived from altimetry with probability-based frontal detection. Used as the input to the trend and width-decomposition diagnostics. |
| `meander_monthly_locations_north_south_boundaries/` | North/south latitude boundaries of the meander at each longitude bin, enabling calculation of meander width and its variability across longitude. |

---

## Workflow

The MATLAB scripts are organised in numerical order. Each script reads the
data folders above and writes its own intermediate or figure outputs.

| Step | Script | Purpose |
|---|---|---|
| 01 | `01-PAR-Argo-Temperature-2004-2023-Build-4D-Cube.m` | Construct 4-D absolute temperature fields (time × lon × lat × pressure) from the Roemmich–Gilson Argo mean and anomalies (2004–2023), concatenate monthly NetCDF inputs, and save MATLAB datasets for downstream use. |
| 02 | `02-CMEMS-Gyre-ADT-TimeSeries-Trend-1993-2023.m` | Build an area-mean monthly ADT anomaly time series for the subtropical gyre (42°–38°S, 150°E–70°W), deseason it, and compute linear and non-parametric trends (Theil–Sen, Mann–Kendall, modified Mann–Kendall, OLS). |
| 03 | `03-Mann_Kendall_Trend_Test.m` | Classical Mann–Kendall test for monotonic trends; returns hypothesis decision, p-value, and S statistic. |
| 04 | `04-PAR-CMEMS-EKE-Trend-Analysis-1993-2023.m` | Concatenate CMEMS surface geostrophic velocity fields (1993–2023), derive eddy kinetic energy, map its 1993–2023 mean, estimate decadal trends, and extract section-based time series with Theil–Sen/Mann–Kendall diagnostics. |
| 05 | `05-Meander-Width-Speed-Trend-Decomposition.m` | Test whether observed meander widening is explained by along-jet speed strengthening; perform width–speed regression and decompose the width trend into explained and residual components. |
| 06 | `06-Modified-Mann-Kendall-Trend-Test.m` | Modified Mann–Kendall test (Hamed and Rao, 1998) with autocorrelation adjustment for robust trend significance on autocorrelated series. |
| 07 | `07-Plot-TimeSeries-With-Trend.m` | Generate publication-quality time-series plots with Theil–Sen slope lines and Mann–Kendall significance annotations. |
| 08 | `08-Theil-Sen-Slope.m` | Theil–Sen slope estimator (median of pairwise slopes); the robust trend slope estimator used throughout the repository. |

---

## Data availability

The original Roemmich–Gilson Argo climatology and CMEMS surface
geostrophic velocity products are publicly available and are not
redistributed in this repository. The monthly meander positions and
north/south boundaries that drive the trend diagnostics are provided in
the two data folders documented above, and are sufficient to reproduce
the figures in the manuscript.

Roemmich–Gilson Argo data can be obtained from
[SIO Argo Marine Atlas](https://sio-argo.ucsd.edu/RG_Climatology.html);
CMEMS satellite altimetry products can be obtained from the
[Copernicus Marine Service](https://data.marine.copernicus.eu/).

---

## Software environment

- MATLAB R2022a or later (development was on MATLAB R2023a).
- Required toolboxes: Statistics and Machine Learning Toolbox (for the
  parametric significance tests), Mapping Toolbox (for the geographic
  plots in step 07).

The scripts can be run interactively from the MATLAB IDE or from the
command line via `matlab -batch "run('01-PAR-Argo-Temperature-...m')"`.

---

## How to cite

If you use this code or the derived outputs, please cite the published
paper and this repository. A machine-readable `CITATION.cff` file is
provided in the repository root and is automatically rendered by
GitHub's "Cite this repository" button.

**Paper**

> Liu, X., Yang, C., and Chen, Y. (2026). Standing Meanders of the
> Antarctic Circumpolar Current: Evidence for Ridge-Controlled Eddy
> Saturation. *Journal of Geophysical Research: Oceans*.
> https://doi.org/10.1029/2025JC023527

**Repository (this release)**

> Liu, X., Yang, C., and Chen, Y. (2026). *Pacific–Antarctic Ridge
> Meander Analysis: code and supporting figures for "Standing Meanders
> of the Antarctic Circumpolar Current: Evidence for Ridge-Controlled
> Eddy Saturation"* (v1.0.0) [Software].
> https://github.com/xinlongliu0307/southern-ocean-pacific-antarctic-ridge-meander-trends/releases/tag/v1.0.0

---

## Licence

This repository is released under the [MIT Licence](LICENSE).

---

## Contact

Xinlong Liu  
Institute for Marine and Antarctic Studies, University of Tasmania,
Hobart, Tasmania, Australia  
xinlong.liu@utas.edu.au
