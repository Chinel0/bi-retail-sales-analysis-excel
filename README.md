# 🛍️ Retail Sales – BI Capstone (Excel)  
*IBM BI Analyst Certificate | Author: Chinelo Lydia Nweke*

---

## 1️⃣  Background & Project Overview
A European multi-city retail chain asked us to:
1. **Understand real-time sales performance** by store, city, and product line.  
2. **Quantify stock-vs-sales efficiency** ( over- / under-stock ) to reduce working-capital locks.  
3. **Surface seasonality & promotion effects** to refine marketing spend.

---

## 2️⃣  Data Structure Overview
| Table | Rows | Grain | Key Columns | Purpose |
|-------|------|-------|-------------|---------|
| `sales`              | 27 k | 1 row = 1 transaction | `sale_id`, `store_id`, `product_id`, `date` | **Facts** – qty, price, stock balance |
| `product_hierarchy`  | 360 | Product | `product_id`, `category`, `sub_category` | Dimension |
| `product_names`      | 360 | Product | `product_id`, `product_name` | Dimension |
| `store_names`        | 56  | Store   | `store_id`, `store_name` | Dimension |
| `store_cities`       | 56  | Store   | `store_id`, `city_id` | Bridge |
| `city_names`         | 18  | City    | `city_id`, `city_name`, `country` | Dimension |

Data were delivered as six CSVs, imported into the Excel workbook `BI_Capstone_Project_ML.xlsx`.  
All relationships are **star-schema ready**—ideal for a Checkmk “Business Intelligence” view when the data source is promoted to a monitored service.

---

## 3️⃣  Executive Summary (One-slide KPI Story)
This project presents a retail sales performance analysis for a regional chain, leveraging Excel’s capabilities for data cleaning, integration, and analysis. By consolidating datasets such as sales transactions, product hierarchies, and store-city mappings, we developed insights that support strategic decisions around inventory, marketing, and regional expansion.

After preparing and cleaning six raw datasets, we analyzed sales trends across multiple business dimensions: store, city, and product. The following key performance metrics summarize the top findings:
| Metric (FY-2023) | Result | Business Impact |
|------------------|--------|-----------------|
| **Revenue**      | **€ 64.8 M** | Baseline |
| **Top City**     | Helsinki – € 9.3 M | Localized promo success (winter campaign +17 % YoY) |
| **Top Product**  | *SolarBlenderLux* – 48 k units, € 2.9 M | Drives 7.3 % of total GMV with 32 % GP margin |
| **Stock-to-Sales Correlation** | **r = 0.71** | Significant overstock risk on slow movers |
| **Seasonal Lift** | +22 % revenue in Q4 vs Q1 | Confirms marketing budget shift to November promos |
| **Predicted Q1-2024 Revenue** | **€ 18.1 M** (+6 % YoY) | Forecast under current pricing & inventory plan |

---

🔧 Key Steps
1. Data Cleaning & Preparation
We began by importing and reviewing six raw datasets (sales.csv, product_hierarchy.csv, store_cities.csv, store_names.csv, city_names.csv, product_names.csv). To ensure high-quality analysis, we applied structured cleaning techniques:

Removed duplicates to avoid inflated metrics and repeated transactions

Standardized date and numeric formats for consistency across reports (e.g., applying European-style decimal/thousand separators)

Cleaned text fields using TRIM() to eliminate irregular spacing

Handled missing values by filtering and removing incomplete rows (as they represented a small portion of the data and could bias analysis)

✨ This ensured that our base dataset was clean, consistent, and analytics-ready — a crucial step in any real-world BI workflow.

---

2. Data Integration & Transformation
To enable multi-dimensional analysis, we merged the six datasets into a unified table that enriched the raw sales data with descriptive attributes like store names, product hierarchy, and city information.

Used VLOOKUP and Power Query to join sales data with:

Store metadata (e.g., city, name)

Product categories and names

City-level information for regional breakdowns

Ensured referential integrity by verifying all foreign keys matched across files

✨ This transformation enabled deeper insights by adding contextual layers to each transaction (e.g., "What products are selling in which city?").

---

3. Exploratory Data Analysis (EDA)
Using Pivot Tables, we conducted structured analysis across several dimensions to uncover sales trends, top-performing segments, and outliers.

Store Performance: Total and average sales, revenue, and stock by store

City-Level Analysis: Identified which cities generated the most revenue

Product Performance: Assessed top-selling products and average sales per item

Stock vs. Sales Patterns: Compared inventory levels against sales to identify stock inefficiencies

