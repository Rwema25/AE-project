# AE-project
The “Advancing Climate Data Integration in Agroecological Research” project, aims to improve the capacity of agroecological researchers and practitioners to integrate climate data into their work.

Documenting the datasets and packages is part of the project’s activities. The table below provides details on the datasets mentioned during user engagement interviews. 


| Rank | Dataset name  | Data source | Data format | Data type | Temp. resolution | Temp. coverage | Update freq | H. resolution | Variable | Perm | APIs | Package | Doc | 
|-----:|---------------|-------------|-------------|-----------|------------------|----------------|-------------|---------------|----------|------|------|---------|-----|
|     1|  ERA5         | ECMWF       | GRIB        | Gridded   | Hourly           | 1940 to present| Daily       | 0.25 x 0.25 degrees for the reanalysis              | Total precipitation, Sea surface temperature,...         | Register/ create account      | [Link](https://cds.climate.copernicus.eu/how-to-api)     | cdsapi (Python)  | [Link](https://confluence.ecmwf.int/display/CKB/ERA5%3A+data+documentation)    |
|     2|  CHIRPS       | Climate Hazards Group at the University of California, Santa Barbara | NetCDF, TIFF, BIL, PNG  | Gridded       |   Daily to annual time intervals| 1981 to near-real time  | April 2015 | 0.05 x 0.05 degrees  | precipitation |      |  [Link](https://data.chc.ucsb.edu/products/CHIRPS-2.0/africa_daily/tifs/p05/)    |         | [Link](https://data.chc.ucsb.edu/products/CHIRPS-2.0/README-CHIRPS.txt)    |
|     3|  NASA power   |             |             |           |                  |                |             |               |          |      |      |         |     |
|     4|  Agri-food    | Gardian-CGIAR         |             |           |                  |                |             |               | Agri-food data |      |  [Link](https://documenter.getpostman.com/view/15684001/2s9YBz3ajj) ; [Link](https://gardian.cgiar.org/api)   |         | [Link](https://gardian.cgiar.org/maps/)    |

<details>
<summary> For User Engagement </summary>

| PERSONA | STAKEHOLDER  | CONTACT     | EMAIL       | DATE      | REGION           | INTERV.        | STATUS      | COMMENTS      |  
|---------|--------------|-------------|-------------|-----------|------------------|----------------|-------------|---------------|
| Scientist | AIMS RIC   | Dr. Mouhamadou Bamba Sylla| msylla@aimsric.org| Rwanda   |                  |                |             |               |     
| Policy Advisor  | Agrimet             |             |             |           |                  |                |             |               |   
| Policy Advisor   | ICPAC  |             |             |           |                  |                |             |               |   
| Policy Advisor|  Met service   | Dr. Vedaste Iyakaremye|viyakaremye@meteorwanda.gov.rw| Rwanda |                  |                |             |               |    
| Policy Advisor   | RICA  | Dr. Magnifique Ndambe Nzaramba | mnzaramba@rica.rw| Rwanda| | | | |
| Policy Advisor    | RAB | | | | | | | |
| Policy Advisor    | REMA|David Ukwishaka |dukwishaka@rema.gov.rw | Rwanda | | | | |
| Policy Advisor  | GIZ | Olivier Niyompuhwe | olivier.niyompuhwe@giz.de | Rwanda | | | | |
| Policy Advisor   | SADEC| | | | | | | |

</details>


<details>
<summary> Existing Climate Data Tools </summary>

| Name    | Source       | Uded for    | Package     | Data format| Output      | Rainy season Char. | Climate Extr. indices | Drought indices      | Available | Issues |
|---------|--------------|-------------|-------------|-----------|------------------|----------------|-------------|---------------|---------------|------------|
| CDT     | International Research Institute for Climate and Society   |Data preparation, Quality control, Gridding, Validation, Analysis, Visualization | CDT (in R)| Csv, NetCDF   | Data, Maps, Time series    | Onset, Cessation, Season Length               | Precipitation, temperature    | SPI, SPEI, Deciles | GitHub: [Link](https://github.com/rijaf-iri/CDT) | GitHub: [Link](https://github.com/rijaf-iri/CDT/issues/1) |
| East Africa Drought Watch||||||||SPI, SMA, CDI, FAPAR Anomaly||[Link](https://droughtwatch.icpac.net/report-v2/?qstr=eyJwYXJhbXMiOnsicmVwb3J0aW5nX3VuaXQiOiJFYXN0IEFmcmljYSBSZWdpb24iLCJhZG1pbl9sZXZlbCI6bnVsbCwidW5pdF9pZCI6bnVsbCwicGFfaWQiOm51bGwsInBsYWNlbmFtZSI6IkVhc3QgQWZyaWNhIFJlZ2lvbiIsInBlcmlvZF9jeWNsZSI6IkRla2FkYWwiLCJkYXRhX2RhdGUiOiIyMDE4LTAxLTIxIiwic21hX2RhdGFfZGF0ZSI6IjIwMTgtMDEtMTEiLCJmYXBhbl9kYXRhX2RhdGUiOiIyMDE4LTAxLTIxIiwic3BpX2RhdGFfZGF0ZSI6IjIwMTgtMDEtMDEiLCJ0aW1lc2NhbGUiOm51bGwsInByb2plY3RfbmFtZSI6bnVsbCwicmVzdG9yZV9wZGYiOmZhbHNlfSwic2hhcmUiOnsib3BlbiI6ZmFsc2UsImNvcGllZCI6ZmFsc2UsInRpbnlfdXJsIjpudWxsfSwic2VsZWN0ZWQiOnsiZGF0YV9kYXRlIjoiMjAxOC0wMS0yMSIsInBlcmlvZF9jeWNsZSI6IkRla2FkYWwiLCJ0aW1lc2NhbGUiOm51bGwsInJlc3RvcmVfcGRmIjpmYWxzZX0sImV4cG9ydCI6eyJwZGYiOnsibG9hZGluZyI6ZmFsc2UsImVycm9yIjpudWxsfX19)|
</details>


<details>
<summary> Indicators </summary>
  
# Drought Indicators 
  
## Standardized Precipitation Index (SPI)

This indicator measures anomalies of accumulated precipitation during a given period (e.g. 1, 3, 12 months), and is the most commonly used indicator for detecting and characterizing meteorological droughts.

## Soil Moisture Anomaly (SMA)

This indicator measures anomalies of daily soil moisture (water) content, and is used to measure the start and duration of agricultural drought conditions.

## Combined Drought Indicator (CDI)

This indicator integrates information on anomalies of precipitation, soil moisture and satellite-measured vegetation condition, into a single index that is used to monitor both the onset of agricultural drought and its evolution in time and space.

## Anomaly of Vegetation Condition (FAPAR Anomaly)
This indicator measures anomalies of satellite-measured FAPAR (Fraction of Absorbed Photosynthetically Active Radiation), and is used to highlight areas of relative vegetation stress due to agricultural drought
</details>
