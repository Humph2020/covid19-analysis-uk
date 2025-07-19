## 📂 Analyzing Global COVID-19 Trends and Vaccination Progress with a Focus on the UK
*A Public Health Data Analysis Using BigQuery*

### 📌 Description

This project presents global COVID-19 trends with a focuse on the United Kingdom. Using BigQuery's public datasets. I cleaned and analyzed the datasets to examines confirmed cases, death rates, and vaccination progress from early 2020 to 2023.

###  Objectives

- Analyze daily and monthly COVID-19 case and death trends in the UK  
- Compare the UK’s vaccination progress with Canada 
- Visualize patterns to understand when major surges or improvements occurred  

### 🔧 Tools Used:
- Google BigQuery (SQL)
- Google Spreadsheet/Excel (for charting)
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

## 📈 Visualizations

### Dashboard
A visual dashboard was created using Google spreadsheets, displaying:
- Monthly averages
- Comparative vaccination charts

### 1. Monthly COVID-19 Cases and Deaths in the UK
- Spikes in early 2021 indicate pandemic waves.
- Deaths follow similar trends but lag behind cases.

### 2. UK vs Canada Vaccination Progress
- UK's rollout was sharper and faster than Canada's.
- Canada started tracking earlier but grew slower initially.
- Vaccination helped reduce deaths significantly in the UK by late 2021

## Conclusion
Vaccinations helped flatten the curve in the UK, as seen in the decline in both cases and deaths after mass vaccination began.

The UK’s faster rollout may have contributed to earlier control over virus spread compared to Canada.

This analysis shows the value of cloud-based public health analysis using BigQuery and SQL. Due to data availability limitations for the United States in the BigQuery dataset, Canada was selected as an alternative for comparison.

---

### Author
Humphery Okechukwu Ezeh 
humpheryokechukwuezeh@gmail.com
