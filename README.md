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
   
## 🗂️ Data Dictionary

Here is the complete Data Dictionary for the Singapore HDB Resale Flats Analytics project, detailing the business context, table descriptions, and every attribute included in the dataset:   

## Business Context
The Singapore HDB Resale Flats dataset contains residential property resale transactions for Housing and Development Board (HDB) flats in Singapore. It supports real estate analytics, housing market research, property valuation studies, urban planning, and geographic trend analysis. By combining property characteristics, lease information, transaction values, and geographic attributes, analysts can evaluate housing demand, resale price trends, property affordability, and location-based market performance.   

Table Description: HDB Resale FlatsThe primary transactional table within the dataset. Each record represents a single resale transaction for a residential flat.   

## Column Definitions

| Column Name | Data Type | Unit |
| :--- | :--- | :--- |
| **block** | Block number or identifier of the residential unit | Identifier |
| **flat_model** | Model or design type of the residential flat (e.g., Improved, New Generation, Model A). | Category |
| **flat_type** | Flat type classification (e.g., 1-room, 2-room, 3-room, 4-room, 5-room, Executive).    | Category |
| **floor_area_sqm** | Floor area of the residential flat. | Square Metres |
| **lease_commence_date** | Year in which the lease commenced | Year |
| **month** | Transaction month (formatted as YYYY-MM). | Month |
| **remaining_lease** | Remaining lease period of the residential flat (available in recent files as years/months or calculated). | Years |
| **resale_price** | Final price at which the residential flat was resold | SGD |
| **story_range** | Storey range in which the residential flat is located (e.g., 07 TO 09) | Category |
| **street_name** | Street where the residential flat is located | Text |
| **town** | Town in which the residential flat is situated (e.g., Ang Mo Kio, Tampines, Jurong West). | Text |
| **street_lat** | Latitude coordinate of the street location. | Decimal Degrees |
| **street_lon** | Longitude coordinate of the street location. | Decimal Degrees |
| **town_lat** | Latitude coordinate of the town location | Decimal Degrees |
| **town_lon** | Longitude coordinate of the town location. | Decimal Degrees |

## 🔍 Data Quality & Cleaning Notes

Here are the Data Quality & Cleaning Notes for the historical Singapore HDB Resale Flats dataset. These notes outline structural variations across the time-period files, data anomalies, missing value handling, and standardization steps required prior to deep analysis.

1. Schema & File Harmonization
The historical dataset is split into four distinct CSV files covering different chronological periods:
 * File 1 (2000 – Feb 2012): 369,651 rows, 10 columns (missing remaining_lease)
 * File 2 (Mar 2012 – Dec 2014): 52,203 rows, 10 columns (missing remaining_lease)
 * File 3 (2015 – 2016): 37,153 rows, 11 columns (includes numeric remaining_lease)
 * File 4 (2017 – Present): 169,584 rows, 11 columns (includes string-formatted remaining_lease, e.g., "61 years 04 months")

Cleaning Action:
When concatenating the datasets into a master dataframe, standardize column names and handle schema mismatches (e.g., computing or parsing remaining_lease uniformly across all periods).

2. Missing Values & Data Integrity
 * Null Check: Across all four raw CSV files, there are 0 explicit null/NaN values in any standard column.
 * Implicit Missingness: The primary "missing" attribute is the remaining_lease field in datasets prior to 2015.
 * Correction Strategy: Backfill or calculate remaining lease dynamically using the formula: $\text{Remaining Lease} = 99 - (\text{Transaction Year} - \text{Lease Commence Date})$, or parse string values from post-2017 records into decimal years.

3. Data Type Standardization
To ensure accurate aggregations, filtering, and modeling, enforce the following data type conversions during ingestion:
 * month / transaction_date: Convert from string (YYYY-MM) to datetime objects (pd.to_datetime). Extract year and month as discrete integer columns for temporal grouping.
 * resale_price & floor_area_sqm: Ensure numeric types (float or int) for mathematical operations, price-per-sqm calculations, and statistical summaries.
 * lease_commence_date: Ensure integer format to accurately calculate property age and lease decay.
 * Categorical Features (town, flat_type, flat_model, story_range): Convert to string/categorical type to optimize memory usage and group-by performance.

