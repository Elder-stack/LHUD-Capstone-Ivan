* **Prepared By: Ivan Ho**
* **Dataset Used: Singapore HDB Resale Flats**

# Singapore HDB Resale Flats Analytics

<p align="center">
<img width="700" height="349" alt="image" src="https://github.com/user-attachments/assets/460bf08b-5a45-41ce-9e9f-f4f1b4391ab7" />
</p>

## Problem Statement

How to comprehensively analyse historical Singapore Housing and Development Board (HDB) resale flat transactions to understand housing demand, resale price trends, property valuation drivers, housing affordability, and location-based market performance across different towns, flat types, and lease periods from 2000 onwards.

## Main Objective

To analyse historical Singapore HDB resale flat transactions from 2000 onwards to understand resale market activity, price trends, property characteristics, relative housing costs and differences across towns.

## 5 Research Objectives

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

## Exploratory Data Analysis (EDA)

EDA was carried out using Python Pandas to understand the dataset before cleaning and further analysis.

The checks included:

1. Dataset size, column names and data types.
2. Sample records and summary statistics.
3. Missing values and duplicate records.
4. Different flat types and towns.

These checks helped identify data quality issues and understand the structure of the dataset.

---

## Data Dictionary

The Singapore HDB Resale Flats dataset contains historical resale transactions of Housing and Development Board flats in Singapore.

Each record represents a resale transaction and includes information such as the transaction month, town, flat type, floor area, remaining lease and resale price.

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

---

## Data Integration

The historical HDB resale data was obtained from four CSV datasets covering different periods.

| Dataset Period | Number of Records |
|---|---:|
| 2000 – February 2012 | 369,651 |
| March 2012 – December 2014 | 52,203 |
| January 2015 – December 2016 | 37,153 |
| January 2017 – January 2024 | 169,584 |
| **Total** | **628,591** |

The four datasets were combined using Python Pandas to analyse HDB resale transactions over a longer period.

---

## Data Cleaning

Data cleaning was carried out to check and handle data quality issues before analysis.

### 1. Missing Values

The combined dataset contained 421,854 missing values in the `remaining_lease` column, mainly from older datasets.

An estimated remaining lease was calculated using:

**Estimated Remaining Lease = 99 − (Transaction Year − Lease Commencement Year)**

This is an approximation based on a 99-year lease assumption and is not the official remaining lease period.

The original remaining lease values were kept unchanged.

### 2. Duplicate Records

A total of 1,066 duplicate rows were identified, representing approximately 0.17% of the dataset.

These records were retained because the dataset does not contain a unique transaction ID, and identical recorded details may belong to different transactions.

### 3. Data Type and Value Checks

The following checks were carried out using Python:

- Converted transaction month into date format.
- Checked resale prices and floor areas for missing or invalid values.
- Checked different flat types and towns for consistency.
- Checked estimated remaining lease values for unusual values.

Fifteen estimated remaining lease values above 99 years were marked as missing in the lease analysis column without removing their transaction records.

---

## Data Preparation

The dataset was prepared for further analysis by creating additional columns and selecting the analysis period.

### 1. Analysis Period

The original dataset contains transactions from January 2000 to January 2024.

Since the dataset only includes January 2024, the year 2024 was excluded from full-year comparisons.

The prepared analysis dataset covers **2000–2023**, with **628,180 records**.

### 2. Remaining Lease

Estimated remaining lease values were used where original values were unavailable, while preserving the original data.

### 3. Price per Square Metre

Price per square metre was calculated using:

**Price per sqm = Resale Price ÷ Floor Area (sqm)**

This allows comparison of relative resale costs across flats of different sizes.

---

## Descriptive Analytics – Research Objectives

Descriptive Analytics was carried out using Python, Pandas and Matplotlib.

The analysis was organised according to the five research objectives, with charts and key findings to support each objective.

### Objective 1: Housing Demand & Market Activity

The following charts were used:

- HDB resale transaction volumes by year.
- HDB resale transaction volumes by flat type.

**Key Finding:**

HDB resale transaction volumes fluctuated between 2000 and 2023, with the highest volume of 38,055 transactions recorded in 2001.

Four-room flats recorded the highest number of resale transactions during the analysis period.

### Objective 2: Resale Price Trends & Market Cycles

The following chart was used:

- Median HDB resale price by year.

**Key Finding:**

Median HDB resale prices increased from S$239,000 in 2000 to S$550,000 in 2023.

Although resale prices fluctuated over the years, the overall trend shows an increase in HDB resale prices.

### Objective 3: Property Valuation Drivers

The following charts were used:

- Floor area vs resale price.
- Remaining lease vs resale price.
- Median resale price by storey range.

**Key Finding:**

Larger flats generally had higher resale prices.

Floor area showed a positive correlation of 0.683 with resale price in 2023, while estimated remaining lease showed a weaker positive correlation of 0.367.

### Objective 4: Housing Affordability & Relative Housing Costs

The following charts were used:

- Median resale price by flat type.
- Median resale price by flat type in 2023.
- Median price per square metre by flat type.
- Median price per square metre by town.

**Key Finding:**

Resale prices and price per square metre varied across flat types and towns.

Queenstown recorded a median price of approximately S$8,145 per sqm in 2023, showing relatively higher housing costs.

### Objective 5: Location-Based Market Performance

The following charts were used:

- Median resale price by town.
- Median resale price by town in 2023.
- Resale transaction volume by town in 2023.

**Key Finding:**
- Resale market activity and prices differed across HDB towns.
- Bukit Timah recorded the highest median resale price of S$825,500 in 2023.

The Python notebook containing the charts and analysis is available here: [RealEstateAnalysis.ipynb](RealEstateAnalysis.ipynb)

---

## Power BI Dashboard

The Power BI dashboard presents HDB resale market trends and property comparisons across the five research objectives.

### Dashboard 1: HDB Resale Market Overview (Objectives 1 & 2)

<img width="684" height="379" alt="Dashboard 1" src="https://github.com/user-attachments/assets/036e243f-e6f9-4669-ab5c-03ac2784c9f1" />

### Dashboard 2: Property & Town Analysis (Objectives 3, 4 & 5)

<img width="622" height="382" alt="Dashboard 2" src="https://github.com/user-attachments/assets/140a1027-1b8e-4b56-bf5a-4e439251f964" />

---
## Predictive Analytics – Multiple Linear Regression

Multiple Linear Regression was used to predict HDB resale prices using several property factors based on 2023 transaction data.

The model used six factors:
1. Floor area
2. Town
3. Flat type
4. Remaining lease
5. Storey range
6. Flat model

Text categories such as town and flat type were converted into numerical values using `pd.get_dummies()`.

The dataset was split into 80% training data and 20% testing data.

The chart below compares actual resale prices with the prices predicted by the model.
<img width="796" height="475" alt="image" src="https://github.com/user-attachments/assets/bc2ee237-7e9e-44c7-a5f1-b5ea925aab08" />

### Model Results

| Metric | Result |
|---|---:|
| Number of Records | 25,777 |
| R² Score | 0.888 (88.8%) |
| Mean Absolute Error (MAE) | S$43,495.64 |

### Key Finding

The model explains approximately 88.8% of the variation in HDB resale prices in the 2023 testing data.

Using six property factors improved the prediction results compared with using floor area alone.

However, predicted prices may still differ from actual resale prices.

---

## Project Limitations

- Some historical remaining lease values were missing and had to be estimated.
- Identical transaction records were retained because no unique transaction ID was available.
- Transaction volume represents resale market activity rather than total housing demand.
- Price per square metre compares relative housing costs but does not directly measure affordability against household income.
- The dataset only covers transactions up to January 2024, with the main analysis ending in 2023.
- Price comparisons across towns and flat types may be influenced by differences in property characteristics.
- The regression model was trained and tested using 2023 transactions, so its performance on future transactions has not been tested.

---

## Project Progress

| Task | Status |
|---|---|
| Problem statement and research objectives | Completed |
| Original datasets uploaded to GitHub | Completed |
| Data integration | Completed |
| Exploratory Data Analysis | Completed |
| Data cleaning and preparation | Completed |
| Descriptive Analytics – 5 research objectives | Completed |
| Predictive Analytics – Multiple Linear Regression | Completed |
| Power BI Dashboard | Completed |
| Business insights and recommendations | Completed |
| Final presentation | Work In Progress |

---

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

## Business Insights & Recommendations

Based on the analysis, the following recommendations can help HDB resale buyers make more informed decisions.

### 1. Compare Resale Prices Across Towns

Resale prices vary across HDB towns. Buyers should compare median resale prices and price per square metre across different locations to identify suitable options within their budget.

### 2. Consider Property Characteristics

Floor area and remaining lease are associated with resale prices. Buyers should consider flat size, remaining lease and other property characteristics when comparing resale flats.

### 3. Use Historical Trends and Price Predictions as References

Historical resale price trends and the regression model can provide useful price references. However, predicted prices are estimates and should not be treated as guaranteed transaction prices.

### Conclusion

The project shows how historical HDB resale data can be used to understand market trends, compare property prices and support more informed housing decisions.
