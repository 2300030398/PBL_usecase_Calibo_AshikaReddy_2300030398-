# Power BI Sales Intelligence

Sales Performance, Profitability and Business Intelligence Dashboard

A Business Intelligence case study from Calibo AI Academy. It turns three years of retail sales data, spread across nine disconnected tables, into one interactive Power BI model that drills from company-wide KPIs down to a single order, product or location.

## Business Problem

**Situation:** Sales, product, location, customer, salesperson and budget data sit in nine disconnected tables that are refreshed by hand every month.

**Complication:** Managers cannot quickly tell which products, cities or salespeople are driving revenue, or which ones are falling short of budget.

**Key question:** Where are we generating the most revenue and profit, and where should management focus attention next?

**Primary stakeholder:** Business managers who need a self-serve view instead of a monthly Excel rebuild.

**Success definition:** One interactive Power BI model that drills from company-wide KPIs down to a single order, product or location.

## Project Snapshot

| Metric | Value |
|---|---|
| Total revenue | $25.66M |
| Gross profit | $8.34M |
| Orders | 10,889 |
| Gross margin | 32.5% |
| Units sold | 21,078 |
| Products | 101 |
| Locations | 74 |
| Customers | 801 |
| Salespeople | 45 |

- **Analysis period:** 01 Jan 2021 to 15 Mar 2023
- **Source tables (9):** Sales for 2021, 2022 and 2023, Products, Locations, Customers, Sales People, Budgeting and Date Ranges

## Tech Stack

- Power BI
- DAX
- Excel (source data)

## Project Workflow

```
Data Quality -> Star-Schema Model -> DAX Measures -> Dashboard Design -> Key Findings -> Recommendations
```

### 1. Data Preparation

1. **Import:** Loaded all 9 sheets (3 yearly sales tables, Products, Locations, Customers, Sales People, Budgeting, Date Ranges).
2. **Clean:** Fixed data types, removed blanks, standardized column names and checked for duplicate Order IDs.
3. **Append:** Combined the 2021 to 2023 sales (10,889 rows) into one consistent `Fact_Sales` table.
4. **Model-ready:** Added calculated Revenue and Cost columns for the star-schema model.

### 2. Data Quality Findings

| Check | Result |
|---|---|
| Duplicate orders | None. All 10,889 Order IDs are unique, so the tables were safe to append directly. |
| Missing values | None. Sales, Products, Locations and Customers passed null checks column by column. |
| Budgeting key mismatch | 23 of 97 Location IDs in Budgeting do not match `Dim_Location`. Flagged for reconciliation. |
| Partial year | 2023 sales run only from 1 Jan to 15 Mar, so 2023 is labelled and not compared like-for-like. |

### 3. Data Model: Star Schema

One fact table, four dimensions and a marked date table, with a single direction of filter flow. There is no snowflaking and there are no many-to-many relationships.

| Table | Key columns |
|---|---|
| `Fact_Sales` | Order ID, Product ID, Location ID, Salesperson ID, Customer ID, Order Date, Quantity, Price |
| `Dim_Product` | Product ID, Name, Cost, Price |
| `Dim_Location` | Location ID, City, State, Population |
| `Dim_Customer` | Customer ID, Customer Name |
| `Dim_Salesperson` | Salesperson ID, Name |
| `Dim_Date` (marked date table) | Year, Quarter, Month, Week, Day |

### 4. DAX Measures

Every KPI on the dashboard is a measure, not a hard-typed number.

**Sales and profitability:** Total Sales, Total Orders, Total Quantity Sold, Average Order Value, Total Cost, Gross Profit, Gross Margin %, Revenue per Unit.

**Time intelligence and budget:** Current and Previous Year Sales, YoY Sales Growth and YoY Growth %, MTD Sales, YTD Sales and Previous Year YTD, Budget and Actual Sales, Budget Variance, Budget Achievement %.

Sample measures:

```dax
Total Sales =
SUMX ( Fact_Sales, Fact_Sales[Quantity] * Fact_Sales[Price] )

Gross Profit =
[Total Sales] -
SUMX ( Fact_Sales, Fact_Sales[Quantity] * RELATED ( Dim_Product[Cost] ) )

Gross Margin % =
DIVIDE ( [Gross Profit], [Total Sales], 0 )

YoY Growth % =
VAR PY = CALCULATE ( [Total Sales], SAMEPERIODLASTYEAR ( Dim_Date[Date] ) )
RETURN DIVIDE ( [Total Sales] - PY, PY, 0 )

YTD Sales =
TOTALYTD ( [Total Sales], Dim_Date[Date] )

Budget Achievement % =
DIVIDE ( [Actual Sales], [Budget], 0 )
```

### 5. Dashboard Design

| Page | What it shows |
|---|---|
| **Executive Overview** | 8 KPI cards (Total Sales, Total Profit, Margin %, Orders, Quantity, AOV, Budget Achievement %, YoY %), sales trend line, sales by year, top 10 products, top 10 customers, top salespeople, actual vs budget |
| **Product Performance** | Top and bottom 10 products, sales vs profit scatter, margin by product table, product sales trend |
| **Customer Insights** | Top customers by revenue, orders and AOV by customer, revenue contribution %, high-sales low-margin flags |
| **Salesperson Performance** | Sales and profit by rep, orders handled, YoY performance by rep, contribution % ranking |
| **Geographic Analysis** | Filled map of 74 California locations, sales vs population scatter, location ranking matrix |
| **Budget vs Actual** | Actual vs Budget columns, variance chart, achievement KPI, monthly trend by location |

Interactive features on every page:

- **Slicers:** Year, Month, State, Location, Product, Customer, Salesperson
- **Drill-down:** Year to Quarter to Month to Day, and State to Location
- **Drill-through:** Dedicated pages for Product, Customer, Salesperson and Location
- **Tooltips and cross-filtering:** Report tooltips and synced selection across all visuals

## Key Findings

### Revenue and Profitability

| Year | Revenue |
|---|---|
| 2021 | $11.69M |
| 2022 | $11.57M |
| 2023 (Jan to Mar only) | $2.40M |

- 2023 covers only about 2.5 months, so it is a partial year and not a decline.
- Total cost is 67.5% of revenue and gross profit is 32.5%.
- The overall margin is steady at about 32.5%, but product-level margins range from about 15% (Products 4, 95 and 27) to about 50% (Products 41, 96 and 40). This gives a clear shortlist for a pricing and cost review.

### Customers, Salespeople and Locations

| Area | Finding |
|---|---|
| Top city | Rialto, with $465.6K in revenue, leading all 74 California locations |
| Top salesperson | Kenneth Bradley, with $678.8K in sales, the highest of 45 reps |
| Top customer | Jesse Hill, with $171.3K, the highest single-customer revenue |
| Customer concentration | The top 10 customers contribute only about 5.4% of total revenue, so the customer base is broad and low risk |
| Population and sales | The correlation between location population and revenue is about 0.07, essentially no relationship |
| Weakest cities | Antioch, Costa Mesa and San Francisco each generate about $280K, roughly 40% below the leaders at about $450K or more |

## Business Recommendations

1. **Reconcile Budgeting location keys:** 23 of 97 Budgeting Location IDs do not match `Dim_Location`. Fix this before using the budget data for accountability reporting.
2. **Review low-margin products:** Investigate pricing and cost for Products 4, 95 and 27 (about 15 to 18% margin) while protecting Products 41, 96 and 40 (about 50%).
3. **Invest by performance, not population:** Population barely predicts revenue, so direct marketing and staffing toward proven performers such as Rialto.
4. **Label 2023 as a partial year:** Make this clear in every YoY view so a 2.5-month slice is not misread as a sales decline.
5. **Prioritize reps and locations over VIP accounts:** With the top 10 customers at only about 5.4% of revenue, retention effort is better spent on salespeople and cities.

## Conclusion

Clean data leads to a trustworthy model, the model supports measures that never disagree, and the measures feed dashboards that any manager can question directly. Every insight in this project ties back to a DAX measure or a table check.

## Author

**M.V. Ashika Reddy**
Business Intelligence Case Study, Calibo AI Academy, 2026
Email: ashikareddymajjiga@gmail.com
