# Child Malnutrition in Sub-Saharan Africa

## Overview
This project analyzes child malnutrition and mortality trends across Sub-Saharan African countries (2010–2024) using real-world data from the WHO Global Health Observatory (GHO). It covers the full pipeline from data collection through cleaning, exploratory analysis, predictive modeling, and a regional disparity check.

## Motivation
Child malnutrition remains a major public health challenge across Sub-Saharan Africa, and understanding its trends and drivers has real implications for policy and resource allocation. This project is also a way to build hands-on experience with real data for advancement.

## Data Source
- **WHO Global Health Observatory (GHO) OData API**: https://www.who.int/data/gho/info/gho-odata-api
- Indicators include stunting, wasting, under-five/infant/neonatal mortality rates (JME: UNICEF-WHO-World Bank Joint Malnutrition Estimates).
- Data is pulled live via the API rather than stored as static files, so the notebook always reflects the latest published estimates.

## Methodology
1. **Data collection** — Queried the WHO GHO API for nutrition and mortality indicators across Sub-Saharan African countries.
2. **Data cleaning** — Identified that the API returns multiple estimates for a country per year (e.g. across sex/age subgroups), and this was resolved by aggregating with the mean per country and year rather than discarding data.
3. **Missing data handling** — Dropped indicators with low coverage, interpolated remaining gaps by country (justified by the gradual year-to-year nature of health indicators), and removed the small number of countries still missing data after interpolation.
4. **Exploratory & trend analysis** — Visualized regional trends (2010–2024), ranked countries by change in stunting and mortality, and examined correlations between malnutrition and mortality indicators.
5. **Predictive modeling** — Built a Random Forest model to predict under-five mortality from stunting and wasting. An early version leaked information through infant mortality rate (mathematically nested inside under-five mortality) and was corrected before drawing conclusions.
6. **Regional disparity check** — Grouped countries into West, East, Middle, and Southern Africa and checked whether the model's prediction errors were consistent across regions.


## Key Findings
- Stunting declined steadily from ~33% (2010) to ~28% (2020), then reversed sharply to ~34% by 2024, erasing a decade of progress in just two years.
- Wasting and neonatal mortality continued improving even as stunting reversed, while under-five mortality also began ticking upward.
- Regional averages mask major country-level disparities although a few crisis-affected countries (notably Sudan) are pulling the regional stunting average upward, many countries individually continued to improve.
- Stunting and wasting alone explain roughly half the variation in under-five mortality (R² 0.51–0.56), with Random Forest clearly outperforming Linear Regression (0.56 vs 0.21), suggesting the relationship is non-linear rather than a simple straight-line effect.
- Checking prediction bias by region revealed a consistent pattern across two different train/test splits: the model overpredicts mortality in Southern Africa and underpredicts it in East Africa, while West Africa shows almost no bias. This could mean the same stunting/wasting rate doesn't translate to the same mortality outcome everywhere, likely due to differences in healthcare access, conflict, or other unobserved factors
