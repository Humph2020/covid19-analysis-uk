## 📂 Analyzing Global COVID-19 Trends and Vaccination Progress with a Focus on the UK
*A Public Health Data Analysis Using BigQuery*

### 📌 Description

This project explores global COVID-19 trends with a focuse on the United Kingdom. Using BigQuery's public datasets, the analysis examines confirmed cases, death rates, and vaccination progress from early 2020 to 2023. This project also compares the UK's vaccination rollout with that of Canada.

###  Objectives

- Analyze daily and monthly COVID-19 case and death trends in the UK  
- Compare the UK’s vaccination progress with Canada 
- Visualize patterns to understand when major surges or improvements occurred  

### 🔧 Tools Used:
- Google BigQuery (SQL)
- Excel (for charting)
- GitHub (for documentation)
- Public Datasets: `bigquery-public-data.covid19_open_data`

---

## 📊 Key Analyses

### 1. UK Daily COVID-19 Cases and Deaths

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

### 2. Monthly Averages of New Cases and Deaths in the UK

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

### 3. UK vs Canada Cumulative Vaccination Comparison

```sql
 SELECT
  date,
  MAX(CASE WHEN country_name = 'United Kingdom' THEN cumulative_persons_vaccinated ELSE NULL END) AS uk_vaccinated,
  MAX(CASE WHEN country_name = 'Canada' THEN cumulative_persons_vaccinated ELSE NULL END) AS canada_vaccinated
FROM
  `bigquery-public-data.covid19_open_data.covid19_open_data`
WHERE
  country_name IN ('United Kingdom', 'Canada')
  AND cumulative_persons_vaccinated IS NOT NULL
GROUP BY date
ORDER BY date;
```
---

## 📈 Dashboard
A visual dashboard was created using Looker Studio, displaying:
- Daily trends
- Monthly averages
- Comparative vaccination charts

## Key Insights
- Clear spikes in cases during 2020 and 2021
- Vaccination helped reduce deaths significantly in the UK by late 2021
- UK vaccine rollout was faster than several other countries during early stages

## Conclusion
This project demonstrates the power of cloud-based public health analysis using BigQuery and SQL. Due to data availability limitations for the United States in the BigQuery dataset, Canada was selected as an alternative for comparison.

---

### Author
Humphery Okechukwu Ezeh 
humpheryokechukwuezeh@gmail.com
Location: Nigeria [Open to relocate to UK]