4. Data Anomalies & Edge Cases
 * Lease Format Inconsistencies: Post-2017 records store remaining lease as descriptive strings (e.g., "61 years 04 months"), whereas 2015–2016 records store integers (e.g., 70). A custom parsing function is required to convert string formats into decimal floats.
 * Storey Range Formatting: Storey ranges are formatted as text intervals (e.g., "07 TO 09" or "01 TO 03"). For advanced valuation modeling or regression, consider engineering features for lower bound, upper bound, or median storey.
 * Spatial Coordinates: Note that town-level and street-level coordinate attributes (street_lat, street_lon, town_lat, town_lon) may require validation for missing spatial projections or outlier geo-mapping if performing geospatial clustering.

## 🛠️ Usage Example (Python & Pandas)

Get started analyzing this dataset quickly using Python:

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# 1. Load the four CSV files
df_2000 = pd.read_csv('https://raw.githubusercontent.com/Elder-stack/LHUD-Capstone-Ivan/refs/heads/main/resale-flat-prices-based-on-approval-date-2000-feb-2012.csv')
df_2012 = pd.read_csv('https://raw.githubusercontent.com/Elder-stack/LHUD-Capstone-Ivan/refs/heads/main/resale-flat-prices-based-on-registration-date-from-mar-2012-to-dec-2014.csv')
df_2015 = pd.read_csv('https://raw.githubusercontent.com/Elder-stack/LHUD-Capstone-Ivan/refs/heads/main/resale-flat-prices-based-on-registration-date-from-jan-2015-to-dec-2016.csv')
df_2017 = pd.read_csv('https://raw.githubusercontent.com/Elder-stack/LHUD-Capstone-Ivan/refs/heads/main/ResaleflatpricesbasedonregistrationdatefromJan2017onwards.csv')

# 2. Combine all dataframes into one master dataset
df_master = pd.concat([df_2000, df_2012, df_2015, df_2017], ignore_index=True)

print(f"Master Dataset Shape: {df_master.shape}")
print(df_master.head())
```
<img width="464" height="300" alt="image" src="https://github.com/user-attachments/assets/fc7eb319-4756-4282-85d4-5130350b6648" />

```python
# Convert month to datetime and extract transaction year
df_master['transaction_date'] = pd.to_datetime(df_master['month'])
df_master['year'] = df_master['transaction_date'].dt.year

# Ensure numeric columns are properly formatted
numeric_cols = ['floor_area_sqm', 'resale_price', 'lease_commence_date']
for col in numeric_cols:
    if col in df_master.columns:
        df_master[col] = pd.to_numeric(df_master[col], errors='coerce')

# Handle remaining lease for 2017+ data if needed (extracting decimal years from strings)
def parse_remaining_lease(val):
    if pd.isna(val):
        return None
    if isinstance(val, (int, float)):
        return float(val)
    # If string like "61 years 04 months"
    parts = str(val).split()
    years = float(parts[0]) if len(parts) > 0 and parts[0].isdigit() else 0.0
    months = float(parts[2]) if len(parts) > 2 and parts[2].isdigit() else 0.0
    return years + (months / 12.0)

if 'remaining_lease' in df_master.columns:
    df_master['remaining_lease_years'] = df_master['remaining_lease'].apply(parse_remaining_lease)
else:
    # Approximate remaining lease if missing in older files
    df_master['remaining_lease_years'] = 99 - (df_master['year'] - df_master['lease_commence_date'])
```

```python
# Aggregate transaction count by year
demand_trend = df_master.groupby('year').size().reset_index(name='transaction_count')

plt.figure(figsize=(10, 5))
sns.lineplot(data=demand_trend, x='year', y='transaction_count', marker='o', color='teal', linewidth=2.5)
plt.title('HDB Resale Transaction Volume (2000 – Present)')
plt.xlabel('Year')
plt.ylabel('Number of Transactions')
plt.grid(True, linestyle='--', alpha=0.6)
plt.show()
```
 <img width="879" height="470" alt="image" src="https://github.com/user-attachments/assets/e6951fbe-9f78-431f-afff-62e4c7ba6bc1" />

```python
# Calculate median resale price and floor area price per sqm by year
price_trend = df_master.groupby('year')['resale_price'].agg(['median', 'mean']).reset_index()

