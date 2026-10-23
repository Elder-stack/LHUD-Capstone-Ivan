# Singapore HDB Resale Flats Analytics

**Prepared By:** Ivan Ho  
**Course:** NTUC LearningHub SCTP Associate Data Analyst  
**Project Type:** Business Analytics  
**Tools:** Python, Google Colab, Pandas, Matplotlib, Power BI (planned)

## 1. Problem Statement

How can historical Singapore HDB resale transaction data be analysed to understand housing demand, resale price trends, property valuation factors, housing affordability and market performance across different towns, flat types and lease periods?

## 2. Research Objectives

**Objective 1: Housing Demand and Market Activity**

Analyse HDB resale transaction volumes over time and identify changes in market activity across different flat types.

**Objective 2: Resale Price Trends**

Examine historical HDB resale price trends and identify periods of increasing or decreasing prices.

**Objective 3: Property Valuation Drivers**

Examine how floor area, flat type, storey range and remaining lease relate to resale prices.

**Objective 4: Housing Affordability**

Compare resale prices and price per square metre across flat types and locations to understand differences in relative housing costs.

**Objective 5: Location-Based Market Performance**

Compare transaction activity, median resale prices and price per square metre across different HDB towns.

## 3. Dataset Overview

The project uses four historical HDB resale transaction datasets.

| Dataset Period | Records |
|---|---:|
| 2000 – February 2012 | 369,651 |
| March 2012 – December 2014 | 52,203 |
| January 2015 – December 2016 | 37,153 |
| January 2017 – January 2024 | 169,584 |
| **Total** | **628,591** |

The four datasets were combined to allow analysis across a longer period.

The main columns include transaction month, town, flat type, floor area, flat model, storey range, lease commencement date, remaining lease and resale price.

The main analysis covers **2000–2023**, excluding the incomplete year 2024 from full-year comparisons.

## 4. Data Preparation

Data preparation was carried out using Python in Google Colab.

The main steps included:

1. Loading and combining the four original datasets using Pandas.
2. Checking missing values, duplicate records and data types.
3. Estimating missing remaining lease values using lease commencement dates and a 99-year lease assumption.
4. Checking unusual resale prices, floor areas and lease values.
5. Converting transaction dates into a suitable format.
6. Calculating price per square metre for comparisons.
7. Preparing a separate analysis dataset covering 2000–2023.

**Data Quality Notes:**

- The original remaining lease column contained 421,854 missing values.
- There were 1,066 identical records, which were retained because a unique transaction ID was unavailable.
- Fifteen unusual estimated lease values were marked as missing for lease-specific analysis.
- Original CSV files were preserved without modification.

The prepared analysis dataset contains **628,180 records**.

## 5. Exploratory Data Analysis (EDA)

Python was used to analyse the following areas:

| Analysis | Method |
|---|---|
| Resale market activity | Yearly transaction counts |
| Resale price trends | Median resale prices by year |
| Flat type comparison | Median resale prices and price per sqm |
| Town comparison | Median resale prices and price per sqm |
| Floor area and resale price | Scatter plot and correlation |
| Remaining lease and resale price | Scatter plot and correlation |
| Storey range comparison | Median resale prices by storey range |

Pandas was used for data preparation and calculations, while Matplotlib was used to create charts.

## 6. Initial Findings

The analysis identified several trends:

- The median resale price increased from S$239,000 in 2000 to S$550,000 in 2023.
- Resale transaction volumes fluctuated over the years, with the highest recorded annual volume in 2001.
- Larger flats generally had higher resale prices.
- Floor area had a positive correlation of approximately 0.683 with resale price in 2023.
- Median resale prices and price per square metre varied across HDB towns.
- Higher storey ranges generally showed higher median resale prices in 2023.

These are descriptive findings based on the historical dataset.

## 7. Limitations

- Missing historical remaining lease values were estimated rather than taken from official transaction records.
- Transaction counts indicate resale market activity but do not measure total housing demand.
- Price per square metre measures relative housing costs, not affordability based on household income.
- The analysis uses historical data through 2023 and does not represent current market conditions.

## 8. Project Progress

| Task | Status |
|---|---|
| Upload original datasets to GitHub | Completed |
| Data preparation and cleaning checks | Completed |
| Exploratory data analysis | Completed |
| Python charts | Completed |
| Power BI dashboard | In progress |
| Business insights and recommendations | Pending |
| Final presentation | Pending |

## 9. Next Steps

The next stage is to develop a Power BI dashboard to present the analysis results using charts, key metrics and interactive filters.

The final stage will be to summarise the business insights, provide recommendations and prepare the capstone presentation.

## 10. Project Files

- Four original HDB resale CSV datasets
- `RealEstateAnalysis.ipynb` – Python data preparation and exploratory analysis
- `README.md` – Project overview and progress documentation

**Data Source:** Singapore HDB Resale Flat Prices datasets, available through [data.gov.sg](https://data.gov.sg/).
