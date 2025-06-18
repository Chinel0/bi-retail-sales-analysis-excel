# 🛍️ Retail Sales – BI Capstone (Excel)  
*IBM BI Analyst Certificate | Author: Chinelo Lydia Nweke*

---

## 1️⃣  Background & Project Overview
A European multi-city retail chain asked us to:
1. **Understand real-time sales performance** by store, city, and product line.  
2. **Quantify stock-vs-sales efficiency** ( over- / under-stock ) to reduce working-capital locks.  
3. **Surface seasonality & promotion effects** to refine marketing spend.

**Why it matters at Checkmk**  
Checkmk delivers unified monitoring. Retail groups using Checkmk want dashboards that combine *operational* KPIs (device health, network uptime) **and** *commercial* KPIs (sales, revenue, margin). Clean, well-modeled data is the prerequisite for wiring those metrics into Checkmk’s data-source plug-ins and custom BI tiles.

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
| Metric (FY-2023) | Result | Business Impact |
|------------------|--------|-----------------|
| **Revenue**      | **€ 64.8 M** | Baseline |
| **Top City**     | Helsinki – € 9.3 M | Localized promo success (winter campaign +17 % YoY) |
| **Top Product**  | *SolarBlenderLux* – 48 k units, € 2.9 M | Drives 7.3 % of total GMV with 32 % GP margin |
| **Stock-to-Sales Correlation** | **r = 0.71** | Significant overstock risk on slow movers |
| **Seasonal Lift** | +22 % revenue in Q4 vs Q1 | Confirms marketing budget shift to November promos |
| **Predicted Q1-2024 Revenue** | **€ 18.1 M** (+6 % YoY) | Forecast under current pricing & inventory plan |

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



 📸  Workbook & Evidence
- `BI_Capstone_Project_ML.xlsx` — cleaned data, queries, pivot sheets.  
- `screenshots/` — before/after cleaning, pivot views, visualizations.


🙋‍♀️ About Me

I'm a Business Informatics student and aspiring BI Analyst, passionate about data storytelling, dashboards, and business insights.  
I recently completed the IBM BI Analyst Professional Certificate, where this project was developed.

📫 Connect with me on LinkedIn: www.linkedin.com/in/chinelo-nweke
