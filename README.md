# 📊 Databricks Assignment 

## 🔹 Overview

This project implements a **Medallion Architecture (Bronze → Silver → Gold)** using PySpark in Databricks. It processes employee-related datasets and an external API to build structured and analytics-ready data.

---

##  Folder Structure

* `source_to_bronze/`
* `bronze_to_silver/`
* `silver_to_gold/`

---

##  Notebooks

1. **utils** – Common reusable functions
2. **employee_source_to_bronze** – Reads raw CSV and writes to Bronze
3. **employee_bronze_to_silver** – Cleans and transforms data
4. **employee_silver_to_gold** – Business aggregations

---

##  Bronze Layer

* Reads Employee, Department, Country CSV files
* Writes raw data to storage as CSV
* Acts as ingestion layer

---

##  Silver Layer

* Reads Bronze data using custom schema
* Converts column names (CamelCase → snake_case)
* Adds `load_date`
* Writes cleaned data as Delta tables:

  * `dim_employee`
  * `dim_department`
  * `dim_country`

---

##  Gold Layer

* Joins all Silver tables
* Performs business transformations:

  * Salary per department (descending)
  * Employee count per department & country
  * Department–country mapping
  * Average age per department
* Adds `at_load_date`
* Writes final dataset as:

  * `fact_employee` (Delta)

---

## 🔗 Question 2 – API Pipeline

* Fetches paginated data from API
* Removes unwanted fields
* Applies custom schema & flattens data
* Derives `site_address` from email
* Adds `load_date`
* Writes to Delta table:

  * Database: `site_info`
  * Table: `person_info`

---
