# Flood Susceptibility Assessment of the Gomti River-Influenced Lucknow Region

A GIS, remote sensing, and machine-learning project for analysing flood-conditioning factors and land-use/land-cover change around Lucknow, Uttar Pradesh, India.

## Project Overview

The project builds a reproducible spatial workflow for the Gomti River-influenced Lucknow region. It combines:

- Study-area and river-network data
- DEM-derived terrain factors
- Hydrological and drainage factors
- Landsat surface-reflectance imagery
- Rainfall and soil data
- Land-use/land-cover classification
- Raster harmonisation and exploratory analysis
- Machine-learning flood-susceptibility modelling
- Model validation and temporal comparison

The work is organised as sequential Jupyter notebooks so that each stage can be inspected, rerun, and validated independently.

## Study Area

The study area covers Lucknow and a 20 km surrounding analysis zone, with the Gomti River network providing the primary hydrological context.

Key spatial data prepared in Notebook 01 include:

- Gomti River network from HydroRIVERS
- HydroBASINS Level-12 basin context
- Lucknow city boundary
- Lucknow 20 km search-area geometry

The selected Gomti river network uses HydroRIVERS identifier `MAIN_RIV = 41067217` and contains 160 reaches. The network is associated with 34 Level-12 hydrological units, six of which intersect the Lucknow city boundary.

Project spatial processing uses UTM Zone 44N, `EPSG:32644`, unless a notebook documents a source-specific CRS transformation.

## Workflow

```text
01 Study Area and Spatial Data
   ->
02 DEM and Terrain
   ->
03 River and Hydrological Factors
   ->
04 Land Use / Land Cover
   ->
05 Rainfall and Soil
   ->
06 Feature Harmonisation
   ->
07 Exploratory Analysis and Factor Selection
   ->
08 Flood Susceptibility Model
   ->
09 Validation
   ->
10 Temporal Analysis
   ->
11 Final Results and Figures
```

## Notebook Guide

| Notebook | Focus | Status |
| --- | --- | --- |
| [01 Study Area and Spatial Data](notebooks/01_Study_Area_%26_Spatial_Data.ipynb) | Study boundary, Gomti River network, HydroBASINS context, and spatial framework | Complete |
| [02 DEM and Terrain](notebooks/02_DEM_%26_Terrain.ipynb) | DEM preparation and terrain-derived variables | Complete |
| [03 River and Hydrological Factors](notebooks/03_River_%26_Hydrological_Factors.ipynb) | River distance, drainage network, flow accumulation, and drainage density | Complete |
| [04 Land Use and Land Cover](notebooks/04_Land_Use_Land_Cover.ipynb) | Landsat processing, spectral indices, Random Forest LULC classification, and temporal change | Complete |
| [05 Rainfall and Soil](notebooks/05_Rainfall_%26_Soil.ipynb) | Rainfall and soil conditioning factors | Planned |
| [06 Feature Harmonisation](notebooks/06_Feature_Harmonization.ipynb) | Common CRS, resolution, extent, alignment, and NoData handling | Planned |
| [07 Exploratory Analysis and Factor Selection](notebooks/07_Exploratory_Analysis_%26_Factor.ipynb) | Distributions, correlations, multicollinearity, and predictor selection | Planned |
| [08 Flood Susceptibility Model](notebooks/08_Flood_Susceptibility_Model.ipynb) | Machine-learning susceptibility modelling | Planned |
| [09 Validation](notebooks/09_Validation.ipynb) | Independent validation and model performance assessment | Planned |
| [10 Temporal Analysis](notebooks/10_2006-2016-2026_Analysis.ipynb) | Temporal comparison of susceptibility and conditioning factors | Planned |
| [11 Final Results and Figures](notebooks/11_Final_Results_%26_Figures.ipynb) | Final maps, figures, tables, and interpretation | Planned |

## Notebook 04: LULC Analysis

Notebook 04 is the current completed checkpoint. It processes Landsat Collection 2 Level-2 imagery for:

- 2003: Landsat 7 ETM+
- 2014: Landsat 8 OLI
- 2025: Landsat 8/9 OLI

### Processing Steps

1. Identify sensor-specific spectral bands.
2. Apply the Collection 2 surface-reflectance transformation:

   `SR = DN * 0.0000275 - 0.2`

3. Mask fill, dilated-cloud, cirrus, cloud, cloud-shadow, and snow/ice QA flags.
4. Reproject the established study-area geometry to each raster CRS.
5. Calculate NDVI, NDBI, and MNDWI.
6. Build nine-feature stacks for each year.
7. Extract training pixels from manually prepared reference polygons.
8. Train one Random Forest classifier per observation year.
9. Classify the study area and calculate class-wise area statistics.

### LULC Classes

| Class ID | Class |
| ---: | --- |
| 1 | Water |
| 2 | Built-up |
| 3 | Vegetation |
| 4 | Agriculture |
| 5 | Bare/Open land |

