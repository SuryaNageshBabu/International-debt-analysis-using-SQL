# Analyzing international debt statistics

![techstack1](https://camo.githubusercontent.com/9edf0a1d750cedbb64e89a53a8ec40a14a46abd81765059ef1285114cda0a282/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f506f737467726553514c2d3431363945312e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d506f737467726553514c266c6f676f436f6c6f723d7768697465)  ![techstack2](https://camo.githubusercontent.com/410d86e43f847d3f6e3027fa6f0c2fb7641d893fa601d863a943eac968c41890/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6769746875622d2532333132313031312e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d676974687562266c6f676f436f6c6f723d7768697465) 
![techstack3](https://camo.githubusercontent.com/998382ebc9a32162128b00b597ea488192df024fd015e5edec001fe29fcb93a6/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f56697375616c25323053747564696f253230436f64652d3030373864372e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d76697375616c2d73747564696f2d636f6465266c6f676f436f6c6f723d7768697465) 
![techstack4](https://camo.githubusercontent.com/b0dd0c2b3bbe007ae4eef1f59c17c24ce53a334ad46bfdb80b5c841eaeccdde3/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f6d61726b646f776e2d2532333030303030302e7376673f7374796c653d666f722d7468652d6261646765266c6f676f3d6d61726b646f776e266c6f676f436f6c6f723d7768697465)


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

## Technologies used

**Database Management System**: PostgreSQL to host and manage the dataset.

**Programming languages**: SQL for data extraction, processing and data exploration.

## Get in touch

Feel free to share your feedback. You can reachout to me through [Linkedin]("www.linkedin.com/in/suryanageshbabu")

 


