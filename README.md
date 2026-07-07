# Child Malnutrition in Sub-Saharan Africa

## Overview
This project analyzes child malnutrition and mortality trends across Sub-Saharan African countries (2010–2024) using real-world data from the WHO Global Health Observatory (GHO). It covers the full pipeline from data collection through cleaning, exploratory analysis, and trend/correlation analysis, built as part of a graduate school application portfolio focused on algorithmic fairness and causal AI. Predictive modeling and causal analysis are planned as next steps.

## Motivation
Child malnutrition remains a major public health challenge across Sub-Saharan Africa, and understanding its trends and drivers has real implications for policy and resource allocation. This project is also a way to build hands-on experience with real, messy public health data, and to explore how fairness and causal reasoning apply in a development context, both areas I want to pursue at the graduate level.

## Data Source
- **WHO Global Health Observatory (GHO) OData API**: https://www.who.int/data/gho/info/gho-odata-api
- Indicators include stunting, wasting, under-five/infant/neonatal mortality rates (JME: UNICEF-WHO-World Bank Joint Malnutrition Estimates).
- Data is pulled live via the API rather than stored as static files, so the notebook always reflects the latest published estimates.

## Methodology
1. **Data collection** — Queried the WHO GHO API for nutrition and mortality indicators across Sub-Saharan African countries.
2. **Data cleaning** — Identified that the API returns multiple estimates per country-year (e.g. across sex/age subgroups); resolved by aggregating with the mean per country-year rather than discarding data.
3. **Missing data handling** — Dropped indicators with low coverage, interpolated remaining gaps by country (justified by the gradual year-to-year nature of health indicators), and removed the small number of countries still missing data after interpolation.
4. **Exploratory & trend analysis** — Visualized regional trends (2010–2024), ranked countries by change in stunting and mortality, and examined correlations between malnutrition and mortality indicators.
5. **Next steps** — Predictive modeling, fairness auditing (`fairlearn`), and causal analysis to understand disparities and drivers behind the trends.

## Key Findings
- Stunting declined steadily from ~33% (2010) to ~28% (2020), then reversed sharply to ~34% by 2024 — erasing a decade of progress in just two years.
- Wasting and neonatal mortality continued improving even as stunting reversed, while under-five mortality also began ticking upward.
- Regional averages mask major country-level disparities — a few crisis-affected countries (notably Sudan) are pulling the regional stunting average upward, while many countries individually continued to improve.
- Stunting and under-five mortality show a weak negative correlation, suggesting other factors (healthcare access, data quality, nutrition programs) mediate the relationship more than malnutrition alone.

