# BrewMetrics BI: Version-Controlled Analytics Solution

An enterprise Power BI solution for BrewMetrics Coffee Co. built using Power BI Projects (`.pbip`), Tabular Model Definition Language (TMDL), and Git version control.

## Data Model Architecture (Star Schema)

- **Fact_Sales:** 15,482 retail sales transactions from April–July 2026
- **Dim_Date:** 92-row date dimension with Year, Month, Quarter, and Day columns (marked as Date Table)
- **Dim_City:** 4 South Indian markets — Bengaluru, Chennai, Hyderabad, Coimbatore (with State mapping)
- **Dim_Product:** 10 SKUs across Coffee, Bakery, and Merchandise categories
- **Relationships:** Three 1-to-many, single-direction relationships from dimensions to the fact table

## DAX Measures

1. **Sales MoM Growth %** — Month-over-month percentage change using `DATEADD` time intelligence
2. **Running Total Sales** — Cumulative sales using `ALLSELECTED` date filtering
3. **City Sales Rank** — Dynamic ranking using `RANKX` with `ALLSELECTED` context
4. **Cold Brew Sales Share %** — Cold Brew contribution with an `ALL`-based denominator for correct filtering

## Dashboard Visuals

1. **Monthly Sales Trend with Cold Brew Overlay** — Line and column chart showing Cold Brew seasonal spike (21% share in April–May, dropping to 15.5% in June)
2. **Sales by City & Store Format** — Clustered bar chart with drill-down hierarchy revealing Bengaluru's 36% revenue lead over Coimbatore
3. **Product Performance Matrix** — Detailed table showing all products with sales, ranking, running totals, and Cold Brew share
4. **City Slicer** — Interactive tile slicer for filtering all visuals by city

## Key Business Insights

1. **Cold Brew Seasonality:** Cold Brew sales peak in April (₹2.77L) and May (₹3.01L) during peak summer, then decline 38.5% in June (₹1.85L)
2. **City Performance Gap:** Bengaluru leads all markets at ₹11.20L (28.2% of total), outperforming Coimbatore (₹8.23L) by over 36%
3. **Store Format Dominance:** Flagship stores generate 45.8% of revenue across all cities, followed by Drive-Thru (32.2%) and Kiosk (22.0%)

## How to Open

1. Ensure Power BI Desktop has the `.pbip` preview feature enabled.
2. Open `BrewMetrics.pbip` from the project folder.
