# Banking Operations & Portfolio Analytics

A Power BI portfolio project analyzing banking transaction activity, operational performance, customer behavior, and product utilization across a simulated financial institution.

The project combines **Power Query, DAX, dimensional data modeling, data validation, interactive reporting, and mobile report design** across:

- **250,000 transactions**
- **15,000 accounts**
- **10,000 customers**
- **20 branches**
- **$411.22M in transaction volume**

> **Power BI Report:** The complete `.pbix` file is included in this repository for review in Power BI Desktop.

---

## Project Overview

This project was built to demonstrate an end-to-end business intelligence workflow rather than simply create dashboard visuals.

The work included:

- Data profiling and validation
- Data cleaning with Power Query
- Relationship and dimensional model design
- DAX measure development
- KPI creation
- Operational and exception analysis
- Interactive filtering and cross-filter validation
- Desktop dashboard design
- Mobile-optimized report layouts
- Investigation of ambiguous and incomplete source data

The final report contains three analytical pages designed for different levels of investigation, with dedicated desktop and mobile layouts.

---

## Report Pages

### 1. Executive Overview

Provides a high-level view of transaction activity and operational performance.

**Key metrics:**

- **250,000 total transactions**
- **$411.22M total transaction volume**
- **$1.64K average transaction amount**
- **1.25% overall transaction failure rate**

**Analysis includes:**

- Transaction volume and failure rate over time
- Top branches by transaction count
- Transaction activity by source system
- Failed, returned, pending, and manual-review transactions

Interactive filters allow analysis by branch, transaction type, and month.

---

### 2. Transaction & Operations Analysis

Focuses on operational performance and transaction exceptions.

**Analysis includes:**

- Failure rate by branch
- Failure rate by transaction type
- Exception reasons by transaction outcome
- Average processing time by transaction status
- Branch, date, and transaction-type filtering

One notable finding was that **Pending and Manual Review transactions averaged approximately 123 seconds of processing time compared with roughly 16 seconds for Failed, Returned, and Completed transactions**.

The report also identified a **February 2026 increase in failure rate to approximately 2.7%**, substantially above the overall 1.25% baseline.

---

### 3. Customer, Account & Product Analysis

Examines the institution's customer and account portfolio.

**Key metrics:**

- **10,000 customers**
- **15,000 accounts**
- **13,779 active accounts**
- **1.50 accounts per customer**

**Analysis includes:**

- Accounts by banking product
- Customers by risk tier
- Customers by segment
- Customers by preferred banking channel

Interactive filters support segmentation by customer segment, risk tier, and preferred channel.

---

## Mobile-Optimized Report Design

All three report pages include dedicated **mobile-optimized Power BI layouts** in addition to their desktop layouts.

Rather than duplicating the analytical model, the mobile experience reorganizes the existing filters, KPIs, and visualizations for phone-sized viewing while retaining the same underlying DAX measures, relationships, and filter behavior.

### Executive Overview — Mobile

The mobile layout prioritizes:

1. Report title and page context
2. Branch, transaction type, and month filters
3. Four primary KPI cards
4. Monthly transaction and failure-rate trend
5. Transaction exceptions
6. Top branches
7. Transaction activity by source system

### Transaction & Operations Analysis — Mobile

The operational mobile layout prioritizes:

1. Date, branch, and transaction-type filters
2. Failure rate by branch
3. Failure rate by transaction type
4. Transaction exceptions by failure reason and status
5. Processing time by transaction status

### Customer, Account & Product Analysis — Mobile

The customer and portfolio mobile layout prioritizes:

1. Customer segment, risk tier, and preferred-channel filters
2. Customer and account KPI cards
3. Accounts by product
4. Customers by risk tier
5. Customers by segment
6. Customers by preferred channel

The mobile layouts were manually arranged and reviewed for phone-sized presentation rather than relying solely on automatically generated layouts.

---

## Data Preparation & Quality Assurance

Data quality was treated as part of the analysis rather than simply as a preprocessing step.

### Duplicate Investigation

Duplicate transaction IDs were investigated to determine whether they represented conflicting records or exact duplicate records.

The investigation identified **25 exact duplicate transaction pairs**. Exact duplicate rows were removed, and the cleaned model's validated analytical baseline contains **250,000 unique Transaction IDs**.

### Categorical Data Standardization

Transaction attributes were reviewed and normalized to eliminate inconsistent capitalization and categorical values.

Final transaction statuses were standardized to:

- Completed
- Failed
- Manual Review
- Pending
- Returned

Source-system values were standardized to:

- Digital Banking
- Core
- Mobile
- Treasury Portal

### Relationship Validation

Transactions were reconciled against account-level branch assignments.

A Power Query validation confirmed:

**250,000 / 250,000 transactions matched their account-assigned branch.**

This allowed a redundant direct relationship between Branches and Transactions to be removed, reducing ambiguity in the model.

### Exception Data Investigation

Failure-reason data was reconciled against transaction status.

The analysis identified:

- **3,114 failed transactions**
- **2,294 returned transactions**
- **58 failed transactions with no recorded failure reason**
- One completed transaction containing an `Insufficient Funds` failure-reason value

Rather than fabricating corrections for ambiguous source records, the original information was preserved when there was insufficient evidence to determine the correct business interpretation.

This reflects a deliberate analytical principle used throughout the project: **investigate anomalies, but do not manufacture data to make the dataset appear cleaner than the available evidence supports.**

---

## Data Model

The report uses a dimensional model connecting:

- Customers
- Accounts
- Products
- Branches
- Transactions
- Transaction Types
- Date

