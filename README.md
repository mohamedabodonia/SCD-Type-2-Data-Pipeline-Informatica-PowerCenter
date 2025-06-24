
# 📊 SCD Type 2 Data Pipeline – Informatica PowerCenter

This project demonstrates how to implement a **Slowly Changing Dimension (SCD) Type 2** pipeline using **Informatica PowerCenter**, with **Oracle** as the source and target databases. The solution uses versioning to preserve historical records and track changes in customer data over time.

---

## 🧰 Tools & Technologies
- **Informatica PowerCenter**
- **Oracle Database**
- **ETL Concepts: SCD Type 2, Versioning, Data Warehousing**

---

## 🧱 Project Architecture

### 🗂 Source:
- `CUSTOMERSCD` (Oracle Table)  
  Columns: `CUSTOMERID`, `FIRSTNAME`, `ADDRESS`, `COUNTRY`

  ### 🎯 Target:
- `TRG_CUSTOMER1` (Oracle Table)  
  Columns: `CUSTOMER_KEY`, `CUSTOMER_ID`, `FIRST_NAME`, `ADDRESS`, `COUNTRY`, `VERSION`

---

## 🔄 Pipeline Workflow

### 1. **Source Qualifier**
- Reads data from the `CUSTOMERSCD` table.

### 2. **Lookup Transformation**
- Looks up existing customer records in the target table `TRG_CUSTOMER' using `CUSTOMER_ID`.

### 3. **Expression Transformation**
- Compares source and lookup fields.
- Generates flags (`Insert_Flag`, `Update_Flag`, `Default_Flag`) to determine action.
- Calculates next version using lookup version + 1.

### 4. **Router Transformation**
- Routes records based on the type of change:
  - `Insert`: Insert New records.
  - `Update`: Modified records.
  - `Default`: No change.

### 5. **Sequence Generator**
- Generates unique surrogate keys (`CUSTOMER_KEY`) for new records.

### 6. **Target Tables**
- Loads data into `TRG_CUSTOMER1` with proper versioning:
  - Closes old records (if any) by updating `VERSION`.
  - Inserts new records with Defult value of version=1.

## 📌 Features

- Preserves **historical data** using **SCD Type 2 with versioning**.
- Avoids data overwrite by closing old records and inserting updated ones.
- Ensures **data consistency** and auditability.
- Handles **new**, **updated**, and **unchanged** records efficiently.

---

## 📸 Pipeline Screenshot

<img src="https://github.com/mohamedabodonia/sql-datawarehouse-project/blob/main/docs/data_architecture.png?raw=true">

