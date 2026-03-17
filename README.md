# Invoice Automation Analytics for Accounts Payable

**Author:** Yashpal Saini

## Overview

This project showcases an **invoice operations analytics solution** built to improve visibility into supplier spending, invoice activity, discount capture, and cost behavior across vendors, products, categories, locations, and time. It is designed for **Accounts Payable, Finance Operations, Procurement, and Business Analytics** teams that need a structured way to monitor invoice data and identify opportunities for stronger cost control, process standardization, and faster decision-making.

The current repository contains:
- a **Power BI report export** (`PowerBi invoice.pdf`) that presents the analytics layer
- an **Excel-based source dataset** (`Database.xlsx`) containing invoice header and invoice line-item data

This project demonstrates the **data and reporting foundation** of an invoice automation workflow. While the repository is centered on the analytics layer, the model is well suited for extension into an approval and exception-handling workflow using **Power Automate, SharePoint, or Power Apps**.

---

## Business Problem

Manual invoice tracking often creates avoidable friction across finance operations:
- limited visibility into total spend by supplier and category
- weak monitoring of discounts and payment timing
- difficulty identifying high-cost vendors and recurring purchasing patterns
- fragmented invoice records across header-level and line-level data
- slow manager reporting and ad hoc analysis

Without a centralized reporting layer, finance teams spend too much time compiling operational updates and too little time analyzing spend behavior, supplier concentration, and process inefficiencies.

---

## Project Objectives

This solution was built to:
- centralize invoice and supplier data into a clean reporting model
- monitor **total spend**, **discounts**, and **supplier concentration**
- analyze invoices by **date**, **vendor**, **product**, **category**, and **location**
- support finance teams with interactive reporting for operational reviews
- provide a scalable analytics base that can be extended into a broader invoice automation workflow

---

## Solution Summary

The project combines structured invoice data with a Power BI reporting layer to create a clear view of accounts payable activity.

### Core capabilities
- spend monitoring across time periods
- supplier analysis by total invoice value
- product and category breakdowns
- discount tracking
- geographic analysis by location
- trend analysis for monthly spend and discount behavior

### Current dashboard highlights
Based on the report export included in the repository, the solution surfaces key operational metrics such as:
- **Total spend:** approximately **147.48K**
- **Total discount:** approximately **620.25**
- **Active suppliers:** **9**
- top suppliers by total cost contribution
- top products and categories by value
- time-series view of costs and discounts

---

## Repository Structure

```text
InvoiceAutomation-main/
├── Database.xlsx             # Source data containing invoice header and invoice line-item tables
├── PowerBi invoice.pdf       # Exported view of the Power BI dashboard
└── README.md                 # Project documentation
```

---

## Data Sources

### 1. Invoice Header Data
The first worksheet contains invoice-level records, including fields such as:
- supplier name
- invoice number
- invoice date
- payment date
- net amount
- tax amount
- total amount
- location
- discount
- confidence / precision score

This table acts as the **invoice header fact source** for tracking invoice totals, payment timing, and vendor-level spend.

### 2. Invoice Line-Item Data
The second worksheet contains item-level transaction detail, including:
- supplier name
- invoice number
- product code
- product description
- category
- quantity
- unit
- unit value
- line amount
- confidence / precision score

This table enables detailed analysis of **what was purchased**, at what quantity, and in which cost category.

---

## Data Model

The project is structured around a **header-detail invoice model**:

- **Invoice Header Table** stores supplier, invoice, payment, and monetary totals
- **Invoice Line Table** stores product-level breakdowns for each invoice
- **Shared Key:** invoice number (`NFatura` / `Nfatura`)

### Recommended modeling approach in Power BI
- create a relationship between invoice header and invoice line-item tables using invoice number
- standardize date fields for proper time intelligence
- normalize numeric formats for currency analysis
- trim supplier and category text fields to avoid duplicate categories caused by spacing inconsistencies
- create DAX measures for spend, discounts, supplier count, and monthly trends

---

## Key Metrics and KPI Logic

This project is built to answer the finance questions that matter most in invoice operations.

### Example KPIs
- **Total Spend** = sum of invoice total amount
- **Total Cost Excluding Tax** = sum of pre-tax invoice value
- **Total Discount** = sum of discount amount
- **Supplier Count** = distinct count of suppliers
- **Spend by Supplier** = total invoice value grouped by supplier
- **Spend by Category** = total line amount grouped by category
- **Monthly Spend Trend** = invoice total amount by year-month
- **Top Products by Value** = total line amount by product description

