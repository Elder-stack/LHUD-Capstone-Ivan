* **Prepared By: Ivan Ho**
* **Dataset Used: Singapore HDB Resale Flats**
* **Course: NTUC LearningHub SCTP Associate Data Analyst**
* **Project Type: Business Analytics**

# Singapore HDB Resale Flats Analytics

<p align="center">
  <img width="1024" height="572" alt="image" src="https://github.com/user-attachments/assets/bbb991c9-761e-4913-8ac6-f4516e6fd5c8" />
</p>

## Problem Statement

How to comprehensively analyse historical Singapore Housing and Development Board (HDB) resale flat transactions to understand housing demand, resale price trends, property valuation drivers, housing affordability, and location-based market performance across different towns, flat types, and lease periods from 2000 onwards.

## Primary Research Objective

To comprehensively analyse historical Singapore Housing and Development Board (HDB) resale flat transactions from 2000 onwards to evaluate market demand, resale price trends, property valuation drivers, housing affordability, and location-based performance across different towns, flat types, and lease durations.

## Specific Research Objectives

### Objective 1: Housing Demand & Market Activity

**Goal:** Analyse resale transaction volumes and market activity across different years and flat types.

**Key Questions:**
- How have HDB resale transaction volumes changed from 2000 onwards?
- Which flat types have the highest resale transaction volumes?

### Objective 2: Resale Price Trends & Market Cycles

**Goal:** Track historical resale price trends and identify periods of price increases and decreases.

**Key Questions:**
- How have median HDB resale prices changed over time?
- Which periods experienced significant changes in resale prices?

### Objective 3: Property Valuation Drivers

**Goal:** Examine how property characteristics relate to HDB resale prices.

**Key Questions:**
- How do floor area, storey range and flat type relate to resale prices?
- What is the relationship between remaining lease and resale price?

### Objective 4: Housing Affordability & Relative Housing Costs

**Goal:** Compare resale prices and price per square metre across different flat types and locations.

**Key Questions:**
- How do resale prices differ across flat types?
- Which flat types and towns have higher or lower prices per square metre?

### Objective 5: Location-Based Market Performance

**Goal:** Compare resale market performance across different HDB towns.

**Key Questions:**
- Which towns have the highest and lowest median resale prices?
- How do transaction volumes and prices per square metre differ across towns?

---

## Data Dictionary

The Singapore HDB Resale Flats dataset contains historical resale transactions of Housing and Development Board flats in Singapore.

Each record represents a resale transaction and includes information such as the transaction month, town, flat type, floor area, remaining lease and resale price.

### Business Context

The dataset supports analysis of resale market activity, historical price trends, property characteristics, relative housing costs and differences between HDB towns.

### Column Definitions

| Column Name | Description | Unit |
|---|---|---|
| block | Block number of the residential flat | Identifier |
| flat_model | Model or design of the flat | Category |
| flat_type | Flat type, such as 3-room, 4-room or 5-room | Category |
| floor_area_sqm | Floor area of the flat | Square metres |
| lease_commence_date | Year the flat's lease commenced | Year |
| month | Month of resale transaction | YYYY-MM |
| remaining_lease | Remaining lease period, available in later datasets | Years/months |
| resale_price | Resale transaction price | SGD |
| storey_range | Storey range of the flat | Category |
| street_name | Street where the flat is located | Text |
| town | HDB town where the flat is located | Text |

**Additional columns created during data preparation:**

- `year` – Transaction year.
- `remaining_lease_estimated` – Estimated remaining lease based on lease commencement year.
- `lease_for_analysis` – Estimated lease values used for analysis, excluding unusual estimates.
- `price_per_sqm` – Resale price divided by floor area.

The original Data Dictionary also describes geographical coordinate fields, but these are not included in the four CSV files used for the current analysis.

---

## Data Quality & Cleaning Notes

### 1. Dataset Integration

The historical HDB resale data was obtained from four CSV datasets covering different periods.

| Dataset Period | Number of Records | Columns |
|---|---:|---:|
| 2000 – February 2012 | 369,651 | 10 |
| March 2012 – December 2014 | 52,203 | 10 |
| January 2015 – December 2016 | 37,153 | 11 |
| January 2017 – January 2024 | 169,584 | 11 |
| **Total** | **628,591** | |

The datasets were combined using Python Pandas to analyse HDB resale transactions over a longer period.

### 2. Missing Values

The combined dataset contained 421,854 missing values in the `remaining_lease` column, mainly from older datasets.

An estimated remaining lease was calculated using:

**Estimated Remaining Lease = 99 − (Transaction Year − Lease Commencement Year)**

This is an approximation based on a 99-year lease assumption and is not the official remaining lease period.

The original remaining lease values were kept unchanged.

