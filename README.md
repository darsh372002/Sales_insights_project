# 📊 Sales Insights Data Analysis Project
## 📌 Project Overview
This project is a complete end‑to‑end **Sales Insights Data Analysis** case study built for a computer hardware business operating in a highly competitive and dynamically changing market. The sales director wants a **Power BI dashboard** that provides real‑time insights into revenue, profit margins, customer performance, and product trends.

This project covers:
* Data extraction using SQL
* Data cleaning and transformation with Power Query
* Data modelling
* DAX measures for insights
* Interactive Power BI dashboards
 -------------------------------------------
## 🗂️ Project Components
### 1️⃣ **Database Setup (MySQL)**

* Import the provided `db_dump.sql` file into MySQL.
* Dataset contains: Customers, Sales Transactions, Products, Markets, Date Dimension.
---
## 🧮 Key SQL Queries Used
### ✔ Show all customer records
```
SELECT * FROM customers;
```
### ✔ Total number of customers
```
SELECT COUNT(*) FROM customers;
```
### ✔ Transactions for Chennai market (Mark001)
```
SELECT * FROM transactions WHERE market_code = 'Mark001';
```
### ✔ Distinct product codes sold in Chennai
```
SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
```
### ✔ Transactions in USD
```
SELECT * FROM transactions WHERE currency = 'USD';
```
### ✔ Year 2020 transactions using date table
```
SELECT t.*, d.*
FROM transactions t
INNER JOIN date d ON t.order_date = d.date
WHERE d.year = 2020;
```
### ✔ Total revenue in 2020
```
SELECT SUM(t.sales_amount)
FROM transactions t
INNER JOIN date d ON t.order_date = d.date
WHERE d.year = 2020
  AND (t.currency = 'INR' OR t.currency = 'USD');
```
---
## 🔧 Power Query Transformations
### ✔ Normalizing currency column (INR/USD)
```
= Table.AddColumn(#"Filtered Rows", "norm_amount", each
    if [currency] = "USD" or [currency] = "USD#(cr)"
    then [sales_amount] * 75
    else [sales_amount], type any)
```
This ensures all sales amounts are converted to one currency for consistent reporting.
---
## 📐 DAX Measures Used in Power BI

### ✔ Revenue
```
Revenue = SUM('Sales transactions'[norm_sales_amount])
```
### ✔ Sales Quantity
```
Sales Qty = SUM('sales transactions'[sales_qty])
```
### ✔ Total Profit Margin
```
Total Profit Margin = SUM('Sales transactions'[Profit_Margin])
```
### ✔ Profit Margin %
```
Profit Margin % = DIVIDE([Total Profit Margin], [Revenue], 0)
```
### ✔ Profit Margin Contribution %
```
Profit Margin Contribution % = DIVIDE(
    [Total Profit Margin],
    CALCULATE([Total Profit Margin], ALL('sales products'), ALL('sales customers'), ALL('sales markets'))
)
```
### ✔ Revenue Contribution %
```
Revenue Contribution % = DIVIDE(
    [Revenue],
    CALCULATE([Revenue], ALL('sales products'), ALL('sales customers'), ALL('sales markets'))
)
```
### ✔ Revenue Last Year
```
Revenue LY = CALCULATE([Revenue], SAMEPERIODLASTYEAR('sales date'[date]))
```
---
## 📊 Power BI Dashboard
The dashboard provides insights on:
* Revenue trends (MoM / YoY)
* Customer segmentation
* Market performance
* Product‑wise contribution
* Profit margin behaviour
---

## 📁 Files Included
* `db_dump.sql` → MySQL database dump
* `Sales_insights_project1.pbix` → Power BI Report
* `README.md` → Documentation
---
## 🚀 Conclusion
This project replicates how real‑world sales analytics is implemented in organizations. It is an excellent hands‑on practice for aspiring **Data Analysts**, **BI Developers**, and **Data Enthusiasts**.
If you like this project, feel free to ⭐ the repository!
---
�
