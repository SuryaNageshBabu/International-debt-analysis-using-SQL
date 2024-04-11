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

- What are the distinct debt indicators present? Let the output column be aliased as distinct_debt_indicators and the output should be ordered by it.

```sql
SELECT DISTINCT(indicator_name) AS distinct_debt_indicators
FROM international_debt
ORDER BY distinct_debt_indicators;
```

- What is the total amount of debt owed by all countries (in millions, rounded to two decimals)? Let the output column should be as total_debt.

```sql
SELECT ROUND(SUM(debt)/1000000,2) AS total_debt
FROM international_debt;
```

- Now to check the country with the highest amount of debt.

```sql
SELECT country_name, SUM(debt) AS total_debt
FROM international_debt
GROUP BY country_name
ORDER BY total_debt DESC
LIMIT 1;
```

- What is the average amount of debt for different debt indicators? Include indicator code aliased as debt_indicator and let the average debt column in the output be aliased as average_debt.

```sql
SELECT indicator_code AS debt_indicator, indicator_name, AVG(debt) AS average_debt
FROM international_debt
GROUP BY indicator_code, indicator_name
ORDER BY average_debt DESC;
```

- Now to check the country with highest amount of principal repayments in 'DT.AMT.DLXF.CD' category.

```sql
SELECT country_name, indicator_name
FROM international_debt 
WHERE debt = (SELECT MAX(debt)
              FROM international_debt 
              WHERE indicator_code = 'DT.AMT.DLXF.CD');
```



