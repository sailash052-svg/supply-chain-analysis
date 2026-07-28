# Power BI Dashboard — Build Guide
### Global Supply Chain Performance Dashboard

This guide walks you through building the Power BI dashboard from `supply_chain_cleaned.xlsx` in Power BI Desktop. Follow it top to bottom and you'll end up with a 3-page report suitable for a portfolio.

---

## 1. Import the data

1. Open **Power BI Desktop** → **Get Data** → **Excel workbook** → select `supply_chain_cleaned.xlsx`.
2. Load the **Supply Chain Data** sheet.
3. In **Power Query Editor**, confirm data types:
   - `Price`, `Revenue generated`, `Costs`, `Profit`, `Shipping costs`, `Manufacturing costs` → Decimal Number
   - `Availability`, `Number of products sold`, `Stock levels`, all `*Lead Time*`, `Order quantities`, `Shipping Time (days)`, `Production volumes` → Whole Number
   - `Defect rates`, `Profit Margin %` → Decimal Number (format as % where relevant)
   - `Stockout Risk`, `High Defect Flag` → True/False
4. Click **Close & Apply**.

## 2. Create DAX measures

Go to **Modeling → New Measure** and add each of these (paste one at a time):

```dax
Total Revenue = SUM('Supply Chain Data'[Revenue generated])

Total Cost = SUM('Supply Chain Data'[Costs])

Total Profit = [Total Revenue] - [Total Cost]

Profit Margin % = DIVIDE([Total Profit], [Total Revenue], 0)

Avg Defect Rate = AVERAGE('Supply Chain Data'[Defect rates])

Total Units Sold = SUM('Supply Chain Data'[Number of products sold])

Avg Shipping Cost = AVERAGE('Supply Chain Data'[Shipping costs])

Pass Rate % =
DIVIDE(
    CALCULATE(COUNTROWS('Supply Chain Data'), 'Supply Chain Data'[Inspection results] = "Pass"),
    COUNTROWS('Supply Chain Data'),
    0
)

Avg Total Lead Time = AVERAGE('Supply Chain Data'[Total Lead Time (days)])
```

## 3. Page 1 — Executive Overview

**Layout:** 4 KPI cards across the top, 2 charts below.

| Visual | Fields |
|---|---|
| Card | `Total Revenue` |
| Card | `Total Profit` |
| Card | `Profit Margin %` (format as %) |
| Card | `Pass Rate %` (format as %) |
| Clustered column chart | Axis: `Product type` · Value: `Total Revenue`, `Total Profit` |
| Donut chart | Legend: `Inspection results` · Value: Count of rows |

**Slicers (top of page, apply to all pages via sync):** `Product type`, `Location`, `Supplier name`.

## 4. Page 2 — Supplier & Quality Deep Dive

| Visual | Fields |
|---|---|
| Bar chart (horizontal) | Axis: `Supplier name` · Value: `Avg Defect Rate` |
| Stacked bar chart | Axis: `Supplier name` · Legend: `Inspection results` · Value: Count of rows |
| Scatter chart | X: `Price`, Y: `Defect rates`, Size: `Number of products sold`, Legend: `Product type` |
| Table | `Supplier name`, `Avg Defect Rate`, `Pass Rate %`, `Avg Total Lead Time` (use a matrix visual, rows = Supplier name) |

## 5. Page 3 — Logistics & Cost

| Visual | Fields |
|---|---|
| Column chart | Axis: `Transportation modes` · Value: `Avg Shipping Cost` |
| Map (if geocoding resolves) or bar chart | Axis: `Location` · Value: `Total Revenue` |
| Line/clustered chart | Axis: `Routes` · Value: `Avg Shipping Cost`, `Avg Total Lead Time` |
| Card row | `Avg Total Lead Time`, count of `Stockout Risk = TRUE` rows |

## 6. Formatting checklist

- Theme: use a custom theme with the palette `#2E4057` (navy), `#4F6D7A` (slate), `#C0D6DF` (light blue) — **View → Themes → Browse for themes** and upload a theme JSON with these colors, or set them manually per visual.
- Add a title text box at the top of each page: "Global Supply Chain Performance — [Page Name]".
- Turn on **tooltips** showing SKU-level detail on hover for the scatter and bar charts.
- Add a page-level filter/slicer sync so `Product type`, `Location`, and `Supplier name` selections carry across all 3 pages (**View → Sync Slicers**).

## 7. Publish for your portfolio

1. **File → Publish → Publish to Power BI** (requires a free Power BI account).
2. In the Power BI Service, open the report → **File → Embed report → Publish to web (public)** if you want a shareable public link (note: this makes the data public — fine for this open dataset, not for confidential data).
3. Copy the embed link and add it to your portfolio site / GitHub README under "Live Dashboard."
4. Also export a few screenshots (**File → Export → PDF**, then screenshot key pages) to include directly in your portfolio in case the viewer doesn't have a Power BI account.

---
*Pairs with: `supply_chain_cleaned.xlsx` (data source), `Supply_Chain_Analysis_Report.docx` (written analysis), `dashboard_prototype.html` (interactive preview you can host immediately without Power BI Desktop).*
