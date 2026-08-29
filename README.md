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
| [05 Rainfall and Soil](notebooks/05_Rainfall_%26_Soil.ipynb) | Rainfall and soil conditioning factors | Complete |
| [06 Feature Harmonisation](notebooks/06_Feature_Harmonization.ipynb) | Common CRS, resolution, extent, alignment, NoData handling, masking, and predictor-table generation | Complete |
| [07 Exploratory Analysis and Factor Selection](notebooks/07_Exploratory_Analysis_%26_Factor.ipynb) | Distributions, correlations, multicollinearity, temporal consistency, and predictor selection | Complete |
| [08 Flood Susceptibility Model](notebooks/08_Flood_Susceptibility_Model.ipynb) | Machine-learning susceptibility modelling | Planned |
| [09 Validation](notebooks/09_Validation.ipynb) | Independent validation and model performance assessment | Planned |
| [10 Temporal Analysis](notebooks/10_2006-2016-2026_Analysis.ipynb) | Temporal comparison of susceptibility and conditioning factors | Planned |
| [11 Final Results and Figures](notebooks/11_Final_Results_%26_Figures.ipynb) | Final maps, figures, tables, and interpretation | Planned |

## Notebook 06: Feature Harmonisation (Completed)

Notebook 06 is the current completed checkpoint for the model-preparation stage. It established the common 250 m modelling grid, harmonised the study predictors to the same CRS, extent, resolution, and alignment, applied the study-area mask, checked common valid-cell coverage, and generated the final year-specific predictor rasters and tables required for downstream analysis.

### Notebook 06 workflow

- Harmonised continuous conditioning rasters to the common 250 m grid in EPSG:32644.
- Harmonised LULC, rainfall, and soil rasters for 2003, 2014, and 2025.
- Masked all harmonised rasters to the Lucknow study area.
- Verified that all masked predictors share the same spatial grid and valid-cell structure.
- Created the final predictor tables used for later exploratory analysis and modelling.

### Notebook 06 outputs and save locations

#### Harmonised rasters

All harmonised rasters are stored in [data/processed/notebook_06/harmonised](data/processed/notebook_06/harmonised):

- Continuous predictors: [Elevation_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/Elevation_250m_EPSG32644.tif), [Slope_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/Slope_250m_EPSG32644.tif), [Flow_Accumulation_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/Flow_Accumulation_250m_EPSG32644.tif), [River_Distance_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/River_Distance_250m_EPSG32644.tif), [Drainage_Density_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/Drainage_Density_250m_EPSG32644.tif)
- LULC rasters: [LULC_2003_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/lulc/LULC_2003_250m_EPSG32644.tif), [LULC_2014_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/lulc/LULC_2014_250m_EPSG32644.tif), [LULC_2025_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/lulc/LULC_2025_250m_EPSG32644.tif)
- Rainfall rasters: [CHIRPS_monsoon_rainfall_2003_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/rainfall/CHIRPS_monsoon_rainfall_2003_250m_EPSG32644.tif), [CHIRPS_monsoon_rainfall_2014_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/rainfall/CHIRPS_monsoon_rainfall_2014_250m_EPSG32644.tif), [CHIRPS_monsoon_rainfall_2025_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/rainfall/CHIRPS_monsoon_rainfall_2025_250m_EPSG32644.tif)
- Soil rasters: [Clay_0-5cm_percent_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/soil/Clay_0-5cm_percent_250m_EPSG32644.tif), [Sand_0-5cm_percent_250m_EPSG32644.tif](data/processed/notebook_06/harmonised/soil/Sand_0-5cm_percent_250m_EPSG32644.tif)

#### Masked rasters

The study-area masked predictor rasters are stored in [data/processed/notebook_06/masked](data/processed/notebook_06/masked):

