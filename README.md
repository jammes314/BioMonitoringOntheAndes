# BioMonitoringOnTheAndes

A research-oriented repository focused on environmental and spectral analysis workflows for Andean ecosystem monitoring using Google Earth Engine, Sentinel-2 satellite imagery, and Python-based data processing.

---

## Overview

This project develops a reproducible workflow for extracting satellite-based environmental indicators over an Andean region of interest. The current implementation uses Sentinel-2 Surface Reflectance imagery from Google Earth Engine to generate raw spectral datasets sampled from a polygonal study area.

The workflow is designed to support future ecological monitoring, vegetation analysis, biomass proxy estimation, and machine learning experiments.

---

## Current Implementation

The current data collection notebook performs satellite data extraction using:

- Google Earth Engine
- Geemap
- Sentinel-2 Surface Reflectance Harmonized imagery
- Python data processing with Pandas
- A polygon shapefile defining the region of interest

The script loads a study area from a shapefile named:

```text
acha_poligono.shp
```

Then it creates an output folder called:

```text
RawData/
```

where the extracted CSV files are saved.

---

## Data Collection Workflow

The implemented workflow follows these steps:

1. Defines the spectral bands and vegetation/environmental indices used for analysis.
2. Loads the region of interest from a shapefile using `geemap.shp_to_ee`.
3. Generates dates from `2015-01-01` to `2026-03-31` with a 5-day interval.
4. For each 5-day window, searches for available Sentinel-2 images over the study region.
5. Creates a median composite from all images available in that time window.
6. Clips the composite image to the region of interest.
7. Computes spectral indices such as NDVI, NDMI, and BSI.
8. Samples representative pixels from the study area.
9. Saves each valid extraction as a CSV file in the `RawData/` directory.

---

## Spectral Bands and Indices

The extracted dataset includes the following Sentinel-2 bands:

```text
B1, B2, B3, B4, B5, B6, B7, B8, B8A, B9, B11, B12
```

It also includes the following calculated indices:

```text
NDVI, NDMI, BSI
```

### NDVI

The Normalized Difference Vegetation Index is calculated using:

```text
NDVI = (B8 - B4) / (B8 + B4)
```

NDVI is commonly used to estimate vegetation greenness and photosynthetic activity.

### NDMI

The Normalized Difference Moisture Index is calculated using:

```text
NDMI = (B8 - B11) / (B8 + B11)
```

NDMI is useful for analyzing vegetation water content and moisture conditions.

### BSI

The Bare Soil Index is calculated using:

```text
BSI = ((B11 + B4) - (B8 + B2)) / ((B11 + B4) + (B8 + B2))
```

BSI helps identify exposed soil and areas with low vegetation cover.

---

## Output Data

For each valid date, the script generates a CSV file with the following naming format:

```text
dataset_satellite_raw_YYYY-MM-DD.csv
```

Each CSV file contains sampled pixel values from the region of interest, including spectral bands, calculated indices, geometry information, and a cloud percentage placeholder.

Example output:

```text
RawData/dataset_satellite_raw_2019-06-15.csv
```

---

## Repository Structure

```text
BioMonitoringOntheAndes/
│
├── ControlCase.ipynb
├── TricosineEvaluationCase.ipynb
├── DataCollection.ipynb
│
├── data/
│   ├── sample/
│   └── .gitkeep
│
├── README.md
├── IMPLEMENTATION_NOTES.md
└── .gitignore
```

---

## Current Status

This repository is currently under active development.

At the moment, the project includes:

- Satellite data extraction from Sentinel-2
- Temporal sampling from 2015 to 2026
- Computation of NDVI, NDMI, and BSI
- CSV generation for future analysis
- Initial notebooks for control and tricosine evaluation cases

Raw datasets are not included in the repository because they may be large and are still being processed.

---

## Technologies

- Python
- Jupyter Notebook
- Google Earth Engine
- Geemap
- Pandas
- Sentinel-2 Surface Reflectance data

---

## Future Work

Planned additions include:

- Improved cloud filtering and cloud percentage estimation
- Data cleaning and preprocessing scripts
- Consolidated dataset generation
- Exploratory data analysis
- Biomass proxy estimation
- Machine learning models for ecological monitoring
- Complete methodological documentation

---

## Author

Developed by Jammes Asero.

---

## License

This project is currently intended for academic and research purposes. Further licensing details will be added in future releases.
