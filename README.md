# Sales Analytics Power BI Project

## Overview
This project contains a Power BI dashboard built to monitor sales performance, profitability, customer value, and fulfillment efficiency from 2017 to 2019.

The dashboard answers three business questions:
- How much are we selling, and how profitable is that growth?
- Which products, customers, and channels contribute most to profit?
- Where are operational bottlenecks increasing delivery time?

## Dashboard Highlights (From the Current View)
Based on the dashboard snapshot:
- Total Sales: `$155M`
- Total Profit: `$58M`
- Profit Margin: `37.4%`
- Total Orders: `8K`
- Avg Fulfillment Time: `10.4 days`

These top-line KPIs show strong margin performance while still leaving room to improve delivery speed.

## Business Insights From the Dashboard

### 1. Revenue Growth Is Profitable
The KPI cards indicate that the business is generating both high revenue (`$155M`) and strong profit (`$58M`).

Insight:
- Profitability is healthy at `37.4%`, suggesting pricing and cost structure are currently effective.

### 2. Channel Mix Is Concentrated
The donut chart `Total Sales by Channel` shows the following split:
- Wholesale: about `$83M` (`53.67%`)
- Distributor: about `$49M` (`31.68%`)
- Export: about `$23M` (`14.64%`)

Insight:
- More than half of sales come from Wholesale, so channel concentration risk exists.
- Export is the smallest share and may represent a growth opportunity.

### 3. Product-Level Profit Is Uneven
The bar chart `Total Profit by Product Name` ranks products by profitability, with a clear spread between top and lower performers.

Insight:
- Top products should be protected (inventory, promotions, account focus).
- Lower-profit products should be reviewed for pricing, discounting, or cost optimization.

### 4. Customer Portfolio Has Clear High-Value Accounts
The customer table highlights major contributors, including names like `Medline`, `Pure Group`, and `OUR Ltd`.

Insight:
- High-value customers can be prioritized for retention and upsell plans.
- Combining `Total Orders`, `Total Sales`, and `Total Profit` helps identify accounts with volume but weak margin.

### 5. Fulfillment Performance Varies by Warehouse
The column chart `Avg Fulfillment Time by Warehouse Code` shows warehouses clustered around roughly `10` to `11` days.

Insight:
- Small differences across warehouse locations can still impact service-level agreements and customer satisfaction.
- Slowest warehouse codes should be targeted first for process improvement.

### 6. Sales Volatility Across Time and Currency
Time-series visuals (`Total Sales by OrderDate` and `Total Sales by OrderDate and Currency Code`) show frequent fluctuations across the period.

Insight:
- Demand varies significantly over time, so forecasting and inventory planning should account for volatility.
- Currency segmentation helps separate growth from true volume change versus market/currency effects.

## Filters Available in the Report
The dashboard includes slicers for:
- `OrderDate` (visible range starts from `01-01-2017`)
- `Channel` (`Distributor`, `Export`, `Wholesale`)
- `Currency Code` (`AUD`, `EUR`, `GBP`, `NZD`, `USD`)

These slicers allow business users to move from executive-level KPIs to specific segments quickly.

## KPI Logic (DAX Measures)
Measures are defined in `sales.SemanticModel/definition/tables/Sales Orders.tmdl`:
- `Total Sales = SUM('Sales Orders'[Total Revenue])`
- `Total Cost = SUMX('Sales Orders', 'Sales Orders'[Order Quantity] * 'Sales Orders'[Total Unit Cost])`
- `Total Profit = [Total Sales] - [Total Cost]`
- `Profit Margin % = DIVIDE([Total Profit], [Total Sales], 0)`
- `Total Orders = DISTINCTCOUNT('Sales Orders'[OrderNumber])`
- `Avg Fulfillment Time = AVERAGEX('Sales Orders', DATEDIFF('Sales Orders'[OrderDate], 'Sales Orders'[Ship Date], DAY))`

## Repository Contents
- `sales.pbip`: Power BI project entry file
- `sales.Report/`: report pages and visual definitions
- `sales.SemanticModel/`: semantic model, tables, relationships, and measures

## How to Open
1. Open `sales.pbip` in Power BI Desktop (PBIP-compatible version).
2. Refresh the model if local data source paths differ.
3. Use slicers to analyze performance by date, channel, and currency.
4. Use product, customer, and warehouse visuals to convert insights into actions.
