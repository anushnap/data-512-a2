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