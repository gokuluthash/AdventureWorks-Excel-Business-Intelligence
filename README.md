# Adventure Works Sales Analysis

**Author: Gokulraj J**

An interactive sales and profitability analysis built in **Microsoft Excel**, using **Power Query** for data preparation, **Power Pivot** for relational data modelling, and Excel / DAX calculations for business performance analysis.

This project follows an analytics workflow from data preparation and modelling through KPI analysis and interactive dashboard reporting.

---

## 1. Business Problem

A business needs a clear view of its sales performance to understand how revenue and profitability change over time and across business dimensions.

The analysis addresses questions such as:

- How much revenue and profit is the business generating?
- What are the cost of goods sold (COGS) and overall profit margin?
- How does profit vary by year, month, quarter, and day of the week?
- What proportion of profit is generated on weekdays compared with weekends?
- How can users explore performance for a selected country and reporting period?

**Project objective:** Prepare and model sales data, calculate key performance indicators, and build an interactive Excel dashboard that makes these performance patterns easier to explore.

## 2. About the Data

The workbook uses an Adventure Works sales dataset organised into a central sales fact table and supporting dimension tables.

### Data model tables

| Table | Role | Fields visible in the model |
|---|---|---|
| `FactInternetSales` | Fact table | ProductKey, OrderDateKey, DueDateKey, ShipDateKey, CustomerKey, SalesTerritoryKey, OrderQuantity, UnitPrice, Cost, OrderDate, Total Revenue, COGS, Total Profit |
| `DimProduct` | Dimension | ProductKey, Product Name, Color |
| `DimDate` | Dimension | Date, Year, Month Number, Month Name, Day Name, WeekTypes, Quarter, WeekNumber, and date hierarchy fields |
| `DimCustomer` | Dimension | CustomerKey, GeographyKey, CustomerAlternateKey, Full Name, BirthDate, Gender |
| `DimGeography` | Dimension | GeographyKey, City, Country, SalesTerritoryKey |
| `DimSalesTerritory` | Dimension | SalesTerritoryKey, SalesTerritoryAlternateKey, SalesTerritoryRegion, SalesTerritoryCountry, SalesTerritoryGroup |
| `All Measures` | Measures table | Central location for measures, including transaction and product-related measures |

### Data preparation with Power Query

The following operations were performed:

- Removed duplicate records where appropriate.
- Reviewed and handled null values.
- Corrected column data types.
- Merged queries using matching fields.
- Appended queries to combine rows.
- Created custom and conditional columns.
- Filtered records and columns.
- Grouped data for aggregation.

## 3. Data Modelling and Relationships

The prepared tables were loaded into **Power Pivot** and connected through key-based relationships. The supplied model diagram shows `FactInternetSales` as the central fact table, connected to product, date, customer, geography, and sales-territory data.

### Data model relationship diagram

![Adventure Works Power Pivot data model relationship diagram](./images/data-model-relationships.png)

> **If the image does not display:** confirm that the image file is uploaded to the repository at exactly `images/data-model-relationships.png`. GitHub paths are case-sensitive.

### Relationship overview

| Dimension table | Key shown | Related fact-table key | Cardinality shown |
|---|---|---|---|
| `DimProduct` | ProductKey | ProductKey | One-to-many (`1:*`) |
| `DimDate` | Date | Order-date relationship | One-to-many (`1:*`) |
| `DimCustomer` | CustomerKey | CustomerKey | One-to-many (`1:*`) |
| `DimGeography` | GeographyKey | Customer geography path shown in model | One-to-many (`1:*`) |
| `DimSalesTerritory` | SalesTerritoryKey | SalesTerritoryKey | One-to-many (`1:*`) |

The `All Measures` table is displayed separately; no relationship line is visible for it in the supplied diagram.

**Date relationship note:** `FactInternetSales` contains OrderDateKey, DueDateKey, and ShipDateKey. The supplied diagram does not show separate active relationship lines for all three date keys. Refer to the diagram when describing the exact relationship configuration.

## 4. Analysis Performed and Results

The dashboard combines financial KPIs with time-based and geographic views.

### 4.1 Overall business KPIs

The supplied dashboard screenshot displays:

| KPI | Dashboard value |
|---|---:|
| Total Quantity | 556 |
| Total COGS | $3.59M |
| Total Revenue | $6.05M |
| Total Profit | $2.46M |
| Profit Margin | 40.7% |
| Transactions | 0.27K |

Core calculations:

- **Profit** = Revenue − COGS
- **Profit Margin** = Profit ÷ Revenue × 100

### 4.2 Year-wise performance

The dashboard includes a year selector for 2005, 2006, 2007, and 2008, alongside a visual comparing average profit by year and a highlighted-year contribution indicator.

### 4.3 Monthly profit trend

The monthly line chart displays profit from January through December. In the supplied dashboard view, December, January, and August are selected, with a combined contribution of **37.2%**.

