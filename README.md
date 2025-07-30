# Loan-Disbursement-Bank-Analysis-Dashboard

---

This repository contains a Power BI dashboard for analyzing loan data across disbursements, portfolio risk, and data quality. It is designed for financial institutions to track performance and take action based on insights.

---

## Data Model Overview

The data model follows a star schema consisting of:

### 1. **FactLoan**

Holds transactional data for each loan.

* `charge_amount`, `interest_amount_accrued`, `currency_code`, `fx_date`
* Disbursement and payment amounts in EUR and local currencies
* `DisbursementDateId` links to the **DimDate** table
* `loan_key` links to the **Dimension** table

### 2. **Dimension**

Contains master data for each loan.

* `loan_key`, `branch_key`, `loan_officer_user_code`
* `interest_planned_amount_eur`, `interest_planned_amount_lccy`
* `disbursement_dateid`, `modification_dateid`, `is_current`

### 3. **DimDate**

Standard calendar table with:

* `DateKey`, `Day`, `Day Name`, `Day of Week`, `Day of Year`

### Relationships:

* One-to-many from **DimDate** to **FactLoan** via `DisbursementDateId`
* One-to-many from **Dimension** to **FactLoan** via `loan_key`

---

## Dashboard Summary

The dashboard consists of multiple pages, each focusing on different aspects of the loan data:

---

### Loan Disbursement Overview

This page tracks loan disbursement amounts across the last six months.
**Key filters available:** Branch, Product Type, Loan Officer.

**Monthly Disbursement in EUR:**

* **September**: €1,09,287
* **October**: €28,223
* **November**: €36,666
* **December**: €25,337
* **January**: €20,275
* **February**: €42,528

These values represent disbursements for the respective months ending on **29 February 2020**.

---

### Portfolio At Risk (PAR)

This section monitors the loan risk based on overdue balances and aging.

**Key Performance Indicators (KPIs):**

* **Outstanding 30 days or more**: €52,294
* **Total Outstanding**: €3,56,150
* **PAR 30%**: 14.68%

**Loan Portfolio Breakdown:**

| Category       | Outstanding      | Outstanding 30+ Days | PAR 30%    |
| -------------- | ---------------- | -------------------- | ---------- |
| OUTST\_NO\_ARR | €45,174.65       | —                    | —          |
| OUTST\_PAR1    | €2,58,681.24     | —                    | —          |
| OUTST\_PAR30   | €44,743.91       | €44,744              | 12.56%     |
| OUTST\_PAR90   | €7,549.73        | €7,550               | 2.12%      |
| **Total**      | **€3,56,149.53** | **€52,294**          | **14.68%** |

Color coding is applied to PAR% to indicate high risk and acceptable levels.

---

### Invalid Loans

This section lists loans with missing or corrupted master data. These loans may not appear correctly in other reports and need correction.

**Summary:**

* **Total Invalid Loans**: 730
* **Total Principal Amount**: €24,44,165.31
* **Total Outstanding**: €11,63,037.62

**Details include:**

* Loan Number
* Principal Amount
* Start Date
* Outstanding Amount

---

## Tools and Technologies Used

* Power BI Desktop
* DAX (Data Analysis Expressions)
* Star Schema Data Modeling
* Relational Database (assumed as the backend)
* Calendar table integration

---

## Folder Structure

```
LoanDashboard/
├── PowerBI_Dashboard.pbix
├── screenshots/
│   ├── loan-disbursement.png
│   ├── kpi-par.png
│   └── invalid-loans.png
├── README.md
```

---

## How to Use

1. Open the `.pbix` file using Power BI Desktop.
2. Refresh the data from your source system.
3. Apply filters (Branch, Product, Officer) to explore the reports.
4. Review KPIs and take appropriate actions based on the results.

---

## Notes

* Ensure all master data is complete to avoid invalid loan entries.
* Use the PAR breakdown to monitor and mitigate portfolio risk.
* Monthly disbursement helps track seasonal trends or irregularities.

---