plt.figure(figsize=(10, 5))
sns.lineplot(data=price_trend, x='year', y='median', marker='s', color='coral', linewidth=2.5)
plt.title('Median HDB Resale Price Over Time')
plt.xlabel('Year')
plt.ylabel('Median Resale Price (SGD)')
plt.grid(True, linestyle='--', alpha=0.6)
plt.show()
```
<img width="888" height="470" alt="image" src="https://github.com/user-attachments/assets/c2e5e9d7-5e06-43d0-bec5-99eb8b25cbeb" />

```python
# Compare resale price distribution across flat types
plt.figure(figsize=(12, 6))
sns.boxplot(data=df_master, x='flat_type', y='resale_price', palette='Set2')
plt.title('Resale Price Distribution by Flat Type')
plt.xlabel('Flat Type')
plt.ylabel('Resale Price (SGD)')
plt.xticks(rotation=45)
plt.show()
```
<img width="1001" height="639" alt="image" src="https://github.com/user-attachments/assets/c19151b9-80b1-4176-b4a8-8ab0b8e22271" />

```python
# Find top towns by average resale price and transaction volume
town_performance = df_master.groupby('town').agg(
    avg_price=('resale_price', 'mean'),
    total_transactions=('town', 'count')
).reset_index().sort_values(by='avg_price', ascending=False)

print("Top 10 Towns by Average Resale Price:")
print(town_performance.head(10))
```
<img width="353" height="180" alt="image" src="https://github.com/user-attachments/assets/bab22f03-66a5-4c83-b7da-6dc5c0a94344" />

## 💡 Potential Projects & Analysis Directions
Base on the compelling Potential Projects & Analysis Directions designed to leverage your historical Singapore HDB resale flat dataset (~628,591 transactions spanning 2000 onwards). These project tracks align directly with your analytical objectives and provide clear roadmaps for data exploration, modeling, and visualization.

Project Track 1: Predictive Property Valuation Model (Machine Learning)
* Objective: Build a regression model to predict HDB resale prices based on structural, temporal, and spatial attributes.
* Key Features to Engineer:

  1. Property Age / Remaining Lease: Calculate exact remaining lease years at the time of transaction.
  
  2. Storey Midpoint: Convert range strings (e.g., "07 TO 09") into numeric midpoints (8).
  
  3. Spatial Proximity / Town Premiums: One-hot encode towns or compute distance metrics relative to the Core Central Region (CCR).
  
* Modeling Approaches: Random Forest Regressor, XGBoost, or LightGBM to capture non-linear relationships between floor area, lease decay, and price.

Project Track 2: Lease Decay & Depreciation Impact Study
* Objective: Quantify how a flat's remaining lease affects its market value, especially for older flats approaching the 99-year leasehold limit.
* Analytical Focus:

  1. Group transactions by remaining lease brackets (e.g., 90+ years, 70–89 years, <70 years).
  
  2. Calculate the price-per-square-metre discount associated with each decade of lease aging.
  
  3. Compare depreciation rates across mature estates (e.g., Queenstown, Tampines) versus non-mature estates (e.g., Sengkang, Punggol).

Project Track 3: Geographic & Spatial Heatmapping (GIS Analysis)
* Objective: Uncover spatial price clustering and identify HDB resale demand hotspots across Singapore using coordinate data (street_lat, street_lon, town_lat, town_lon).
* Analytical Focus:

  1. Plot transaction densities using geospatial scatter plots or hexbin maps.
  
  2. Analyze price gradients moving outward from the city center.
  
  3. Examine town-level affordability variations mapped against geographic coordinates.

Project Track 4: Macroeconomic & Policy Impact Dashboard
* Objective: Analyze how historical cooling measures, government housing grants, and broader economic cycles (e.g., 2008 Financial Crisis, post-2020 pandemic property boom) influenced HDB resale price indices and transaction volumes.
* Analytical Focus:

  1. Construct a custom HDB Resale Price Index (median price per sqm indexed to year 2000 = 100).
  
  2. Analyze volume spikes versus price appreciation phases.
  
  3. Examine shifts in demand across flat types (e.g., rising popularity of larger 4-room and 5-room flats vs. 3-room flats).

Project Track 5: Automated Interactive HDB Analytics DashboardObjective: Build an interactive Power BI or Streamlit dashboard enabling users to filter resale transactions by town, flat type, date range, and floor area to instantly view pricing benchmarks.
* Key Visualizations:

  1. KPI Cards: Median resale price, total transaction volume, average price per sqm.
  
  2. Trend Lines: Multi-year price trajectory by flat type.
  
  3. Box Plots: Price distribution across different towns and storey ranges.
  
  4. Scatter Plot: Floor area ($\text{m}^2$) versus Resale Price (SGD) colored by remaining lease


