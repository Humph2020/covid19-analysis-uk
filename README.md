## 📂 Analyzing Global COVID-19 Trends and Vaccination Progress with a Focus on the UK
*A Public Health Data Analysis Using BigQuery*

## 📌 Description

This project explores global COVID-19 trends with a focused lens on the United Kingdom. Using BigQuery's public datasets, the analysis examines confirmed cases, death rates, and vaccination progress from early 2020 to 2023.

The goal is to derive actionable insights from public health data to support decision-making in healthcare, especially for environments like the NHS. The project also compares the UK's vaccination rollout with that of the United States, providing a benchmark for evaluating public health strategies.

## ⚙️ Tools

- Google BigQuery – SQL queries and data processing  
- Looker Studio – Dashboard and visualizations  
- GitHub – Version control and portfolio showcase  
- Dataset Used: `bigquery-public-data.covid19_open_data.covid19_open_data`

##  Objectives

- Analyze daily and monthly COVID-19 case and death trends in the UK  
- Compare the UK’s vaccination progress with the US  
- Visualize patterns to understand when major surges or improvements occurred  
- Create a shareable dashboard and GitHub repository for job applications (NHS/data analyst roles)

## 📊 Key Analyses

### UK Daily COVID-19 Cases and Deaths

```sql

SELECT
  date,
  country_name,
  new_confirmed AS daily_cases,
  new_deceased AS daily_deaths
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name = 'United Kingdom'
  AND new_confirmed IS NOT NULL
ORDER BY date;
```


### Monthly Averages of New Cases and Deaths

```sql
SELECT
  FORMAT_DATE('%Y-%m', date) AS month,
  AVG(new_confirmed) AS avg_cases,
  AVG(new_deceased) AS avg_deaths
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name = 'United Kingdom'
  AND new_confirmed IS NOT NULL
GROUP BY month
ORDER BY month;
```

### UK vs US Vaccination Comparison
```sql
SELECT
  date,
  country_name,
  cumulative_persons_vaccinated
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name IN ('United Kingdom', 'United States')
  AND cumulative_persons_vaccinated IS NOT NULL
ORDER BY date;
```
### 📈 Dashboard
A visual dashboard was created using Looker Studio, displaying:
▪︎ Daily trends
▪︎ Monthly averages
▪︎ Comparative vaccination charts

### Conclusion
This project demonstrates how to use BigQuery for public health analysis. It showcases:
▪︎ Practical SQL skills
▪︎ Data cleaning and aggregation
▪︎ Data storytelling
▪︎ Visual communication using dashboards
