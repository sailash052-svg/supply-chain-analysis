# Global Supply Chain Performance Analysis

A data analytics portfolio project: cleaning, exploratory analysis, and dashboarding of a 100-SKU supply chain dataset spanning skincare, haircare, and cosmetics product lines — from manufacturing and supplier quality through logistics and revenue.

**[▶ View the interactive dashboard](./dashboard_prototype.html)** &nbsp;|&nbsp; **[📄 Read the full report](./Supply_Chain_Analysis_Report.docx)** &nbsp;|&nbsp; **[📊 Power BI build guide](./PowerBI_Dashboard_Guide.md)**

> Tip: GitHub doesn't render `.html` files live — host `dashboard_prototype.html` on **GitHub Pages** (Settings → Pages → deploy from this repo) to get a clickable live link, or open it locally by downloading the file.

---

## What's in this project

| File | Description |
|---|---|
| `supply_chain_cleaned.csv` / `.xlsx` | Cleaned dataset with added fields: Profit, Profit Margin %, Revenue per Unit, Cost per Unit, Total Lead Time, Stockout Risk flag, High Defect flag |
| `Supply_Chain_Analysis_Report.docx` | Full written EDA report — data overview, cleaning notes, 6 key findings with charts, recommendations |
| `dashboard_prototype.html` | Self-contained interactive dashboard (Chart.js) — filter by product, location, supplier, transportation mode |
| `PowerBI_Dashboard_Guide.md` | Step-by-step guide to rebuild this dashboard in Power BI Desktop, including exact DAX measures and page layouts |
| `charts/` | Individual PNG charts used in the report |

## Key findings

- **Skincare** drives the most revenue ($241.6K) on volume, not price — it sold ~21K units vs. ~12–14K for the other two categories.
- **Supplier 1** has the lowest average defect rate (1.80%); **Supplier 5** the highest (2.67%) — a ~48% quality gap between best and worst.
- **77% of inspected batches are not yet a confirmed Pass** (41% Pending, 36% Fail) — the clearest operational bottleneck in the data.
- **Air freight costs ~21% more** than sea freight on average — a direct lever for cutting logistics spend on non-urgent shipments.
- **Mumbai and Kolkata** are the top two revenue locations; **Delhi** trails by ~41%.

See the full report for methodology, all six charts, and recommendations.

## Tools used

`Python (pandas, matplotlib)` for cleaning and EDA · `Chart.js` for the interactive dashboard prototype · `Power BI Desktop` (build guide included) for the production dashboard · `Excel/CSV` as the interchange format.

## Data source

Supply chain dataset (100 SKUs, cosmetics/skincare/haircare), originally sourced as a public Kaggle sample dataset.

## About this project

Built as a self-guided data analyst portfolio project to demonstrate the full workflow: data cleaning → exploratory analysis → business insight → dashboard delivery.