### 3. Duplicate Records

A total of 1,066 duplicate rows were identified, representing approximately 0.17% of the dataset.

These records were retained because the dataset does not contain a unique transaction ID, and identical recorded details may belong to different transactions.

### 4. Data Type and Value Checks

The following checks were carried out using Python:

- Converted transaction month into date format.
- Checked resale prices and floor areas for missing or invalid values.
- Checked different flat types and towns for consistency.
- Checked estimated remaining lease values for unusual values.

Fifteen estimated remaining lease values above 99 years were marked as missing in the lease analysis column without removing their transaction records.

### 5. Analysis Period

The original dataset contains transactions from January 2000 to January 2024.

Since the dataset only includes January 2024, the year 2024 was excluded from full-year comparisons.

The prepared analysis dataset covers **2000–2023**, with **628,180 records**.

### 6. Price per Square Metre

Price per square metre was calculated using:

**Price per sqm = Resale Price ÷ Floor Area (sqm)**

This allows comparison of relative resale costs across flats of different sizes.

---

## Exploratory Data Analysis (EDA)

Python, Pandas and Matplotlib were used to perform exploratory data analysis.

The main analysis covered:

1. Yearly HDB resale transaction volumes.
2. Median resale price trends from 2000 to 2023.
3. Median resale prices by flat type.
4. Median resale prices across different towns.
5. Price per square metre by town and flat type.
6. Relationship between floor area and resale price.
7. Relationship between estimated remaining lease and resale price.
8. Median resale prices by storey range.

The analysis was carried out mainly using descriptive statistics, bar charts, line charts, scatter plots and correlation.

The Python notebook is available in this repository:

[RealEstateAnalysis.ipynb](RealEstateAnalysis.ipynb)

---

## Initial Findings

Based on the historical analysis:

- Median HDB resale prices increased from **S$239,000 in 2000 to S$550,000 in 2023**.
- Annual resale transaction volume fluctuated, with the highest recorded volume of **38,055 transactions in 2001**.
- Larger flats generally had higher resale prices.
- Floor area showed a positive correlation of approximately **0.683** with resale price in 2023.
- Estimated remaining lease showed a positive correlation of approximately **0.367** with resale price in 2023.
- Bukit Timah had the highest median resale price in 2023 at **S$825,500**.
- Queenstown had the highest median price per square metre in 2023 at approximately **S$8,144.96**.
- Higher storey ranges generally showed higher median resale prices in 2023.
- One-room flats had the highest median price per square metre among flat types in 2023, although they had the lowest median total resale price.

These findings describe patterns in the historical transaction data. They do not establish that individual property characteristics directly cause price changes.

---

## Power BI Dashboard
The Power BI dashboard presents HDB resale market trends and property comparisons across the five research objectives.
### Dashboard 1: HDB Resale Market Overview (Objectives 1 & 2)
<img width="977" height="541" alt="image" src="https://github.com/user-attachments/assets/036e243f-e6f9-4669-ab5c-03ac2784c9f1" />

### Dashboard 2: Property & Town Analysis (Objectives 3, 4 & 5)
<img width="888" height="545" alt="image" src="https://github.com/user-attachments/assets/140a1027-1b8e-4b56-bf5a-4e439251f964" />

---

## Project Limitations

- Some historical remaining lease values were missing and had to be estimated.
- Identical transaction records were retained because no unique transaction ID was available.
- Transaction volume represents resale market activity rather than total housing demand.
- Price per square metre compares relative housing costs but does not directly measure affordability against household income.
- The dataset only covers transactions up to January 2024, with the main analysis ending in 2023.
- Price comparisons across towns and flat types may be influenced by differences in property characteristics.

---

## Project Progress

| Task | Status |
|---|---|
| Problem statement and research objectives | Completed |
| Original datasets uploaded to GitHub | Completed |
| Data integration and preparation | Completed |
| Data quality checks | Completed |
| Exploratory Data Analysis | Completed |
| Python charts and analysis | Completed |
| Power BI Dashboard | Completed |
| Business insights and recommendations | In Progress |
| Final presentation | Pending |

## Project Files

- `resale-flat-prices-based-on-approval-date-2000-feb-2012.csv`
- `resale-flat-prices-based-on-registration-date-from-mar-2012-to-dec-2014.csv`
- `resale-flat-prices-based-on-registration-date-from-jan-2015-to-dec-2016.csv`
- `ResaleflatpricesbasedonregistrationdatefromJan2017onwards.csv`
- `RealEstateAnalysis.ipynb`
- `HDB_Resale_Prepared.csv`
- `HDB_Resale_Analytics.pbix`
- `README.md`

**Data Source:** Singapore HDB Resale Flat Prices, available from [data.gov.sg](https://data.gov.sg/).

