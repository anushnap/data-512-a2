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
This data comes from [this](https://figshare.com/articles/dataset/Untitled_Item/5513449) repository. The file was downloaded from the linked location and unzipped into the `data_raw` folder in this repository. The original data was extracted via the Wikimedia API using the associated code. It is formatted as a CSV and saved as `page_data.csv` in the `data` directory. The schema is:

| Columns  |
| ----- |
| country  |
| page  |
| rev_id |


1. "country", containing the sanitised country name, extracted from the category name;
2. "page", containing the unsanitised page title.
3. "rev_id", containing the edit ID of the last edit to the page.

### World population data set
This data comes from [this](https://www.prb.org/international/indicator/population/table/) location from the PRB. It is downloaded as a .csv and saved into `data_raw` under `WPDS_2020_data.csv`. It is a publicly available data set containing 2019 world population estimates by country and region. Its schema is:  

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
This data comes from a machine learning system called ORES. This was originally an acronym for "Objective Revision Evaluation Service" but was simply renamed “ORES”. ORES is a machine learning tool that can provide estimates of Wikipedia article quality. These were learned based on articles in Wikipedia that were peer-reviewed using the Wikipedia content assessment procedures. These quality classes are a sub-set of quality assessment categories developed by Wikipedia editors. The API documentation can be found [here](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context). The model called `articlequality` is used to generate the predicted quality class of each Wikipedia article passed to it.

## Data Output
The outputted data is in one of two folders: `data_clean` or `results`. 
### `data_clean`
This folder contains the data that is cleaned and saved as part of the analysis, for example countries without the subregions from the WPDS data set. The files contained are:  
- `WPDS_countries_only.csv`: Only the countries and population from the population data set.
- `articles_missing_prediction.csv`: The articles that are missing predictions from the ORES API output.
- `wp_wpds_countries-no_match.csv`: The articles or countries that do not have a match in either data set.
- `wp_wpds_politicians_by_country.csv`: The articles and countries with population that have a prediction and have a listed population fromthe population data set.

### `results`
This folder contains the tables that are outputted as a final list of results of countries with top/bottom performance in terms of article quality and articles as a percentage of population.  
- `top_10_countries_by_coverage.csv` Top 10 countries by coverage: 10 highest-ranked countries in terms of number of high-quality politician articles as a proportion of country population  
- `bottom_10_countries_by_coverage.csv` Bottom 10 countries by coverage: 10 lowest-ranked countries in terms of number of high-quality politician articles as a proportion of country population    
- `top_10_countries_by_quality.csv` Top 10 countries by relative quality: 10 highest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality   
- `bottom_10_countries_by_quality.csv` Bottom 10 countries by relative quality: 10 lowest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality   
- `regions_by_coverage.csv` Geographic regions by coverage: Ranking of geographic regions (in descending order) in terms of the total count of politician articles from countries in each region as a proportion of total regional population   
- `regions_by_quality.csv` Geographic regions by coverage: Ranking of geographic regions (in descending order) in terms of the relative proportion of politician articles from countries in each region that are of GA and FA-quality   

## Reflection
Before working with this data, I expected that the data would be heavily biased towards English-speaking countries, particularly North America. It is well-known that natural language processing models are best performing on English, since that is where a majority of the research has been done. I can see why that is the case, but I can imagine that there would be bias introduced in creating articles about politicians from other countries that North American politics does not concern itself with. Second, even if we were able to expand this analysis to include non-English Wikipedia, I would expect there to be bias in the prediction quality of the NLP API Ores, because of the fact that NLP is mostly studied in English.  

I was surprised to see some of the results that showed up, for example that smaller countries that I had not known of like Tuvalu and Vanuatu having the highest quality articles as a percentage of the population, but I imagine that this is because there are simply so little population in these countries that it drives the denominator down. Conversely, India is at the bottom of the list in terms of high-quality articles per population, but India is also the second most-populous country in the world. I was not surprised to see that Northern America topped the regional list by article quality as a percentage of total articles. Clearly, there is some bias towards English-speaking countries and Western countries in general in this data.  

I imagine that this means that English Wikipedia is not representative of the world at large, but mostly the world that English-speaking people care about ie Westerners care about. I would be interested in seeing how the Wikipedias from other languages compare in terms of qualitiy, even though that ability  may not exist at the moment. I would expect that coverage about Western topics would still exist, since the English-speaking world does dominate world politics whether it deserves to or not, but there would be additional informational nuggets that are of interest to the population that just speaks the language that the Wikipedia article is written in. Hence, if a researcher is trying to use these results to gain a picture or better understanding of what *all people* care about or think is important, English Wikipedia is not the way to go. However, if the researcher is trying to understand what *English-speaking people* care about or think is important, I think this data could be quite useful.