- [Elevation_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Elevation_250m_EPSG32644_masked.tif)
- [Slope_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Slope_250m_EPSG32644_masked.tif)
- [Flow_Accumulation_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Flow_Accumulation_250m_EPSG32644_masked.tif)
- [River_Distance_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/River_Distance_250m_EPSG32644_masked.tif)
- [Drainage_Density_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Drainage_Density_250m_EPSG32644_masked.tif)
- [Clay_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Clay_250m_EPSG32644_masked.tif)
- [Sand_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Sand_250m_EPSG32644_masked.tif)
- [LULC_2003_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/LULC_2003_250m_EPSG32644_masked.tif)
- [LULC_2014_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/LULC_2014_250m_EPSG32644_masked.tif)
- [LULC_2025_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/LULC_2025_250m_EPSG32644_masked.tif)
- [Rainfall_2003_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Rainfall_2003_250m_EPSG32644_masked.tif)
- [Rainfall_2014_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Rainfall_2014_250m_EPSG32644_masked.tif)
- [Rainfall_2025_250m_EPSG32644_masked.tif](data/processed/notebook_06/masked/Rainfall_2025_250m_EPSG32644_masked.tif)

#### Predictor tables

The final predictor tables are saved in [data/processed/notebook_06/predictors_table](data/processed/notebook_06/predictors_table):

- [predictors_2003_250m_EPSG32644.tif](data/processed/notebook_06/predictors_table/predictors_2003_250m_EPSG32644.tif)
- [predictors_2014_250m_EPSG32644.tif](data/processed/notebook_06/predictors_table/predictors_2014_250m_EPSG32644.tif)
- [predictors_2025_250m_EPSG32644.tif](data/processed/notebook_06/predictors_table/predictors_2025_250m_EPSG32644.tif)

These rasters are the harmonised predictor stack inputs prepared for the next stage of exploratory analysis and modelling.

## Notebook 07: Exploratory Analysis and Factor Selection (Completed)

Notebook 07 completed the statistical screening phase for the harmonised 250 m predictor stack. It reviewed the distribution of continuous predictors, checked temporal consistency across 2003, 2014, and 2025, quantified pairwise relationships with Pearson correlation, and assessed multicollinearity using VIF diagnostics to support the final model-ready predictor set.

### Notebook 07 workflow

- Inspect distribution shapes for elevation, slope, river distance, flow accumulation, drainage density, rainfall, clay, and sand.
- Compute year-specific Pearson correlation matrices for the candidate predictors.
- Evaluate multicollinearity using VIF across the static and dynamic predictor sets.
- Compare rainfall and static-predictor temporal consistency across the three study years.
- Save a final summary of the model-eligible predictor dataset used for downstream susceptibility modelling.

### Notebook 07 outputs and save locations

#### Figures

- [Pearson correlation matrix, 2003](outputs/figures/notebook_07/correlation/pearson_correlation_2003.png)
- [Pearson correlation matrix, 2014](outputs/figures/notebook_07/correlation/pearson_correlation_2014.png)
- [Pearson correlation matrix, 2025](outputs/figures/notebook_07/correlation/pearson_correlation_2025.png)
- [Static predictor correlation matrix](outputs/figures/notebook_07/correlation/static_predictor_pearson_correlation.png)
- [Elevation distribution](outputs/figures/notebook_07/distributions/Elevation_distribution.png)
- [Slope distribution](outputs/figures/notebook_07/distributions/Slope_distribution.png)
- [River distance distribution](outputs/figures/notebook_07/distributions/River_Distance_distribution.png)
- [Flow accumulation distribution](outputs/figures/notebook_07/distributions/Flow_Accumulation_distribution.png)
- [Drainage density distribution](outputs/figures/notebook_07/distributions/Drainage_Density_distribution.png)
- [Rainfall distribution, 2003-2025](outputs/figures/notebook_07/distributions/Rainfall_distribution_2003_2014_2025.png)

#### Tables