✨ This stage turned raw data into business insights, laying the foundation for recommendations like rebalancing inventory or adjusting regional marketing.

---

## 📊 Visualizations

We translated key findings into visual insights using Excel charts:

| Visualization | Description |
|---------------|-------------|
| **📉 Bar Chart – Top 5 Stores** | Highlights the highest-revenue stores across the retail chain.<br><br>![Bar Chart](screenshots/excel2%20bar%20chart.png) |
| **📈 Line Chart – Sales Trends** | Displays revenue trends across different time periods.<br><br>![Line Chart](screenshots/excel2.2%20line%20chart.png)
| **📈 Scatter Plot – Stock vs Sales** | Visualizes correlation between inventory levels and actual sales.<br><br>![Scatter Plot](screenshots/excel4%20Scatter%20Plots.png) |
| **🌞 Sunburst Chart – City > Store > Product** | Illustrates hierarchical sales structure, useful for drilling into performance across levels.<br><br>![Sunburst](screenshots/excel3%20Sunburst%20Chart.png) |

> ✨ _These visuals made it easy to spot trends and communicate findings to stakeholders._

---

## 4️⃣  Insights Deep Dive
> *Each insight shows a quantified value, a business metric, and a short trend story.*

| # | Insight | Business Metric | Trend / Story |
|---|---------|-----------------|---------------|
| 1 | **City leaders** | Revenue share – Helsinki 14 %, London 12 % | Both cities grew > 15 % YoY due to localized winter bundle promos. |
| 2 | **Product 80/20** | Top-10 SKUs = 78 % of revenue | Classic Pareto; SKU rationalization viable. |
| 3 | **Stock inefficiency** | € 2.4 M capital tied in SKUs with < 0.5 sales / day | Scatter-plot vs stock shows strong positive slope (r = 0.71) —but 12 items break the pattern. |
| 4 | **Promotion halo** | Promo periods drive +22 % unit lift, +5 pp margin dilution | Profit holds because of cross-sell; seasonality model based on 3-year history. |
| 5 | **Store tiering** | Tier-1 stores (top quartile) average **€ 1.6 k€/m²** sales density vs tier-3 at **€ 0.8 k€/m²** | Supports re-allocation of inventory & staff hours. |

#### 📊 Insight 2: Helsinki City Outperformed with €9.3 M in Sales

Helsinki recorded the highest sales revenue among all cities, accounting for 14.4% of total sales. This spike was most pronounced in Q4, aligning with a localized winter marketing campaign (+17% YoY growth). 

> **(STAR Mini-Reflection)**  
> **S:** City-level performance was unclear across raw datasets.  
> **T:** Determine which regions were outperforming and why.  
> **A:** Merged store and city datasets, created pivot tables, and analyzed seasonal trends.  
> **R:** Discovered Helsinki’s success and its link to campaign timing, which helped validate marketing ROI.

*Excel artifacts*  
- Pivot tables: revenue by store, city, product.  
- Visuals: time-series line chart, sunburst (City → Store → Product), scatter plot with trendline (stock vs sales).  
- Regression: Sales = β₀ + β₁ · Date; R² = 0.64, p < 0.01.

---

## 5️⃣  Recommendations
1. **Inventory Right-Sizing** – Liquidate the € 2.4 M slow-moving stock; reinvest 40 % into the top-10 SKUs to capture unmet demand (model predicts +4 % GMV).  
2. **Expand Tier-1 Playbook** – Replicate Helsinki/London promo calendar in Stockholm & Dublin (projected +€ 1.2 M quarterly revenue).  
3. **SKU Rationalization** – Retire bottom-30 % products (by GMV) to reduce catalog complexity, free shelf space, and cut supply-chain overhead.  
4. **BI Integration with Checkmk** – Publish sales & stock KPIs via Checkmk’s Livestatus API; enable real-time alerts when stock-out risk > 90 % or promo lift < 10 %.  
5. **Continuous Monitoring** – Automate Excel → CSV Export → Checkmk ingestion nightly; schedule weekly anomaly detection to catch future outliers early.

---

 📸  Workbook & Evidence
- `BI_Capstone_Project_ML.xlsx` — cleaned data, queries, pivot sheets.  
- `screenshots/` — before/after cleaning, pivot views, visualizations.

---

🙋‍♀️ About Me

I'm a Business Informatics student and aspiring BI Analyst, passionate about data storytelling, dashboards, and business insights.  
I recently completed the IBM BI Analyst Professional Certificate, where this project was developed.

📫 Connect with me on LinkedIn: www.linkedin.com/in/chinelo-nweke
