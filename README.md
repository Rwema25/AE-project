# AE-project
The “Advancing Climate Data Integration in Agroecological Research” project, aims to improve the capacity of agroecological researchers and practitioners to integrate climate data into their work.

Documenting the datasets and packages is part of the project’s activities. The table below provides details on the datasets mentioned during user engagement interviews. 


| Rank | Dataset name  | Data source | Data format | Data type | Temp. resolution | Temp. coverage | Update freq | H. resolution | Variable | Perm | APIs | Package | Doc | 
|-----:|---------------|-------------|-------------|-----------|------------------|----------------|-------------|---------------|----------|------|------|---------|-----|
|     1|  ERA5         | ECMWF       | GRIB        | Gridded   | Hourly           | 1940 to present| Daily       | 0.25 x 0.25 degrees for the reanalysis              | Total precipitation, Sea surface temperature,...         | Register/ create account      | [Link](https://cds.climate.copernicus.eu/how-to-api)     | cdsapi (Python)  | [Link](https://confluence.ecmwf.int/display/CKB/ERA5%3A+data+documentation)    |
|     2|  CHIRPS       | Climate Hazards Group at the University of California, Santa Barbara | NetCDF, TIFF, BIL, PNG  | Gridded       |   Daily to annual time intervals| 1981 to near-real time  | April 2015 | 0.05 x 0.05 degrees  | precipitation |      |      |         | [Link](https://data.chc.ucsb.edu/products/CHIRPS-2.0/README-CHIRPS.txt)    |
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

</details>