### Classification Features

The nine predictor features are:

- Blue, Green, Red
- NIR, SWIR1, SWIR2
- NDVI, NDBI, MNDWI

All feature rasters were checked for matching CRS, 30 m resolution, dimensions, transform, and spatial extent.

### QA Coverage Within the Study Area

| Year | Usable pixels | Unusable pixels |
| ---: | ---: | ---: |
| 2003 | 99.76% | 0.24% |
| 2014 | 96.70% | 3.30% |
| 2025 | 87.78% | 12.22% |

### Random Forest Validation

| Year | Overall accuracy | Cohen's kappa | Macro F1 |
| ---: | ---: | ---: | ---: |
| 2003 | 93.96% | 0.9124 | 0.9173 |
| 2014 | 100.00% | 1.0000 | 1.0000 |
| 2025 | 98.13% | 0.9715 | 0.9654 |

The unusually high 2014 score should be interpreted cautiously and checked against sample design and spatial representativeness.

### LULC Change: 2003 to 2025

| Class | 2003 area (km2) | 2014 area (km2) | 2025 area (km2) | Net change (km2) | Change |
| --- | ---: | ---: | ---: | ---: | ---: |
| Agriculture | 242.7345 | 284.2821 | 238.6044 | -4.1301 | -1.70% |
| Bare/Open land | 1541.1078 | 1074.1275 | 609.9543 | -931.1535 | -60.42% |
| Built-up | 660.7764 | 1096.0542 | 1227.9150 | +567.1386 | +85.83% |
| Vegetation | 507.3426 | 410.7762 | 533.2608 | +25.9182 | +5.11% |
| Water | 23.9139 | 19.3266 | 8.5419 | -15.3720 | -64.28% |

These are LULC statistics only. They are not flood-susceptibility results.

## Outputs

### LULC Maps

- [LULC Random Forest map, 2003](outputs/lulc_maps/LULC_RF_2003.tif)
- [LULC Random Forest map, 2014](outputs/lulc_maps/LULC_RF_2014.tif)
- [LULC Random Forest map, 2025](outputs/lulc_maps/LULC_RF_2025.tif)

### Tables

- [LULC area statistics](outputs/tables/LULC_statistic/LULC_area_statistics_2003_2014_2025.csv)
- [LULC temporal change](outputs/tables/LULC_statistic/LULC_temporal_change_2003_2014_2025.csv)
- [Random Forest validation metrics](outputs/tables/RF_Validation/RF_validation_metrics.csv)
- [Random Forest classification reports](outputs/tables/RF_Validation/)
- [Feature-importance tables](outputs/tables/RF_Feature_Importance/)
- [Training samples](outputs/tables/LULC_training_samples/)

### Figures

- [LULC classification comparison](outputs/figures/notebook_04/LULC_RF_classification_2003_2014_2025.png)
- [LULC temporal change](outputs/figures/notebook_04/LULC_temporal_change_2003_2014_2025.png)
- [Water diagnostic](outputs/figures/notebook_04/LULC_RF_water_diagnostic_2003_2014_2025.png)
- [Feature importance, 2003](outputs/figures/notebook_04/RF_feature_importance_2003.png)
- [Feature importance, 2014](outputs/figures/notebook_04/RF_feature_importance_2014.png)
- [Feature importance, 2025](outputs/figures/notebook_04/RF_feature_importance_2025.png)

## Repository Structure

```text
GeoAI-Flood-Susceptibility/
├── data/
│   ├── processed/
│   ├── raw/
│   └── final
├── notebooks/
├── outputs/
│   ├── figures/
│   ├── lulc_maps/
│   └── tables/
├── requirements.txt
└── README.md
```

Large geospatial datasets and generated rasters may not be suitable for storage in a remote Git repository. Keep the local data layout consistent with the paths used by the notebooks.

## Environment Setup

Create and activate a virtual environment, then install the project dependencies:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Open the notebooks in VS Code with the `.venv` interpreter selected. Run the notebooks in order so that intermediate data and output directories are created before later stages use them.

## Reproducibility Notes

- Use the same CRS, resolution, extent, and pixel alignment when combining conditioning factors.
- Keep training and validation polygons independent to avoid spatial leakage.
- Treat masked pixels as NoData rather than valid land-cover observations.
- Record source-data dates, processing parameters, and model settings for every final result.
- Recheck the unusually high 2014 validation score before publication.

## Important Temporal Note

The original project concept used 2006, 2016, and 2026. The implemented Notebook 04 LULC workflow uses 2003, 2014, and 2025. Future notebooks and the final manuscript must use one temporal scheme consistently, or clearly document any deliberate change.

## Current Status

Notebook 04 is complete and quality checked. The next implementation stage is Notebook 05, covering rainfall and soil factors.
