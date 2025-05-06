# AE-project
The “Advancing Climate Data Integration in Agroecological Research” project, aims to improve the capacity of agroecological researchers and practitioners to integrate climate data into their work.

<details>
  <summary> Climate datasets documentation </summary>

  Documenting the datasets and packages is part of the project’s activities. The table below provides details on the datasets mentioned during user engagement interviews. 

# 1. Climate Hazards Group InfraRed Precipitation with Station data (CHIRPS)

## Overview

| Attribute                  | Description            |
| :------------------------- | :--------------------- |
| **Short Description**      | CHIRPS is a 35+ year quasi-global rainfall dataset blending satellite imagery and station data for high-resolution precipitation information. |
| **Provider/Source**        | Climate Hazards Center (CHC), University of California, Santa Barbara (UCSB) |
| **Homepage/Link**          | [https://www.chc.ucsb.edu/data/chirps](https://www.chc.ucsb.edu/data/chirps)   |
| **License/Terms of Use**   | Generally open for research and non-commercial use. |
| **Spatial Coverage**       | Quasi-global, 50°S to 50°N latitude, 180°W to 180°E longitude    |
| **Temporal Coverage**      | January 1, 1981, to near-present (updated frequently)           |
| **Spatial Resolution**     | 0.05° x 0.05° latitude/longitude (approximately 5 km x 5 km at the equator) |
| **Temporal Resolution**    | Daily, pentadal (5-day totals), dekadal (10-day totals), monthly aggregations  |
| **Key Variables**          | Precipitation (mm)   |

## Data Access and Format

| Attribute                      | Description                            |
| :----------------------------- | :------------------------------------- |
| **Access Methods** | Download via FTP/HTTP (CHC website), FEWS NET Data Portal, Google Earth Engine (GEE), potential intermediary APIs. |
| **Data Formats** | Primarily NetCDF (.nc), potentially GeoTIFF (.tif) for some derived products.  |
| **Data Organization** | By temporal resolution (daily, monthly, etc.), then by year within each resolution. NetCDF files contain multi-dimensional arrays (time, latitude, longitude, variable).  |
| **Potential Challenges** | Large file sizes, need for specific software libraries (e.g., `netCDF4`, `xarray`), potential missing data (handle fill values), awareness of data update frequency.  |

## Technical Details 

| Attribute                       | Description                                                    |
| :------------------------------ | :------------------------------------------------------------- |
| **File Naming Conventions**     | Typically includes product name (`chirps`), temporal resolution (`v2.0.daily`), year, and sometimes day or month (e.g., `chirps-v2.0.daily.1981.01.01.nc`).  |
| **Variable Names & Units** | Primary variable is usually `precip` (precipitation) with units of millimeters (`mm`). Verify metadata within the NetCDF files.  |
| **Coordinate Systems** | Latitude and longitude based on World Geodetic System 1984 (WGS 84) datum. Coordinate variables are typically named `lat` and `lon`. |
| **Data Processing** | Use libraries like `xarray`, `rioxarray`, `netCDF4` (Python) or `raster` (R) for NetCDF handling. Correctly handle latitude/longitude coordinates and the time dimension. Be aware of and manage missing data flags. Consider the need for data aggregation or resampling.   |

## API Information for Climate Datasets

| API Availability | Link to API Information    | How to Utilize        |
| :--------------- | :------------------------- | :-------------------- |
| No Direct API    | [Google Earth Engine API Docs](https://developers.google.com/earth-engine/api_docs) (if using GEE) <br> [R Package `chirps` CRAN](https://cran.r-project.org/package=chirps) | Access via Google Earth Engine API (if applicable). Download files and use libraries like `xarray` (Python) or `raster` (R). Explore R package `chirps`. |


## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                                                           |
| :------------------------------ | :-------------------------------------------------------------------- |
| **Potential Applications** | Rainfall pattern analysis, drought monitoring, extreme precipitation event analysis, climate risk assessment, crop yield modeling, water resource management, agroclimatic zoning, validation of local climate data.   |
| **Strengths for AE Research** | High spatial resolution for localized analysis, long temporal coverage for trend analysis, quasi-global coverage for broad studies, integration of satellite and station data for spatial completeness and accuracy. |
| **Limitations for AE Research** | Indirect satellite measurements with potential biases, does not include other crucial variables (temperature, solar radiation, etc.), spatial resolution might still be coarse for very localized microclimatic studies.  |

## Further Resources

| Resource Type             | Description/Link                                                       |
| :------------------------ | :--------------------------------------------------------------------- |
| **User Guides/Documentation** | Primary source is the CHC website: [https://www.chc.ucsb.edu/data/chirps](https://www.chc.ucsb.edu/data/chirps). Look for sections like "Documentation" or "About CHIRPS."     |
| **Community/Support** | No dedicated CHIRPS forum is likely. General remote sensing or climate data forums might have discussions. Contact the Climate Hazards Center directly for specific support inquiries via their website.       |

# 2. ERA5: ECMWF Reanalysis v5

## Overview

| Attribute                  | Description                             |
| :------------------------- | :-------------------------------------- |
| **Short Description** | ERA5 is the fifth generation ECMWF atmospheric reanalysis of the global climate, providing hourly estimates for a large number of atmospheric, land, and ocean climate variables.   |
| **Provider/Source** | European Centre for Medium-Range Weather Forecasts (ECMWF) |
| **Homepage/Link** | [https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/era5](https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/era5) |
| **License/Terms of Use** | Copernicus license. Registration with the Copernicus Data Space Ecosystem (CDSE) is required. See: [https://cds.climate.copernicus.eu/terms-and-conditions](https://cds.climate.copernicus.eu/terms-and-conditions).  |
| **Spatial Coverage** | Global         |
| **Temporal Coverage** | 1950 to near-present (updated daily)      |
| **Spatial Resolution** | 0.25° x 0.25° latitude/longitude (approximately 31 km x 31 km at the equator) for atmospheric variables. Other variables may have different resolutions.    |
| **Temporal Resolution** | Hourly. Monthly means are also available.  |
| **Key Variables** | Air temperature (various levels), precipitation (total, convective, large-scale), surface radiation (solar, thermal), wind speed and direction (various levels), soil moisture, evaporation, sea surface temperature, sea ice, and many more.   |

## Data Access and Format

| Attribute                      | Description                                           |
| :----------------------------- | :---------------------------------------------------- |
| **Access Methods** | Copernicus Data Space Ecosystem (CDSE) via Web Interface and CDS API (Python), ECMWF Data Catalogue (MARS), Cloud Platforms (AWS, GCP, Azure). CDSE is the recommended primary access point.   |
| **Data Formats** | Primarily GRIB (GRIdded Binary). Can be converted to other formats like NetCDF.   |
| **Data Organization** | By variable, by time (hourly/monthly), often separated by year. GRIB files contain gridded data with metadata. |
| **Potential Challenges** | Registration required, large dataset volume, GRIB format (requires specific libraries), vast number of variables (careful selection needed), potentially high computational demands for analysis. |

## Technical Details 

| Attribute                       | Description                                      |
| :------------------------------ | :----------------------------------------------- |
| **File Naming Conventions** | GRIB file names vary depending on the download method from CDSE. Typically include variable name, date, time, and other metadata. Refer to file metadata.       |
| **Variable Names & Units** | Variable names in GRIB are often abbreviated (ECMWF conventions). Units are in the metadata. Consult ECMWF/CDSE documentation.  |
| **Coordinate Systems** | Typically regular latitude-longitude grid. Projection and datum info in GRIB metadata.  |
| **Data Processing** | Use libraries like `cfgrib` or `eccodes` (Python) for GRIB. Explore CDS API for efficient download. Consider conversion to NetCDF. Implement spatial and temporal subsetting. Be mindful of unit conversions.   |

## API Information for Climate Datasets

| API Availability | Link to API Information    | How to Utilize         |
| :--------------- | :------------------------- | :--------------------- |
| Yes (CDSE API)   | [CDSE API Documentation](https://www.google.com/search?q=https://cds.climate.copernicus.eu/cdsapp%23\!/documentation/api-how-to)                             | Register on CDSE, install `cdsapi` Python library, follow documentation for making requests.  |
|                  | [CDSE Platform](https://cds.climate.copernicus.eu/)          |            |


## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                                     |
| :------------------------------ | :---------------------------------------------- |
| **Potential Applications** | Temperature analysis (growing degree days, frost risk, heat stress), precipitation analysis (drought monitoring, variability), evapotranspiration estimation, solar radiation assessment, wind patterns, soil moisture monitoring, extreme weather event analysis, climate change impact studies. |
| **Strengths for AE Research** | Comprehensive variable set, long temporal coverage (since 1950), global coverage, hourly resolution allows for detailed analysis, continuously updated.|
| **Limitations for AE Research** | Coarser spatial resolution than CHIRPS (may miss localized variations), reanalysis data (model-based with inherent uncertainties), complexity of access and format, potentially high computational demands.   |

## Further Resources

| Resource Type             | Description/Link                                     |
| :------------------------ | :--------------------------------------------------- |
| **Publications** | Search Google Scholar and the ECMWF website for ERA5 related publications.      |
| **User Guides/Documentation** | ECMWF website: [https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/era5](https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/era5). Copernicus Data Space Ecosystem documentation: [https://cds.climate.copernicus.eu/cdsapp#!/documentation](https://cds.climate.copernicus.eu/cdsapp#!/documentation).    |
| **Community/Support** | Copernicus Discourse forum: [https://community.copernicus.eu/](https://community.copernicus.eu/). ECMWF also provides support via their website. |

# 3. AgERA5: Hourly Reanalysis Data for Agriculture

## Overview

| Attribute                  | Description                                                |
| :------------------------- | :--------------------------------------------------------- |
| **Short Description** | AgERA5 is a reanalysis dataset specifically tailored for agricultural applications, produced by the European Centre for Medium-Range Weather Forecasts (ECMWF) in collaboration with the Copernicus Climate Change Service (C3S). It is based on the ERA5 dataset but includes additional variables and adjustments relevant for agriculture. |
| **Provider/Source** | European Centre for Medium-Range Weather Forecasts (ECMWF) / Copernicus Climate Change Service (C3S). |
| **Homepage/Link to Dataset** | [https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/agera5](https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/agera5) (This is the main ECMWF page; specific access might be through the Copernicus Data Space Ecosystem).   |
| **License and Terms of Use** | Likely the same as ERA5: Copernicus license. Registration with the Copernicus Data Space Ecosystem (CDSE) will be required. See: [https://cds.climate.copernicus.eu/terms-and-conditions](https://cds.climate.copernicus.eu/terms-and-conditions). |
| **Spatial Coverage** | Global, consistent with ERA5.      |
| **Temporal Coverage** | 1979 to near-present (updated daily with a delay).  |
| **Resolution** | **Spatial:** 0.1° x 0.1° latitude/longitude (approximately 10 km x 10 km at the equator). This is a higher spatial resolution than standard ERA5. <br>**Temporal:** Hourly.     |
| **Key Variables** | Includes all standard ERA5 variables, plus additional and enhanced variables relevant for agriculture, such as: <br> - Evapotranspiration (potential, actual) <br> - Soil water content (at various levels) <br> - Leaf area index (LAI) <br> - Fraction of absorbed photosynthetically active radiation (FAPAR) <br> - Crop-specific indicators |

## Data Access and Format

| Attribute                      | Description                                           |
| :----------------------------- | :---------------------------------------------------- |
| **Access Methods**             | Primarily through the Copernicus Data Space Ecosystem (CDSE) via the Web Interface and CDS API (Python). It might also be accessible through other platforms that host Copernicus data. Check the AgERA5 ECMWF page and the CDSE catalogue for the most up-to-date access methods.  |
| **Data Formats** | Likely GRIB (GRIdded Binary) format, consistent with ERA5. Conversion to other formats like NetCDF will likely be supported through CDSE tools or other software.  |
| **Data Organization** | Similar to ERA5: organized by variable, by time (hourly), and often separated by year. GRIB files contain the gridded data and associated metadata. The specific organization might differ slightly due to the additional agricultural variables. Consult the CDSE documentation.    |
| **Potential Challenges** | Registration with CDSE required, potentially large dataset volume (though higher resolution might mean larger files than standard ERA5 for the same area), GRIB format (requires specific libraries), understanding the specific agricultural variables and their units (refer to documentation), computational resources for analysis.  |

## Technical Details 

| Attribute                       | Description                                          |
| :------------------------------ | :--------------------------------------------------- |
| **File Naming Conventions** | Likely similar to ERA5 GRIB files but will include indicators for the AgERA5 product and the specific agricultural variables. Consult the CDSE catalogue and the metadata within the downloaded files for precise naming conventions.     |
| **Variable Names & Units** | Will include standard ERA5 variable names as well as specific names for the agricultural variables (e.g., `e`, `swvl1`, `lai`, `fapar`). Units will be specified in the GRIB metadata. Refer to the ECMWF and CDSE documentation for the definitions and units of the AgERA5 specific variables.  |
| **Coordinate Systems** | Likely the same regular latitude-longitude grid as ERA5 (WGS 84), but at the higher 0.1° resolution. Coordinate information will be in the GRIB metadata.       |
| **Data Processing** | Use GRIB decoding libraries (`cfgrib`, `eccodes` in Python). Utilize the CDS API for efficient data access. Consider converting to NetCDF for easier manipulation with libraries like `xarray`. Pay close attention to the specific units and definitions of the agricultural variables. Implement spatial and temporal subsetting to manage data volume.     |

## API Information for Climate Datasets

| API Availability | Link to API Information    | How to Utilize          |
| :--------------- | :------------------------- | :---------------------- |
| Yes (CDSE API)   | [CDSE API Documentation](https://www.google.com/search?q=https://cds.climate.copernicus.eu/cdsapp%23\!/documentation/api-how-to)                             | Register on CDSE, install `cdsapi` Python library, specify "agera5" dataset in requests.   |
|                  | [ECMWF AgERA5 Info](https://www.google.com/search?q=https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/agera5)   |                   |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                                        |
| :------------------------------ | :------------------------------------------------- |
| **Potential Applications** | Crop yield forecasting, irrigation management, pest and disease modeling, assessment of land suitability for different crops, drought and heat stress monitoring specific to agriculture, analysis of vegetation dynamics (LAI, FAPAR), water resource management in agricultural contexts, climate change impact assessments on agriculture, soil moisture studies for plant growth.                   |
| **Strengths for AE Research** | **Higher spatial resolution (0.1°)** compared to standard ERA5, providing more detailed information for agricultural landscapes. Includes **agriculture-specific variables** like evapotranspiration, soil water at multiple levels, LAI, and FAPAR, which are directly relevant to agroecological studies. Long temporal coverage (since 1979) for historical analysis. Hourly resolution for capturing diurnal variations important for plant processes. Globally consistent dataset for comparative studies.      |
| **Limitations for AE Research** | Reanalysis data (model-based with inherent uncertainties, potentially biases that might be different from standard ERA5). Still might not capture very localized microclimatic variations relevant for small farms. Requires registration and familiarity with the CDSE and potentially GRIB format. Can be computationally demanding to process large volumes of high-resolution data. Understanding the specific definitions and limitations of the agricultural variables is crucial.|

## Further Resources

| Resource Type             | Description/Link                                        |
| :-------------------------- | :---------------------------------------------------- |
| **Publications** | Search Google Scholar and the ECMWF website specifically for "AgERA5" related publications and documentation. Look for scientific reports and validation studies.  |
| **User Guides/Documentation** | The main ECMWF AgERA5 page: [https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/agera5](https://www.ecmwf.int/en/forecasts/datasets/reanalysis-datasets/agera5). The Copernicus Data Space Ecosystem documentation ([https://cds.climate.copernicus.eu/cdsapp#!/documentation](https://cds.climate.copernicus.eu/cdsapp#!/documentation)) will also be crucial for access and understanding the data. Look for sections specifically mentioning AgERA5.   |
| **Community/Support** | The Copernicus Discourse forum ([https://community.copernicus.eu/](https://community.copernicus.eu/)) is the recommended platform for questions and discussions related to Copernicus datasets, including AgERA5. ECMWF support channels might also be relevant.    |

# 4. CMIP6: Coupled Model Intercomparison Project Phase 6

## Overview

| Attribute                  | Description                          |
| :------------------------- | :----------------------------------- |
| **Short Description** | CMIP6 is the sixth phase of the Coupled Model Intercomparison Project, a major international effort to coordinate climate model experiments and make the output publicly available. It provides a framework for understanding past, present, and future climate changes.  |
| **Provider/Source** | An international effort coordinated by the World Climate Research Programme (WCRP) Working Group on Coupled Modelling (WGCM). Data is produced by numerous modeling centers worldwide. |
| **Homepage/Link** | [https://wcrp-cmip.org/cmip-phases/cmip6/](https://wcrp-cmip.org/cmip-phases/cmip6/)   |
| **License/Terms of Use** | Data access and use are governed by terms specified by the contributing modeling groups. These terms vary, so it's crucial to check the license associated with each specific dataset on the Earth System Grid Federation (ESGF) or other access points. Generally, data is available for research and educational purposes with proper attribution.  |
| **Spatial Coverage** | Global. The spatial resolution varies significantly depending on the climate model used.  |
| **Temporal Coverage** | Historical simulations (typically 1850-near present) and future projections covering various Shared Socioeconomic Pathways (SSPs) extending to 2100 and beyond, depending on the experiment.  |
| **Spatial Resolution** | Varies greatly depending on the climate model. Resolutions can range from coarse (e.g., ~100 km) to relatively high (e.g., ~25 km or finer) depending on the model and the specific output.    |
| **Temporal Resolution** | Output is available at various temporal resolutions, including daily, monthly, and sometimes sub-daily, depending on the model and the requested variables. Monthly data is common for many analyses.   |
| **Key Variables** | A vast array of atmospheric, oceanic, land surface, and sea ice variables are available, including: <br> - Temperature (surface air, ocean, etc.) <br> - Precipitation (total, convective, large-scale) <br> - Radiation (solar, thermal, top-of-atmosphere, surface) <br> - Wind (surface and at various levels) <br> - Humidity <br> - Sea level pressure <br> - Sea ice concentration and thickness <br> - Ocean currents and salinity <br> - Land surface variables (soil moisture, runoff, etc.) <br> - Biogeochemical variables (carbon cycle, etc. - depending on the Earth System Model). |

## Data Access and Format

| Attribute                      | Description                                          |
| :----------------------------- | :--------------------------------------------------- |
| **Access Methods** | Primarily through the **Earth System Grid Federation (ESGF)** ([https://esgf.llnl.gov/](https://esgf.llnl.gov/)). Users can search and download data from a distributed network of data nodes. Access may require registration depending on the data provider. Some data is also available through platforms like the Copernicus Climate Data Store (CDS) ([https://cds.climate.copernicus.eu/](https://cds.climate.copernicus.eu/)).    |
| **Data Formats** | All CMIP6 output is stored in **NetCDF (.nc)** files. These files adhere to the **Climate and Forecast (CF) Metadata Conventions**, which provide a standardized description of the data, including variable definitions and spatial/temporal properties.  |
| **Data Organization** | Data is organized following a specific directory structure based on the CMIP6 Data Reference Syntax (DRS). This structure includes: `mip_era/activity_id/institution_id/source_id/experiment_id/variant_label/table_id/variable_id/grid_label/version`. Filenames also follow a standardized pattern: `<variable_id>_<table_id>_<source_id>_<experiment_id>_<variant_label>_<grid_label>_<time_range>.nc`.     |
| **Potential Challenges** | The sheer volume of data can be overwhelming. Understanding the CMIP6 experimental design, model variations (ensemble members), and the DRS is crucial for effective data discovery. Different models have different spatial resolutions and variable availability. License terms vary. Downloading large datasets can be time-consuming and require significant storage.    |

## Technical Details 

| Attribute                       | Description                                |
| :------------------------------ | :----------------------------------------- |
| **File Naming Conventions** | Adherence to the CMIP6 DRS is crucial for programmatic data access. Developers need to understand how to parse the directory structure and filenames to identify specific models, experiments, variables, and time periods. Refer to the official CMIP6 documentation for the complete DRS specification.  |
| **Variable Names & Units** | Variable names are standardized according to the CMIP6 data request and CF conventions. Units are included as metadata within the NetCDF files. Developers should rely on the metadata within the files for accurate unit information. Standard libraries (e.g., `netCDF4`, `xarray` in Python) can be used to access this metadata.  |
| **Coordinate Systems** | Typically uses latitude and longitude coordinates. The specific grid information (`grid` and `grid_label` global attributes in NetCDF files) should be examined to understand the spatial referencing of the data. Regridding to a common grid might be necessary for comparisons across different models.   |
| **Data Processing** | Utilize Python libraries like `xarray`, `rioxarray`, `netCDF4`, or `dask` for efficient handling of multi-dimensional NetCDF data. Be prepared to handle large datasets and potentially implement parallel processing techniques. Implement robust methods for spatial and temporal subsetting and for regridding data to common grids if needed. Ensure the toolkit can handle the complexities of the CMIP6 DRS for automated data discovery and access.   |

## API Information for Climate Datasets

| API Availability | Link to API Information                                                                 | How to Utilize                                                                                                                                                                                                 |
| :--------------- | :-------------------------------------------------------------------------------------- | :----------------------------------|
| Yes (ESGF API)   | [ESGF API Nodes](https://wcrp-cmip.org/cmip-data-access/)                                | Use Python libraries like `pyesgf.search` or CLI tools like `esgpull` to query datasets. Construct requests using facets (e.g., `project=CMIP6`, `variable=tas`). Access OpenDAP URLs via `xarray` for analysis. |
|                  | [CMIP6 Data Request](https://cmip6dr.github.io/Data_Request_Home/)                      | Search variables/experiments by name, MIP, or frequency. Use spreadsheets or web interfaces to verify requested variables and metadata standards (CF conventions).                                              |
|                  | [CMIP6 Citation API](https://www.wdc-climate.de/docs/pdf/CMIP6_Citation_Userguide.pdf)  | Submit JSON-formatted author lists, ORCIDs, and references via API or GUI. Use error-checking tools to validate citations before publishing.                                                                    |
|                  | [CEDA STAC API](https://stac.ceda.ac.uk/collections/cmip6)                              | Query CMIP6 metadata using SpatioTemporal Asset Catalog (STAC) standards. Filter by model, experiment, or variable.                                                                                            |
|                  | [Copernicus CDS API](https://cds.climate.copernicus.eu/datasets/projections-cmip6)       | Install `cdsapi` Python library. Requires registration and dataset-specific syntax (e.g., `experiment_id=ssp585`). Limited to subset of CMIP6 data hosted by Copernicus.                                        |  

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                                        |
| :------------------------------ | :------------------------------------------------- |
| **Potential Applications** | Long-term climate change impact assessments on agriculture, analysis of future temperature and precipitation changes relevant for crop suitability, studying the frequency and intensity of extreme events (heatwaves, droughts, floods) and their agricultural impacts, informing adaptation strategies, downscaling CMIP6 data for regional agricultural modeling, assessing climate risks under different socioeconomic scenarios.    |
| **Strengths for AE Research** | Provides a wide range of future climate projections based on different scenarios, allowing for the exploration of uncertainties. The multi-model ensemble approach helps in assessing the robustness of climate change signals. The long historical simulations provide context for understanding past climate variability. The global coverage allows for studies in diverse agroecological zones. The standardized NetCDF format and metadata conventions facilitate data processing and comparison across models.    |
| **Limitations for AE Research** | The spatial resolution of many CMIP6 models might be too coarse to directly capture the climate variability relevant for local-scale agricultural systems. Downscaling techniques are often required. Biases in climate models can affect the accuracy of regional projections. The complexity of the CMIP6 experiment design and model variations requires careful consideration when selecting and interpreting data. Some agricultural-specific variables (like detailed soil moisture or vegetation indices) might not be directly available and may need to be derived or obtained from other datasets.  |

## Further Resources

| Resource Type             | Description/Link                                           |
| :------------------------ | :--------------------------------------------------------- |
| **Publications** | The overview paper on the CMIP6 experimental design and organization (Eyring et al., 2016) is a key reference. Search for "CMIP6" in scientific databases like Google Scholar and the IPCC reports (AR6) for analyses based on CMIP6 data.    |
| **User Guides/Documentation** | The official CMIP6 website ([https://wcrp-cmip.org/cmip-phases/cmip6/](https://wcrp-cmip.org/cmip-phases/cmip6/)) provides extensive information. The PCMDI (Program for Climate Model Diagnosis and Intercomparison) at LLNL also hosts valuable resources ([https://pcmdi.llnl.gov/CMIP6/](https://pcmdi.llnl.gov/CMIP6/)). The ESGF website ([https://esgf.llnl.gov/](https://esgf.llnl.gov/)) has user guides and documentation for data access. The CMIP6 Data Request documentation provides details on variables and experiments.  |
| **Community/Support** | The ESGF user support forums and mailing lists are good resources for technical questions related to data access. The CMIP community is large and active; relevant scientific conferences and workshops can also provide opportunities for interaction.  |

# 5. TAMSAT: Tropical Applications of Meteorology using SATellite data and ground-based observations

## Overview

| Attribute                  | Description                                    |
| :------------------------- | :--------------------------------------------- |
| **Short Description** | TAMSAT is a long-term, high-resolution rainfall dataset for Africa, developed by the University of Reading. It blends infrared satellite imagery with ground-based rain gauge observations to provide reliable rainfall estimates, particularly valuable in regions with sparse gauge networks. |
| **Provider/Source** | Department of Meteorology, University of Reading.     |
| **Homepage/Link** | [https://www.tamsat.org.uk/](https://www.tamsat.org.uk/)   |
| **License and Terms of Use** | The TAMSAT dataset is generally made available for non-commercial research, educational, and applications use. Specific terms of use, including citation requirements, are usually outlined on the TAMSAT website. It's important to consult the "Data Access" or "Terms of Use" section on their site.  |
| **Spatial Coverage** | Africa (continental).  |
| **Temporal Coverage** | Typically spans from 1981 to near-present, with updates occurring regularly. The exact start and end dates should be verified on the TAMSAT website.     |
| **Spatial Resolution** | 0.0375° x 0.0375° latitude/longitude (approximately 4 km x 4 km at the equator). This is a relatively high spatial resolution.  |
| **Temporal Resolution** | Daily, dekadal (10-day), and monthly rainfall estimates are commonly available. Other aggregations might also be provided.    |
| **Key Variables** | Rainfall/Precipitation. Units are typically millimeters (mm).   |

## Data Access and Format

| Attribute                      | Description                                          |
| :----------------------------- | :--------------------------------------------------- |
| **Access Methods** | Data can usually be accessed through the TAMSAT website, often via a dedicated "Data Access" or "Download" section. This might involve direct download via FTP or HTTP. They may also have a data portal or require registration for access. Inquire about any potential API access from their website or contact them directly.  |
| **Data Formats** | Data is often provided in NetCDF (.nc) format, as well as potentially other formats like GeoTIFF (.tif) for easier integration with GIS software. The format can vary depending on the specific product and how it's accessed. |
| **Data Organization** | Files are typically organized by temporal resolution (daily, dekadal, monthly) and then by year. Filenames often include the date or date range and the product version. NetCDF files will contain multi-dimensional arrays (time, latitude, longitude, rainfall).  |
| **Potential Challenges** | Access methods might vary over time, so always refer to the TAMSAT website for the latest instructions. Large file sizes can be a consideration, especially for long time series at high spatial resolution. NetCDF files require specific software libraries for processing. Ensure you understand any specific data flags or quality control information provided with the dataset.  |

## Technical Details 

| Attribute                       | Description                                    |
| :------------------------------ | :--------------------------------------------- |
| **File Naming Conventions** | Typically include the product name (`TAMSAT`), temporal resolution (e.g., `daily`, `dekadal`, `monthly`), year, and potentially the day or month. Refer to the TAMSAT website and the filenames of downloaded data for the exact conventions.  |
| **Variable Names & Units** | The primary rainfall variable is usually named something like `rainfall` or `precip`. Units are typically millimeters (`mm`). Check the metadata within the NetCDF files for confirmation of variable names and units.   |
| **Coordinate Systems** | Uses latitude and longitude coordinates. The specific datum is usually WGS 84 but should be verified in the NetCDF metadata. |
| **Data Processing** | Utilize standard geospatial and NetCDF processing libraries in your chosen programming language (e.g., `xarray`, `rioxarray`, `netCDF4` in Python; `raster` in R). Be prepared to handle spatial subsets for specific agricultural regions within Africa. Consider implementing functions for temporal aggregation or disaggregation if needed. Pay attention to any missing data flags or quality control layers that might be provided. |

## API Information for Climate Datasets

| Available API                     | Link to API Information                                    | How to Utilize         |
|-----------------------------------|------------------------------------------------------------|------------------------|
| No formal, public REST API      | [TAMSAT Website (for data access information)](https://www.tamsat.org.uk/) | Programmatic access likely involves downloading files from the website or provided links and then using libraries like `xarray` (Python) or `raster` (R) to process the data. Check the TAMSAT website for any potential future API updates. |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                              |
| :------------------------------ | :--------------------------------------- |
| **Potential Applications** | Rainfall pattern analysis across Africa, drought monitoring and early warning systems, agricultural planning and decision-making, crop yield modeling (especially in rainfed agriculture), assessment of water availability for irrigation, climate risk assessment in agricultural regions, validation of other rainfall datasets or climate models over Africa, studies on the impact of rainfall variability on vegetation and agricultural productivity.   |
| **Strengths for AE Research** | **High spatial resolution** is particularly valuable for capturing localized rainfall patterns relevant to agricultural fields. **Long temporal coverage** allows for historical analysis of rainfall trends and variability. **Focus on Africa** makes it a directly relevant dataset for agroecological research on the continent, especially in areas with limited ground station data. Blending of satellite and gauge data aims to provide more accurate estimates than satellite-only products.  |
| **Limitations for AE Research** | Primarily a rainfall dataset; does not include other essential agroclimatic variables like temperature, solar radiation, or evapotranspiration. Accuracy can still be limited in very remote regions with minimal gauge input. While high for regional data, the 4 km resolution might still be too coarse for very micro-scale agricultural studies. Understanding the specific algorithms and potential biases in the TAMSAT product is important for interpretation. |

## Further Resources

| Resource Type             | Description/Link                                                |
| :-------------------------- | :------------------------------------------------------------ |
| **Publications** | The TAMSAT website ([https://www.tamsat.org.uk/](https://www.tamsat.org.uk/)) often lists key publications describing the dataset methodology and validation. Search for "TAMSAT rainfall" in scientific databases like Google Scholar.  |
| **User Guides/Documentation** | The TAMSAT website is the primary source for user guides, data documentation, and any FAQs. Look for sections like "Data," "Documentation," or "About TAMSAT." They might provide specific guidelines for data access and usage.   |
| **Community/Support** | The TAMSAT website might provide contact information for inquiries or support. You could also look for relevant discussions in online forums or communities focused on African climate data or remote sensing in agriculture.    |

# 6. NASA POWER: Prediction Of Worldwide Energy Resources

## Overview

| Attribute                  | Description                                   |
| :------------------------- | :-------------------------------------------- |
| **Short Description** | NASA POWER provides freely available gridded solar and meteorological datasets derived from NASA satellite observations and climate models. It is designed to support renewable energy, agricultural, and building energy efficiency applications.  |
| **Provider/Source** | NASA Langley Research Center (LaRC) POWER Project, supported by the NASA Earth Science Directorate Applied Sciences Program.  |
| **Homepage/Link** | [https://power.larc.nasa.gov/](https://power.larc.nasa.gov/)  |
| **License and Terms of Use** | NASA POWER data is generally considered public domain and freely available for use with proper attribution to NASA/POWER. Consult the "About" or "Documentation" section on the POWER website for specific citation guidelines. |
| **Spatial Coverage** | Global.    |
| **Temporal Coverage** | Varies depending on the specific data product. Some parameters are available from 1981 to near-present, while others might have different temporal ranges. Consult the POWER website for the specific temporal coverage of each variable and dataset.  |
| **Spatial Resolution** | The standard spatial resolution is 0.5° x 0.5° latitude/longitude (approximately 50 km x 50 km at the equator). Some parameters might be available at higher resolutions. Check the specific dataset details on the POWER website.   |
| **Temporal Resolution** | Data is available at various temporal resolutions, including daily, monthly, and sometimes hourly (depending on the parameter and dataset). Users can often select the desired temporal aggregation through the web interface or API.  |
| **Key Variables** | A wide range of solar and meteorological parameters are available, including: <br> - Solar radiation (insolation, direct normal irradiance, diffuse horizontal irradiance) <br> - Surface meteorology (temperature, wind speed and direction, humidity, pressure) <br> - Precipitation <br> - Evapotranspiration <br> - Soil moisture (for some datasets) <br> - Cloud cover. |

## Data Access and Format

| Attribute                      | Description                                      |
| :----------------------------- | :----------------------------------------------- |
| **Access Methods** | **POWER Web Data Viewer:** An interactive web interface allows users to select parameters, specify geographic locations and time ranges, and download data in various formats. <br> **POWER API (Application Programming Interface):** Provides programmatic access to the data, allowing developers to integrate POWER data directly into their applications and workflows. Documentation for the API is available on the POWER website.   |
| **Data Formats** | Data can be downloaded in various formats, including: <br> - **CSV (Comma Separated Values):** Suitable for simple data extraction and analysis. <br> - **JSON (JavaScript Object Notation):** A lightweight format often used with web APIs. <br> - **NetCDF (.nc):** A standard format for gridded climate data, often preferred for more complex spatial and temporal analyses. <br> - **GeoJSON:** For geospatial applications. The availability of formats may vary depending on the access method and the selected parameters.    |
| **Data Organization** | When using the web interface, data is typically downloaded as a time series for a specified location or as gridded data for a spatial extent. The organization within NetCDF files follows standard conventions with dimensions for time, latitude, and longitude, and variables representing the meteorological parameters. API responses are usually structured in JSON. CSV files contain columns for time and the selected parameters.   |
| **Potential Challenges** | Understanding the different datasets and their temporal coverage is important. The spatial resolution (0.5°) might be too coarse for very localized agricultural studies. While the API is powerful, it requires some programming knowledge. Ensure proper handling of units and potential missing data flags as described in the data documentation. Be aware of any rate limits or usage policies when using the API.     |

## Technical Details 

| Attribute                       | Description                                          |
| :------------------------------ | :--------------------------------------------------- |
| **File Naming Conventions** | When downloading via the web interface, filenames typically include the location (latitude/longitude) and date range. When using the API, the structure of the returned data (JSON or NetCDF) is more important than a specific filename convention. For NetCDF downloads, standard CF conventions are generally followed.    |
| **Variable Names & Units** | Variable names are generally descriptive (e.g., `T2M` for 2-meter temperature, `ALLSKY_SFC_SWDN` for surface downwelling shortwave radiation). Units are clearly specified in the metadata when downloading NetCDF files or within the JSON API responses. The POWER website provides documentation on the available parameters and their units.    |
| **Coordinate Systems** | Uses latitude and longitude coordinates. The standard projection is typically a regular latitude-longitude grid (Plate Carrée). Coordinate information is included in the metadata of NetCDF files and within the structure of JSON responses. |
| **Data Processing** | For API integration, developers will need to handle HTTP requests and parse JSON responses. For NetCDF data, use libraries like `xarray` or `netCDF4` in Python. Be prepared to handle spatial extraction (selecting data for specific areas) and temporal filtering. Pay close attention to the units of each variable and perform any necessary conversions. Handle missing data as indicated in the data values or metadata. The POWER API allows for specifying the desired output format (CSV, JSON, NetCDF), which can simplify integration with different parts of your toolkit.       |

## API Information for Climate Datasets

| API Availability | Link to API Information                                                                 | How to Utilize                       |
| :--------------- | :-------------------------------------------------------------------------------------- | :----------------------------------- |
| Yes (REST API)   | [API Getting Started](https://power.larc.nasa.gov/docs/tutorials/api-getting-started/)   | Construct API URLs with parameters (lat, lon, dates, variables). Use output formats (JSON/CSV/NetCDF) directly in scripts. Python/R clients available (`pynasapower`, `nasapower`).                            |
|                  | [API Documentation](https://power.larc.nasa.gov/docs/services/api/)                     | Follow parameter guidelines for temporal ranges and spatial resolution (0.5° for meteo). Handle HTTP codes (200=success, 429=throttling).                                                                     |
|                  | [Data Access Viewer](https://power.larc.nasa.gov/data-access-viewer/)                   | Generate starter API URLs via GUI. Copy/paste requests into scripts. Supports multi-point downloads through CSV coordinate uploads.                                                                            |
|                  | [Python Client](https://pynasapower.readthedocs.io)                                     | Install via pip. Use `get_data()` with coordinates/time ranges. Handles API pagination and rate limits automatically.                                                                                          |
|                  | [R Client](https://docs.ropensci.org/nasapower/)                                        | Install from CRAN. Use `get_power()` with community codes ("ag", "sb") and temporal resolutions ("daily", "monthly"). Returns tidy data frames.                                                                 |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                                           |
| :------------------------------ | :---------------------------------------------------- |
| **Potential Applications** | Assessing solar radiation for crop growth and solar energy potential in agricultural areas, analyzing temperature and humidity impacts on crop and livestock, estimating potential evapotranspiration for irrigation planning, monitoring precipitation patterns, studying wind patterns for wind erosion or pollination, assessing soil moisture availability (for some datasets), providing input data for agricultural models, climate risk assessments related to solar and meteorological variables.|
| **Strengths for AE Research** | **Freely available and easy to access** through both a user-friendly web interface and a programmatic API. **Global coverage** allows for studies in any agricultural region worldwide. Provides a **wide range of relevant solar and meteorological variables** in a single source. Multiple temporal resolutions offer flexibility for different types of analyses. Data is derived from reliable NASA satellite observations and climate models.   |
| **Limitations for AE Research** | The standard **0.5° spatial resolution** can be too coarse for detailed local-scale agricultural analysis. While precipitation data is available, datasets like CHIRPS or TAMSAT might be preferred for higher resolution rainfall information in specific regions. The temporal coverage varies by parameter and dataset, so careful selection is needed. Direct access to very high temporal resolution (e.g., sub-hourly) might be limited for some parameters. |

## Further Resources

| Resource Type             | Description/Link                                                |
| :------------------------ | :-------------------------------------------------------------- |
| **Publications** | The NASA POWER website ([https://power.larc.nasa.gov/](https://power.larc.nasa.gov/)) usually lists relevant publications and citations related to the dataset and its methodology.  |
| **User Guides/Documentation** | The "Documentation" or "About" sections on the NASA POWER website are comprehensive resources, providing details on the available datasets, parameters, temporal coverage, spatial resolution, data access methods (web interface and API), and data formats. The API documentation is particularly important for developers.     |
| **Community/Support** | The NASA POWER website may provide contact information for questions or support. You might also find discussions or examples of using POWER data in online forums related to remote sensing, renewable energy, or agricultural modeling.   |

# 7. Integrated Multi-satellitE Retrievals for GPM (IMERG)

## Overview

| Attribute           | Description                                                                               |
|---------------------|-------------------------------------------------------------------------------------------|
| Short Description   | IMERG is a NASA product estimating global surface precipitation rates by combining data from the GPM satellite constellation, including microwave, infrared, and gauge data.     |
| Provider/Source     | NASA (National Aeronautics and Space Administration) / JAXA (Japan Aerospace Exploration Agency) as part of the Global Precipitation Measurement (GPM) mission.       |
| Homepage/Link       | [GPM Website](https://gpm.nasa.gov/) and [GES DISC IMERG Page](https://disc.gsfc.nasa.gov/datasets?keywords=IMERG)        |
| License/Terms of Use | Generally open for research and non-commercial use. Users should acknowledge NASA/JAXA/GPM in publications. See specific data access portals for detailed terms.      |
| Spatial Coverage    | Quasi-global, 90°S to 90°N latitude, 180°W to 180°E longitude.     |
| Temporal Coverage   | June 2000 to near-present (updated with a latency depending on the product: Early, Late, and Final Runs).    |
| Spatial Resolution  | 0.1° x 0.1° latitude/longitude (approximately 10 km x 10 km at the equator).         |
| Temporal Resolution | Half-hourly (30-minute), daily, and monthly aggregations available depending on the product (Early, Late, Final).   |
| Key Variables       | Precipitation rate (mm/hr), accumulated precipitation (mm), and associated error estimates. Different runs (Early, Late, Final) offer varying latency and accuracy.   |

## Data Access and Format

| Attribute            | Description                                        |
|----------------------|----------------------------------------------------|
| Access Methods       | Download via NASA GES DISC (HTTP/FTP), potential access through облачные платформы like Google Earth Engine (GEE), and possibly through intermediary APIs or ERDDAP servers.    |
| Data Formats         | Primarily NetCDF (.nc), sometimes available in GeoTIFF (.tif) for certain products or through specific portals. |
| Data Organization    | By temporal resolution (half-hourly, daily, monthly), then by year and sometimes month. NetCDF files contain multi-dimensional arrays (time, latitude, longitude, variable). Different "Runs" (Early, Late, Final) are often organized as separate datasets. |
| Potential Challenges | Large file sizes, especially for high temporal resolution data. Requires specific software libraries (e.g., `netCDF4`, `xarray`, `rioxarray` in Python) for handling. Be aware of the latency and accuracy differences between the Early, Late, and Final Runs. Potential missing data (handle fill values). |

## Technical Details

| Attribute                 | Description                                       |
|---------------------------|---------------------------------------------------|
| File Naming Conventions | Typically includes product name (e.g., 3B-HHR, 3B-DAY), version number (e.g., V06, V07), date (YYYYMMDD), start and end times for half-hourly data (HHMMSS), and sometimes a time-of-day indicator (in minutes). For example: `3B-HHR.MS.MRG.3IMERG.20241201-S233000-E235959.1410.V07B.nc4`.  |
| Variable Names & Units    | Primary variable is usually `precipitationCal` or similar, representing the merged satellite-gauge precipitation estimate, often with units of millimeters per hour (mm/hr) or millimeters per day (mm/day) for daily products. Verify metadata within the NetCDF files for precise variable names and units. Other variables include error estimates (`err`), and counts of contributing satellite retrievals (`nobs`, `HQprecipitation`).  |
| Coordinate Systems        | Latitude and longitude based on the World Geodetic System 1984 (WGS 84) datum. Coordinate variables are typically named `lat` and `lon`. The time coordinate is usually in UTC (Coordinated Universal Time) as seconds or days since a reference epoch.   |
| Data Processing           | Use libraries like `xarray`, `rioxarray`, `netCDF4` (Python) or `raster` (R) for NetCDF file handling. Pay close attention to latitude and longitude coordinates and the time dimension. Handle missing data flags appropriately. Consider the need for temporal aggregation (e.g., daily or monthly totals) or spatial averaging Runs) and their implications for data quality and latency.     |

## API Information for Climate Datasets

| API Availability          | Link to API Information                   | How to Utilize                   |
|---------------------------|-------------------------------------------|----------------------------------|
| No Direct API             | [Google Earth Engine API Docs](https://developers.google.com/earth-engine/datasets/catalog/NASA_GPM_L3_IMERG_V07) (if using GEE) | Access via Google Earth Engine API if the IMERG dataset is available in the GEE catalog. Use GEE's Python or JavaScript API to filter by time and spatial extent, and to download or process the data.  |
| ERDDAP Servers (Potential) | Search for ERDDAP servers hosting IMERG data (e.g., NOAA ERDDAP).  | ERDDAP provides a web interface and APIs (e.g., OPeNDAP, griddap) to access and download subsets of the data in various formats (NetCDF, CSV, etc.).  |
| Python Libraries          | Libraries like `requests` or `urllib` can be used to directly download files from the GES DISC FTP/HTTP servers if you know the file URLs. | Construct the appropriate URLs based on the GES DISC file structure and use Python to download the files. Then, use `netCDF4` or `xarray` to read and process the downloaded NetCDF files.  |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
| Potential Applications        | Rainfall pattern analysis, drought monitoring, extreme precipitation event analysis relevant to agricultural impacts (floods, dry spells), crop yield modeling (as precipitation is a key input), water resource management for irrigation, agroclimatic zoning based on rainfall regimes, validation of local rainfall data or downscaled climate model outputs. The half-hourly and daily resolutions can capture sub-daily and daily rainfall variability important for hydrological processes affecting agriculture. |
| Strengths for AE Research       | High spatial resolution allows for localized analysis relevant to farm-level studies. Long temporal coverage (since 2000) enables trend analysis and understanding of historical precipitation variability. Quasi-global coverage allows for studies across different agroecological zones. Integration of multiple satellite sensors and ground gauge data generally leads to higher accuracy compared to satellite-only products, especially in the Final Run.  |
| Limitations for AE Research     | Indirect satellite measurements can still have biases, especially in regions with complex terrain, coastlines, or during frozen precipitation. Does not include other crucial agroecological variables like temperature, solar radiation, humidity, etc. Spatial resolution might still be too coarse for very localized microclimatic studies within farms. Different IMERG runs have varying latency and accuracy; the near real-time products (Early, Late) might be less accurate than the research-oriented Final Run.   |

## Further Resources

| Resource Type           | Description/Link                                                 |
|-------------------------|------------------------------------------------------------------|
| User Guides/Documentation | Primary source is the NASA GES DISC website: [GES DISC IMERG Documentation](https://www.google.com/search?q=https://disc.gsfc.nasa.gov/information/documents%3Fkeywords%3DIMERG). Look for documents related to the algorithm, data quality, and user guides. The GPM mission website ([https://gpm.nasa.gov/](https://gpm.nasa.gov/)) also has relevant information. |
| Community/Support       | NASA GES DISC provides user support. Contact information can usually be found on their website. Online forums related to remote sensing, climate data, or specific software (e.g., Earth Engine Developer Forum) might also have discussions and solutions related to IMERG data.   |

# 8. NASA Earth Exchange Global Daily Downscaled Projections (NEX-GDDP)

## Overview

| Attribute           | Description                                                                                          |
|---------------------|------------------------------------------------------------------------------------------------------|
| **Short Description**   | NEX-GDDP provides global, high-resolution (0.25°) daily climate projections downscaled from CMIP5 and CMIP6 GCMs, including key variables for climate impact studies. |
| **Provider/Source**     | NASA Earth Exchange (NEX)                                                                            |
| **Homepage/Link**       | [NEX-GDDP CMIP5](https://www.nccs.nasa.gov/services/data-collections/land-based-products/nex-gddp), [NEX-GDDP-CMIP6](https://www.nccs.nasa.gov/services/data-collections/land-based-products/nex-gddp-cmip6) |
| **License/Terms of Use**| Open for scientific research; not recommended for commercial/engineering use without expert consultation. |
| **Spatial Coverage**    | Global (CMIP5: 50°S–50°N; CMIP6: 60°S–90°N).                                                  |
| **Temporal Coverage**   | 1950–2100 (CMIP5: 1950–2099; CMIP6: 1950–2100).                                             |
| **Spatial Resolution**  | 0.25° x 0.25° (~25 km).                                                                     |
| **Temporal Resolution** | Daily                                                                                                |
| **Key Variables**       | tasmin (daily min temperature, K), tasmax (daily max temperature, K), precipitation (kg m⁻² s⁻¹). |

## Data Access and Format

| Attribute         | Description                                                                                                               |
|-------------------|---------------------------------------------------------------------------------------------------------------------------|
| **Access Methods**    | Download via NASA NCCS THREDDS, AWS S3, Google Earth Engine.                                                  |
| **Data Formats**      | netCDF4 (classic and enhanced).                                                                                     |
| **Data Organization** | Organized by scenario (RCP/SSP), model, variable, and year. Files are typically per variable per year per model.     |
| **Potential Challenges** | Large dataset size (up to 38 TB for CMIP6), requires netCDF-compatible tools (e.g., xarray, netCDF4, CDO).        |

## Technical Details

| Attribute             | Description                                                                                 |
|-----------------------|---------------------------------------------------------------------------------------------|
| **File Naming Conventions** | Typically includes model, scenario, variable, and year (e.g., pr_day_ACCESS-CM2_historical_2014.nc). |
| **Variable Names & Units** | tasmin (K), tasmax (K), pr (kg m⁻² s⁻¹).                                         |
| **Coordinate Systems**     | Latitude/longitude, WGS84 datum.                                                        |
| **Data Processing**        | Downscaling via Bias-Correction Spatial Disaggregation (BCSD); time in days since model-dependent reference. |
| **Handling Missing Data**  | Standard netCDF conventions; check metadata for fill values.                               |

## API Information

| API Availability | Description                                                                                      |
|------------------|--------------------------------------------------------------------------------------------------|
| **Direct API**       | No dedicated REST API.                                                                           |
| **Google Earth Engine** | Datasets available for analysis via GEE Python/JavaScript APIs.                         |
| **Programmatic Access** | Download and subsetting via THREDDS (NetCDFSubset), AWS S3, wget/cURL scripting.        |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
| Potential Applications| Climate risk assessment, crop yield modeling, drought and heat stress analysis, water resource planning, agroclimatic zoning, validation of local climate data. |
| Strengths | High spatial and temporal resolution for local/regional studies, global coverage, daily data for temperature and precipitation, bias-corrected projections from multiple GCMs and scenarios.|
| Limitations | Does not include other agroclimatic variables (e.g., solar radiation, humidity), file sizes can be challenging, requires technical expertise for data handling, and projections are subject to GCM and downscaling uncertainties. |

## Further Resources

| Resource Type     | Description/Link                                                                                  |
|-------------------|--------------------------------------------------------------------------------------------------|
| **User Guides**       | [NEX-GDDP Technical Note (CMIP5)](https://esgf.nccs.nasa.gov/esgdoc/NEX-GDDP_Tech_Note_v0.pdf) |
|                   | [NEX-GDDP-CMIP6 Technical Note](https://www.nccs.nasa.gov/sites/default/files/NEX-GDDP-CMIP6-Tech_Note_4.pdf) |
| **Community/Support** | Contact NASA NEX team or NCCS Support for technical questions.                              |
| **Documentation**     | Dataset homepages (see above), Google Earth Engine dataset pages.                           |

# 9. TerraClimate

*TerraClimate is a foundational resource for agroecological, ecological, and hydrological research, offering consistent, high-resolution climate and water balance data for global terrestrial surfaces.*

## Overview

| Attribute            | Description |
|----------------------|-------------|
| **Short Description** | TerraClimate is a global, high-resolution (~4 km, 1/24°) monthly dataset of climate and climatic water balance variables for terrestrial surfaces, spanning from 1958 to the present. It blends high-resolution climatological normals with coarser time-varying data to provide detailed, temporally consistent climate information. |
| **Provider/Source**  | Climatology Lab, University of California Merced (UCM) |
| **Homepage/Link**    | [Climatology Lab TerraClimate](https://www.climatologylab.org/terraclimate.html) |
| **License/Terms of Use** | Public domain (Creative Commons CC0 license); free for research and operational use. |
| **Spatial Coverage** | Global (all terrestrial surfaces). |
| **Temporal Coverage** | January 1958 to present (updated annually). |
| **Spatial Resolution** | 1/24° (~4 km) latitude/longitude grid. |
| **Temporal Resolution** | Monthly. |
| **Key Variables** | Precipitation, maximum temperature, minimum temperature, wind speed, vapor pressure, vapor pressure deficit, downward shortwave radiation, reference evapotranspiration, actual evapotranspiration, climatic water deficit, soil moisture, runoff, snow water equivalent, Palmer Drought Severity Index (PDSI). |

## Data Access and Format

| Attribute            | Description |
|----------------------|-------------|
| **Access Methods**   | Download via [Climatology Lab website](https://www.climatologylab.org/terraclimate.html), [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/dataset/terraclimate), [Google Earth Engine](https://developers.google.com/earth-engine/datasets/catalog/IDAHO_EPSCOR_TERRACLIMATE), and THREDDS servers. |
| **Data Formats**     | NetCDF (.nc), GeoTIFF (.tif) for some derived products. |
| **Data Organization**| Files organized by variable and year/month; NetCDF files contain multi-dimensional arrays (time, latitude, longitude, variable). |
| **Potential Challenges** | Large file sizes; requires software (e.g., netCDF4, xarray, raster, R) for handling; be aware of missing data flags and annual updates. |

## Technical Details

| Attribute            | Description |
|----------------------|-------------|
| **File Naming Conventions** | Typically includes variable name, year, and month (e.g., `TerraClimate_ppt_1981.nc`). |
| **Variable Names & Units** | See documentation; e.g., `ppt` (precipitation, mm), `tmax`/`tmin` (max/min temperature, °C), `ws` (wind speed, m/s), `srad` (solar radiation, W/m²), `aet` (actual evapotranspiration, mm), `pet` (reference evapotranspiration, mm), etc. |
| **Coordinate Systems** | Latitude and longitude (WGS 84 datum), grid cell centers. |
| **Data Processing** | Combines WorldClim v2 climatological normals with CRU Ts4.0 and JRA55 reanalysis for monthly variability, using climatically aided interpolation. Water balance variables are generated using a modified Thornthwaite-Mather model. |
| **Handling Missing Data** | Missing values are flagged; users should check metadata and handle fill values appropriately. |

## API Information

| API Availability | Description |
|------------------|-------------|
| **Direct API**   | No dedicated API. |
| **Programmatic Access** | Accessible via [Google Earth Engine](https://developers.google.com/earth-engine/datasets/catalog/IDAHO_EPSCOR_TERRACLIMATE), [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/dataset/terraclimate), and THREDDS servers; can be scripted in Python, R, or other languages using standard geospatial libraries. |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
| Potential Applications |  <br> - Climate trend and variability analysis at local to global scales  <br> - Drought monitoring, water balance studies, and agricultural risk assessment  <br> - Crop yield modeling, agroclimatic zoning, and ecological/hydrological modeling  <br> - Validation and downscaling of coarser climate datasets |
|Strengths | <br> - High spatial resolution (~4 km) and long temporal coverage (1958–present) <br> - Comprehensive set of climate and water balance variables  <br> - Freely available and widely validated against station and streamflow data|
|Limitations|  <br> - Monthly temporal resolution may not capture short-term extremes <br> - Large data volumes require robust data handling tools <br> - Some variables are model-derived and may have uncertainties in data-sparse regions |

## Further Resources

| Resource Type       | Description/Link |
|---------------------|------------------|
| **User Guides/Documentation** | [Climatology Lab TerraClimate](https://www.climatologylab.org/terraclimate.html), [Scientific Data article](https://www.nature.com/articles/sdata2017191) |
| **Community/Support** | No dedicated forum; general support via Climatology Lab or climate data user communities. |
| **R Package** | [datazoom.amazonia vignette for TerraClimate](https://cran.r-project.org/web/packages/datazoom.amazonia/vignettes/TERRACLIMATE.html) |
  

</details>

<details>
  <summary> Crop Calendar dataset </summary>

  # 1. AgMIP-GGCMI Crop Calendar

*This crop calendar is a foundational input for global crop modeling, enabling harmonized and reproducible assessments of climate change impacts on agriculture.*
## Overview

| Attribute            | Description |
|----------------------|-------------|
| **Short Description** | The AgMIP-GGCMI Crop Calendar is a global dataset providing multi-year average planting (sowing) and maturity (harvest) dates for 18 major crops, distinguishing between rainfed and irrigated systems, at 0.5° spatial resolution. It is a composite product merging various observational data sources and is designed to support harmonized crop modeling and climate impact assessments. |
| **Provider/Source**  | AgMIP (Agricultural Model Intercomparison and Improvement Project) and GGCMI (Global Gridded Crop Model Intercomparison), led by institutions including NASA GISS, Potsdam Institute for Climate Impact Research, University of Minnesota, and University of Goettingen. |
| **Homepage/Link**    | [Zenodo Dataset](https://doi.org/10.5281/zenodo.5062513) |
| **License/Terms of Use** | Open for research and non-commercial use; cite original sources as appropriate. |
| **Spatial Coverage** | Global, 0.5° x 0.5° land grid cells. |
| **Temporal Coverage** | Multi-year average (static growing periods; no interannual variability). |
| **Spatial Resolution** | 0.5° x 0.5° latitude/longitude. |
| **Temporal Resolution** | One growing season per crop per grid cell (with exceptions for wheat and rice). |
| **Key Variables** | Planting day of year (DOY), maturity (harvest) day of year (DOY) for 18 crops, with separate values for rainfed and irrigated systems. |
| **18 crops covered** | The 18 crops covered in the AgMIP-GGCMI Crop Calendar are: 1. Maize, 2. Wheat (including winter and spring wheat), 3. Rice (including two main growing seasons), 4. Soybean, 5. Barley, 6. Millet, 7. Rapeseed, 8. Rye, 9. Sorghum, 10. Sugar beet, 11. Sugar cane, 12. Cotton, 13. Cassava, 14. Groundnut, 15. Field pea, 16. Sunflower, 17. Dry bean, 18. Potato. |
## Data Access and Format

| Attribute            | Description |
|----------------------|-------------|
| **Access Methods**   | Download from [Zenodo](https://doi.org/10.5281/zenodo.5062513); source code and tools available on [GitHub](https://github.com/AgMIP-GGCMI/cropCalendars). |
| **Data Formats**     | NetCDF (.nc), CSV, and R data objects. |
| **Data Organization**| Organized by crop, grid cell, and management system (rainfed/irrigated); one growing season per crop/cell, except for wheat and rice (multiple seasons). |
| **Potential Challenges** | Static averages only; no crop rotations or interannual variability; gap-filling and spatial extrapolation in areas lacking observations. |

## Technical Details

| Attribute            | Description |
|----------------------|-------------|
| **File Naming Conventions** | Typically includes crop name, management system, and phase (e.g., `maize_rainfed_phase3.nc`). |
| **Variable Names & Units** | Planting_day (DOY), Maturity_day (DOY); units are day of year (1–365/366). |
| **Coordinate Systems** | Latitude and longitude in WGS 84 datum; grid cell centers. |
| **Data Processing** | Composite of multiple observational sources; spatial extrapolation and gap-filling for uncultivated or missing areas; only a single season per crop/cell except for wheat and rice. |
| **Handling Missing Data** | Gap-filled using best available sources; uncultivated areas extrapolated. |

## API Information

| API Availability | Description |
|------------------|-------------|
| **Direct API**   | No direct API. |
| **Programmatic Access** | Data and scripts available for download and batch processing via [Zenodo](https://doi.org/10.5281/zenodo.5062513) and [GitHub](https://github.com/AgMIP-GGCMI/cropCalendars); R scripts provided for simulation and adaptation of crop calendars. |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
| Potential Applications| <br> - Calibration of crop model phenology (e.g., heat unit/PHU requirements) <br> - Harmonization of growing periods for multi-model crop simulations and climate impact studies <br> - Assessment of climate change impacts on crop timing and yields at regional to global scales <br> - Scenario development for adaptation strategies by simulating changes in planting/harvest dates|
| Strengths | <br> - Consistent, global, crop-specific growing periods for 18 major crops <br> - Distinguishes between rainfed and irrigated systems <br> - Supports harmonized, reproducible crop modeling and climate impact research|
| Limitations | <br> - Provides static (multi-year average) growing periods only; no annual variability or crop rotations <br> - Extrapolated data in areas with sparse observations; users should check data quality for their region of interest|

## Further Resources

| Resource Type       | Description/Link |
|---------------------|------------------|
| **User Guides/Documentation** | [Zenodo Dataset Documentation](https://doi.org/10.5281/zenodo.5062513); [GitHub Repository for Scripts](https://github.com/AgMIP-GGCMI/cropCalendars). |
| **Primary Publication** | Jägermeyr et al. (2021), "Climate impacts on global agriculture emerge earlier in new generation of climate and crop," Nature Food, [DOI](https://www.nature.com/articles/s43016-021-00400-y). |
| **Additional Studies** | Minoli et al. (2022), "Global crop yields can be lifted by timely adaptation of growing periods to climate change," Nature Communications, [DOI](https://doi.org/10.1038/s41467-022-34411-5). |
| **Community/Support** | Contact dataset authors via Zenodo or institutional affiliations listed in the dataset record. |

# 2. WorldCereal Project Crop Calendars

*WorldCereal crop calendars are a foundational input for global crop mapping and monitoring, enabling harmonized and reproducible assessments of crop seasonality and supporting operational agricultural monitoring at scale.*

## Overview

| Attribute            | Description |
|----------------------|-------------|
| **Short Description** | The WorldCereal Project Crop Calendars provide global, season-specific maps of the start (SOS) and end (EOS) of the growing seasons for key temporary crops, initially focusing on maize and wheat. These calendars are essential for global crop mapping and monitoring, supporting the generation of high-resolution, seasonally updated crop type and irrigation maps. |
| **Provider/Source**  | WorldCereal Consortium (funded by the European Space Agency, ESA) |
| **Homepage/Link**    | [WorldCereal Project](https://esa-worldcereal.org/en) <br> [Global crop calendars of maize and wheat (figshare)](https://tandf.figshare.com/articles/dataset/Global_crop_calendars_of_maize_and_wheat_in_the_framework_of_the_WorldCereal_project/20005293) |
| **License/Terms of Use** | Open and free for research and operational use under Creative Commons Attribution 4.0 License. |
| **Spatial Coverage** | Global, with stratification into agro-ecological zones (AEZs). |
| **Temporal Coverage** | Currently available for 2021 (Phase I); designed for seasonal and annual updates. |
| **Spatial Resolution** | 0.5° x 0.5° latitude/longitude grid (approx. 50 km at equator); crop type maps at 10 m resolution. |
| **Temporal Resolution** | Seasonally updated; provides start and end dates for each major growing season per crop. |
| **Key Variables** | Start of Season (SOS), End of Season (EOS) for maize and wheat (winter and spring cereals); future versions will include additional crops (sunflower, rapeseed, millet, sorghum, barley, rye, soybean). |

## Data Access and Format

| Attribute            | Description |
|----------------------|-------------|
| **Access Methods**   | Download from [figshare dataset page](https://tandf.figshare.com/articles/dataset/Global_crop_calendars_of_maize_and_wheat_in_the_framework_of_the_WorldCereal_project/20005293) (includes gridded SOS/EOS maps and documentation); additional products and documentation available on the [WorldCereal website](https://esa-worldcereal.org/en). |
| **Data Formats**     | NetCDF, GeoTIFF, and CSV for spatial data; PDF and web documentation. |
| **Data Organization**| Organized by crop, season (winter cereals, main maize, secondary maize), and grid cell; maps provided globally at 0.5° resolution. |
| **Potential Challenges** | Currently focused on maize and wheat; spatial resolution of crop calendars is coarser (0.5°) than crop type maps (10 m); future versions will expand crop and temporal coverage. |

## Technical Details

| Attribute            | Description |
|----------------------|-------------|
| **File Naming Conventions** | Files typically include crop, season, and variable (e.g., `SOS_maize_main_2021.tif`). |
| **Variable Names & Units** | SOS (start of season), EOS (end of season); units are day-of-year (1–365/366). |
| **Coordinate Systems** | Latitude/longitude (WGS84 datum) for gridded data; crop type maps use UTM or geographic coordinates. |
| **Data Processing** | Crop calendars are generated by merging national/subnational calendars (GEOGLAM, USDA-FAS, FAO, ASAP) and training a spatially aware Random Forest model using ERA5 climate data to estimate SOS/EOS at each grid cell. This enables stratification into zones with similar growing seasons for crop mapping. |
| **Handling Missing Data** | In areas lacking source data, crop calendars are simulated using climate and geographic predictors; quality flags and confidence layers are provided. |

## API Information

| API Availability | Description |
|------------------|-------------|
| **Direct API**   | No dedicated API for crop calendars. |
| **Programmatic Access** | Data downloadable via [figshare](https://tandf.figshare.com/articles/dataset/Global_crop_calendars_of_maize_and_wheat_in_the_framework_of_the_WorldCereal_project/20005293) and [WorldCereal website](https://esa-worldcereal.org/en); can be integrated into GIS and remote sensing workflows using standard geospatial libraries. |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
| Potential Applications  | <br> - Crop-type mapping and monitoring at global and regional scales  <br> - Crop condition monitoring, yield estimation, and forecasting   <br> - Agroecological zoning and adaptation scenario development  <br> - Supporting operational crop monitoring systems and early warning  <br> - Input for crop models and remote sensing analysis |
| Strengths  |  <br> - Combines multiple authoritative sources and machine learning for robust, spatially explicit crop calendars  <br> - Season-specific, global coverage for maize and wheat, with future expansion to more crops  <br>- Supports high-resolution (10 m) crop type and irrigation mapping |
| Limitations |  <br> - Currently limited to maize and wheat (expansion ongoing)  <br> - Crop calendars at 0.5° resolution, which may be coarse for local studies  <br> - Simulated data in regions with sparse observational input; users should review confidence layers|

## Further Resources

| Resource Type       | Description/Link |
|---------------------|------------------|
| **User Guides/Documentation** | [WorldCereal Final Report (PDF)](https://esa-worldcereal.org/sites/worldcereal/files/VITO-WorldCereal-rapport-FINAL_0.pdf) <br> [ESSD Data Descriptor Article](https://essd.copernicus.org/articles/15/5491/2023/) |
| **Dataset Download** | [figshare: Global crop calendars of maize and wheat](https://tandf.figshare.com/articles/dataset/Global_crop_calendars_of_maize_and_wheat_in_the_framework_of_the_WorldCereal_project/20005293) |
| **Community/Support** | Contact via [WorldCereal website](https://esa-worldcereal.org/en) or through project partners. |

# 3. MIRCA-OS (Monthly Irrigated and Rainfed Cropped Area, Open Source)

*The MIRCA-OS dataset is a valuable resource for agroecological research, providing detailed spatial and temporal crop area information essential for modeling and monitoring agricultural systems globally.*
## Overview

| Attribute            | Description |
|----------------------|-------------|
| **Short Description** | MIRCA-OS is a global, open-source dataset providing monthly irrigated and rainfed cropped area maps for 23 crop classes at 5-arcminute (~10 km) spatial resolution for the years 2000, 2005, 2010, and 2015. It combines subnational crop-specific harvested area statistics with global gridded land cover and crop calendar data to produce monthly growing area grids and annual harvested area maps. |
| **Provider/Source**  | Developed by an international team led by researchers associated with AgMIP and global land use modeling groups. |
| **Homepage/Link**    | [MIRCA-OS Dataset Description (Nature Scientific Data)](https://www.nature.com/articles/s41597-024-04313-w) | [GitHub Repository (Code)](https://github.com/MIRCA-OS/MIRCA-OS_Code) | [HydroShare Dataset](https://www.hydroshare.org/resource/60a890eb841c460192c03bb590687145/) |
| **License/Terms of Use** | Open for research and non-commercial use; citation of original dataset recommended. |
| **Spatial Coverage** | Global (180°W to 180°E longitude, 90°S to 90°N latitude). |
| **Temporal Coverage** | Years 2000, 2005, 2010, and 2015. |
| **Spatial Resolution** | 5 arcminutes (approx. 10 km x 10 km); also annual maps at 0.5° resolution. |
| **Temporal Resolution** | Monthly growing area grids representing crop growth stages from planting to maturity. |
| **Key Variables** | Monthly growing area (ha) for irrigated and rainfed systems, annual harvested area (ha), crop calendars (planting and maturity months). |
|**23 crops covered**|The 23 major crops covered in the MIRCA-OS dataset, with distinctions for irrigated and rainfed systems, are: 1. Barley, 2. Cassava (Tapioca), 3. Cocoa, 4. Coffee, 5. Cotton, 6. Fodder (Alfalfa; grasses and legumes; clover; hay; haylage), 7. Groundnuts (Peanuts), 8. Maize (Corn, including grain, silage, sweet corn, popcorn), 9. Millet (Pearl millet; finger millet; small millet), 10. Oil palm, 11. Potatoes, 12. Pulses (Chickpeas; pigeon peas; cowpeas; peas, beans; lentils; other pulses), 13. Rapeseed (Canola; mustard), 14. Rice (Paddy), 15. Rye, 16. Sugar beet, 17. Sugar cane, 18. Sorghum (grain and silage), 19. Soybeans, 20. Sunflower, 21. Wheat (spring soft wheat; winter soft wheat; durum), 22. Other perennials (e.g., almonds, apples, bananas, citrus fruits, grapes, olives, etc.), 23. Other annuals (various crops not listed above)|

## Data Access and Format

| Attribute            | Description |
|----------------------|-------------|
| **Access Methods**   | Download via [HydroShare](https://www.hydroshare.org/resource/60a890eb841c460192c03bb590687145/), [GitHub (code)](https://github.com/MIRCA-OS/MIRCA-OS_Code), and journal supplementary materials. |
| **Data Formats**     | GeoTIFF and NetCDF for spatial data; CSV for crop calendars. |
| **Data Organization**| Organized by crop, year, irrigation system (irrigated/rainfed), and month; includes monthly growing area grids, maximum monthly growing area maps, and annual harvested area maps. |
| **Potential Challenges** | Large file sizes; requires GIS or scientific programming tools to process (e.g., Python with xarray, R, QGIS). |

## Technical Details

| Attribute            | Description |
|----------------------|-------------|
| **File Naming Conventions** | Format includes crop name, sub-crop number (for multiple cropping), year, irrigation system, and version (e.g., MIRCA-OS_Rice1_2015_ir_v0.1.nc). |
| **Variable Names & Units** | Growing area or harvested area in hectares (ha). Monthly layers numbered 1–12 represent January to December. |
| **Coordinate Systems** | Longitude/latitude in WGS84 datum. |
| **Data Processing** | Combines subnational harvested area statistics with global land cover and crop calendars; downscaled to 5-arcminute grids using area weighting and cropping calendars; gap-filling and mosaicking applied. |
| **Handling Missing Data** | Areas with no crop presence assigned zero; gap-filling based on regional statistics and land cover. |

## API Information

| API Availability | Description |
|------------------|-------------|
| **Direct API**   | No dedicated API available. |
| **Programmatic Access** | Data and processing scripts available on [GitHub](https://github.com/MIRCA-OS/MIRCA-OS_Code); datasets downloadable for use in GIS and programming environments. |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
|**Potential Applications:**  | <br> - Mapping spatial and temporal distribution of crop areas for yield modeling and food security assessments  <br> - Differentiating irrigated and rainfed cropping systems in climate impact and water resource studies  <br> - Supporting crop phenology and cropping intensity analyses  <br> - Input for crop models requiring spatially explicit cropped area and calendar information |
| **Strengths:**  |  <br> - High spatial (5 arcminutes) and temporal (monthly) resolution <br> - Covers 23 major crops with irrigated and rainfed distinctions  <br> - Combines statistical and remote sensing data for improved accuracy |
| **Limitations:**  | <br> - Temporal coverage limited to four years (2000, 2005, 2010, 2015)  <br> - Static within each year, no interannual variability   <br> - Requires technical skills to process large spatial datasets|

## Further Resources

| Resource Type       | Description/Link |
|---------------------|------------------|
| **User Guides/Documentation** | [Nature Scientific Data Article](https://www.nature.com/articles/s41597-024-04313-w) describing dataset and methodology. |
| **Code Repository** | [MIRCA-OS GitHub Repository](https://github.com/MIRCA-OS/MIRCA-OS_Code) with data processing scripts. |
| **Dataset Download** | [HydroShare MIRCA-OS Dataset](https://www.hydroshare.org/resource/60a890eb841c460192c03bb590687145/) |
| **Community/Support** | Contact dataset authors via GitHub or corresponding publication. |

# 4. TerraClimate

*TerraClimate is a foundational resource for agroecological, ecological, and hydrological research, offering consistent, high-resolution climate and water balance data for global terrestrial surfaces.*

## Overview

| Attribute            | Description |
|----------------------|-------------|
| **Short Description** | TerraClimate is a global, high-resolution (~4 km, 1/24°) monthly dataset of climate and climatic water balance variables for terrestrial surfaces, spanning from 1958 to the present. It blends high-resolution climatological normals with coarser time-varying data to provide detailed, temporally consistent climate information. |
| **Provider/Source**  | Climatology Lab, University of California Merced (UCM) |
| **Homepage/Link**    | [Climatology Lab TerraClimate](https://www.climatologylab.org/terraclimate.html) |
| **License/Terms of Use** | Public domain (Creative Commons CC0 license); free for research and operational use. |
| **Spatial Coverage** | Global (all terrestrial surfaces). |
| **Temporal Coverage** | January 1958 to present (updated annually). |
| **Spatial Resolution** | 1/24° (~4 km) latitude/longitude grid. |
| **Temporal Resolution** | Monthly. |
| **Key Variables** | Precipitation, maximum temperature, minimum temperature, wind speed, vapor pressure, vapor pressure deficit, downward shortwave radiation, reference evapotranspiration, actual evapotranspiration, climatic water deficit, soil moisture, runoff, snow water equivalent, Palmer Drought Severity Index (PDSI). |

## Data Access and Format

| Attribute            | Description |
|----------------------|-------------|
| **Access Methods**   | Download via [Climatology Lab website](https://www.climatologylab.org/terraclimate.html), [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/dataset/terraclimate), [Google Earth Engine](https://developers.google.com/earth-engine/datasets/catalog/IDAHO_EPSCOR_TERRACLIMATE), and THREDDS servers. |
| **Data Formats**     | NetCDF (.nc), GeoTIFF (.tif) for some derived products. |
| **Data Organization**| Files organized by variable and year/month; NetCDF files contain multi-dimensional arrays (time, latitude, longitude, variable). |
| **Potential Challenges** | Large file sizes; requires software (e.g., netCDF4, xarray, raster, R) for handling; be aware of missing data flags and annual updates. |

## Technical Details

| Attribute            | Description |
|----------------------|-------------|
| **File Naming Conventions** | Typically includes variable name, year, and month (e.g., `TerraClimate_ppt_1981.nc`). |
| **Variable Names & Units** | See documentation; e.g., `ppt` (precipitation, mm), `tmax`/`tmin` (max/min temperature, °C), `ws` (wind speed, m/s), `srad` (solar radiation, W/m²), `aet` (actual evapotranspiration, mm), `pet` (reference evapotranspiration, mm), etc. |
| **Coordinate Systems** | Latitude and longitude (WGS 84 datum), grid cell centers. |
| **Data Processing** | Combines WorldClim v2 climatological normals with CRU Ts4.0 and JRA55 reanalysis for monthly variability, using climatically aided interpolation. Water balance variables are generated using a modified Thornthwaite-Mather model. |
| **Handling Missing Data** | Missing values are flagged; users should check metadata and handle fill values appropriately. |

## API Information

| API Availability | Description |
|------------------|-------------|
| **Direct API**   | No dedicated API. |
| **Programmatic Access** | Accessible via [Google Earth Engine](https://developers.google.com/earth-engine/datasets/catalog/IDAHO_EPSCOR_TERRACLIMATE), [Microsoft Planetary Computer](https://planetarycomputer.microsoft.com/dataset/terraclimate), and THREDDS servers; can be scripted in Python, R, or other languages using standard geospatial libraries. |

## Relevance for Agroecological Research

| Application/Strength/Limitation | Description                            |
|---------------------------------|----------------------------------------|
| Potential Applications |  <br> - Climate trend and variability analysis at local to global scales  <br> - Drought monitoring, water balance studies, and agricultural risk assessment  <br> - Crop yield modeling, agroclimatic zoning, and ecological/hydrological modeling  <br> - Validation and downscaling of coarser climate datasets |
|Strengths | <br> - High spatial resolution (~4 km) and long temporal coverage (1958–present) <br> - Comprehensive set of climate and water balance variables  <br> - Freely available and widely validated against station and streamflow data|
|Limitations|  <br> - Monthly temporal resolution may not capture short-term extremes <br> - Large data volumes require robust data handling tools <br> - Some variables are model-derived and may have uncertainties in data-sparse regions |

## Further Resources

| Resource Type       | Description/Link |
|---------------------|------------------|
| **User Guides/Documentation** | [Climatology Lab TerraClimate](https://www.climatologylab.org/terraclimate.html), [Scientific Data article](https://www.nature.com/articles/sdata2017191) |
| **Community/Support** | No dedicated forum; general support via Climatology Lab or climate data user communities. |
| **R Package** | [datazoom.amazonia vignette for TerraClimate](https://cran.r-project.org/web/packages/datazoom.amazonia/vignettes/TERRACLIMATE.html) |
  
</details>


<details>
  <summary> Key Climate Indicators of Stress </summary>

#  I.	Direct Environmental Indicators: 
These are measurements of the climatic factors themselves and their deviations from the norm. This section helps to gain a better understanding of the climatic stresses affecting crop production in a given area and makes informed decisions to mitigate potential negative impacts. It provides definitions, calculation methods, formulas, and relevant R and Python packages:

## I. Temperature Extremes
### Definition of Terms
|Term       |	Definition   |
|-----------|--------------|
|Daily Maximum Temperature (Tmax)	|The highest temperature recorded within a 24-hour period (typically from midnight to midnight local time).|
|Daily Minimum Temperature (Tmin) |	The lowest temperature recorded within a 24-hour period.|
|Heatwave	| A prolonged period of abnormally hot weather, often defined based on local climatological conditions (e.g., a certain number of consecutive days exceeding a specific temperature threshold). The threshold and duration can vary.|
|Hot Day |	A day when the daily maximum temperature exceeds a specific threshold (e.g., 30°C, 35°C, or a percentile of historical data).|
|Hot Night	|A night when the daily minimum temperature exceeds a specific threshold (e.g., 20°C, 25°C, or a percentile of historical data).|
|Frost Day |	A day when the daily minimum temperature falls below 0°C.|

## Calculation Methods and Formulas
These indicators are typically calculated from daily temperature data (Tmax and Tmin).


| Indicator | Calculation Method & Formula | 
|------------|----------------------------------------|
| **Heatwave** | <br>  **Method 1 (Absolute Threshold):** Identify periods where Tmax exceeds a fixed threshold (e.g., 32°C) for a minimum number of consecutive days (e.g., 3 days) <br>  **Method 2 (Percentile-Based Threshold):** Calculate a percentile (e.g., 90th percentile) of historical Tmax for a specific period. A heatwave occurs when Tmax exceeds this percentile for a certain number of consecutive days.|
| **Number of Hot Days** | Count the number of days within a specific period (e.g., growing season, year) where Tmax > Threshold_Hot_Day.|
| **Number of Hot Nights** | Count the number of days within a specific period where Tmin > Threshold_Hot_Night.|
| **Number of Frost Days** | Count the number of days within a specific period where Tmin < 0°C.|

## R Packages:

| Packages | Description | 
|------------|----------------------------------------|
| `tidyverse` | For data manipulation and filtering.|
|`dplyr` | Part of `tidyverse`, excellent for filtering days based on temperature thresholds.|
| `climatol` | Specifically designed for climatological analysis, can calculate percentile-based heatwaves and other climate indices. |
| `RClimDex` | Provides functions to calculate a suite of extreme climate indices recommended by the Expert Team on Climate Change Detection and Indices (ETCCDI). This includes heatwave duration index, number of hot days, etc.|

```R
# The R code below performs a basic analysis of simulated daily temperature data. It calculates the number of hot days (Tmax > 30°C), frost days (Tmin < 0°C), and a simplified measure of heatwave days (Tmax > 32°C for at least 3 consecutive days).

library(dplyr)

# Example data frame with daily Tmax and Tmin
climate_data <- data.frame(
  date = seq(as.Date("2024-01-01"), as.Date("2024-12-31"), by = "day"),
  tmax = runif(366, 15, 40),
  tmin = runif(366, 5, 25)
)

# Number of hot days (threshold > 30°C)
hot_days <- climate_data %>% filter(tmax > 30) %>% nrow()
print(paste("Number of hot days:", hot_days))

# Number of frost days (threshold < 0°C)
frost_days <- climate_data %>% filter(tmin < 0) %>% nrow()
print(paste("Number of frost days:", frost_days))

# Identifying heatwaves (Tmax > 32°C for 3 consecutive days - simplified)
climate_data <- climate_data %>%
  mutate(hot_day = ifelse(tmax > 32, 1, 0)) %>%
  mutate(consecutive_hot = ave(hot_day, cumsum(hot_day == 0), FUN = cumsum))
heatwave_days <- climate_data %>% filter(consecutive_hot >= 3) %>% nrow()
print(paste("Number of heatwave days (simplified):", heatwave_days))

```
## Python Packages:

| Packages | Description | 
|------------|----------------------------------------|
| `pandas` | For data manipulation and filtering.|
| `numpy` | For numerical operations. |
| `xarray` | For working with multi-dimensional climate data (often in NetCDF format). |
| `rioxarray` |Extends `xarray` for geospatial raster data. |
| `climopy` | A Python package specifically designed for climate analysis, including the calculation of various climate indices. |
| `ecopy` | Another Python package with some functions for ecological and climate data analysis. |


```python
import pandas as pd
import numpy as np

# Example DataFrame with daily Tmax and Tmin
dates = pd.to_datetime(pd.date_range('2024-01-01', '2024-12-31', freq='D'))
climate_data = pd.DataFrame({
    'date': dates,
    'tmax': np.random.uniform(15, 40, len(dates)),
    'tmin': np.random.uniform(5, 25, len(dates))
})

# Number of hot days (threshold > 30°C)
hot_days = len(climate_data[climate_data['tmax'] > 30])
print(f"Number of hot days: {hot_days}")

# Number of frost days (threshold < 0°C)
frost_days = len(climate_data[climate_data['tmin'] < 0])
print(f"Number of frost days: {frost_days}")

# Identifying heatwaves (Tmax > 32°C for 3 consecutive days - simplified)
climate_data['hot_day'] = (climate_data['tmax'] > 32).astype(int)
climate_data['consecutive_hot'] = (climate_data['hot_day']
                                   .groupby((climate_data['hot_day'] == 0).cumsum())
                                   .cumsum())
heatwave_days = len(climate_data[climate_data['consecutive_hot'] >= 3])
print(f"Number of heatwave days (simplified): {heatwave_days}")

```

## II. Precipitation Anomalies

### Definition of Terms

|Term       |	Definition   |
|-----------|--------------|
|Daily Precipitation | The amount of rainfall recorded in a 24-hour period (typically in millimeters or inches).|
|Dry Spell | A period of consecutive days with rainfall below a certain threshold (e.g., < 1 mm per day). The duration can vary (e.g., 5, 10, or more consecutive dry days). |
|Season Rainfall Amount | The total amount of rainfall received during a defined rainy season. |
|Rain Season Duration | The length of the rainy season, often defined by the onset and cessation dates.|
|Onset of the Rainy Season | The start date of the rainy season, often determined based on specific criteria involving cumulative rainfall over a short period after a certain date or a sequence of wet days. Various methodologies exist (e.g., simple threshold, moving average). |
|Cessation of the Rainy Season | The end date of the rainy season, often determined by criteria involving a prolonged dry spell after a certain date or a sequence of dry days. |
|Intensity of Rainfall Events | Measures like maximum daily rainfall, the number of heavy rainfall days (exceeding a certain threshold), or the Simple Daily Intensity Index (SDII - average rainfall on wet days). |

## Calculation Methods and Formulas
These indicators are calculated from daily precipitation data.


| Indicator | Calculation Method & Formula | 
|------------|----------------------------------------|
|	Dry Spell| Identify consecutive days where daily precipitation < Threshold_Dry_Day (e.g., 1 mm). The length of the dry spell is the number of such consecutive days. |
|	Season Rainfall Amount | Sum of daily precipitation within the defined rainy season (from onset to cessation). $$SeasonRainfall = \sum_{onset}^{cessation} Precipitation_t$$|
|	Rain Season Duration| Number of days between the onset and cessation dates (inclusive). $$Duration = CessationDate − OnsetDate + 1$$ |
|	Onset of the Rainy Season (Example Method - Simple Threshold) | After a specific date (e.g., a climatological start of the season), look for a period of, say, 3 consecutive days with a total rainfall of at least 20 mm, with at least one day receiving more than 10 mm. |
|	Cessation of the Rainy Season (Example Method - Fixed Date after Last Significant Rainfall)| <br>  1.	Identify the last significant rainfall event (e.g., > 10 mm) <br> 2.	The cessation might be defined as a fixed number of days after this event, or when a prolonged dry spell begins. |
|	Intensity of Rainfall Events| <br> **1.	Maximum Daily Rainfall:** The highest daily precipitation value within a period <br> **2.	Number of Heavy Rainfall Days:** Count the number of days within a period where daily precipitation > Threshold_Heavy_Rain (e.g., 10 mm, 20 mm) <br> **3. Simple Daily Intensity Index (SDII):** Sum of daily precipitation on wet days (precipitation ≥ 1 mm) divided by the number of wet days in the period. $$SDII = \frac{\sum_{i=1}^{n} PR_i}{n_{wet}}$$ where $PR_i$ is daily precipitation on wet days, and $n_{wet}$ is the number of wet days. |

## R Packages:

| Packages | Description | 
|------------|----------------------------------------|
|	`tidyverse` | For data manipulation and filtering. |
|	`dplyr` | For filtering days based on precipitation thresholds. |
|	`rclimdex` | Can calculate indices related to precipitation extremes (e.g., consecutive dry days, heavy precipitation days). |
|	`SPEI` | Specifically designed to calculate the Standardized Precipitation-Evapotranspiration Index (SPEI) and also includes functionality for SPI calculation. |
|	`hydroTSM` | Provides functions for time series analysis in hydrology, which can be useful for analyzing precipitation patterns and identifying dry spells. |
|	`rainmaker` | Focuses on rainfall analysis, including onset and cessation of rainy seasons. |

## Python Packages:

| Packages | Description | 
|------------|----------------------------------------|
|	`pandas` | For data manipulation and filtering. |
|	`numpy` | For numerical operations. |
|	`xarray` | For working with multi-dimensional climate data. |
|	`rioxarray` | For geospatial raster data. | 
|	`scipy.stats` | For statistical distributions needed for SPI calculation (e.g., `gamma`). |
|	`pySPI` | A dedicated Python package for calculating the Standardized Precipitation Index (SPI). | 
|	`climatools` | A Python library with various climate analysis functions, potentially including precipitation-related indices. |
|	`esmtools` | A library for Earth System Model analysis, which might contain relevant functions for precipitation analysis. |


</details>


<details>
<summary> Drought Indices </summary>
  
# Drought Indicators and Indices



## Outline

1.  [Introduction](#introduction)

2.  [Types of Drought](#types-of-drought)

3.  [Drought Indicators and Indices](#drought-indicators-and-indices)
4.  [Calculation Details of Drought Indices](#Calculation-Details-of-Drought-Indices)

5.  [Drought Monitoring and Assessment](#drought-monitoring-and-assessment)

6.  [Impacts of Drought](#impacts-of-drought)

7.  [Conclusion](#conclusion)
8.  [References (Optional)](#references-optional)

## 1. Introduction <a name="introduction"></a>

### 1.1. Definition of Drought <a name="definition-of-drought"></a>
Drought is a prolonged period of abnormally low rainfall, leading to a shortage of water. Its precise definition can vary depending on the region, the specific needs for water, and the perspective being considered.

* From a **meteorological** standpoint, drought is defined based on the degree of dryness and the duration of the dry period.
* **Agricultural drought** links meteorological drought to agricultural impacts, focusing on soil moisture deficits and their effect on crop production and livestock.
* **Hydrological drought** refers to deficiencies in surface and subsurface water resources, such as rivers, lakes, reservoirs, and groundwater.
* **Socioeconomic drought** occurs when the supply of water fails to meet the demand of human activities, leading to social and economic consequences.

### 1.2. Importance of Drought Monitoring <a name="importance-of-drought-monitoring"></a>
Accurate and timely drought monitoring is essential for effective water resource management and disaster preparedness.

Drought indicators and indices provide crucial information for:

* **Early Warning Systems:** Identifying the onset and progression of drought to allow for timely interventions.
* **Impact Assessment:** Quantifying the severity and spatial extent of drought on various sectors.
* **Policy Development:** Informing the creation of drought management plans and mitigation strategies.
* **Resource Allocation:** Guiding decisions on water distribution and conservation efforts.
* **Risk Management:** Helping individuals, communities, and businesses prepare for and cope with drought impacts.

### 1.3. Purpose of the Document <a name="purpose-of-the-document"></a>
This document aims to provide a comprehensive overview of drought and the key indicators and indices used to monitor and assess its characteristics. It can also be considered as a guide for understanding and interpreting common drought indices.

It will cover the different types of drought, explain the methodologies behind various indicators, discuss their strengths and limitations, and highlight their role in drought monitoring and impact assessment.

* **Important point to keep in mind when deciding which indicators to use in a study, consider:**
* **The region you are focusing on:** Some indicators are more relevant in certain climate zones or hydrological regimes.
* **The type of drought you want to emphasize:** Agricultural drought will benefit from soil moisture and vegetation indices, while hydrological drought will focus on streamflow and water storage.
* **The availability of data:** Some indicators require more complex or less readily available data.


## 2. Types of Drought <a name="types-of-drought"></a>

### 2.1. Meteorological Drought <a name="meteorological-drought"></a>
Meteorological drought is primarily defined by a significant deviation from normal precipitation patterns over a specified period. This definition is region-specific, as normal precipitation varies greatly geographically.

Key characteristics include the duration of the dry period, the intensity of the precipitation deficit, and its timing relative to the annual precipitation cycle.

Indicators like the Standardized Precipitation Index (SPI) and Percentage of Normal Precipitation are commonly used to quantify meteorological drought.

### 2.2. Agricultural Drought <a name="agricultural-drought"></a>
Agricultural drought occurs when there is insufficient soil moisture available to meet the water demands of crops during different growth stages, ultimately affecting yields.

It takes into account factors like precipitation deficits, evapotranspiration rates, soil water holding capacity, and the specific water requirements of different crops.

Agricultural drought can occur even if meteorological drought is not yet severe, especially if there are prolonged dry spells during critical crop growth periods.

Indicators such as soil moisture content, the Palmer Drought Severity Index (PDSI), and vegetation indices (like NDVI and VCI) are relevant for monitoring agricultural drought.

### 2.3. Hydrological Drought <a name="hydrological-drought"></a>
Hydrological drought refers to deficiencies in surface and subsurface water resources. It typically lags behind meteorological and agricultural drought because it takes time for precipitation deficits to translate into reduced streamflow, lake and reservoir levels, and groundwater storage.

The severity and duration of hydrological drought depend on factors like precipitation amounts and timing, evapotranspiration, surface runoff, and subsurface geological conditions.

Impacts include reduced water availability for irrigation, hydropower generation, industrial and domestic use, and negative effects on aquatic ecosystems.

Indicators used to monitor hydrological drought include streamflow discharge, reservoir and lake levels, groundwater levels, and the Surface Water Supply Index (SWSI).

### 2.4. Socioeconomic Drought <a name="socioeconomic-drought"></a>
Socioeconomic drought is the impact of meteorological, agricultural, or hydrological drought on human activities and the economy. It occurs when water shortages begin to affect the supply and demand of economic goods and services.

The impacts can be wide-ranging and include reduced agricultural production leading to food shortages and price increases, loss of income for farmers and related industries, increased energy costs (due to reduced hydropower), health problems, and social unrest.

Socioeconomic drought is often context-specific and depends on the vulnerability of the population and the water management infrastructure in place.

While not directly measured by a single index, socioeconomic drought is assessed by analyzing the economic and social consequences of the other types of drought.

## 3. Drought Indicators and Indices <a name="drought-indicators-and-indices"></a>

### 3.1. Standardized Precipitation Index (SPI) <a name="standardized-precipitation-index-spi"></a>
* **Description:** The Standardized Precipitation Index (SPI) is a widely used index to characterize meteorological drought on a range of timescales (e.g., 1, 3, 6, 12, 24, 48 months). It quantifies precipitation deficits (or surpluses) relative to the long-term average for a specific location and time period. These different durations reflect the impact of precipitation anomalies on different components of the hydrological system and various human activities.
   
* **Calculation/Methodology (Simplified):** The SPI is calculated by fitting a probability distribution (typically a Gamma distribution) to the long-term precipitation data for a given location and timescale. The cumulative probability is then transformed to a standard normal distribution, resulting in the SPI value. A negative SPI indicates drought, and the magnitude of the negative value reflects the severity.

| SPI Value           | Category | General Interpretation (Meteorological Drought)   | General Relationship to Crop Hazards |
|---------------------|----------|----------------------------------------------------|--------------------------------------|
| ≥ 2.00              | Extremely Wet        | Significantly above average precipitation for the specified duration. | Generally beneficial, but excessive wetness can also cause issues (e.g., waterlogging for some crops).  |
| 1.50 to 1.99        | Very Wet             | Well above average precipitation for the specified duration.  | Generally favorable, but potential for waterlogging in susceptible crops/soils. |
| 1.00 to 1.49        | Moderately Wet    | Above average precipitation for the specified duration.    | Generally positive for crop growth. |
| -0.99 to 0.99       | Near Normal          | Precipitation close to the long-term average for the specified duration.        | Generally adequate for most crops under normal conditions. |
| -1.00 to -1.49      | Moderately Dry       | Below average precipitation, indicating a moderate drought for the duration.      | Potential for moisture stress, especially for water-sensitive crops or during critical growth stages. Yield reductions possible.   |
| -1.50 to -1.99      | Severely Dry         | Significantly below average precipitation, indicating a severe drought.           | Likely to cause significant moisture stress, impacting growth and potentially leading to substantial yield losses for many crops. |
| ≤ -2.00             | Extremely Dry        | Exceptionally low precipitation, indicating an extreme drought.                   | High probability of severe crop failure or significant yield losses for most crops without irrigation.  |

* **Temporal and Spatial Scale:** SPI can be calculated for various time scales, allowing for the monitoring of short-term (e.g., agricultural drought) and long-term (e.g., hydrological drought) precipitation deficits. It is spatially flexible and can be calculated for individual stations, regions, or even globally.

  | SPI Timescale (Months) | Phenomena Reflected                                      | Applications                                                                 |
  |------------------------|----------------------------------------------------------|------------------------------------------------------------------------------|
  | **1-3 (Short-Term)**   | Topsoil moisture, small streamflow, early vegetation stress, fire risk | Agricultural drought monitoring (early warning), short-term water resource management, fire risk assessment |
  | **6-12 (Medium-Term)** | Larger streamflow, smaller to medium reservoir levels, early groundwater recharge impacts, established agricultural drought | Agricultural drought assessment, water resource management (rivers, medium reservoirs), hydropower planning |
  | **24-48+ (Long-Term)** | Large reservoir and lake levels, major aquifer levels, ecological drought, socio-economic impacts | Long-term water resource planning, groundwater monitoring, ecological drought assessment, drought preparedness and mitigation |

* **Strengths:**
    * Simple to calculate and interpret.
    * Can be used to analyze drought at multiple timescales, making it useful for different applications.
    * Allows for comparisons of drought severity across different regions and time periods.
    * Probabilistically based, providing a statistical measure of drought.
* **Limitations:**
    * Only considers precipitation and does not account for other factors like temperature, evapotranspiration, or soil moisture.
    * Requires a long period of historical precipitation data for reliable calculation.
    * The choice of the probability distribution can influence the results in some cases.
* **Data Sources:** Historical precipitation data from rain gauge stations or gridded precipitation datasets.

### 3.2. Palmer Drought Severity Index (PDSI) <a name="palmer-drought-severity-index-pdsi"></a>
* **Description:** The Palmer Drought Severity Index (PDSI) is a more complex index that attempts to measure the cumulative deficit in the water balance. It considers precipitation, temperature, and evapotranspiration, as well as factors like soil moisture, runoff, and recharge.
* **Calculation/Methodology (Simplified):** The PDSI uses a water balance equation to estimate the amount of moisture supply needed for normal conditions in a region. It then compares this with the actual moisture supply to determine the severity of drought or wet spells. The index values typically range from -4.0 (extreme drought) to +4.0 (extremely wet).

| PDSI Value          | Category             | General Interpretation (Long-Term Moisture Conditions) | General Relationship to Crop Hazards|
|---------------------|----------------------|--------------------------------------------------------|-------------------------------------|
|≥ +4.00	|Extremely Wet |	Prolonged period of exceptionally high moisture surplus. Soil moisture is excessive, and water resources are abundant. | |
|+3.00 to +3.99	| Very Wet	| Extended period of significant moisture surplus. Soil moisture is well above average, and water resources are plentiful. | |
|+2.00 to +2.99 |	Moderately Wet	| Extended period of moderate moisture surplus. Soil moisture is above average, and water resources are generally good. | |
|+1.00 to +1.99	| Slightly Wet	|Extended period with a small moisture surplus. Soil moisture is slightly above average. | |
|+0.5 to +0.99	| Incipient Wet Spell	| Beginning of a period with slightly above normal moisture. | |
|-0.49 to +0.49	| Near Normal	| Moisture conditions are close to the long-term average. | |
|-0.50 to -0.99	| Incipient Dry Spell |	Beginning of a period with slightly below normal moisture. | |
|-1.00 to -1.99 |	Mild Drought	| Extended period of mild moisture deficit. Soil moisture is below average, and some water stress may begin to appear. | |
|-2.00 to -2.99 |	Moderate Drought	| Extended period of moderate moisture deficit. Soil moisture is significantly below average, and crop stress is likely. Water shortages may develop. | |
|-3.00 to -3.99 |	Severe Drought	| Extended period of substantial moisture deficit. Soil moisture is very low, and significant crop damage and water shortages are expected.| |
|≤ -4.00	| Extreme Drought	| Prolonged period of exceptionally severe moisture deficit. Soil moisture is critically low, widespread crop failure and severe water shortages are highly probable.| |

* **Temporal and Spatial Scale:** PDSI is typically calculated on a monthly basis and is suitable for assessing long-term drought conditions. It is often used at regional or larger scales.

  | PDSI Characteristic          | Phenomena Reflected       |   Key Applications  |                                                                                        
  |------------------------------|---------------------------|---------------------|
  | **Timescale Relevance**      | Primarily reflects **long-term drought conditions** (months to years) due to its cumulative nature. Responds slower to short-term changes. | Assessing prolonged drought impacts on agriculture and water resources. Historical drought analysis.|
  | **Phenomena Reflected**      | Cumulative moisture deficit or surplus, considering precipitation, temperature, and soil moisture. Good for broad-scale, long-term conditions.| Identifying long-lasting drought events and their severity. Comparing drought severity across different regions.|
  | **Key Applications**         | Historical drought analysis, broad-scale drought monitoring, assessing long-term agricultural and hydrological impacts.| Policy decisions related to long-term drought management and water allocation.|

* **Strengths:**
    * Considers both precipitation and temperature, providing a more comprehensive assessment of drought.
    * Attempts to account for soil moisture conditions.
    * Has been widely used for decades, providing a long historical record.
* **Limitations:**
    * Can be slow to respond to rapidly changing conditions due to its cumulative nature.
    * The underlying model relies on several assumptions and empirical relationships that may not be universally applicable.
    * Can be influenced by the accuracy of temperature and evapotranspiration estimates.
* **Data Sources:** Monthly precipitation and temperature data, as well as estimates of potential evapotranspiration and soil water holding capacity.

### 3.3. Vegetation Condition Index (VCI) <a name="vegetation-condition-index-vci"></a>
* **Description:** The Vegetation Condition Index (VCI) uses satellite-derived Normalized Difference Vegetation Index (NDVI) data to assess the health and vigor of vegetation relative to its historical range. It expresses the current NDVI as a percentage of the historical maximum-minimum range for a given location and time of year.
* **Calculation/Methodology (Simplified):** VCI = (NDVI\_current - NDVI\_min) / (NDVI\_max - NDVI\_min) \* 100. Where NDVI\_current is the NDVI for the current period, and NDVI\_min and NDVI\_max are the minimum and maximum NDVI values observed in the historical record for the same period.
* **Temporal and Spatial Scale:** VCI can be calculated at various temporal resolutions (e.g., weekly, bi-weekly, monthly) and spatial resolutions depending on the satellite data used. It is particularly useful for monitoring agricultural drought and vegetation stress.

| VCI Characteristic          | Phenomena Reflected           |    Key Applications    |
|-----------------------------|-------------------------------|------------------------|
| **Timescale Relevance**     | Typically used for **short-to-medium term** impacts on vegetation health (weeks to months), aligning with vegetation growth cycles.| Monitoring real-time vegetation stress due to drought. Early warning of agricultural drought impacts.|
| **Phenomena Reflected**     | Vegetation health and vigor relative to its historical range, indicating moisture stress affecting plant growth.                             | Assessing the spatial extent and severity of vegetation drought stress. Identifying areas with potential crop yield reductions. |
| **Key Applications**        | Agricultural drought monitoring, vegetation stress assessment, early warning of famine or food insecurity, land degradation monitoring.      | Guiding targeted interventions for agricultural support and disaster relief. |
  
* **Strengths:**
    * Provides a direct measure of vegetation health and response to moisture stress.
    * Utilizes readily available satellite data, allowing for broad spatial coverage.
    * Can provide early indications of agricultural drought impacts.
* **Limitations:**
    * Can be influenced by factors other than drought, such as pests, diseases, and land management practices.
    * May not be suitable for areas with sparse or non-uniform vegetation.
    * The accuracy depends on the quality and resolution of the satellite data.
* **Data Sources:** Satellite imagery providing NDVI data (e.g., MODIS, AVHRR).

### 3.4. Standardized Precipitation-Evapotranspiration Index (SPEI) <a name="standardized-precipitation-evapotranspiration-index-spei"></a>
* **Description:** The Standardized Precipitation-Evapotranspiration Index (SPEI) is an extension of the SPI that considers the impact of temperature on drought. It quantifies the deficit or surplus of water supply (precipitation) relative to atmospheric water demand (potential evapotranspiration - PET) over a specific period.
* **Calculation/Methodology (Simplified):**
    1.  Calculate the difference between monthly precipitation and potential evapotranspiration (PET). Various methods can be used to estimate PET (e.g., Thornthwaite, Hargreaves).
    2.  Aggregate these monthly differences over different timescales (similar to SPI: 1, 3, 6, 12, etc. months).
    3.  Fit a probability distribution (often a Log-logistic distribution) to the aggregated water balance data.
    4.  Transform the cumulative probability to a standard normal distribution, resulting in the SPEI value. Negative SPEI values indicate drought, with the magnitude reflecting severity.
* **Temporal and Spatial Scale:** SPEI can be calculated for various time scales, making it suitable for monitoring different types of drought. It is spatially flexible and can be applied at local, regional, and global levels.

| SPEI Timescale (Months) | Phenomena Reflected  | Applications    |
|-------------------------|----------------------|-----------------|
| **1-3 (Short-Term)**    | Short-term **climatic water balance** impacting topsoil moisture under evaporative demand, stress on rain-fed agriculture considering temperature, fire risk influenced by dryness and heat. | Agricultural drought monitoring (early warning considering temperature impacts), short-term water resource management under evaporative stress, fire risk assessment. |
| **6-12 (Medium-Term)**  | Medium-term **climatic water balance** affecting streamflow in larger rivers under thermal influences, reservoir levels considering evaporation, evolving agricultural drought under changing water demand. | Agricultural drought assessment considering temperature, water resource management for rivers and medium reservoirs accounting for evaporation, hydropower planning under climate influences. |
| **24-48+ (Long-Term)** | Long-term **climatic water balance** impacting large reservoir and lake levels with significant evaporation effects, major aquifer recharge under changing climate, prolonged ecological and socio-economic impacts influenced by both precipitation and temperature. | Long-term water resource planning under climate change, groundwater monitoring considering long-term water balance, assessment of ecological drought under thermal stress, drought preparedness and mitigation in a warming climate. |
  
* **Strengths:**
    * Incorporates the effect of temperature and potential evapotranspiration, making it more sensitive to the impacts of climate change on drought.
    * Allows for the assessment of drought severity in terms of water balance rather than just precipitation deficits.
    * Can be used across different timescales, similar to SPI.
    * Provides a standardized measure for comparing drought conditions across different climates.
* **Limitations:**
    * The accuracy depends on the method used to estimate potential evapotranspiration, and different methods can yield varying results.
    * Requires both precipitation and temperature data.
    * Interpretation can be slightly more complex than SPI due to the inclusion of PET.
* **Data Sources:** Monthly precipitation and temperature data.

### 3.5. Rainfall Anomaly Index (RAI) <a name="rainfall-anomaly-index-rai"></a>
* **Description:** The Rainfall Anomaly Index (RAI) is another index used to quantify meteorological drought. It measures the deviation of precipitation from the long-term mean, taking into account whether the anomaly is positive (wet) or negative (dry). The calculation differs slightly for positive and negative anomalies to account for the skewed nature of rainfall data.
* **Calculation/Methodology (Simplified):**
    1.  Calculate the long-term mean precipitation for a specific period (e.g., monthly, seasonal) and location.
    2.  Calculate the mean of the positive deviations from the long-term mean and the mean of the negative deviations from the long-term mean.
    3.  For a given period's precipitation ($P_i$):
        * If $P_i \ge \bar{P}$ (long-term mean):
            $$RAI = +3 \times \frac{P_i - \bar{P}}{\overline{P}_{H10} - \bar{P}}$$
            where $\overline{P}_{H10}$ is the mean of the 10 highest precipitation values in the historical record for that period.
        * If $P_i < \bar{P}$:
            $$RAI = -3 \times \frac{P_i - \bar{P}}{\bar{P} - \overline{P}_{L10}}$$
            where $\overline{P}_{L10}$ is the mean of the 10 lowest precipitation values in the historical record for that period.
* **Temporal and Spatial Scale:** RAI can be calculated for various time scales (monthly, seasonal, annual) and is applicable at different spatial scales depending on the availability of precipitation data.

| RAI Characteristic          | Phenomena Reflected   | Key Applications   |
|-----------------------------|-----------------------|--------------------|
| **Timescale Relevance**     | Calculated for **various timescales** (monthly, seasonal, annual), focusing purely on precipitation deviations.| Simple meteorological drought monitoring, particularly in regions where precipitation data is the primary available variable. |
| **Phenomena Reflected**     | Departure of precipitation from the long-term mean, with separate calculations for positive and negative anomalies. | Identifying and classifying the severity of wet and dry periods based solely on rainfall. |
| **Key Applications**        | Basic meteorological drought assessment, historical rainfall variability studies.    | Providing a straightforward measure of precipitation deficits for non-complex analyses.  |

* **Strengths:**
    * Relatively simple to calculate.
    * Considers the magnitude of both wet and dry anomalies in a way that acknowledges the typical distribution of rainfall.
    * Can be useful in regions where the statistical assumptions of SPI might not be fully met.
* **Limitations:**
    * The use of the 10 highest and lowest values can make it sensitive to extreme events in the historical record.
    * Does not take into account evapotranspiration or other water balance components.
    * The scaling factor of 3 is somewhat arbitrary.
* **Data Sources:** Historical precipitation data.

### 3.6. Percentage of Normal Precipitation (PNP) <a name="percentage-of-normal-precipitation-pnp"></a>
* **Description:** Percentage of Normal Precipitation (PNP) is a straightforward indicator that expresses the current precipitation for a specific period as a percentage of the long-term average (normal) precipitation for the same period.
* **Calculation/Methodology (Simplified):**
    $$PNP = \frac{\text{Current Period Precipitation}}{\text{Long-Term Average Precipitation}} \times 100$$
* **Temporal and Spatial Scale:** PNP can be calculated for any time scale (e.g., monthly, seasonal, annual) and at any location where precipitation data is available.

| PNP Characteristic          | Phenomena Reflected | Key Applications    |
|-----------------------------|---------------------|---------------------|
| **Timescale Relevance**     | Can be calculated for **any timescale**, providing a simple snapshot of precipitation relative to the average.  | Quick and easy communication of precipitation status to a general audience. |
| **Phenomena Reflected**     | Current precipitation as a percentage of the long-term average precipitation for the same period.  | Identifying areas with precipitation deficits or surpluses relative to their normal amounts. |
| **Key Applications**        | Initial drought screening, public awareness campaigns, simple climate summaries.   | Providing a basic understanding of how current precipitation compares to the norm.  |

* **Strengths:**
    * Very simple to calculate and easy to understand.
    * Provides a quick and intuitive measure of precipitation deficit or surplus.
    * Requires only precipitation data.
* **Limitations:**
    * Does not account for the variability of precipitation or the statistical significance of the departure from normal. A 70% of normal precipitation might be a severe drought in a dry region but less so in a wet region.
    * Does not consider the timing or intensity of rainfall events.
    * Ignores other important factors like temperature, evapotranspiration, and soil moisture.
    * Can be less meaningful for short time scales or in regions with highly variable precipitation.
* **Data Sources:** Current and historical precipitation data.
### 3.7. Soil Moisture Content <a name="soil-moisture-content"></a>
* **Description:** Soil Moisture Content refers to the amount of water present in a given volume or mass of soil. It is a direct measure of the water available in the root zone and is a key factor in agricultural drought. It can be expressed in various units, such as volumetric water content (volume of water per unit volume of soil) or gravimetric water content (mass of water per unit mass of dry soil).
* **Calculation/Methodology (Simplified):**
    * **Direct Measurement:** Typically involves collecting soil samples, weighing them, drying them in an oven, and re-weighing them. The difference in weight represents the water content. Various in-situ sensors (e.g., time domain reflectometry - TDR, capacitance sensors) can also provide continuous measurements.
    * **Modeling:** Land surface models use meteorological inputs (precipitation, temperature, radiation, etc.) and soil properties to simulate soil moisture at different depths.
* **Temporal and Spatial Scale:** Soil moisture can be measured or modeled at various temporal resolutions (e.g., hourly, daily, weekly) and spatial scales (from point measurements to regional or global grids).
* **Strengths:**
    * Provides a direct indication of the water available to plants.
    * Highly relevant for assessing agricultural drought.
    * In-situ measurements offer high accuracy at specific locations.
    * Models can provide spatially continuous estimates.
* **Limitations:**
    * Direct measurements are labor-intensive and provide only point information.
    * The spatial variability of soil moisture can be high, making it challenging to extrapolate point measurements.
    * Model accuracy depends on the quality of input data and the complexity of the model.
    * Interpretation can be influenced by soil type and depth.
* **Data Sources:** In-situ soil moisture sensors, soil surveys, land surface models (e.g., GLDAS, SMAP, Sentinel satellite data with soil moisture algorithms).

### 3.8. Soil Moisture Anomaly (SMA) <a name="soil-moisture-anomaly-sma"></a>
* **Description:** Soil Moisture Anomaly (SMA) quantifies the difference between the current soil moisture conditions and the long-term average (climatology) for the same period of the year. It helps to identify areas where soil moisture is significantly above or below normal.
* **Calculation/Methodology (Simplified):**
    1.  Calculate the long-term average soil moisture for each time step (e.g., daily, weekly) based on historical data (either from measurements or models).
    2.  Subtract the long-term average soil moisture from the current soil moisture value for the corresponding time step.
    3.  The anomaly can be expressed in absolute terms (e.g., mm of water) or standardized by dividing by the standard deviation of the historical soil moisture data, similar to the SPI.
* **Temporal and Spatial Scale:** SMA can be calculated at the same temporal and spatial scales as the underlying soil moisture data (measurements or models).
* **Strengths:**
    * Provides a context for the current soil moisture conditions relative to what is typical for the time of year.
    * Useful for identifying regions experiencing unusually dry or wet soil conditions.
    * Standardized SMA allows for comparisons across different regions and soil types.
* **Limitations:**
    * The accuracy depends on the quality and length of the historical soil moisture data.
    * Interpretation can still be influenced by soil type and the specific water holding characteristics of the soil.
    * May not directly reflect the impact on plants without considering plant-available water.
* **Data Sources:** Historical and current soil moisture data from in-situ sensors or models (e.g., those used for Soil Moisture Content).

### 3.9. Percent of Plant Available Water (PAW) <a name="percent-of-plant-available-water-paw"></a>
* **Description:** Percent of Plant Available Water (PAW) estimates the fraction of water in the soil that plants can readily access. It considers the soil's field capacity (the upper limit of water that soil can hold against gravity) and wilting point (the soil moisture level at which plants can no longer extract water).
* **Calculation/Methodology (Simplified):**
    1.  Determine the field capacity (FC) and wilting point (WP) for the specific soil type and depth. These values are often obtained from soil surveys or laboratory analyses.
    2.  Measure or model the current soil moisture content (SMC).
    3.  Calculate the Plant Available Water (PAW) as:
        $$PAW = SMC - WP$$
    4.  Calculate the Percent of Plant Available Water (%PAW) as:
        $$\%PAW = \frac{SMC - WP}{FC - WP} \times 100$$
* **Temporal and Spatial Scale:** %PAW can be determined at the same temporal and spatial scales as the soil moisture content data, provided that information on FC and WP is available for the corresponding locations and depths.
* **Strengths:**
    * Directly relates soil moisture to plant water availability, making it highly relevant for agricultural drought assessment.
    * Accounts for the soil's physical properties that influence water retention and release.
    * Provides a more ecologically relevant measure of drought stress for vegetation.
* **Limitations:**
    * Requires knowledge of soil-specific parameters (FC and WP), which may not be readily available for all locations or depths.
    * The actual water availability to plants can also be influenced by root depth and plant physiology.
    * The accuracy depends on the accuracy of the soil moisture data and the FC/WP values.
* **Data Sources:** In-situ soil moisture sensors, soil surveys (for FC and WP), land surface models that simulate soil moisture and sometimes provide related information.
### 3.10. Streamflow Index <a name="streamflow-index"></a>
* **Description:** Streamflow Index refers to various indices that characterize drought based on the flow of rivers and streams. These indices typically compare current streamflow to historical streamflow data for the same time period. Different variations exist, such as the Standardized Streamflow Index (SSI).
* **Calculation/Methodology (Simplified for SSI):**
    1. Obtain long-term historical streamflow data for a specific river or gauging station.
    2. Fit a probability distribution (often a Gamma or Log-normal distribution) to the streamflow data for a specific time period (e.g., monthly).
    3. Transform the cumulative probability to a standard normal distribution, resulting in the SSI value. Similar to SPI, negative SSI values indicate hydrological drought, with the magnitude reflecting severity. Other simpler streamflow indices might just use percentiles or deviations from the mean.
* **Temporal and Spatial Scale:** Streamflow indices can be calculated for various time scales (e.g., monthly, seasonal, annual) and are specific to the river or stream being monitored at a particular gauging station. Regional indices can be created by aggregating data from multiple stations.
* **Strengths:**
    * Directly reflects the availability of surface water resources.
    * Integrates the effects of precipitation, evapotranspiration, and storage in the watershed.
    * Crucial for managing water supplies for irrigation, municipal use, and hydropower.
    * SSI provides a standardized measure for comparison across different rivers and time periods.
* **Limitations:**
    * Requires long-term historical streamflow data.
    * Can be influenced by upstream water management practices (e.g., dam releases, diversions).
    * May not fully represent groundwater contributions to streamflow, especially in the short term.
    * The choice of probability distribution for SSI can affect results.
* **Data Sources:** Streamflow data from hydrologic gauging stations operated by government agencies (e.g., USGS, local water authorities).

### 3.11. Reservoir and Lake Levels <a name="reservoir-and-lake-levels"></a>
* **Description:** Monitoring the water levels (or storage volumes) of reservoirs and lakes is a direct way to assess hydrological drought, particularly concerning water availability for human uses and ecosystem health. Declining levels indicate water shortages.
* **Calculation/Methodology (Simplified):** Typically involves regular measurements of water surface elevation using gauging stations installed at reservoirs and lakes. These levels are often converted to storage volumes using known bathymetry (depth contours). Drought conditions are assessed by comparing current levels/volumes to historical averages, operational thresholds, or minimum pool levels.
* **Temporal and Spatial Scale:** Reservoir and lake levels are monitored at various time intervals (e.g., daily, weekly, monthly) and are specific to each individual water body.
* **Strengths:**
    * Directly indicates the amount of stored surface water available.
    * Crucial for managing water supply, irrigation releases, hydropower generation, and recreational activities.
    * Easy to understand and communicate to the public.
    * Historical data on reservoir and lake levels is often readily available.
* **Limitations:**
    * Levels are heavily influenced by management decisions (e.g., releases, diversions) and may not solely reflect natural drought conditions.
    * The relationship between precipitation deficits and reservoir/lake level declines can be complex and time-lagged.
    * Does not provide information on streamflow or groundwater conditions.
* **Data Sources:** Water level and storage data from agencies that manage reservoirs and lakes (e.g., dam operators, water management districts).

### 3.12. Groundwater Levels <a name="groundwater-levels"></a>
* **Description:** Groundwater levels, measured in wells, provide an indication of the amount of water stored beneath the Earth's surface. Declining groundwater levels during a prolonged dry period signify hydrological drought and can lead to water shortages for wells and springs, as well as impact baseflow to rivers.
* **Calculation/Methodology (Simplified):** Water levels in wells are measured periodically using various techniques (e.g., electric tapes, pressure transducers). Drought conditions are assessed by comparing current water levels to historical averages, long-term trends, or established thresholds for concern. Indices like the Standardized Groundwater Index (SGI) can also be calculated, similar to SPI and SSI.
* **Temporal and Spatial Scale:** Groundwater levels are monitored at individual wells, with monitoring frequency varying (e.g., monthly, quarterly, annually). Regional assessments require data from a network of wells. The response of groundwater levels to drought can be slow and varies depending on aquifer characteristics.
* **Strengths:**
    * Represents a significant long-term water resource.
    * Provides insights into the sustainability of water supplies.
    * Can indicate the potential for future streamflow reductions (baseflow).
    * SGI provides a standardized measure for assessing groundwater drought.
* **Limitations:**
    * Groundwater levels respond slowly to precipitation changes, so declines may lag behind meteorological drought.
    * Influenced by pumping rates and other human activities.
    * Data availability can be limited in some areas.
    * Interpretation requires understanding of local hydrogeology and aquifer properties.
* **Data Sources:** Groundwater level data from monitoring well networks operated by government agencies (e.g., USGS, state geological surveys, water resource agencies).

### 3.13. Surface Water Supply Index (SWSI) <a name="surface-water-supply-index-swsi"></a>
* **Description:** The Surface Water Supply Index (SWSI) is a composite index specifically designed for snowmelt-dominated regions. It integrates several hydrological variables, including snowpack, streamflow, and reservoir storage, to provide a comprehensive assessment of surface water availability.
* **Calculation/Methodology (Simplified):** SWSI typically combines standardized values of:
    1. Snow water equivalent (SWE) in mountain snowpack.
    2. Streamflow forecasts for the spring and summer runoff period.
    3. Current reservoir storage.
    The specific formula and weighting of these components can vary depending on the region and the relative importance of each water source. The index is often normalized to a scale where negative values indicate water supply deficits (drought) and positive values indicate surpluses.
* **Temporal and Spatial Scale:** SWSI is typically calculated and updated seasonally (e.g., monthly during the snowmelt season) and is relevant for specific river basins or regions where snowmelt is a major contributor to surface water supply.
* **Strengths:**
    * Accounts for the unique hydrological characteristics of snowmelt-driven systems.
    * Integrates key components of the surface water supply.
    * Provides a more holistic assessment of water availability in these regions compared to individual indicators.
    * Useful for forecasting water supply and managing water resources in snow-dependent areas.
* **Limitations:**
    * Only applicable to regions with significant seasonal snowpack.
    * The specific formula and weighting need to be carefully calibrated for each region.
    * Relies on accurate snowpack measurements, streamflow forecasts, and reservoir storage data.
* **Data Sources:** Snowpack data (e.g., from snow surveys or remote sensing), streamflow forecasts from hydrological models, and reservoir storage data from water management agencies.
### 3.14. Enhanced Vegetation Index (EVI) <a name="enhanced-vegetation-index-evi"></a>
* **Description:** The Enhanced Vegetation Index (EVI) is another satellite-derived index that quantifies vegetation greenness. It is designed to optimize the vegetation signal by reducing atmospheric influences (like aerosol scattering) and minimizing soil background effects, making it potentially more sensitive to vegetation changes than NDVI in some cases, especially in high biomass areas.
* **Calculation/Methodology (Simplified):** EVI uses the red, near-infrared (NIR), and blue bands of satellite imagery. The formula typically involves coefficients to correct for atmospheric and soil effects:
    $$EVI = G \times \frac{NIR - Red}{NIR + C_1 \times Red - C_2 \times Blue + L}$$
    where:
    * $G$ is a gain factor (e.g., 2.5).
    * $C_1$ and $C_2$ are coefficients for atmospheric resistance (e.g., 6 and 7.5, respectively).
    * $L$ is a canopy background adjustment factor (e.g., 1).
* **Temporal and Spatial Scale:** Similar to NDVI, EVI can be calculated at various temporal resolutions (e.g., daily, weekly, monthly) and spatial resolutions depending on the satellite data used (e.g., MODIS, VIIRS).
* **Strengths:**
    * Reduced sensitivity to atmospheric effects and soil background noise compared to NDVI.
    * Improved sensitivity in high biomass regions where NDVI can saturate.
    * Can provide a better indication of vegetation health and vigor under certain conditions.
* **Limitations:**
    * The formula is more complex than NDVI.
    * Interpretation still requires understanding of vegetation phenology and other influencing factors.
    * Sensitivity might be reduced in very sparse vegetation areas.
* **Data Sources:** Satellite imagery with red, near-infrared (NIR), and blue spectral bands (e.g., MODIS, VIIRS, Landsat).

### 3.15. Land Surface Temperature (LST) <a name="land-surface-temperature-lst"></a>
* **Description:** Land Surface Temperature (LST) is the radiative skin temperature of the Earth's surface, as measured by thermal infrared sensors on satellites. During drought, reduced soil moisture and vegetation stress can lead to increased LST. Anomalously high LST can therefore be an indicator of drought conditions.
* **Calculation/Methodology (Simplified):** LST is derived from the thermal infrared radiance measured by satellite sensors. The process involves atmospheric correction and often requires knowledge of surface emissivity (how efficiently the surface radiates energy), which can be estimated based on vegetation indices or other land cover information.
* **Temporal and Spatial Scale:** LST is available at various temporal resolutions (e.g., daily, 8-day, monthly) and spatial resolutions depending on the thermal sensors used (e.g., MODIS, Landsat thermal bands).
* **Strengths:**
    * Provides information on the surface energy balance, which is directly linked to moisture availability and evapotranspiration.
    * High LST can indicate water stress in vegetation and dry soil conditions.
    * Can be used to monitor the spatial extent and intensity of thermal anomalies associated with drought.
* **Limitations:**
    * LST is influenced by various factors other than drought, such as solar radiation, air temperature, and land cover type.
    * Interpretation as a drought indicator often requires analyzing LST anomalies relative to the long-term average or in conjunction with vegetation indices.
    * Accuracy depends on atmospheric correction and emissivity estimates.
* **Data Sources:** Thermal infrared satellite imagery (e.g., MODIS, VIIRS, Landsat thermal bands).

### 3.16. Normalized Difference Water Index (NDWI) <a name="normalized-difference-water-index-ndwi"></a>
* **Description:** The Normalized Difference Water Index (NDWI) is a satellite-derived index used to monitor changes in the water content of vegetation and soil. Different versions of NDWI exist, but they typically use combinations of near-infrared (NIR) and short-wave infrared (SWIR) or green spectral bands. SWIR is particularly sensitive to liquid water in vegetation canopies and soil.
* **Calculation/Methodology (Simplified - one common formulation using NIR and SWIR):**
    $$NDWI = \frac{NIR - SWIR}{NIR + SWIR}$$
    Another formulation uses Green and NIR bands, often more related to open water bodies. The specific bands used depend on the satellite sensor and the intended application (vegetation water content vs. open water).
* **Temporal and Spatial Scale:** NDWI can be calculated at various temporal and spatial resolutions depending on the availability of suitable satellite imagery (e.g., MODIS, Landsat).
* **Strengths:**
    * Sensitive to the water content of vegetation and soil.
    * Can provide information on vegetation water stress associated with drought.
    * SWIR-based NDWI can penetrate the atmosphere better than visible bands in some cases.
* **Limitations:**
    * Can be influenced by vegetation density and structure.
    * The relationship between NDWI and actual water content can be complex and may require calibration.
    * Sensitivity to soil background can still be an issue, especially in sparse vegetation areas.
* **Data Sources:** Satellite imagery with near-infrared (NIR) and short-wave infrared (SWIR) bands (e.g., MODIS, Landsat).

### 3.17. Evapotranspiration (ET) and Evaporative Stress Index (ESI) <a name="evapotranspiration-et-and-evaporative-stress-index-esi"></a>
* **Description:**
    * **Evapotranspiration (ET):** Represents the total water lost from the land surface to the atmosphere through evaporation from soil and water bodies and transpiration from plants. Reduced ET can be an indicator of water scarcity during drought.
    * **Evaporative Stress Index (ESI):** Specifically aims to capture anomalies in the ratio of actual to potential evapotranspiration (ET/PET). A low ESI indicates that actual ET is much lower than potential ET, suggesting water stress and drought conditions where the atmospheric demand for water is not being met by the surface supply.
* **Calculation/Methodology (Simplified):**
    * **ET:** Satellite-based ET is typically estimated using energy balance models that incorporate remotely sensed data (e.g., land surface temperature, vegetation indices, radiation) and meteorological data.
    * **ESI:** ESI is often derived from remotely sensed land surface temperature (LST). Anomalously high LST relative to vegetation greenness (e.g., as indicated by VCI) suggests high evaporative stress and low actual ET compared to PET. Various algorithms exist to calculate ESI.
* **Temporal and Spatial Scale:** ET and ESI are typically available at various temporal resolutions (e.g., daily, weekly, monthly) and spatial resolutions depending on the satellite data and models used.
* **Strengths:**
    * ET provides a direct measure of water fluxes from the surface.
    * ESI specifically highlights conditions where there is a mismatch between atmospheric water demand and surface water supply, which is a key aspect of drought.
    * Remote sensing allows for spatially continuous monitoring of ET and ESI.
* **Limitations:**
    * Accuracy of ET estimates depends on the complexity and parameterization of the models used.
    * ESI derived from LST can be influenced by factors other than water stress.
    * Interpretation may require understanding of vegetation types and phenology.
* **Data Sources:** Satellite imagery (e.g., MODIS, Landsat for LST and vegetation indices), meteorological reanalysis data, and land surface models that produce ET estimates.

### 3.18. Vegetation Health Index (VHI) <a name="vegetation-health-index-vhi"></a>
* **Description:** The Vegetation Health Index (VHI) is a composite index that combines information on vegetation greenness (typically from VCI) and thermal stress (typically derived from Land Surface Temperature or a related Temperature Condition Index - TCI). It aims to provide a more comprehensive assessment of vegetation health and drought impacts by considering both water availability and thermal conditions.
* **Calculation/Methodology (Simplified):** VHI is often calculated as a weighted average of the Vegetation Condition Index (VCI) and the Temperature Condition Index (TCI):
    $$VHI = \alpha \times VCI + (1 - \alpha) \times TCI$$
    where $\alpha$ is a weighting factor (often 0.5).
    TCI is typically derived by normalizing the Land Surface Temperature (LST) relative to its historical range, similar to how VCI is derived from NDVI.
* **Temporal and Spatial Scale:** VHI has the same temporal and spatial resolution as the VCI and LST data used in its calculation.
* **Strengths:**
    * Integrates the effects of both moisture stress (from VCI) and thermal stress (from TCI) on vegetation health.
    * Can provide a more robust indicator of agricultural drought and vegetation condition than using VCI or LST alone.
    * Useful for monitoring the combined impacts of water scarcity and heat stress on vegetation.
* **Limitations:**
    * The choice of the weighting factor ($\alpha$) can influence the results and may need to be adjusted based on the region and vegetation type.
    * The accuracy depends on the quality of the underlying NDVI and LST data and the derivation of VCI and TCI.
    * Interpretation still requires consideration of vegetation phenology and other factors affecting plant health.
* **Data Sources:** Satellite imagery providing NDVI and Land Surface Temperature (LST) data (e.g., AVHRR, MODIS).
### 3.19. U.S. Drought Monitor (USDM) <a name="us-drought-monitor-usdm"></a>
* **Description:** The U.S. Drought Monitor (USDM) is a weekly map showing the location and intensity of drought across the United States. It is produced through a synthesis of multiple indices, climate observations, and reports from experts at the national, regional, and state levels. The USDM categorizes drought intensity into five levels: Abnormally Dry (D0), Moderate Drought (D1), Severe Drought (D2), Extreme Drought (D3), and Exceptional Drought (D4).
* **Calculation/Methodology (Simplified):** The USDM is not based on a single mathematical formula but rather on a "convergence of evidence" approach. It integrates various meteorological, hydrological, and agricultural drought indicators, including:
    * **Meteorological:** SPI, SPEI, Palmer indices (PDSI, Palmer Hydrological Drought Index - PHDI, Palmer Moisture Anomaly Index - Z-index), precipitation percentiles.
    * **Hydrological:** Streamflow, reservoir levels, groundwater levels, snow water equivalent.
    * **Agricultural:** Soil moisture, satellite-based vegetation health indices (NDVI, VCI), crop condition reports.
    Experts from various agencies and regions review these data, along with local impacts and conditions, to draw the weekly drought boundaries and assign intensity categories based on a set of descriptive criteria for each level.
* **Temporal and Spatial Scale:** The USDM is produced weekly and covers the entire United States, including Puerto Rico and other U.S. territories. The spatial resolution is at the county level, with finer-scale variations within counties based on the underlying data and expert input.
* **Strengths:**
    * Provides a comprehensive and integrated assessment of drought conditions by considering multiple lines of evidence.
    * Incorporates expert knowledge and local impacts, making it highly relevant for decision-making.
    * Widely recognized and used for drought monitoring, impact assessment, and triggering drought-related actions.
    * Available weekly, providing timely information on evolving drought conditions.
* **Limitations:**
    * Subjectivity can be introduced through the expert interpretation process.
    * The relative weight given to different indicators can vary depending on the region and the experts involved.
    * The spatial resolution is limited to counties, which may mask finer-scale drought variations.
    * Primarily focused on the United States.
* **Data Sources:** A wide range of federal, state, and local data sources, including NOAA (precipitation, temperature, streamflow, reservoirs), USDA (soil moisture, crop conditions), USGS (groundwater, streamflow), NASA (satellite data), and expert reports.

### 3.20. Combined Drought Indicator (CDI) <a name="combined-drought-indicator-cdi"></a>
* **Description:** A Combined Drought Indicator (CDI) is a general term for an index that integrates multiple drought-related variables or indicators across different domains (meteorological, agricultural, hydrological) to provide a more robust and holistic assessment of drought conditions and risks. The specific variables and methodologies used to create a CDI can vary significantly depending on the region, the intended application, and the data availability.
* **Calculation/Methodology (Simplified - varies greatly):** CDIs typically involve the following steps:
    1. **Selection of Component Indicators:** Identifying relevant indicators from different drought types (e.g., SPI for meteorological, soil moisture for agricultural, streamflow for hydrological).
    2. **Standardization or Normalization:** Transforming the component indicators to a common scale to allow for comparison and combination (e.g., using percentiles, z-scores, or other statistical methods).
    3. **Weighting (Optional):** Assigning weights to the component indicators based on their perceived importance or relevance for the specific region and application. Weights can be equal or based on statistical analysis or expert judgment.
    4. **Aggregation:** Combining the standardized (and potentially weighted) component indicators using mathematical formulas (e.g., averaging, weighted sum, or more complex multivariate techniques) to produce a single CDI value or category.
* **Temporal and Spatial Scale:** The temporal and spatial scale of a CDI depends on the scales of the input indicators used in its calculation. It can range from local to regional and can be updated at various time intervals (e.g., weekly, monthly).

| CDI Characteristic          | Phenomena Reflected  | Key Applications     |
|-----------------------------|----------------------|----------------------|
| **Timescale Relevance** | Varies depending on the component indicators included, typically aiming for a **multi-timescale** perspective for a more robust assessment.  | Region-specific drought monitoring and early warning systems, tailored to local conditions and vulnerabilities. Integrated assessment for specific sectors (e.g., agriculture, water supply).   |
| **Phenomena Reflected** | Integrated measure of drought severity by combining standardized and potentially weighted information from meteorological, agricultural, and hydrological indicators. Aims for a holistic view of drought. | Providing a more reliable and context-specific assessment of drought conditions and risks. Enhancing the accuracy of drought monitoring and forecasts for targeted actions.  |
| **Key Applications** | Regional drought management, triggering local drought response plans, sector-specific drought monitoring and decision support, research on integrated drought assessment methodologies. | Improving the effectiveness of drought management strategies by providing a more nuanced and locally relevant understanding of drought conditions. Supporting proactive drought risk management.  |

* **Strengths:**
    * Provides a more comprehensive assessment of drought by integrating information from multiple drought types.
    * Can potentially provide a more reliable indicator of drought onset, persistence, and severity compared to relying on a single indicator.
    * Can be tailored to the specific characteristics and data availability of a particular region.
    * Can be designed to better reflect the impacts of drought on specific sectors (e.g., agriculture, water resources).
* **Limitations:**
    * The development and interpretation of a CDI can be complex and require careful consideration of the selection, standardization, weighting, and aggregation methods.
    * The optimal combination of indicators and weights may vary across different regions and applications.
    * Data availability for all desired component indicators may be a limiting factor in some areas.
    * The "black box" nature of some CDIs can make it challenging to understand the contribution of individual components.
* **Data Sources:** Depends on the component indicators included in the CDI. Common sources include meteorological observations (precipitation, temperature), soil moisture data (in-situ or modeled), streamflow and reservoir data, and satellite-based vegetation indices.

## 4. Calculation Details of Drought Indices <a name="Calculation-Details-of-Drought-Indices"></a>

This section provides more specific details on how the drought indices discussed earlier are calculated, the variables required, the general formulations, and relevant packages/functions available in R and Python.

### 4.1. Standardized Precipitation Index (SPI)

* **How is it calculated?** SPI calculation involves fitting a probability distribution (typically Gamma) to long-term precipitation data for a specific location and time scale (e.g., 1, 3, 6, 12 months). This fitted distribution is then transformed to a standard normal distribution (mean 0, standard deviation 1), and the SPI value is the z-score (number of standard deviations the observed precipitation deviates from the mean).
* **What variables are needed?** Long-term historical precipitation data (at least 30 years is recommended) for the desired location and at a consistent time step (e.g., monthly).
* **Inputs:** A time series of precipitation data.
* **Formulation (Conceptual):**
    1.  Select a time scale ($k$).
    2.  Aggregate precipitation over the chosen time scale for each period in the historical record.
    3.  Fit a Gamma distribution to the aggregated precipitation data. The probability density function of the Gamma distribution is:
        $$f(x; \alpha, \beta) = \frac{1}{\Gamma(\alpha)\beta^\alpha} x^{\alpha-1} e^{-x/\beta} \quad \text{for } x > 0, \alpha > 0, \beta > 0$$
        where $\alpha$ is the shape parameter and $\beta$ is the scale parameter, estimated from the data. $\Gamma(\alpha)$ is the Gamma function.
    4.  Calculate the cumulative probability $H(x) = P(X \le x)$ from the fitted Gamma distribution. For periods with zero precipitation, a separate probability $q = P(X=0)$ is estimated.
    5.  Transform the cumulative probability to a standard normal distribution (with mean zero and variance one). If $H(x) > 0.5$, the SPI is:
        $$SPI = z = \Phi^{-1}(H(x))$$
        where $\Phi^{-1}$ is the inverse standard normal cumulative distribution function. A similar transformation is used if $H(x) \le 0.5$, adjusting for the probability of zero precipitation.
* **R Packages/Functions:**
    * `SPEI` package: `spi()` function. This is a dedicated package for drought indices and includes SPI calculation.
* **Python Packages/Functions:**
    * `scipy.stats`: While `scipy.stats` provides functions for fitting distributions (`gamma.fit`, `gamma.cdf`) and the inverse normal CDF (`norm.ppf`), you would need to implement the SPI calculation steps yourself.
    * `climopy`: This climate analysis library includes a function `spi()` in its `drought` module.
    * `xclim`: For climate data analysis, `xclim` has a `standardized_precipitation_index` function.
* **Efficiency:** The `SPEI` package in R and `xclim` in Python are generally efficient as they are designed for climate time series analysis and often optimized for speed. For Python, using vectorized operations with libraries like NumPy within `climopy` or `xclim` will be more efficient than manual looping with `scipy.stats`.

### 4.2. Palmer Drought Severity Index (PDSI)

* **How is it calculated?** PDSI is calculated based on a water balance equation that considers precipitation, evapotranspiration, soil moisture recharge, runoff, and soil moisture loss. It uses empirically derived coefficients that vary by location and attempts to quantify the cumulative moisture deficit or surplus.
* **What variables are needed?** Monthly precipitation and temperature data, as well as information on the soil's available water capacity.
* **Inputs:** Time series of monthly precipitation and temperature, and a value for the available water capacity of the soil.
* **Formulation (Conceptual - highly simplified):**
    1.  Calculate potential evapotranspiration (PET) using a temperature-based method (e.g., Thornthwaite).
    2.  Estimate potential runoff, potential recharge, and potential loss from the soil based on previous conditions and PET.
    3.  Calculate the moisture anomaly for each month as the difference between the actual precipitation and the "required" precipitation for normal conditions (which depends on PET and the potential terms).
    4.  Accumulate these moisture anomalies over time, weighted by empirically derived coefficients ($K_i$) that vary spatially and temporally. The PDSI value at time $t$ is a function of the PDSI at time $t-1$ and the current moisture anomaly.
* **R Packages/Functions:**
    * `SPEI` package: `pdsi()` function.
* **Python Packages/Functions:**
    * `droughtindices`: This package includes a `pdsi()` function.
* **Efficiency:** The `SPEI` package in R and `droughtindices` in Python provide relatively efficient implementations of the PDSI calculation.

### 4.3. Vegetation Condition Index (VCI)

* **How is it calculated?** VCI is calculated by normalizing the current Normalized Difference Vegetation Index (NDVI) value based on the historical range of NDVI for the same time of year and location. It expresses the current vegetation condition as a percentage of the historical extremes.
* **What variables are needed?** Time series of NDVI data (derived from satellite imagery) over a long period (to establish historical minimum and maximum values).
* **Inputs:** A time series of NDVI values for the area of interest.
* **Formulation:**
    $$VCI = \frac{NDVI_{current} - NDVI_{min}}{NDVI_{max} - NDVI_{min}} \times 100$$
    where $NDVI_{current}$ is the NDVI value for the current period, and $NDVI_{min}$ and $NDVI_{max}$ are the minimum and maximum NDVI values observed in the historical record for the same period (e.g., same week or month of the year).
* **R Packages/Functions:**
    * While no dedicated VCI function might exist in standard drought packages, you can easily implement this using raster processing packages like `raster` or `terra` along with basic arithmetic.
* **Python Packages/Functions:**
    * `rasterio` or `rioxarray` for reading and processing raster (satellite) data. NumPy can then be used for the VCI calculation. Libraries like `xarray` can also be helpful for managing multi-dimensional raster data.
* **Efficiency:** Efficiency depends on the size of the raster datasets. Using vectorized operations in R (`raster` or `terra`) and Python (NumPy, `rioxarray`) is crucial for efficient processing of large satellite imagery.

### 4.4. Standardized Precipitation-Evapotranspiration Index (SPEI)

* **How is it calculated?** SPEI builds upon SPI by first calculating the monthly climatic water balance (precipitation minus potential evapotranspiration). This water balance series is then treated similarly to precipitation in the SPI calculation: fitting a probability distribution (typically Log-logistic), transforming it to a standard normal distribution.
* **What variables are needed?** Long-term historical monthly precipitation and temperature data (to estimate PET).
* **Inputs:** Time series of monthly precipitation and temperature.
* **Formulation (Conceptual):**
    1.  Calculate monthly potential evapotranspiration (PET) using a suitable method (e.g., Thornthwaite, Hargreaves). The Hargreaves method requires temperature and extraterrestrial radiation.
    2.  Calculate the monthly water balance $D_i = P_i - PET_i$.
    3.  Aggregate the water balance over different time scales ($k$).
    4.  Fit a Log-logistic probability distribution to the aggregated water balance series. The cumulative distribution function of the Log-logistic distribution is:
        $$F(x; \alpha, \beta) = \frac{1}{1 + (\frac{\alpha}{x})^\beta}$$
        where $\alpha$ is a scale parameter and $\beta$ is a shape parameter, estimated from the data.
    5.  Transform the cumulative probability to a standard normal distribution to obtain the SPEI value.
* **R Packages/Functions:**
    * `SPEI` package: `spei()` function.
* **Python Packages/Functions:**
    * `SPEI` package (a Python port of the R package).
    * `xclim`: Includes `standardized_precipitation_evapotranspiration_index` function.
* **Efficiency:** Similar to SPI, the `SPEI` package in both R and Python, and `xclim` in Python, are designed for efficiency in processing climate time series.

### 4.5. Rainfall Anomaly Index (RAI)

* **How is it calculated?** RAI measures the normalized departure of precipitation from the long-term mean, calculated separately for positive and negative anomalies using the means of the highest and lowest deciles.
* **What variables are needed?** Long-term historical precipitation data.
* **Inputs:** A time series of precipitation data.
* **Formulation:** (As provided in the previous detailed section for RAI).
* **R Packages/Functions:** No dedicated function readily available in standard drought packages, but it can be implemented using basic R functions.
* **Python Packages/Functions:** No dedicated function readily available in standard drought packages, but it can be implemented using NumPy.
* **Efficiency:** The calculation is straightforward and can be implemented efficiently using vectorized operations in both R and Python.

### 4.6. Percentage of Normal Precipitation (PNP)

* **How is it calculated?** PNP is a simple ratio of current period precipitation to the long-term average precipitation for the same period, multiplied by 100.
* **What variables are needed?** Current precipitation and long-term average precipitation.
* **Inputs:** Current precipitation value and the long-term average precipitation value for the corresponding time period.
* **Formulation:**
    $$PNP = \frac{\text{Current Precipitation}}{\text{Long-Term Average Precipitation}} \times 100$$
* **R Packages/Functions:** Can be easily calculated using basic R arithmetic.
* **Python Packages/Functions:** Can be easily calculated using basic Python arithmetic with libraries like NumPy if dealing with arrays of data.
* **Efficiency:** The calculation is very efficient.

### 4.7. Enhanced Vegetation Index (EVI)

* **How is it calculated?** EVI uses the red, NIR, and blue bands of satellite imagery with specific coefficients to improve vegetation signal and reduce atmospheric and soil effects.
* **What variables are needed?** Reflectance values from the red, near-infrared (NIR), and blue bands of satellite imagery.
* **Inputs:** Raster data containing reflectance values for the required bands.
* **Formulation:** (As provided in the previous detailed section for EVI).
* **R Packages/Functions:** `raster`, `terra`, `rgdal` for reading and manipulating raster data.
* **Python Packages/Functions:** `rasterio`, `rioxarray` for raster data handling, NumPy for the calculation.
* **Efficiency:** Efficient processing requires vectorized operations on raster arrays, which are well supported by the mentioned packages.

### 4.8. Land Surface Temperature (LST)

* **How is it calculated?** LST derivation involves converting thermal radiance measured by satellites to temperature, requiring atmospheric correction and emissivity estimation.
* **What variables are needed?** Thermal band radiance from satellite imagery, and potentially data for atmospheric correction and emissivity estimation (which can be derived from other bands or external datasets).
* **Inputs:** Raster data containing thermal band radiance.
* **Formulation:** The formulation is sensor-specific and involves radiative transfer equations and emissivity adjustments. It's often provided in the documentation for the satellite data.
* **R Packages/Functions:** `raster`, `terra`, `ncdf4` (for NetCDF data) for reading satellite data. Specific LST algorithms might need to be implemented or are available in specialized remote sensing packages.
* **Python Packages/Functions:** `rasterio`, `rioxarray`, `netCDF4` for data handling. Libraries like `pyTSEB` or `eeepy` (for Google Earth Engine) might offer LST processing capabilities or tools to access LST products.
* **Efficiency:** Depends on the complexity of the LST retrieval algorithm and the size of the data. Efficient processing involves optimized array operations.

### 4.9. Normalized Difference Water Index (NDWI)

* **How is it calculated?** NDWI uses the ratio of differences to sums of specific spectral bands (typically NIR and SWIR, or Green and NIR) to highlight water content.
* **What variables are needed?** Reflectance values from the required spectral bands (depending on the NDWI formulation).
* **Inputs:** Raster data containing reflectance values for the required bands.
* **Formulation:** (As provided in the previous detailed section for NDWI).
* **R Packages/Functions:** `raster`, `terra`.
* **Python Packages/Functions:** `rasterio`, `rioxarray`, NumPy.
* **Efficiency:** Efficient with vectorized raster operations.

### 4.10. Evapotranspiration (ET) and Evaporative Stress Index (ESI)

* **How is it calculated?** ET often involves complex energy balance models. ESI typically uses the anomaly of LST relative to vegetation conditions.
* **What variables are needed?** Depends on the ET model (can include radiation, temperature, humidity, wind speed, vegetation indices, LST). ESI often needs LST and a vegetation index like VCI or NDVI.
* **Inputs:** Various meteorological and remote sensing datasets.
* **Formulation:** ET formulations are model-dependent (e.g., Penman-Monteith). ESI formulations vary based on the specific algorithm used to relate LST and vegetation.
* **R Packages/Functions:** Packages like `Evapotranspiration`, `SPEI` (for PET calculation). Remote sensing packages for input data.
* **Python Packages/Functions:** Libraries like `pyet`, `rioxarray`, `xarray`. Google Earth Engine Python API (`eeepy`) provides access to ET products.
* **Efficiency:** Depends heavily on the complexity of the ET/ESI calculation and the size of the input data.

### 4.11. Vegetation Health Index (VHI)

* **How is it calculated?** VHI is a weighted combination of VCI and TCI (Temperature Condition Index, derived from LST).
* **What variables are needed?** NDVI (to calculate VCI) and Land Surface Temperature (LST) (to calculate TCI).
* **Inputs:** Raster data for NDVI and LST.
* **Formulation:** (As provided in the previous detailed section for VHI). TCI is often calculated similarly to VCI:
    $$TCI = \frac{LST_{max} - LST_{current}}{LST_{max} - LST_{min}} \times 100$$
* **R Packages/Functions:** `raster`, `terra`.
* **Python Packages/Functions:** `rasterio`, `rioxarray`, NumPy.
* **Efficiency:** Efficient with vectorized raster operations.

### 4.12. U.S. Drought Monitor (USDM)

* **How is it calculated?** Not a direct calculation but a synthesis of multiple indicators and expert input.
* **What variables are needed?** Numerous meteorological, hydrological, and agricultural variables (as listed in the previous detailed section).
* **Inputs:** Gridded and station-based data for various indicators, expert assessments.
* **Formulation:** No single formula. Relies on thresholds and expert judgment based on the convergence of evidence.
* **R Packages/Functions:** No direct package to replicate the USDM process. Packages for individual component indicators would be used.
* **Python Packages/Functions:** Similarly, no direct package. Libraries for individual component indicators would be used.
* **Efficiency:** Not applicable as it's a human-driven synthesis process.

### 4.13. Combined Drought Indicator (CDI)

* **How is it calculated?** Varies greatly depending on the specific CDI. Involves selecting, standardizing, weighting, and aggregating multiple indicators.
* **What variables are needed?** Depends on the chosen component indicators.
* **Inputs:** Data for the chosen component indicators.
* **Formulation:** Highly variable, ranging from simple averages to complex weighted sums or multivariate methods.
* **R Packages/Functions:** Depends on the component indicators. Packages for time series analysis (`zoo`, `xts`), spatial analysis (`raster`, `sf`), and statistical methods would be used.
* **Python Packages/Functions:** Depends on the component indicators. Libraries like NumPy, Pandas, SciPy, `xarray`, `rioxarray` would be common.
* **Efficiency:** Depends on the complexity of the CDI and the size of the input datasets. Efficient implementations would leverage vectorized operations.




## 5. Drought Monitoring and Assessment <a name="drought-monitoring-and-assessment"></a>

### 5.1. Early Warning Systems <a name="early-warning-systems"></a>
Drought indicators play a critical role in early warning systems by providing timely information on the onset, severity, and spatial extent of drought.

Monitoring trends in meteorological indicators like SPI can signal the beginning of a precipitation deficit. Agricultural indicators like VCI can provide early warnings of vegetation stress.

Integrated monitoring of multiple indicators across different timescales can improve the accuracy and reliability of drought forecasts.

Early warning systems often involve disseminating drought information to stakeholders, including farmers, water managers, and policymakers, to facilitate proactive responses.

### 5.2. Drought Severity Classification <a name="drought-severity-classification"></a>
Drought indicators are often used to classify drought severity into different categories (e.g., D0 - Abnormally Dry, D1 - Moderate Drought, D2 - Severe Drought, D3 - Extreme Drought, D4 - Exceptional Drought, as used by the U.S. Drought Monitor).

These classifications are based on predefined thresholds of indicator values and help to communicate the intensity and potential impacts of drought.

Different indicators may have their own specific thresholds for defining drought severity. For example, SPI values of -1.0 to -1.5 often indicate moderate drought, while values below -2.0 indicate extreme drought.

Consistent and standardized classification systems are essential for effective drought management and communication.

### 5.3. Spatial Analysis and Mapping <a name="spatial-analysis-and-mapping"></a>
Geographic Information Systems (GIS) and remote sensing technologies are crucial for visualizing and analyzing the spatial patterns of drought using indicator data.

Drought maps, generated from spatially interpolated indicator values, provide a clear picture of the geographical distribution and severity of drought.

This spatial information is vital for targeted interventions and resource allocation to the most affected areas.

Time series of drought maps can also be used to track the evolution and progression of drought over time.

### 5.4. Integration of Multiple Indicators <a name="integration-of-multiple-indicators"></a>
A comprehensive assessment of drought often requires considering multiple indicators across different drought types and timescales.

Relying on a single indicator can be misleading, as different indicators capture different aspects of the drought phenomenon.

A 'convergence of evidence' approach, where multiple indicators point towards similar drought conditions, provides a more robust and reliable assessment.

For example, severe agricultural drought is more likely when meteorological indicators show prolonged precipitation deficits, soil moisture levels are low, and vegetation indices indicate significant stress.

## 6. Impacts of Drought <a name="impacts-of-drought"></a>

### 6.1. Agriculture <a name="agriculture"></a>
* Reduced crop yields and quality due to insufficient water availability.
* Livestock losses due to lack of pasture and water.
* Increased risk of plant diseases and pest infestations.
* Economic losses for farmers and the agricultural sector.
* Food price increases and potential food insecurity.

### 6.2. Water Resources <a name="water-resources"></a>
* Reduced streamflow and river levels, impacting water supply for various uses.
* Lowering of lake and reservoir levels, affecting storage capacity and water availability.
* Depletion of groundwater resources, potentially leading to long-term water scarcity.
* Increased competition for limited water resources among different sectors.
* Deterioration of water quality due to reduced dilution of pollutants.

### 6.3. Ecosystems <a name="ecosystems"></a>
* Vegetation stress and mortality, leading to changes in plant communities.
* Habitat loss and reduced water availability for wildlife.
* Increased risk of wildfires due to dry vegetation.
* Impacts on aquatic ecosystems due to low flows and reduced water quality.
* Increased susceptibility of ecosystems to invasive species.

### 6.4. Socioeconomic <a name="socioeconomic"></a>
* Economic losses in agriculture, tourism, energy production (hydropower), and other water-dependent sectors.
* Increased unemployment and reduced income in affected communities.
* Health problems related to water scarcity and poor water quality.
* Social unrest and conflicts over water resources.
* Displacement of populations due to severe water shortages or agricultural failures.
* Increased energy consumption and costs for pumping water from deeper wells.

## 7. Conclusion <a name="conclusion"></a>

Drought is a complex and multifaceted phenomenon with significant environmental, economic, and social consequences.

The use of various drought indicators and indices is crucial for effectively monitoring, assessing, and managing drought risks.

Understanding the strengths and limitations of different indicators is essential for their appropriate application.

An integrated approach that considers multiple indicators and incorporates spatial analysis is vital for a comprehensive understanding of drought conditions.

Continuous monitoring and the development of robust early warning systems are essential for building resilience to future drought events.



## 8. References (Optional) <a name="references-optional"></a>

o	Svoboda, M., & Fuchs, B. A. (2016). Handbook of Drought Indicators and Indices. Integrated Drought Management Programme (IDMP), Integrated Drought Management Tools and Guidelines Series 2. World Meteorological Organization (WMO) and Global Water Partnership (GWP).   
o	Wilhite, D. A. (2000). Drought: A Global Assessment (Vol. 1). Routledge.
o	Heim Jr., R. R. (2002). A review of twentieth-century drought indices used in the United States. Bulletin of the American Meteorological Society, 83(8), 1149-1165.  

o	McKee, T. B., Doesken, N. J., & Kleist, J. (1993). The relationship of drought frequency and duration to time scales. In Eighth Conference on Applied Climatology (pp. 179-184). American Meteorological Society.  
o	Lloyd-Hughes, B., & Saunders, M. A. (2002). A drought climatology for Europe. International Journal of Climatology, 22(11), 1571-1592. 

o	Palmer, W. C. (1965). Meteorological drought. US Department of Commerce, Weather Bureau. 
o	Alley, W. M. (1984). The Palmer drought severity index: Limitations and assumptions. Journal of Climate and Applied Meteorology, 23(7), 1100-1109.   

o	Kogan, F. N. (1990). Remote sensing of drought with AVHRR. In Seventh Conference on Applied Climatology (pp. 175-178). American Meteorological Society. 
o	Kogan, F. N. (1995). Application of vegetation index and brightness temperature for drought detection. Advances in Space Research, 15(11), 91-100. 
o	Vicente-Serrano, S. M., Beguería, S., & López-Moreno, J. I. (2010). A multiscalar drought index sensitive to global warming: The Standardized Precipitation Evapotranspiration Index. Journal of Climate, 23(7), 1696-1718.    

o	Van Rooy, M. P. (1965). A rainfall anomaly index independent of time and space. Notos, 14, 43-48. 


o	Huete, A., Didan, K., Miura, T., Rodriguez, E. P., Gao, X., & Ferreira, L. G. (2002). Overview of the radiometric and biophysical performance of the MODIS vegetation indices. Remote Sensing of Environment, 83(1-2), 195-213. 
o	Gao, B. C. (1996). NDWI—A normalized difference water index for remote sensing of vegetation liquid water from space. Remote Sensing of Environment, 58(3), 257-266.  

o	Anderson, M. C., Norman, J. M., Kustas, W. P., Houborg, R., Starks, P. J., & Agnellus, C. (2013). Mapping daily evapotranspiration at field to continental scales using geostationary and polar orbiting satellite imagery. Hydrology and Earth System Sciences, 17(6), 2451-2469. 
o	Anderson, M. C., Hain, C. R., Karnieli, A., Goetz, S. J.,лое, B. F., Kustas, W. P., ... & White, W. A. (2011). Evaluation of drought indices based on thermal remote sensing and мультисенсорные data. Remote Sensing of Environment, 115(10), 2655-2669. 

o	Kogan, F. N. (1995). Application of AVHRR in large-area drought monitoring. Remote Sensing of Environment, 51(1), 103-115. 

o	Svoboda, M., LeComte, D., Hayes, M., Gleason, K., Heim, R., предательство, T., ... & Rippey, B. (2002). The drought monitor. Bulletin of the American Meteorological Society, 83(8), 1181-1190. 
 
</details>


<details>
<summary> Existing Climate Data Tools </summary>

## 1. Climate Data Tool (CDT)

| Feature                     | Description     | Link                               |
|----------------------------:|-----------------|------------------------------------|
| **Name**                    | Climate Data Tool (CDT)              | [IRI Climate Data Tool Website](http://iridl.ldeo.columbia.edu/maproom/CDT/) |
| **Developer**               | International Research Institute for Climate and Society (IRI) | [IRI Website](https://iri.columbia.edu/)  |
| **License**                 | Free and Open Source  | [CDT Download/Information (likely contains license details)](http://iridl.ldeo.columbia.edu/maproom/CDT/) |
| **Primary Purpose** | Climate data management, quality control, analysis, and visualization, primarily for developing countries.  | [IRI Climate Data Tool Overview](http://iridl.ldeo.columbia.edu/maproom/CDT/Overview.html) |
| **Key Functionalities** | Data organization, QC, merging, extraction, statistical analysis, climatologies, anomalies, rainfall analysis, extremes, visualization. | [CDT Modules and Features](http://iridl.ldeo.columbia.edu/maproom/CDT/Documentation.html) |
| **User Interface** | Graphical User Interface (GUI) built on R   | [CDT Documentation (likely includes UI details)](http://iridl.ldeo.columbia.edu/maproom/CDT/) |
| **Programming Language** | R      | [The R Project for Statistical Computing](https://www.r-project.org/) |
| **Relevance** | Benchmarking, inspiration for features, understanding the existing ecosystem.   |   -         |
</details>