Accounts serve as the intermediate connection between customer/account attributes and transaction activity.

The final model uses the following primary relationships:

- Products → Accounts
- Customers → Accounts
- Branches → Accounts
- Accounts → Transactions
- Transaction Types → Transactions
- Date → Transactions

Relationships were configured as **one-to-many, single-direction relationships** to maintain predictable filter behavior.

A redundant direct relationship between Branches and Transactions was removed after branch-level reconciliation demonstrated that transaction branch assignments matched their associated accounts.

---

## Date Dimension

A dedicated Date table supports chronological analysis and reporting.

The Date dimension includes:

- Date
- Year
- Month Number
- Month
- Month Short
- Year Month
- Quarter
- Day of Week
- Day of Week Number

Month and day names were explicitly sorted using their corresponding numeric fields to preserve chronological order in report visuals.

The analytical date range extends from **January 1, 2024 through August 31, 2026**.

---

## DAX & Analytical Measures

Measures developed for the project include:

- Total Transactions
- Total Transaction Amount
- Average Transaction Amount
- Completed Transactions
- Failed Transactions
- Failure Rate
- Average Processing Seconds
- Total Customers
- Total Accounts
- Active Accounts
- Accounts per Customer

Example failure-rate measure:

```DAX
Failure Rate =
DIVIDE(
    [Failed Transactions],
    [Total Transactions],
    0
)
```

Using `DIVIDE()` provides explicit handling of zero-denominator scenarios.

Measures were tested under increasingly narrow filter contexts to verify that calculations responded correctly to combinations of report filters.

---

## Interactive Report Validation

Report interactions were tested using combinations of branch, transaction type, date, customer segment, risk tier, and preferred-channel filters.

Testing included narrow intersections designed to verify that:

- KPI measures recalculated correctly
- Charts responded to filter context
- Relationships propagated filters as intended
- Exception counts reconciled with underlying records
- Customer and account measures remained internally consistent

For example, filtering the operational report to **Wichita + ACH Debit + February 2026** produced a narrow 66-transaction population with a **7.58% failure rate**, demonstrating that measures continued to recalculate correctly under highly specific filter contexts.

---

## Key Findings

The analysis surfaced several operational patterns:

- Overall transaction failure rate was **1.25%**.
- February 2026 showed an unusual failure-rate increase to approximately **2.7%**.
- Branch failure rates ranged from approximately **1.03% to 1.42%**.
- Transaction-type failure rates ranged from approximately **0.93% to 1.37%**.
- Pending and Manual Review transactions were associated with approximately **8x longer processing times** than Completed, Failed, and Returned transactions.
- Digital Banking represented the largest transaction source, followed by Core, Mobile, and Treasury Portal.
- Consumer Checking represented the largest account product in the portfolio.
- The customer portfolio was primarily Consumer segment, with Small Business and Commercial customers comprising smaller portions of the population.
- Digital was the most common preferred customer banking channel.

These findings are presented as **analytical observations rather than causal conclusions**. The available dataset supports identifying patterns and anomalies but does not necessarily contain sufficient process history to establish why those patterns occurred.

---

## Tools & Skills Demonstrated

### Business Intelligence

- Power BI Desktop
- Interactive Dashboard Design
- KPI Development
- Mobile Report Design
- Desktop and Mobile-Optimized Layouts

### Data Preparation

- Power Query
- Data Profiling
- Data Cleaning
- Data Transformation
- Data Validation
- Data Reconciliation

### Analytics

- DAX
- Filter Context
- Operational Analysis
- Exception Analysis
- Trend Analysis
- Data Quality Investigation

### Data Modeling

- Dimensional Modeling
- Relationship Design
- Date Dimensions
- One-to-Many Relationships
- Single-Direction Filtering

### Domain

- Banking Operations
- Transaction Processing
- Customer & Account Analysis
- Financial Data Validation
- Operational Exception Analysis

---

## Project Purpose

I created this project to extend my professional background in **financial technology, banking data conversion, SQL validation, and production implementation** into business intelligence and data analytics.

My professional experience has included financial-institution data conversions, source-to-target validation, reconciliation, banking systems, and production implementations. This project applies that experience to a modern BI workflow using **Power BI, Power Query, dimensional modeling, DAX, interactive analytics, and mobile report design**.

The goal was not simply to build a visually complete dashboard, but to demonstrate the process behind a defensible analytical product:

**Profile → Clean → Validate → Model → Calculate → Analyze → Visualize → Test**

---

## Repository Contents

### `Banking Operations Analytics with Mobile.pbix`

Complete Power BI Desktop project containing:

- Power Query transformations
- Data model and relationships
- Date dimension
- DAX measures
- Three desktop report pages
- Interactive slicers and cross-filtering
- Three dedicated mobile report layouts

### Report Screenshots

Desktop, mobile, and data-model screenshots will be included in this repository to allow the project to be reviewed without requiring Power BI Desktop.

---

## Report Preview

Screenshots of the completed report will be added here, including:

- Executive Overview — Desktop
- Transaction & Operations Analysis — Desktop
- Customer, Account & Product Analysis — Desktop
- Executive Overview — Mobile
- Transaction & Operations Analysis — Mobile
- Customer, Account & Product Analysis — Mobile
- Power BI Data Model

---

## About This Portfolio Project

This project uses simulated banking data for portfolio and demonstration purposes.

It was developed as an independent Power BI project to demonstrate practical skills in **business intelligence, financial data analysis, data quality, dimensional modeling, DAX, Power Query, dashboard development, analytical validation, and mobile report design**.
