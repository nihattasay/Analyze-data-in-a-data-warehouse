# Analyze-data-in-a-data-warehouse
# Microsoft Fabric: Analyze Data in a Data Warehouse

This repository provides a step-by-step walkthrough for analyzing data in a data warehouse using Microsoft Fabric. It follows the official Microsoft Learn module and includes instructions for creating, modeling, querying, and visualizing data.

## 🏗️ Project Overview

This lab demonstrates how to:

- Create a Microsoft Fabric workspace
- Set up a Synapse Data Warehouse
- Define and populate tables with sample data
- Build a relational data model
- Write SQL queries to analyze data
- Create views for reusable queries
- Use visual query tools for no-code data exploration
- Build a basic Power BI report from warehouse data

## 📂 Table of Contents

- [Setup Requirements](#setup-requirements)
- [Steps](#steps)
- [Schema Overview](#schema-overview)
- [Query Examples](#query-examples)
- [Report Visualization](#report-visualization)

## ⚙️ Setup Requirements

- Microsoft Fabric license (Trial, Premium, or Fabric capacity)
- Access to [https://app.fabric.microsoft.com](https://app.fabric.microsoft.com)

## 🚀 Steps

1. **Create a Workspace**  
   Fabric-enabled workspace for hosting your warehouse and reports.

2. **Create a Data Warehouse**  
   Use the Synapse Warehouse option to create a full-featured SQL-based relational data warehouse.

3. **Create Tables and Load Data**  
   Use `CREATE TABLE` and `INSERT INTO` SQL commands to define dimension and fact tables:
   - `DimCustomer`
   - `DimDate`
   - `DimProduct`
   - `FactSalesOrder`

4. **Define Relationships**  
   Build a star schema by connecting dimension tables to the fact table using:
   - ProductKey
   - CustomerKey
   - SalesOrderDateKey

5. **Query with SQL**  
   Use joins and aggregations to analyze sales across time and region.

6. **Create a View**  
   Encapsulate common queries using SQL views, e.g. `vSalesByRegion`.

7. **Visual Query (No-Code)**  
   Use drag-and-drop visual query builder to merge, filter, and preview data.

8. **Build a Report**  
   Use Power BI in Fabric to visualize sales data. Example: total sales by product category.

## 🗃️ Schema Overview

FactSalesOrder
├── SalesTotal
├── SalesOrderDateKey ──┬── DimDate
├── ProductKey ─────────┴── DimProduct
└── CustomerKey ────────┬── DimCustomer


## 🔍 Query Examples

```sql
SELECT d.[Year], d.MonthName, c.CountryRegion, SUM(so.SalesTotal) AS SalesRevenue
FROM FactSalesOrder AS so
JOIN DimDate AS d ON so.SalesOrderDateKey = d.DateKey
JOIN DimCustomer AS c ON so.CustomerKey = c.CustomerKey
GROUP BY d.[Year], d.MonthName, c.CountryRegion;

📊 Report Visualization

Create a Power BI report in Fabric with:

    A clustered bar chart

    SalesTotal as value

    Category from DimProduct as axis

    Title: "Total Sales by Category"

🧹 Clean Up

Delete the workspace to remove all resources once finished.
