# Banking Operations & Portfolio Analytics

## About This Project

This is an independent Power BI portfolio project built to demonstrate an end-to-end business intelligence workflow using simulated banking data.

I created the project to extend my professional background in **financial technology, banking data conversion, SQL validation, reconciliation, and production implementation** into business intelligence and data analytics.

My professional experience has included financial-institution data conversions, source-to-target validation, banking systems, financial data reconciliation, and production implementations. This project applies that experience to a modern BI workflow using **Power BI, Power Query, dimensional modeling, DAX, interactive analytics, and mobile report design**.

The objective was not simply to build dashboards, but to demonstrate the process behind a defensible analytical product:

**Profile → Clean → Validate → Model → Calculate → Analyze → Visualize → Test**

> **Power BI Report:** The complete `.pbix` file is included in this repository for technical review in Power BI Desktop.

---

## Contents

- [Project at a Glance](#project-at-a-glance)
- [Report Preview](#report-preview)
- [Report Pages](#report-pages)
- [Key Findings](#key-findings)
- [Mobile-Optimized Report Design](#mobile-optimized-report-design)
- [Data Preparation & Quality Assurance](#data-preparation--quality-assurance)
- [Data Model](#data-model)
- [Date Dimension](#date-dimension)
- [DAX & Analytical Measures](#dax--analytical-measures)
- [Interactive Report Validation](#interactive-report-validation)
- [Tools & Skills Demonstrated](#tools--skills-demonstrated)
- [Repository Contents](#repository-contents)
- [Data Disclaimer](#data-disclaimer)

---

## Project at a Glance

The analytical model contains:

- **250,000 transactions**
- **15,000 accounts**
- **10,000 customers**
- **20 branches**
- **$411.22M in transaction volume**
- **January 2024 – August 2026** reporting period
- **3 desktop report pages**
- **3 mobile-optimized report layouts**

The project demonstrates:

- Power Query data preparation
- Data profiling and validation
- Dimensional data modeling
- DAX measure development
- KPI development
- Operational and exception analysis
- Interactive filtering
- Cross-filter validation
- Desktop dashboard design
- Mobile-optimized Power BI design
- Investigation of ambiguous and incomplete source data

---

## Report Preview

### Executive Overview

<img width="1297" height="1654" alt="image" src="https://github.com/user-attachments/assets/c857ec20-130f-4849-b699-1958e478a2b4" />

High-level monitoring of transaction activity, transaction volume, failure rates, branch activity, source systems, and operational exceptions.

---

### Transaction & Operations Analysis

<img width="1282" height="1660" alt="image" src="https://github.com/user-attachments/assets/23a5be99-cbed-43db-8730-78108bce95b4" />

Operational analysis of branch and transaction-type failure rates, exception reasons, and processing performance.

---

### Customer, Account & Product Analysis

<img width="1270" height="1342" alt="image" src="https://github.com/user-attachments/assets/8fe5de72-3892-4483-8923-265e07427ab7" />

Portfolio analysis covering customers, accounts, banking products, customer segments, risk tiers, and preferred banking channels.

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

Interactive filters allow analysis by:

- Branch
- Transaction Type
- Year Month

---

### 2. Transaction & Operations Analysis

Focuses on operational performance and transaction exceptions.

**Analysis includes:**

- Failure rate by branch
- Failure rate by transaction type
- Exception reasons by transaction outcome
- Average processing time by transaction status
- Branch, date, and transaction-type filtering

Pending and Manual Review transactions averaged approximately **123 seconds of processing time**, compared with roughly **16 seconds** for Failed, Returned, and Completed transactions.

The report also identified a **February 2026 failure-rate increase to approximately 2.7%**, compared with the overall 1.25% baseline.

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

Interactive filters support segmentation by:

- Customer Segment
- Risk Tier
- Preferred Channel

---

## Key Findings

The analysis surfaced several operational and portfolio patterns:

- Overall transaction failure rate was **1.25%**.
- February 2026 showed an unusual failure-rate increase to approximately **2.7%**.
- Branch failure rates ranged from approximately **1.03% to 1.42%**.
- Transaction-type failure rates ranged from approximately **0.93% to 1.37%**.
- Pending and Manual Review transactions were associated with approximately **8x longer processing times** than Completed, Failed, and Returned transactions.
- Digital Banking represented the largest transaction source, followed by Core, Mobile, and Treasury Portal.
- Consumer Checking represented the largest account product.
- The customer portfolio was primarily Consumer segment, followed by Small Business and Commercial.
- Digital was the most common preferred customer banking channel.

These findings are presented as **analytical observations rather than causal conclusions**. The available data supports identifying patterns and anomalies but does not necessarily contain sufficient process history to establish why those patterns occurred.

---

## Mobile-Optimized Report Design

All three report pages include dedicated **mobile-optimized Power BI layouts** in addition to their desktop layouts.

Rather than duplicating the analytical model, the mobile experience reorganizes existing filters, KPIs, and visualizations for phone-sized viewing while retaining the same underlying DAX measures, relationships, and filter behavior.

### Executive Overview — Mobile

The mobile layout prioritizes:

1. Report title and page context
2. Branch, transaction type, and month filters
3. Primary KPI cards
4. Monthly transaction and failure-rate trend
5. Transaction exceptions
6. Top branches
7. Transaction activity by source system

<img width="580" height="1047" alt="image" src="https://github.com/user-attachments/assets/b92d15af-4b4b-4ef6-ac24-8398964a65f7" />

---

### Transaction & Operations Analysis — Mobile

The operational mobile layout prioritizes:

1. Date, branch, and transaction-type filters
2. Failure rate by branch
3. Failure rate by transaction type
4. Transaction exceptions by failure reason and status
5. Processing time by transaction status

<img width="562" height="1057" alt="image" src="https://github.com/user-attachments/assets/1f72909c-5da2-4417-bded-f4910844500c" />

---

### Customer, Account & Product Analysis — Mobile

The customer and portfolio mobile layout prioritizes:

1. Customer segment, risk tier, and preferred-channel filters
2. Customer and account KPI cards
3. Accounts by product
4. Customers by risk tier
5. Customers by segment
6. Customers by preferred channel

<img width="610" height="1087" alt="image" src="https://github.com/user-attachments/assets/24249bd5-a6a5-44b5-b856-eb2b7cf04851" />

The mobile layouts were **manually arranged and reviewed for phone-sized presentation** rather than relying solely on automatically generated layouts.

---

## Data Preparation & Quality Assurance

Data quality was treated as part of the analysis rather than simply as a preprocessing step.

### Duplicate Investigation

Duplicate Transaction IDs were investigated to determine whether they represented conflicting records or exact duplicate records.

The investigation identified **25 exact duplicate transaction pairs**. Exact duplicate rows were removed, and the cleaned analytical model was validated at **250,000 unique Transaction IDs**.

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

Power Query validation confirmed:

**250,000 / 250,000 transactions matched their account-assigned branch.**

This validation allowed a redundant direct relationship between Branches and Transactions to be removed, reducing ambiguity in the model.

### Exception Data Investigation

Failure-reason data was reconciled against transaction status.

The investigation identified:

- **3,114 failed transactions**
- **2,294 returned transactions**
- **58 failed transactions with no recorded failure reason**
- One completed transaction containing an `Insufficient Funds` failure-reason value

Rather than fabricating corrections for ambiguous source records, the original information was preserved when there was insufficient evidence to determine the appropriate business interpretation.

This reflects an analytical principle used throughout the project:

**Investigate anomalies, but do not manufacture data to make the dataset appear cleaner than the available evidence supports.**

---

## Data Model

<img width="1572" height="1713" alt="image" src="https://github.com/user-attachments/assets/327cb3c4-c8ad-4d9d-8c25-2256a8b51587" />


The report uses a dimensional model connecting:

- Customers
- Accounts
- Products
- Branches
- Transactions
- Transaction Types
- Date

Accounts serve as the intermediate connection between customer/account attributes and transaction activity.

The primary model relationships are:

- Products → Accounts
- Customers → Accounts
- Branches → Accounts
- Accounts → Transactions
- Transaction Types → Transactions
- Date → Transactions

Relationships use **one-to-many, single-direction filtering** to maintain predictable filter behavior.

A redundant direct relationship between Branches and Transactions was removed after reconciliation demonstrated that transaction branch assignments matched their associated accounts.

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

Example:

```DAX
Failure Rate =
DIVIDE(
    [Failed Transactions],
    [Total Transactions],
    0
)
```

`DIVIDE()` provides explicit handling of zero-denominator scenarios.

Measures were tested under increasingly narrow filter contexts to verify that calculations responded correctly to report interactions.

---

## Interactive Report Validation

Report interactions were tested using combinations of:

- Branch
- Transaction Type
- Date
- Customer Segment
- Risk Tier
- Preferred Channel

Testing verified that:

- KPI measures recalculated correctly
- Charts responded to filter context
- Relationships propagated filters as intended
- Exception counts reconciled with underlying records
- Customer and account measures remained internally consistent

For example, filtering the operational report to **Wichita + ACH Debit + February 2026** produced a narrow population of **66 transactions with a 7.58% failure rate**, demonstrating that measures continued to recalculate correctly under highly specific filter contexts.

---

## Tools & Skills Demonstrated

### Business Intelligence

- Power BI Desktop
- Interactive Dashboard Design
- KPI Development
- Desktop Report Design
- Mobile Report Design
- Mobile-Optimized Layouts

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

### Banking & Financial Data

- Banking Operations
- Transaction Processing
- Customer & Account Analysis
- Financial Data Validation
- Operational Exception Analysis

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

### Screenshots

This repository is designed to include:

- Executive Overview — Desktop
- Transaction & Operations Analysis — Desktop
- Customer, Account & Product Analysis — Desktop
- Executive Overview — Mobile
- Transaction & Operations Analysis — Mobile
- Customer, Account & Product Analysis — Mobile
- Power BI Data Model

---

## Data Disclaimer

This project uses **simulated banking data** for portfolio and demonstration purposes.

It does **not** contain real customer data, proprietary financial-institution data, or confidential employer data.
