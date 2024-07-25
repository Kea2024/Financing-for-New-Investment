# Analysis of Financing Data for New Investment

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning Preparation](#data-cleaning-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results/findings)
- [Recommendation](#recommendation)
- [References](#references)

### Project Overview

The goal is to provide the company some alternatives analysis as they explore probable sources of financing to start offering the new service.

### Data Source

Sales Data: The primary source for this data is the "investment.csv" file containing detailed information about each sale made by the company.

### Tools

- SQL Server - Data Cleaning and Data Analysis
- MS Excel   - Creating a reports

### Data Cleaning/ Preparation

In the Initial data preparation phase, we performed the following tasks:
1. Data loading and inspections
2. Importing the dataset by creating a new table and then filling out the data
3. Handling missing values
4. Data Cleaning and formatting

### Exploratory Data Analysis

EDA involved exploring the sales data to answer key questions such as:

1.  What type of funding would you recommend for the startup company?
2.  Why have you recommended this option?

### Data Analysis

``` SQL
TABLE if not exists INVESTMENT (name text, market text, funding_total_usd numeric, status varchar, country_code varchar, founded_year integer, seed numeric, venture numeric, equity_crowdfunding numeric, undisclosed numeric, convertibel_note numeric, debt_financing numeric, private_equity numeric)

SELECT * FROM investment
ORDER BY funding_total_usd DESC

SELECT * FROM investment
WHERE market='Financial Services'
AND funding_total_usd >0
ORDER BY name ASC

CREATE TABLE investment_subset AS
SELECT * FROM investment
WHERE market = 'Financial Services'
AND (funding_total_usd)>0
ORDER BY name ASC

SELECT * FROM investment_subset
ORDER BY funding_total_usd DESC

SELECT founded_year, COUNT (funding_total_usd) FROM investment_subset
GROUP BY founded_year
ORDER BY founded_year ASC

SELECT country_code,
  COUNT (country_code_ AS num_countries,
  AVG(seed) AS avg_seed,
  AVG(venture) AS avg_venture
FROM investment_subset
WHERE founded_year BETWEEN 2010 AND 2014
GROUP BY country_code
ORDER BY num_countries DESC

SELECT name, founded_year, funding_total_usd, seed, venture,
CASE
  WHEN seed ='0' AND venture >'0' THEN 'Venture Only'
  WHEN seed >'0' AND venture ='0' THEN 'Seed Only'
  ELSE 'Mixed'
END AS funding_type
FROM investment_subset
WHERE (country_code = 'USA') AND (founded_year BETWEEN 2010 AND 2014)
ORDER BY funding_total_usd ASC
```
### Results/Findings:

The analysis results are summarized as follows:
1. 64% of the companies chose to fund SEED ONLY type of funding.
2. VENTURE ONLY type of funding gained the highest fund profit with a total of
   44, 490,725 USD compared to SEED ONLY which only gained 17,098,203 USD.

### Recommendation:

Based from the above shown data, we recommend that start-up company should invest in VENTURE ONLY type of funding because it shows that there are almost 44, 490, 725 FUNDING TOTAL in USD which will secure the company in gaining high profit.

### References:
1. Data Analyst General Course: Refocus
   





  

