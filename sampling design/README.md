# SoilFER Technical Manual for Sampling Design

The *SoilFER Technical Manual for Sampling Design* provides general guidance on soil sampling design methodologies to ensure precision, reproducibility, and reliability in the collection of soil samples for digital soil mapping and monitoring.

## Brief Introduction

This folder contains materials to produce a Soil Sampling Design for the SoilFER Project, using a study case in Zambia as an example. The design applies a three-stage hierarchical hybrid method incorporating both probability and non-probability sampling for soil mapping and monitoring within the SoilFER framework.

The first hierarchical level selects the primary sampling units (PSUs) using covariate space coverage (CSC) sampling method based on environmental covariates at a 2km x 2km pixel resolution. Like the selection of PSUs, the second hierarchical level selects the secondary sampling units (SSUs) (i.e., 100m x 100m) using CSC sampling and a second set of environmental covariates. Lastly, the third hierarchical levels select the tertiary sampling units using simple random sampling without replacement. This implementation standardizes soil sampling methodologies across the various countries involved in the project.

## Folder "data" - Shapes (Shapefiles/Vectors)

The country boundaries, legacy data, country administrative boundaries (i.e., states and/or provinces), protected areas (e.g., national parks) and geology for this training can be downloaded from the [shapes folder](./data/shapes).

## Folder "data" - Rasters

The environmental covariates for this example can be downloaded from the [raster folder](./data/rasters). As for the second set of environmental covariates used to select the SSUs, they can be retrieved using the following codes in Google Earth Engine: 
1. [Terrain derivatives](https://code.earthengine.google.com/038b661e6a022e63ab46411df8ea688f)
2. [Sentinel imagery and indices](https://code.earthengine.google.com/42e997378198c2cc5d06b98150d90e93)
3. [Synthetic Bare Soil Image from Sentinel](https://code.earthengine.google.com/b87f87783a37b6664f0d927fdea19e57)

These variables can be harmonised using the R code [(prep_gee_highres_vars.R)](./scripts)

### Environmental Covariates - Climate, Remote Sensing, Land cover, and Topography

These covariates represent critical environmental factors influencing soil and landscape processes. Climate includes variables such as temperature, precipitation, and evapotranspiration. Remote sensing provides data on vegetation indices, surface temperature, and albedo. Land cover offers insights into vegetation and land use patterns, while topography encompasses elevation, slope, curvature, and terrain indices, all of which are essential for understanding spatial variability.

The file named **`covs_zam_clipped.tif`** contains the environmental variables retrieved from Google Earth Engine using the code in [`gee.txt`](./scripts/GEE). There are two ways to retrieve these variables:
1. By uploading data for the entire country using its ISO Alpha-3 code (e.g., `var ISO = ['ZMB'];`).
2. By using a shapefile with the country boundaries (e.g., `var shapefile = ee.FeatureCollection('projects/ee-soilfer/assets/your_shapefile');`).

### Environmental Covariates - Soil Climate

Soil climate refers to the Normalized Soil Moisture (NSM) factor, which relates to soil water content, precipitation, and evapotranspiration. These factors are essential for assessing soil moisture regimes, soil water availability, and soil-climate interactions.

Environmental variables related to soil climate can be generated using the codes in Google Earth Engine (GEE) [(gee_climate_vars)](./scripts/GEE) and R [(climate_vars.R)](./scripts). 

First of all, create a GEE account and upload the GEE code. Select the desired years, run the code, and upload the resulting files into the [raster folder](./data/rasters). Next, open the R code file [climate_vars.R](./scripts). Follow the provided instructions to calculate the traditional soil climate simulation model known as the [Newhall Simulation Model](https://github.com/ncss-tech/jNSMR).

The file named **`newhall_zam_clipped.tif`** contains these variables, so there is no need to generate them here.

### Land Use - Crops

Land cover data at 10 m or 100 m resolution can be retrieved using the [Hand-in-Hand Geospatial Platform](https://data.apps.fao.org/?lang=en) and Copernicus products via the [`gee.txt`](./scripts/GEE) code.

The crop layer consists of a single raster delineating the location of crops in the region of interest. This layer is named **`cropland_clipped_zmb_v1_epsg_3857.tif`**.

## Folder "scripts"

The R and GEE codes for this training can be downloaded from the [scripts folder](./data/scripts).

## Important Notes

- The three raster files (**cropland_clipped_zmb_v1_epsg_3857.tif**, **covs_zam_clipped.tif**, and **newhall_zam_clipped.tif**) **MUST** be stored in the `./data/rasters` folder. Alternatively, update the corresponding file paths in the R script.

- The R code is available in both `R` and `Rmd` files within the `/scripts` folder.

- All results generated by the scripts will be stored in the `/data/results` folder.
