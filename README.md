Anushna Prakash  
DATA 512 Human-Centered Data Science  
October 14, 2021  

# A2 - Bias in Data

## Purpose
The purpose of this assignment is to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries using NLP data that predicts article quality.

## Project Organization
The project is structured as below, down 2 levels.  
```
.
├── README.md
├── data_clean
│   ├── WPDS_countries_only.csv
│   ├── articles_missing_prediction.csv
│   ├── wp_wpds_countries-no_match.csv
│   └── wp_wpds_politicians_by_country.csv
├── data_raw
│   ├── WPDS_2020_data.csv
│   ├── api_dump
│   ├── country
│   ├── country.zip
│   └── readme.txt
├── license.txt
├── results
│   ├── bottom_10_countries_by_coverage.csv
│   ├── bottom_10_countries_by_quality.csv
│   ├── regions_by_coverage.csv
│   ├── regions_by_quality.csv
│   ├── top_10_countries_by_coverage.csv
│   └── top_10_countries_by_quality.csv
└── src
    └── hcds-a2-bias.ipynb
```

## Data Sources
There are three sources for data used in this project.  
### Wikipedia articles about politicians
This data comes from [this] (https://figshare.com/articles/dataset/Untitled_Item/5513449) repository. The file was downloaded from the linked location and unzipped into the `data_raw` folder in this repository. The original data was extracted via the Wikimedia API using the associated code. It is formatted as a CSV and saved as `page_data.csv` in the `data` directory. The schema is:

| Columns  |
| ----- |
| country  |
| page  |
| rev_id |


1. "country", containing the sanitised country name, extracted from the category name;
2. "page", containing the unsanitised page title.
3. "rev_id", containing the edit ID of the last edit to the page.

### World population data set
This data comes from [this] (https://www.prb.org/international/indicator/population/table/) location from the PRB. It is a publicly available data set containing 2019 world population estimates by country and region. Its schema is:  

| Columns  |
| ----- |
| FIPS  |
| Name  |
| Type |
| TimeFrame |
| Data (M) |
| Population |


1. "FIPS" is a unique identifier for the country/region listed.  
2. "Name" is the name of the country  
3. "Type" is the type of region in the row. This can be "World", "Sub-Region", or "Country".  
4. "TimeFrame" is the year that the data is available for.  
5. "Data (M)" refers to the data value in millions.  
6. "Population" is the estimated population of the region listed. 

The regions are structured such that each country is listed in normal capitalization directly underneath the sub-region it belongs to, and similarly for the region that each sub-region belongs to.

### ORES API Article Quality Predictions
This data comes from a machine learning system called ORES. This was originally an acronym for "Objective Revision Evaluation Service" but was simply renamed “ORES”. ORES is a machine learning tool that can provide estimates of Wikipedia article quality.