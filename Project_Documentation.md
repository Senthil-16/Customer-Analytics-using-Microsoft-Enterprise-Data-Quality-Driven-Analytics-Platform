# Overview
An end-to-end customer analytics platform built in Microsoft Fabric. Raw CSV data is ingested into a Lakehouse, cleaned and validated with PySpark, aggregated into business-ready tables, and shown in a Power BI dashboard through a semantic model. The project follows the Medallion architecture (Bronze, Silver, Gold) and focuses on data quality.

# Architecture
Raw CSV -> Bronze (raw) -> Silver (cleaned and validated) -> Gold (aggregated) -> Semantic model -> Power BI dashboard

| Layer  | Tables                          | Purpose                                                       |
| ------ | ------------------------------- | ------------------------------------------------------------- |
| Bronze | bronze_customers, bronze_orders | Raw data exactly as received; kept for reprocessing and audit |
| Silver | silver_customers, silver_orders | Cleaned and validated data                                    |
| Gold   | gold_customer_summary           | Business-ready customer-level metrics for reporting           |

# Dataset
* Source: Sample dataset created using Chatgpt (Sample CSV file to test it)
* Format: CSV files uploaded to the Fabric Lakehouse
* Customers table columns used: customer_id, customer_name, email, city, signup_date [add others]
* Orders table columns used: customer_id, order_amount, payment_status [add order id, order date and others]
* Approximate size: [rows in each file]

# Data quality rules (Silver layer)

| Table     | Rule                                       | Reason                                     |
| --------- | ------------------------------------------ | ------------------------------------------ |
| Customers | Remove duplicates on customer_id           | One customer must appear once              |
| Customers | Drop rows where email is null              | Customer cannot be identified or contacted |
| Customers | Fill missing city with "Unknown"           | Keeps the customer in city-wise analysis   |
| Customers | Convert signup_date to a date (yyyy-MM-dd) | Standard, consistent date type             |
| Orders    | Keep only order_amount > 0                 | Zero or negative amounts are invalid       |
| Orders    | Keep only payment_status = 'Completed'     | Only successful payments count as revenue  |

# Gold layer
gold_customer_summary has one row per customer: customer_id, customer_name, city, total_orders, total_spent, avg_order_value.
It is built by joining silver_customers to silver_orders (left join, so customers without completed orders stay with zero values) and aggregating the order amounts. See spark_code.txt.

Correction note: the first version of the Gold query calculated the spend columns from the customers table only. It was corrected to join the orders table and sum the amounts.

# Semantic model and measures
* Tables: [list the tables loaded into the semantic model]
* Relationships: [for example one customer to many orders on customer_id]
* Measures: [write the measures you actually created, for example Total Customers, Total Orders, Total Revenue, Average Order Value]

# Dashboard
* KPI cards: Total Customers, Total Orders, Total Revenue
* Customer-wise analytics
* City-wise distribution
* Interactive filters and slicers

Screenshots are in the screenshots folder.

# Tools
Microsoft Fabric (Lakehouse, Spark notebooks), Apache Spark (PySpark), Delta tables, Power BI.

# Challenges and how they were handled
* Missing and inconsistent values: handled with validation rules in the Silver layer.
* Gold metrics: [describe your real challenge; the Gold query was corrected to include order amounts].

# Limitations
* The Fabric trial capacity has ended, so the workspace is no longer active; the code and screenshots are kept in this repository.
* Batch pipeline only; no scheduling or incremental loading.
* No automated data quality report.

# Future improvements
* Incremental loading with MERGE instead of full overwrite
* Pipeline scheduling and failure alerts
* An automated data quality report (null counts, duplicate counts per run)
* Direct Lake semantic model for faster reports

# How to run
1. Create a Fabric workspace and a Lakehouse.
2. Upload the raw CSV files and load them as bronze_customers and bronze_orders.
3. Run the Silver notebook, then the Gold notebook (see spark_code.txt).
4. Create a semantic model on the Gold tables, then build the Power BI report.
