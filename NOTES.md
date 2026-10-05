# DAX Development Notes: Copilot Assistance Log
This document records each DAX measure's development, including the initial 
Copilot suggestions, identified issues, and the final corrected versions.
---
## Measure 1: Sales MoM Growth %
**Prompt Given to Copilot:**
> "Write a DAX measure to calculate Month-over-Month Sales Growth percentage. 
> I have a Fact_Sales table with a sales_amount column and a Dim_Date table 
> marked as a date table with a date column."
**Copilot's Initial Suggestion:**

  

MoM_Growth =
(SUM(Fact_Sales[sales_amount]) -
CALCULATE(SUM(Fact_Sales[sales_amount]), DATEADD(Fact_Sales[date], -1, MONTH))) /
CALCULATE(SUM(Fact_Sales[sales_amount]), DATEADD(Fact_Sales[date], -1, MONTH))


  
**Issues Found:**
1. Copilot used `Fact_Sales[date]` inside DATEADD instead of `Dim_Date[date]`. 
   Time intelligence functions require a column from a proper Date table marked 
   as a date table — not a fact table column.
2. Direct arithmetic division (not DIVIDE) causes errors when there is no prior 
   month data (e.g., April has no March before it).
3. Repeats SUM() multiple times instead of reusing the [Total Sales] base measure.
**Final Corrected DAX:**

  

Sales Prior Month =
CALCULATE([Total Sales], DATEADD(Dim_Date[date], -1, MONTH))


  

Sales MoM Growth % =
DIVIDE(
[Total Sales] - [Sales Prior Month],
[Sales Prior Month],
BLANK()
)


  
---
## Measure 2: Running Total Sales
**Prompt Given to Copilot:**
> "Write a DAX measure for a cumulative running total of sales over time."
**Copilot's Initial Suggestion:**

  

Running Total =
CALCULATE(
SUM(Fact_Sales[sales_amount]),
FILTER(Fact_Sales, Fact_Sales[date] <= MAX(Fact_Sales[date]))
)


  
**Issues Found:**
1. Copilot filters the entire Fact_Sales table (15,482 rows) which is very slow 
   on large datasets and violates star schema best practices.
2. The approach breaks when slicers are applied because it ignores the filter 
   context from the Date dimension table.
3. Should filter through the dimension table, not the fact table.
**Final Corrected DAX:**

  

Running Total Sales =
CALCULATE(
[Total Sales],
FILTER(
ALLSELECTED(Dim_Date[date]),
Dim_Date[date] <= MAX(Dim_Date[date])
)
)


  
---
## Measure 3: City Sales Rank
**Prompt Given to Copilot:**
> "Write a DAX measure using RANKX to rank cities by total sales."
**Copilot's Initial Suggestion:**

  

City Rank = RANKX(Dim_City, [Total Sales])


  
**Issues Found:**
1. In a table visual showing City and Total Sales, each row has a filter context 
   that shows only one city. RANKX(Dim_City, ...) evaluates over the filtered 
   Dim_City which has just 1 row — so every city gets rank 1!
2. Missing ALLSELECTED() to evaluate across all visible cities.
3. Missing ISINSCOPE() to suppress the rank on grand total rows.
**Final Corrected DAX:**

  

City Sales Rank =
IF(
ISINSCOPE(Dim_City[city]),
RANKX(
ALLSELECTED(Dim_City[city]),
[Total Sales],
,
DESC,
DENSE
)
)


  
---
## Measure 4: Cold Brew Sales Share %
**Prompt Given to Copilot:**
> "Write a DAX measure to calculate the percentage share of Cold Brew item sales 
> relative to total sales."
**Copilot's Initial Suggestion:**

  

Cold Brew % =
CALCULATE([Total Sales], Dim_Product[item] = "Cold Brew") / [Total Sales]


  
**Issues Found:**
1. No DIVIDE() wrapper — causes division-by-zero errors when total sales is zero.
2. When the visual is filtered to show only Cold Brew, both numerator and 
   denominator become Cold Brew sales, resulting in a misleading 100%.
**Final Corrected DAX:**

  

Cold Brew Sales =
CALCULATE([Total Sales], Dim_Product[item] = "Cold Brew")


  

Cold Brew Sales Share % =
DIVIDE(
[Cold Brew Sales],
CALCULATE([Total Sales], ALL(Dim_Product)),
0
)