\# BrewMetrics BI: Version-Controlled Analytics Solution

An enterprise Power BI solution for BrewMetrics Coffee Co. built using Power BI 

Projects (.pbip), Tabular Model Definition Language (TMDL), and Git version 

control.

\## Data Model Architecture (Star Schema)

\- \*\*Fact\_Sales:\*\* 15,482 retail sales transactions from April–July 2026

\- \*\*Dim\_Date:\*\* 92-row date dimension with Year, Month, Quarter, Day columns 

&nbsp; (marked as Date Table)

\- \*\*Dim\_City:\*\* 4 South Indian markets — Bengaluru, Chennai, Hyderabad, 

&nbsp; Coimbatore (with State mapping)

\- \*\*Dim\_Product:\*\* 10 SKUs across Coffee, Bakery, and Merchandise categories

\- \*\*Relationships:\*\* Three 1-to-many single-direction relationships from 

&nbsp; dimensions to the fact table

\## DAX Measures

1\. \*\*Sales MoM Growth %\*\* — Month-over-month percentage change using DATEADD 

&nbsp;  time intelligence

2\. \*\*Running Total Sales\*\* — Cumulative sales using ALLSELECTED date filtering

3\. \*\*City Sales Rank\*\* — Dynamic ranking using RANKX with ALLSELECTED context

4\. \*\*Cold Brew Sales Share %\*\* — Cold Brew contribution with ALL-based 

&nbsp;  denominator for correct filtering

\## Dashboard Visuals

1\. \*\*Monthly Sales Trend with Cold Brew Overlay\*\* — Line and column chart 

&nbsp;  showing Cold Brew seasonal spike (21% share in April-May, drops to 15.5% 

&nbsp;  in June)

2\. \*\*Sales by City \& Store Format\*\* — Clustered bar chart with drill-down 

&nbsp;  hierarchy revealing Bengaluru's 36% revenue lead over Coimbatore

3\. \*\*Product Performance Matrix\*\* — Detailed table showing all products with 

&nbsp;  sales, ranking, running totals, and Cold Brew share

4\. \*\*City Slicer\*\* — Interactive tile slicer for filtering all visuals by city

\## Key Business Insights

1\. \*\*Cold Brew Seasonality:\*\* Cold Brew sales peak in April (₹2.77L) and May 

&nbsp;  (₹3.01L) during peak summer, then decline 38.5% in June (₹1.85L)

2\. \*\*City Performance Gap:\*\* Bengaluru leads all markets at ₹11.20L (28.2% of 

&nbsp;  total), outperforming Coimbatore (₹8.23L) by over 36%

3\. \*\*Store Format Dominance:\*\* Flagship stores generate 45.8% of revenue across 

&nbsp;  all cities, followed by Drive-Thru (32.2%) and Kiosk (22.0%)

\## How to Open

1\. Ensure Power BI Desktop has `.pbip` preview feature enabled

2\. Open `BrewMetrics.pbip` from the project folder



&nbsp; 

