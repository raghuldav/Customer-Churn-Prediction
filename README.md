# SQL-Based Customer Churn Prediction System (PostgreSQL)

## 📌 Project Overview
This project implements a **customer churn prediction system built entirely on PostgreSQL**, tailored for **retail banking analytics**. The platform structures customer data into a well-normalized relational database, enables advanced SQL-based analysis, and supports downstream visualization and predictive modeling through BI and ML workflows.

The system emphasizes **data integrity, performance optimization, and automation**, making it suitable for both analytical and operational use cases.

---

## 🧠 Core Capabilities

- **Highly Normalized Schema (up to BCNF)** ensuring minimal redundancy and efficient querying  
- **Strong Data Integrity** enforced via primary/foreign keys, triggers, and cascading rules  
- **Churn Analysis Support** using behavioral, demographic, and financial attributes  
- **Reusable SQL Views & Queries** designed for analysts, business users, and ML pipelines  
- **Stored Procedures & Functions** to automate routine customer operations  
- **Performance Optimization** through indexing and execution plan analysis  
- **Trigger-Based Validation** to prevent duplicates and enforce business rules  

---

## 📂 Dataset Overview
- **Total Records:** ~10,000 customers  
- **Key Attributes:**
  - CustomerId, Surname  
  - CreditScore, Geography, Gender  
  - Age, Tenure, Balance  
  - NumOfProducts, HasCrCard  
  - IsActiveMember, EstimatedSalary  
  - Exited (Churn Flag)

---

## 🧱 Database Design

The database (`MainDB`) consists of **13 interconnected relational tables**, each with clearly defined dependencies and constraints to maintain consistency and scalability.

### 🔹 Core Tables

| Table Name | Purpose |
|----------|---------|
| Customer | Primary entity storing customer demographics |
| LoanApplication | Loan records associated with customers |
| Account | Account details including balance and tenure |
| CreditCard | One-to-one credit card information |
| ActivityStatus | Tracks customer engagement and activity |
| SalaryDetails | Salary data and linked account info |
| RiskScoreDetails | Credit score and risk classification |
| ChurnStatus | Churn indicator, reason, and contact history |
| StatusFlag | Boolean indicators (high-value, review-needed) |
| CustomerLog | Audit log for customer-related actions |
| SalaryBandMapping | Salary-to-band classification |
| ScoreCategoryMapping | Credit score categorization |

---

## ⚠️ Constraints & Data Integrity
- Email uniqueness enforced via both **UNIQUE constraints** and a **custom trigger**
- Referential integrity maintained using `ON DELETE CASCADE` and `SET NULL`
- All tables validated for correct data types, nullability, and dependencies

---

## 🧪 Supported Operations

### Data Manipulation
- Insert new customers and loan applications  
- Update account balances and salary changes  
- Cascade deletes across dependent entities  

### Analytical Queries
- Multi-table joins for customer profiling  
- Churn behavior analysis  
- Risk and value segmentation  

### Stored Procedures
- `FlagHighRiskCustomers()`  
- `AddLoanApp(custid, amt, status)`  
- `UpdateBalance(custid, new_balance)`  
- `DeleteCustomerAndDependencies(custid)`  

### User-Defined Functions
- `GetSalaryBand(custid)`  
- `GetChurnReason(custid)`  

---

## 🚀 Query Performance Optimization

### Tools Used
- `EXPLAIN`
- `ANALYZE`

| Query Scenario | Execution Time (Before Index) | Execution Time (After Index) |
|---------------|------------------------------|-------------------------------|
| Customers under 60 with standard accounts | 732.30 | 726.62 |
| Pending loans for customers under 50 | 67,199.09 | 37,371.39 |
| Balance ranking with window functions | 2,323.25 | N/A* |

\* Sequential scans remained optimal for smaller datasets.

---

## 🔐 Transactions & Trigger Logic
- Custom trigger `trg_customer_prevent_duplicate_email` blocks duplicate email inserts
- Transactions are fully atomic and rollback automatically on failure
- ACID properties (Atomicity, Consistency, Isolation, Durability) enforced by PostgreSQL

---

## 📊 Intended Users

- **Banking & Finance Teams:** Analyze customer retention and churn drivers  
- **Data Analysts:** Execute complex SQL analytics and BI queries  
- **AI / ML Engineers:** Leverage normalized data for churn modeling  
- **Students & Educators:** Study real-world relational database design  
- **Database Administrators:** Maintain and extend a production-grade schema  

---

## ✅ Technology Stack
- **Database:** PostgreSQL  
- **Data Processing:** Python (pandas)  
- **ETL & Automation:** SQL scripts, stored procedures, triggers  

---

## 🔧 Setup Guide

1. Install PostgreSQL  
2. Create the database:
   ```sql
   CREATE DATABASE MainDB;
3. Execute table creation scripts from create_tables.sql
4. Load CSV files using COPY or psql
5. Run SQL scripts to create stored procedures, triggers, and functions

## 📌 Summary

This project demonstrates a robust SQL-driven approach to customer churn prediction, combining strong relational design, automated data handling, and performance-aware query execution. It serves as a practical blueprint for building scalable analytics systems in data-intensive domains such as retail banking.
