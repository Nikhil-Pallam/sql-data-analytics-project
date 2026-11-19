# SQL Data Analytics Project

## About
 
Exploratory Data Analysis and Advanced Analytics in SQL, from the first look at the data to a customer report and a product report. The data and every query.

Exploratory SQL analysis and reporting views built on top of a sales data warehouse in SQL Server, using the `DataWarehouseAnalytics` database's gold-layer schema (`dim_customers`, `dim_products`, `fact_sales`).
 
This project focuses on turning a clean, modeled dataset into business insights — EDA, trend analysis, ranking, segmentation, and two reusable SQL views for ongoing reporting.
 
## Project Overview
 
The warehouse follows a star-schema design:
 
- **`gold.dim_customers`** — customer attributes (demographics, location, account creation date)
- **`gold.dim_products`** — product attributes (category, subcategory, cost, product line)
- **`gold.fact_sales`** — sales transactions linking customers and products (order/shipping/due dates, sales amount, quantity, price)
The analysis is organized into two stages:
 
1. **Exploratory SQL analysis** (scripts 01–11) — understanding the data and surfacing initial insights
2. **Reporting views** (scripts 12–13) — consolidating findings into two production-ready views for repeatable reporting
## Repository Structure
 
```
sql-data-analytics-project/
│
├── datasets/                          # Source CSV files
│   ├── dim_customers.csv
│   ├── dim_products.csv
│   └── fact_sales.csv
│
├── scripts/
│   ├── 00_init_database.sql           # Creates the DataWarehouseAnalytics DB, gold schema & tables, loads CSVs
│   ├── 01_database_exploration.sql    # Explores tables/columns via INFORMATION_SCHEMA
│   ├── 02_dimensions_exploration.sql  # Unique countries, categories, subcategories, products
│   ├── 03_date_range_exploration.sql  # Order date range, customer age range
│   ├── 04_measures_exploration.sql    # Core business metrics: total sales, quantity, avg price, orders, products, customers
│   ├── 05_magnitude_analysis.sql      # Totals grouped by country, gender, category
│   ├── 06_ranking_analysis.sql        # Top/bottom products & customers using RANK(), DENSE_RANK(), TOP
│   ├── 07_change_over_time_analysis.sql  # Monthly/yearly sales trends (DATETRUNC, FORMAT)
│   ├── 08_cumulative_analysis.sql     # Running totals & moving averages (window functions)
│   ├── 09_performance_analysis.sql    # Year-over-year product performance using LAG()
│   ├── 10_data_segmentation.sql       # Product cost segments; customer VIP/Regular/New segments
│   ├── 11_part_to_whole_analysis.sql  # Category contribution to total sales (%)
│   ├── 12_report_customers.sql        # Creates gold.report_customers view
│   └── 13_report_products.sql         # Creates gold.report_products view
│
└── README.md
```
 
## Key Deliverables
 
### `gold.report_customers`
 
A consolidated view of customer behavior, including:
- Age and age group
- Customer segment (**VIP** / **Regular** / **New**, based on spend and lifespan)
- Recency (months since last order)
- Total orders, sales, quantity purchased, distinct products bought
- Average order value and average monthly spend
### `gold.report_products`
 
A consolidated view of product performance, including:
- Category, subcategory, cost
- Product segment (**High-Performer** / **Mid-Range** / **Low-Performer**, based on total sales)
- Recency (months since last sale)
- Total orders, sales, quantity sold, distinct customers
- Average selling price, average order revenue, average monthly revenue
## Analysis Techniques Used
 
- **Exploratory Data Analysis (EDA):** schema inspection, dimension profiling, date range checks
- **Aggregation:** `SUM()`, `COUNT()`, `AVG()` with `GROUP BY`
- **Ranking:** `RANK()`, `DENSE_RANK()`, `TOP`
- **Window Functions:** `SUM() OVER()`, `AVG() OVER()`, `LAG()` for running totals, moving averages, and year-over-year comparisons
- **Conditional Segmentation:** `CASE` expressions for customer and product segmentation
- **Date Functions:** `DATEPART()`, `DATETRUNC()`, `FORMAT()`, `DATEDIFF()` for time-series and recency analysis
- **Views:** encapsulating multi-step CTE logic into two reusable, query-ready reporting views
## Tools Used
 
- SQL Server / T-SQL
- SSMS (SQL Server Management Studio)
## How to Run
 
1. Update the `BULK INSERT` file paths in `00_init_database.sql` to match your local dataset location.
2. Run `00_init_database.sql` to create the database, schema, tables, and load the data.
3. Run scripts `01` through `11` in order to reproduce the exploratory analysis.
4. Run `12_report_customers.sql` and `13_report_products.sql` to create the two reporting views.
5. Query the views directly for reporting, e.g.:
```sql
SELECT * FROM gold.report_customers WHERE customer_segment = 'VIP';
SELECT * FROM gold.report_products WHERE product_segment = 'High-Performer';
```
 
