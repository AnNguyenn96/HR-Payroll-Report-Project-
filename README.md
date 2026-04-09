# 💼 Payroll Project

This project showcases a payroll data warehouse. The main SQL script transforms and centralizes payroll data, which are then connected to Power BI for analytics to support HR and finance operations.

---

## 📑 Table of Contents
- 📊 [Data Source](#data-source)
- 🏗️ [Architecture](#architecture)
- 🧠 [Semantic Model](#semantic-model)
- 📈 [Business Insights](#business-insights)
  - 🔍 [Overview](#overview)
  - 👥 [Employee Details](#employee-details)

---

## 📊 Data Source

The payroll dataset includes employee records, salary details, attendance logs, tax deductions, and benefits information. For demonstration purpose, data was manually generated with Python, in a real-case scenario, these are typically exported from HR/payroll systems and ingested into the pipeline for processing and analytics.

<p align="center">
    <img src="Payroll Dataset /source_relational_model.png" alt="source-relational-model" style="border-radius: 10px;">
    </br>
  Source Relational Model
</p>

---

## 🏗️ Architecture

Data are passed through 3 layers:
- 🟢 **Landing**: Tables from imported raw CSV files  
- 🟡 **Staging**: Standardized Views (Cleaned, Restructured Data)  
- 🔵 **Marts**: Final Data Model (Joined and Enhanced Tables)  

<p align="center">
    <img src="Payroll Dataset /payroll-diagram.svg" alt="architecture" style="border-radius: 10px;">
    </br>
  Project Architecture
</p>

---

## 🧠 Semantic Model

<p align="center">
    <img src="Power BI/Payroll Data Model.png" alt="powerbi" style="border-radius: 10px;">
    </br>
  Power BI Semantic Model
</p>

### 🔗 Defined Relationships

| From Table (Column)             | Relationship Type | To Table (Column)                               |
| ------------------------------- | ----------------- | ----------------------------------------------- |
| `dim_date(date_pk)`             | One to Many       | `fact_allowances(allowance_start_date_fk)`      |
| `dim_date(date_pk)`             | One to Many       | `fact_allowances(allowance_end_date_fk)`        |
| `dim_employees(employee_pk)`    | One to Many       | `fact_allowances(employee_fk)`                  |
| `dim_pay_period(pay_period_pk)` | One to Many       | `fact_allowances(pay_period_fk)`                |
| `dim_contracts(contract_pk)`    | One to Many       | `fact_allowances(contract_fk)`                  |
| `dim_date(date_pk)`             | One to Many       | `fact_bonuses(bonus_date_fk)`                   |
| `dim_employees(employee_pk)`    | One to Many       | `fact_bonuses(employee_fk)`                     |
| `dim_pay_period(pay_period_pk)` | One to Many       | `fact_bonuses(pay_period_fk)`                   |
| `dim_contracts(contract_pk)`    | One to Many       | `fact_bonuses(contract_fk)`                     |
| `dim_employees(employee_pk)`    | One to Many       | `fact_employee_leaves(employee_fk)`             |
| `dim_pay_period(pay_period_pk)` | One to Many       | `fact_employee_leaves(pay_period_fk)`           |
| `dim_contracts(contract_pk)`    | One to Many       | `fact_employee_leaves(contract_fk)`             |
| `dim_date(date_pk)`             | One to Many       | `fact_employee_leaves(leave_start_date_fk)`     |
| `dim_date(date_pk)`             | One to Many       | `fact_employee_leaves(leave_end_date_fk)`       |
| `dim_employees(employee_pk)`    | One to Many       | `fact_roster(employee_fk)`                      |
| `dim_pay_period(pay_period_pk)` | One to Many       | `fact_roster(pay_period_fk)`                    |
| `dim_contracts(contract_pk)`    | One to Many       | `fact_roster(contract_fk)`                      |
| `dim_date(date_pk)`             | One to Many       | `fact_roster(work_date_fk)`                     |
| `dim_employees(employee_pk)`    | One to Many       | `fact_timesheet(employee_fk)`                   |
| `dim_pay_period(pay_period_pk)` | One to Many       | `fact_timesheet(pay_period_fk)`                 |
| `dim_contracts(contract_pk)`    | One to Many       | `fact_timesheet(contract_fk)`                   |
| `dim_date(date_pk)`             | One to Many       | `fact_timesheet(timesheet_transaction_date_fk)` |
| `dim_employees(employee_pk)`    | One to Many       | `dim_contracts(employee_id)`                    |

---

## 📈 Business Insights

## 🔍 Page 1 – Executive Payroll Overview

Ensure employees are not underpaid against Australian employment laws, while monitoring payroll variance caused by overtime and workforce inefficiencies.

<p align="center">
    <img width="1454" height="814" alt="{282DD332-BC55-4FE0-8861-7BDDBF49DED0}" src="https://github.com/user-attachments/assets/0f6448d2-8eac-4764-be4b-c2d2a356b448" />
    </br>
  Executive Payroll Overview
</p>

### 🎯 Objective  
Understand overall payroll cost and identify key drivers of payroll variance.

### 💡 Key Insights  
- Overtime contributes ~16% of total payroll → main driver of pay variance  
- Payroll is concentrated in IT, Software, and Security roles  
- High cost per employee (~$102K) driven by skilled roles and overtime  

### 📌 Recommendations  

| Area | Action |
|------|--------|
| Overtime impact | Monitor overtime vs base hours regularly |
| High-cost roles | Focus compliance checks on key roles |
| Payroll drivers | Track variance between base pay and actual pay |
---

## ⚖️ Page 2 – Payroll Compliance Analysis

<p align="center">
    <img src="Power BI/Payroll_Dashboard-2.png" alt="Employee Analysis" style="border-radius: 10px;">
    </br>
  Employee Analysis
</p>

### 🎯 Objective
Detect underpayment risk by comparing actual pay against mandatory pay baseline.

### 💡 Key Insights  
- Underpayment is minimal ($34K) → no significant compliance risk detected  
- Underpayment trend is stable → no systemic payroll issue  
- Overpayment ($5.39M) mainly driven by overtime and penalty rates  
- Payroll variance is concentrated in specific job roles  

### 📌 Recommendations  

| Area | Action |
|------|--------|
| Underpayment | Continue monitoring mandatory vs actual pay |
| Compliance | Audit high-risk roles periodically |
| Payroll variance | Investigate unusual spikes (non-OT related) |
| System accuracy | Validate pay rules and multipliers |

---

## 👥 Page 3 – Employee Analysis  

### 🎯 Objective  
Identify employee-level drivers of payroll variance.

### 💡 Key Insights  
- Some employees have extremely high overtime (e.g. 715 hours)  
- Minimal undertime → workforce is fully utilized  
- Payroll variance is mainly driven by overtime, not base salary  
- Leave patterns are consistent → low compliance impact  

### 📌 Recommendations  

| Area | Action |
|------|--------|
| High overtime employees | Redistribute workload |
| Workforce balance | Avoid over-reliance on key individuals |
| Payroll tracking | Monitor pay vs hours at employee level |
| Leave management | Maintain accurate leave records |

---

## ⚙️ Page 4 – Workforce Behavior & Cost Efficiency  

### 🎯 Objective  
Evaluate workforce utilization and its impact on payroll efficiency.

### 💡 Key Insights  
- Utilization exceeds 100% → heavy workload across roles  
- Overtime (~29.85K hours) significantly exceeds undertime (~2.26K hours)  
- Strong correlation between overtime and payroll cost  
- IT and Software roles dominate total labor hours  

### 📌 Recommendations  

| Area | Action |
|------|--------|
| Workforce planning | Reduce reliance on overtime |
| Utilization control | Balance workload across roles |
| Cost efficiency | Monitor overtime vs productivity |
| Payroll variance | Identify non-OT related pay increases |

---

## 🎯 Final Impact  

This dashboard enables HR and Finance teams to ensure employees are not underpaid, while understanding payroll variance driven by overtime and workforce utilization.

