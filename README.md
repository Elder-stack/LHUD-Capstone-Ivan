* **Prepared By: Ivan Ho**
* **Dataset Used: Real Estate Resale Flats**

# Singapore HDB Resale Flats Analytics

<p align="center">
 <img width="1024" height="559" alt="image" src="https://github.com/user-attachments/assets/a60ed822-80d0-48c8-9212-7523d3e1e986" />
</p>

## Problem Statement 

How to comprehensively analyze historical Singapore Housing and Development Board (HDB) resale flat transactions to understand housing demand, resale price trends, property valuation drivers, housing affordability, and location-based market performance across different towns, flat types, and lease periods from 2000 onwards

## Primary Research Objective
To comprehensively analyze historical Singapore Housing and Development Board (HDB) resale flat transactions from 2000 onwards to evaluate market demand, temporal price dynamics, property valuation drivers, housing affordability, and location-based performance across different towns, flat types, and lease durations.   

## Specific Research Objectives

Objective 1: Housing Demand & Market ActivityGoal: Analyze transaction volumes and market liquidity trends across different years, months, and flat types.   
         
         Key Questions:
         - How have trading volumes fluctuated from 2000 to the present?
         - Which flat types (e.g., 3-room, 4-room, 5-room, Executive) experience the highest buyer demand and turnover?

Objective 2: Resale Price Trends & Macroeconomic CyclesGoal: Track historical price trajectories, growth rates, and market cycles for HDB resale flats.   
         
         Key Questions:
         - What are the long-term compound annual growth rates (CAGR) of HDB resale prices?
         - How have government policy changes, cooling measures, or economic shifts impacted median and mean transaction prices over the decades?

Objective 3: Property Valuation DriversGoal: Quantify the structural and physical attributes that drive flat valuations.   
         
         Key Questions:
         - To what extent do floor area ($\text{m}^2$), storey range, and flat model impact the final resale price?
         - How does lease decay (remaining lease years vs. lease commencement date) affect property resale valuations over time?

Objective 4: Housing Affordability & Spatial AccessibilityGoal: Assess the financial accessibility of public housing relative to property characteristics and temporal inflation.   
         
         Key Questions:
         - How has the price-to-area ratio ($\text{SGD per m}^2$) evolved across different flat types?
         - What is the distribution of entry-level versus premium resale housing across various market segments?

Objective 5: Location-Based Market PerformanceGoal: Compare real estate performance, price premiums, and geographic variations across different HDB towns and spatial coordinates.   
         
         Key Questions:
         - Which towns command the highest price premiums and transaction densities?
         - How do spatial coordinates (latitude and longitude) correlate with resale price clustering across Singapore?



<h1 align="center">Singapore HDB Resale Flats Dataset</h1>
<img width="1317" height="742" alt="image" src="https://github.com/user-attachments/assets/fd2d0b2f-b7d0-4953-8c8b-868132c2485a" />


## 📋 Dataset Overview

* **File Name:** `product_sales_practice.csv`
* **Time Horizon:** January 2026 – June 2026
* **Target Category:** Electronics
* **Key Entities:** Products, Sales Team, Regional Markets, Revenue Metrics

  Link to Jupyter Notebook in Google Colab:
  https://colab.research.google.com/drive/1zdPR2ig9qFp6Q1gPrZvky3Ac7UITW3Mv?usp=sharing
   
## 🗂️ Data Dictionary

Here is the complete Data Dictionary for the Singapore HDB Resale Flats Analytics project, detailing the business context, table descriptions, and every attribute included in the dataset:   

## Business Context
The Singapore HDB Resale Flats dataset contains residential property resale transactions for Housing and Development Board (HDB) flats in Singapore. It supports real estate analytics, housing market research, property valuation studies, urban planning, and geographic trend analysis. By combining property characteristics, lease information, transaction values, and geographic attributes, analysts can evaluate housing demand, resale price trends, property affordability, and location-based market performance.   

Table Description: HDB Resale FlatsThe primary transactional table within the dataset. Each record represents a single resale transaction for a residential flat.   

Column DefinitionsColumn NameDescriptionUnitblockBlock number or identifier of the residential unit.   Identifier   flat_modelModel or design type of the residential flat (e.g., Improved, New Generation, Model A).   Category   flat_typeFlat type classification (e.g., 1-room, 2-room, 3-room, 4-room, 5-room, Executive).   Category   floor_area_sqmFloor area of the residential flat.   Square Metres   lease_commence_dateYear in which the lease commenced.   Year   monthTransaction month (formatted as YYYY-MM).   Month   remaining_leaseRemaining lease period of the residential flat (available in recent files as years/months or calculated).   Years   resale_priceFinal price at which the residential flat was resold.   SGD   story_rangeStorey range in which the residential flat is located (e.g., 07 TO 09).   Category   street_nameStreet where the residential flat is located.   Text   townTown in which the residential flat is situated (e.g., Ang Mo Kio, Tampines, Jurong West).   Text   street_latLatitude coordinate of the street location.   Decimal Degrees   street_lonLongitude coordinate of the street location.   Decimal Degrees   town_latLatitude coordinate of the town location.   Decimal Degrees   town_lonLongitude coordinate of the town location.   Decimal Degrees   

## 🔍 Data Quality & Cleaning Notes

If you are using this dataset for data cleaning projects, please note that it intentionally contains realistic real-world data anomalies:
* **Missing Values (NaNs):** Features like `Region`, `Salesperson`, `Unit_Price`, `Discount`, and `Sales` contain scattered missing fields (e.g., missing revenue values or unattributed regional boundaries).
* **Calculated Columns:** The `Sales` column follows the general formula:  
  \[\text{Sales} = (\text{Quantity} \times \text{Unit\_Price}) \times (1 - \text{Discount})\]
  This relationship can be exploited to programmatically restore missing metrics.
* **Empty Rows:** The raw structure contains blank structural divider rows (`,,,,,,,,,`) that should be filtered out during preprocessing.

## 🛠️ Usage Example (Python & Pandas)

Get started analyzing this dataset quickly using Python:

```python
import pandas as pd

# Load the dataset and drop completely empty structural lines
df = pd.read_csv('sales_data.csv').dropna(how='all')

# Convert date column to datetime object
df['Date'] = pd.to_datetime(df['Date'])

# Quick view of total sales revenue by product
revenue_by_product = df.groupby('Product')['Sales'].sum().sort_values(ascending=False)
print("Revenue by Product:\n", revenue_by_product)
```

## 💡 Potential Projects & Analysis Directions
1. **Sales Performance Dashboards:** Create interactive Tableau or Power BI visualizations mapping regional performance by salesperson.
2. **Predictive Modeling:** Build machine learning regression models to predict expected order values or customer quantity demands.
3. **Discount Impact Studies:** Assess whether offering a $10\%$ vs $15\%$ discount yields a statistically significant increase in total items sold.