### 4.4 Weekday profit analysis

The weekday chart displays the following profit values in the supplied view:

| Weekday | Profit shown |
|---|---:|
| Sunday | $382.99K |
| Monday | $315.48K |
| Tuesday | $230.14K |
| Wednesday | $351.82K |
| Thursday | $356.03K |
| Friday | $526.18K |
| Saturday | $296.11K |

Friday has the largest displayed weekday profit. The highlighted weekdays are reported as contributing **51.5% of total profit** in this dashboard view.

### 4.5 Weekday vs. weekend contribution

The doughnut chart displays:

- **Weekday:** 72.4% of total profit (approximately $1.78M shown).
- **Weekend:** approximately $679.10K, representing the remaining contribution.

These values reflect the filter state shown in the dashboard screenshot.

### 4.6 Quarterly profit analysis

| Quarter | Profit shown | Contribution shown |
|---|---:|---:|
| Q1 | $690.73K | 28% |
| Q2 | $359.01K | 15% |
| Q3 | $668.28K | 27% |
| Q4 | $740.73K | 30% |

In the supplied view, Q4 has the highest quarterly profit and Q2 the lowest.

### 4.7 Geographic filtering

The dashboard provides country selection controls for Australia, Canada, France, Germany, the United Kingdom, and the United States. The supplied screenshot shows the United Kingdom selected.

## 5. Interactive Dashboard

![Adventure Works Sales Analysis Excel dashboard](./images/sales-analysis-dashboard.png)

The dashboard includes:

- KPI cards for quantity, COGS, revenue, profit, profit margin, and transactions.
- Year-wise performance comparison.
- Monthly profit trend.
- Weekday profit comparison.
- Weekday vs. weekend contribution.
- Quarterly profit cards.
- Country, month, and year selection controls.

## 6. Tools and Technical Skills

| Area | Skills demonstrated |
|---|---|
| Data preparation / ETL | Power Query: duplicate and null handling, data types, merge, append, custom columns, filtering, grouping |
| Data modelling | Power Pivot, table relationships, fact and dimension table concepts |
| Analysis | KPI calculations, revenue and cost analysis, profit and margin analysis, time-based aggregation |
| Excel | PivotTables, formulas, lookups, ranking logic, conditional calculations, interactive dashboard controls |
| DAX | Model-based KPI calculations and measures, alongside Excel formula calculations |
| Reporting | KPI cards, line chart, column chart, doughnut chart, quarterly summary cards, filters |

## 7. Limitations and Considerations

1. **Filter context matters.** KPI values and contribution percentages can change when year, month, or country selections change. Interpret results with the active filters in mind.
2. **Displayed figures require reconciliation.** Dashboard cards are rounded and may reflect a particular filter state. Reconcile them with the underlying PivotTables and Data Model using the same selections before presenting final results.
3. **No causal analysis.** The project identifies high- and low-performing periods but does not establish the operational or commercial reasons behind those differences.
4. **No forecasting or predictive modelling.** The analysis is descriptive.
5. **Limited customer and product deep dives in the dashboard.** Customer and product dimensions exist in the model, but the supplied dashboard focuses on financial KPIs, time trends, weekdays, quarters, and country filtering.
6. **Date-role coverage should be documented.** The fact table contains OrderDateKey, DueDateKey, and ShipDateKey, but the supplied diagram does not show separate active relationships for all three date keys.
7. **Source-data metadata is not shown in the supplied screenshots.** Add source provenance, row count, refresh date, and a full data dictionary if available.

## 8. How to View the Project

1. Download the Excel workbook from this repository, if it has been uploaded.
2. Open it in Microsoft Excel with Power Pivot / Data Model support.
3. Open the dashboard worksheet.
4. Use the year, month, and country controls to explore the report.
5. Review the model diagram and analysis worksheets for the underlying structure and calculations.

> The workbook must be uploaded separately for visitors to interact with the live Excel dashboard. The images in this README are static previews.

## 9. Repository Structure

Keep this exact structure when uploading to GitHub:

```text
Adventure-Works-Sales-Analysis/
│
├── README.md
│
└── images/
    ├── data-model-relationships.png
    └── sales-analysis-dashboard.png
```

## 10. Conclusion

This project demonstrates an Excel-based analytics workflow combining data preparation, relational data modelling, KPI calculations, and interactive reporting. Power Query was used to prepare the data, Power Pivot to establish table relationships, and Excel / DAX calculations to support the analysis.

The resulting report provides a consolidated view of sales and profitability across time periods and selected geographic markets, supporting business performance review and further investigation.

---

**Author:** Gokulraj J  
**Project:** Adventure Works Sales Analysis  
**Tools:** Microsoft Excel · Power Query · Power Pivot · DAX  
**Focus:** Sales Analytics · ETL · Data Cleaning · Data Modelling · KPI Analysis · Dashboard Reporting