### Example DAX measures
```DAX
Total Spend = SUM('Invoice Header'[valor total ])

Total Cost Excl Tax = SUM('Invoice Header'[Valor_s_iva])

Total Discount = SUM('Invoice Header'[desconto ])

Supplier Count = DISTINCTCOUNT('Invoice Header'[Nome])

Total Tax = SUM('Invoice Header'[valor do iva])
```

These measures can be extended with time-intelligence logic for month-over-month analysis, rolling averages, supplier concentration, or discount utilization rates.

---

## Dashboard Use Cases

This solution is built for practical finance and operations reporting.

### Finance Operations
- monitor spend patterns across reporting periods
- identify high-cost suppliers and products
- compare pre-tax and total cost behavior
- review discounts captured over time

### Procurement and Vendor Management
- assess vendor concentration risk
- identify major categories driving purchasing volume
- evaluate which suppliers contribute the highest share of spend

### Management Reporting
- provide quick executive visibility into total cost, discount capture, and vendor mix
- support monthly operational reviews with interactive filters
- reduce manual reporting effort by centralizing invoice analytics

---

## Workflow Extension Opportunities

The repository currently focuses on the **analytics layer**, but it can be evolved into a broader invoice automation solution.

### Natural next-step architecture
- **Power Apps** for invoice submission or exception review
- **Power Automate** for approval routing, reminder notifications, and escalation logic
- **SharePoint / Dataverse** for process-state tracking
- **Power BI** for monitoring operational KPIs and exceptions

### Example automated workflow
1. invoice is received or uploaded
2. invoice metadata is captured and validated
3. approval routing is triggered based on supplier, amount, or category
4. exceptions are flagged for review
5. payment status is updated
6. Power BI dashboard reflects current activity and historical trends

This makes the project highly relevant for business analyst, finance systems, and operations reporting roles.

---

## Technical Skills Demonstrated

- **Power BI** dashboard development
- **Excel data modeling** and multi-table reporting
- **Invoice header-detail data design**
- **KPI and measure development using DAX**
- **Spend analysis and supplier analytics**
- **Business reporting for finance operations**
- **Data cleaning and field normalization**
- **Operational dashboard storytelling**

---

## Data Preparation Considerations

Before building the report, several data quality checks are recommended:
- standardize supplier names with trailing spaces removed
- convert mixed-format payment dates into consistent date types
- validate invoice number uniqueness at the header level
- verify tax and total values against line-item amounts where appropriate
- normalize category naming conventions
- review confidence or precision fields for potential data-quality scoring

These steps strengthen the accuracy and reliability of downstream reporting.

---

## How to Use the Project

### Option 1: Review the dashboard output
Open `PowerBi invoice.pdf` to review the exported Power BI dashboard and understand the reporting layout, KPIs, and analytical lens.

### Option 2: Rebuild or enhance the Power BI model
1. Open `Database.xlsx`
2. Load both worksheets into Power BI Desktop
3. Create the relationship between header and line-item tables using invoice number
4. Build DAX measures for spend, tax, discounts, and supplier count
5. Add slicers for date, supplier, and category
6. Publish or export the report for stakeholder review

### Option 3: Extend into a workflow solution
Use the existing data model as a foundation for a Power Platform solution that includes intake, approvals, exception handling, and SLA tracking.

---

## Suggested Enhancements

Future versions of this project could include:
- invoice aging analysis
- payment timeliness and overdue invoice tracking
- exception dashboards for mismatched totals or low-confidence records
- duplicate invoice detection logic
- supplier scorecards
- approval workflow monitoring
- row-level security for finance managers or business units
- integration with SharePoint, SQL, or Dataverse for production use

---

## Why This Project Matters

This project goes beyond a simple dashboard. It demonstrates how raw invoice data can be transformed into a structured **finance operations reporting asset** that supports better visibility, stronger process control, and smarter vendor oversight.

It is especially relevant for roles involving:
- business analysis
- finance operations
- procurement analytics
- process improvement
- Power BI reporting
- business systems and workflow design

---

## Resume-Ready Project Summary

Built a Power BI-based invoice analytics solution using structured Excel invoice header and line-item data to monitor supplier spend, discounts, product-level costs, and monthly trends, creating a scalable reporting foundation for accounts payable and invoice automation workflows.

---

## Author

**Yashpal Saini**  
Business Analytics | Data Analysis | Power BI | SQL | Process Improvement

If you are a recruiter, hiring manager, or collaborator reviewing this project, this work reflects my ability to translate operational business data into structured reporting systems that support decision-making, workflow visibility, and scalable process improvement.
