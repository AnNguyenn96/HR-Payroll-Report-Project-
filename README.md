# Payroll-Project

This project showcases a payroll data warehouse. The main SQL script transforms and centralizes payroll data, which are then connected to Power BI for analytics to support HR and finance operations.

## Table of Contents
- [Payroll Project](#payroll-project)
  - [Table of Contents](#table-of-contents)
  - [Data Source](#data-source)
  - [Architecture](#architecture)
  - [Semantic Model](#semantic-model)
  - [Business Insights](#business-insights)
    - [Overview](#overview)
    - [Employee Details](#employee-details) 

## Data Source

The payroll dataset includes employee records, salary details, attendance logs, tax deductions, and benefits information. For demonstration purpose, data was manually generated with Python, in a real-case scenario, these are typically exported from HR/payroll systems and ingested into the pipeline for processing and analytics.

<p align="center">
    <img src="Payroll Dataset Generator/source_relational_model.png"" alt="source-relational-model" style="border-radius: 10px;">
    </br>
  Source Relational Model
</p>

## Architecture

Data are passed through 3 layers:
- Landing: Tables from imported raw CSV files
- Staging: Standardized Views (Cleaned, Restructured Data)
- Marts: Final Data Model (Joined and Enhanced Tables)

<p align="center">
    <img src="Payroll Dataset Generator/payroll-diagram.svg" alt="architecture" style="border-radius: 10px;">
    </br>
  Project Architecture
</p>



## Semantic Model
<p align="center">
    <img src="Power BI/powerbi.png" alt="powerbi" style="border-radius: 10px;">
    </br>
  Power BI Semantic Model
</p>

Defined Relationships:
| From Table (Column)                  | Relationship Type | To Table (Column)                     |
|-------------------------------------|-------------------|---------------------------------------|
| `dim_date(date_pk)`  | One to Many   |  `fact_allowances (allowance_start_date_fk)`    |
| `dim_employees(employee_pk)`     | One to Many     |    `fact_allowances(employee_fk)`    | 
| `dim_pay_period(pay_period_pk)`| One to Many      | `fact_allowances(pay_period_fk)`         | 
| `dim_date(date_pk)`| One to Many      | `fact_bonuses(bonus_date_fk)`         | 
| `dim_eployees(employee_pk)`      | One to Many     | `fact_bonuses(employee_fk)`      | 
| `dim_pay_period(pay_period_pk)`| One to Many      | `fact_bonuses(pay_period_fk)`         | 
|`dim_employees(employee_pk)`  | One to Many      |      `fact_employee_leaves(employee_fk)`   | 
|  `dim_pay_period(pay_period_pk)` | One to Many      |   `fact_employee_leaves(pay_period_fk)`     | 
| `dim_employees(employee_pk)`     | One to Many     |    `fact_roster(employee_fk)`    | 
|  `dim_pay_period(pay_period_pk)` | One to Many      |   `fact_roster(pay_period_fk)`     | 
| `dim_date(date_pk)`  | One to Many   |  `fact_roster(work_date_fk)`    |
| `dim_employees(employee_pk)`     | One to Many     |    `fact_timesheet(employee_fk)`    | 
| `dim_pay_period(pay_period_pk)`| One to Many      | `fact_timesheet(pay_period_fk)`         | 
| `dim_contract(contract_pk)`| One to Many      | `fact_timesheet(contract_fk)`         |
| `dim_date(date_pk)`| One to Many      | `fact_timehseet(timesheet)_transition_date_fk)`         | 
| `dim_date(date_pk)`| One to Many      | `fact_employee_leaves(leave_start_date_fk)`          | 

## Business Insights:

### Overview
<p align="center">
    <img src="Power BI/Payroll_Dashboard-1.png" alt="Payroll Remediation" style="border-radius: 10px;">
    </br>
  Payroll Remediation
</p>
...

### Employee Details
<p align="center">
    <img src="Power BI/Payroll_Dashboard-2.png" alt="Employee Analysis" style="border-radius: 10px;">
    </br>
  Employee Analysis
</p>
...