- [Continuous predictor descriptive statistics](outputs/tables/notebook_07/continuous_predictor_descriptive_statistics_2003_2014_2025.csv)
- [Multicollinearity summary](outputs/tables/notebook_07/diagnostics/predictor_relationship_multicollinearity_summary.csv)
- [VIF diagnostics, 2003](outputs/tables/notebook_07/vif/predictor_vif_2003.csv)
- [VIF diagnostics, 2014](outputs/tables/notebook_07/vif/predictor_vif_2014.csv)
- [VIF diagnostics, 2025](outputs/tables/notebook_07/vif/predictor_vif_2025.csv)
- [Static predictor VIF diagnostics](outputs/tables/notebook_07/vif/static_predictor_vif.csv)
- [Rainfall temporal consistency](outputs/tables/notebook_07/temporal_consistency/rainfall_temporal_consistency.csv)
- [Final predictor dataset summary](outputs/tables/notebook_07/final_summary/final_predictor_dataset_summary.csv)

These outputs mark Notebook 07 as the completed exploratory-analysis checkpoint that prepared the final predictor set for model calibration.

## Notebook 04: LULC Analysis

Notebook 04 processed Landsat Collection 2 Level-2 imagery for:

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
- [CHIRPS monsoon rainfall statistics](outputs/tables/rainfall_statistics/CHIRPS_monsoon_rainfall_statistics_2003_2014_2025.csv)
- [SoilGrids soil statistics](outputs/tables/Soil_statistics/SoilGrids_soil_statistics_0-5cm.csv)

### Figures

- [LULC classification comparison](outputs/figures/notebook_04/LULC_RF_classification_2003_2014_2025.png)
- [LULC temporal change](outputs/figures/notebook_04/LULC_temporal_change_2003_2014_2025.png)
- [Water diagnostic](outputs/figures/notebook_04/LULC_RF_water_diagnostic_2003_2014_2025.png)
- [Feature importance, 2003](outputs/figures/notebook_04/RF_feature_importance_2003.png)
- [Feature importance, 2014](outputs/figures/notebook_04/RF_feature_importance_2014.png)
- [Feature importance, 2025](outputs/figures/notebook_04/RF_feature_importance_2025.png)
- [CHIRPS rainfall quality assessment](outputs/figures/notebook_05/CHIRPS_monsoon_rainfall_QA_2003_2014_2025.png)
- [CHIRPS rainfall statistics](outputs/figures/notebook_05/CHIRPS_monsoon_rainfall_statistics_2003_2014_2025.png)
- [SoilGrids clay and sand comparison](outputs/figures/notebook_05/SoilGrids_clay_sand_0-5cm_2003_2014_2025.png)
- [SoilGrids statistical analysis](outputs/figures/notebook_05/SoilGrids_statistical_analysis_0-5cm.png)
- [Notebook 07 Pearson correlation, 2003](outputs/figures/notebook_07/correlation/pearson_correlation_2003.png)
- [Notebook 07 Pearson correlation, 2014](outputs/figures/notebook_07/correlation/pearson_correlation_2014.png)
- [Notebook 07 Pearson correlation, 2025](outputs/figures/notebook_07/correlation/pearson_correlation_2025.png)
- [Notebook 07 static predictor correlation](outputs/figures/notebook_07/correlation/static_predictor_pearson_correlation.png)
- [Notebook 07 distribution overview](outputs/figures/notebook_07/distributions/Rainfall_distribution_2003_2014_2025.png)

### Rainfall and Soil Rasters

- [CHIRPS monsoon rainfall rasters](data/processed/notebook_05/rainfall/)
- [SoilGrids clay and sand rasters](data/processed/notebook_05/soil/)

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

Notebooks 01-06 are complete and quality checked. Notebook 06 established the common 250 m modelling grid, harmonised the predictor rasters to a consistent study-area grid in EPSG:32644, applied the study-area mask, assessed common valid-cell coverage, and generated the final predictor stacks for 2003, 2014, and 2025.

The completed Notebook 06 .tif files are saved under [data/processed/notebook_06/](data/processed/notebook_06/), with subfolders for harmonised rasters, masked rasters, and predictor tables, and figures are saved under [outputs/figures/notebook_06/](outputs/figures/notebook_06/). The next implementation stage is Notebook 07, covering exploratory analysis and predictor relationships.
