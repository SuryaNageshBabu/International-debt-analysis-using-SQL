# Analyzing international debt statistics

## Overview

This project aims to analyze the international debt data collected by the World bank. The data is processed using SQL and the main focus of this project is to explore the debt data by country and the debt indicators. 

## Dataset

The dataset used in this project contains information about the amount of debt owed by developing countries (in USD). The data is collected by the World bank.

## Exploratory analysis

- Initially to check how many different countries are present in this database? The output column should be aliased as total_distinct_countries.

```sql
SELECT COUNT(DISTINCT country_name) AS total_distinct_countries
FROM international_debt;
```

- What are the distinct debt indicators present? The output column should be aliased as distinct_debt_indicators and the output should be ordered by it.

```sql
SELECT DISTINCT(indicator_name) AS distinct_debt_indicators
FROM international_debt
ORDER BY distinct_debt_indicators;
```


