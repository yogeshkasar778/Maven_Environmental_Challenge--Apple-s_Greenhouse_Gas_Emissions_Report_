# Maven Environmental Challenge - Apple's Greenhouse Gas Emissions Report

![image](https://github.com/yogeshkasar778/FP20_Analytics_Challenge_8-IT_Help_Desk_Analysis/assets/118357991/4643fa9c-9025-40df-9ffc-af36e8981c31)

## Table of Contents :

- [Challenge Objective](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#dart-challenge-objective-)
- [Data Gathering / Requirement](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#data-gathering--requirement)
- [Data Perparation](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#data-preparation)
- [Data Modelling](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#data-modelling)
- [Data Analysis Expression (DAX) Calculation ](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#data-analysis-expression-dax-calculation-)
- [Report](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#chart_with_upwards_trend-report)
- [Tools, Software](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_#tools-software-)

## :dart: Challenge Objective :

For this challenge, the focal point was illustrating Apple's remarkable journey towards the realization of their ambitions 2030 target of achieving carbon neutrality across all aspects of their corporate operations and the entire life cycle of their products. In this competition, I assumed the dual role of an independent journalist and a passionate data visualization enthusiast. My task involved utilizing the data generously provided by Apple within their Environmental Progress Reports to visualize their progress toward becoming carbon neutral in 2030

In 2020, after announcing their corporate operations were officially carbon neutral, Apple pledged to make their products carbon neutral by 2030. To achieve this goal, they set their emissions for 2015 (38.4 million metric tons CO2e) as the baseline and will aim to reduce them by 75% by 2030. The remaining 25% of gross emissions (9.6 million metric tons CO2e) will be removed using carbon offsets, bringing the net emissions to 0.

## Data Gathering / Requirement:
The Dataset used for this challenge was presented by [Maven Environmental Challenge](https://mavenanalytics.io/challenges/maven-environmental-challenge/27) and Carbon Footprint by product, Greenhouse gas emissions, and Normalizing factors dataset:

About the Dataset: 

The dataset contains 3 tables, in CSV format. The "Greenhouse Gas Emissions" table contains the sources of Apple's greenhouse gas emissions from 2015 to 2022 divided by category (corporate & product life cycle), scope (direct scope 1 emissions & indirect scope 2 and 3 emissions), and type (emissions & removals). The "Carbon Footprint by Product" table contains the emissions from the product life cycle of every baseline iPhone model released between 2015-2022. The "Normalizing Factors" table contains Apple's revenue, market cap, and employees during the same period.
 - [Apple Emission Dataset](Apple+Emissions/apple_emissions)

## Data Preparation:
Completed the Data transformation in Power Query and the dataset was loaded into Microsoft Power BI Desktop for modeling.

Carbon Footprint by product, Greenhouse gas emissions, and Normalizing factors dataset are given tables named:

- `Carbon Footprint by product` which has `10 rows and 4 Columns` of observation.
- ` Greenhouse gas emissions` which has `136 rows and 6 Columns` of observation.
- ` Normalizing factors` which has `8 rows and 4 Columns` of observation.


## Data Modelling:
Then dataset was cleaned and transformed, it was ready for data modeled.

- The `Carbon Footprint by product, Greenhouse gas emissions, and Normalizing factors` tables as shown below:

We will create the data model connecting all tables and utilize the Calendar table that has already been set up.

![image](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_/assets/118357991/f7160d20-ef6a-4133-b91b-dabcc31ccebe)


## Data Analysis Expression (DAX) Calculation :
Measures used in visualization are:

  - `Total Revenue = SUMX(normalizing_factors,normalizing_factors[Revenue])`
  - `Total Market capitalization = SUMX(normalizing_factors,normalizing_factors[Market Capitalization])`
  - `Total Product life cycle Emissions = CALCULATE(SUM(greenhouse_gas_emissions[Emissions]),'greenhouse_gas_emissions'[Category]="Product life cycle emissions")`
  - `Total Gross Emissions = CALCULATE(SUM(greenhouse_gas_emissions[Emissions]),'greenhouse_gas_emissions'[Type]="Gross Emissions")`
  - `Total Greenhouse Emissions = SUM(greenhouse_gas_emissions[Emissions])`
  - `Total Corporate Emissions = CALCULATE(SUM(greenhouse_gas_emissions[Emissions]),'greenhouse_gas_emissions'[Category]="Corporate Emissions")`
  - `Total Carbon Removals = CALCULATE(SUM(greenhouse_gas_emissions[Emissions]),'greenhouse_gas_emissions'[Type]="Carbon Removals")`
    
  - `Revenue Growth Rate - YoY = 
        VAR CurrentYearRevenue = SUMX(FILTER('normalizing_factors', 'normalizing_factors'[Fiscal Year] = MAX('normalizing_factors'[Fiscal Year])), 'normalizing_factors'[Revenue])
        VAR PreviousYearRevenue = SUMX(FILTER('normalizing_factors', 'normalizing_factors'[Fiscal Year] = MAX('normalizing_factors'[Fiscal Year]) - 1), 'normalizing_factors'[Revenue])
           RETURN DIVIDE(CurrentYearRevenue - PreviousYearRevenue, PreviousYearRevenue)
`
  - `Market Capitilation Growth Rate - YoY = 
       VAR CurrentYearMarketCapitilation = SUMX(FILTER('normalizing_factors', 'normalizing_factors'[Fiscal Year] = MAX('normalizing_factors'[Fiscal Year])), 'normalizing_factors'[Market Capitalization])
       VAR PreviousYearMarketCapitilation = SUMX(FILTER('normalizing_factors', 'normalizing_factors'[Fiscal Year] = MAX('normalizing_factors'[Fiscal Year]) - 1), 'normalizing_factors'[Market Capitalization])
          RETURN DIVIDE(CurrentYearMarketCapitilation - PreviousYearMarketCapitilation, PreviousYearMarketCapitilation)
`
  - `Employees Growth Rate - YoY = 
       VAR CurrentYearEmployees = SUMX(FILTER('normalizing_factors', 'normalizing_factors'[Fiscal Year] = MAX('normalizing_factors'[Fiscal Year])), 'normalizing_factors'[Employees])
       VAR PreviousYearEmployees = SUMX(FILTER('normalizing_factors', 'normalizing_factors'[Fiscal Year] = MAX('normalizing_factors'[Fiscal Year]) - 1), 'normalizing_factors'[Employees])
           RETURN DIVIDE(CurrentYearEmployees - PreviousYearEmployees, PreviousYearEmployees)`
    
  - `Count Employees = sum(normalizing_factors[Employees])`
  - `Avg carbon footprint = AVERAGE(carbon_footprint_by_product[Carbon Footprint])`

## :chart_with_upwards_trend: Report:
Data visualization for the dataset was done using Microsoft Power BI Desktop and shared this report on Power BI Services:

View Report - [Report](https://mavenanalytics.io/project/9732)

|    Apple's Greenhouse Gas Emissions      |
| --------------- |
|![image](https://github.com/yogeshkasar778/Maven_Environmental_Challenge--Apple-s_Greenhouse_Gas_Emissions_Report_/assets/118357991/1d89c0a5-179f-445c-b543-7973678ea309)|


## Tools, Software :
1. Power BI
2. DAX
3. Power Query Editor
4. Power BI Service
5. Power BI Desktop
6. Power BI Dashboard
7. Excel
---
