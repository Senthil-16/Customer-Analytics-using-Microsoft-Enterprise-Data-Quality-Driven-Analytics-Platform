# Customer Analytics using Microsoft Enterprise Data Quality–Driven Analytics Platform
Using Microsoft Fabric & Power BI:
 Project Overview:

This project demonstrates an end-to-end enterprise analytics platform built using Microsoft Fabric, following the Medallion Architecture (Bronze–Silver–Gold).
The solution focuses on data quality, transformation, and analytics-ready reporting using Spark, Lakehouse, and Power BI.

The final outcome is a professional, interactive Power BI dashboard designed for business decision-making.

 Objectives:

Build a complete data engineering + analytics pipeline

Apply data quality checks and transformations

Implement Bronze, Silver, and Gold layers

Create a semantic model for reporting

Design a professional Power BI dashboard

Simulate a real enterprise analytics workflow

 Tech Stack:

Microsoft Fabric

Lakehouse

Spark Notebooks

Semantic Model

Apache Spark (PySpark)

Delta Tables

Power BI

Medallion Architecture

 Architecture Overview :
Raw Data (CSV)
     ↓
Bronze Layer (Raw Ingestion)
     ↓
Silver Layer (Cleaned & Validated Data)
     ↓
Gold Layer (Aggregated Business Metrics)
     ↓
Semantic Model
     ↓
Power BI Dashboard

📂 Project Structure :
Customer-Analytics-Microsoft-Fabric
│
├── README.md
├── Project_Documentation.md
├── spark_code.txt
│
└── screenshots
    ├── dashboard.png
    ├── lakehouse_tables.png
    └── semantic_model.png

🔄 Data Pipeline Description :
🔹 Bronze Layer

Raw CSV files ingested into Fabric Lakehouse

No transformations applied

Purpose: preserve original data

🔹 Silver Layer

Data cleaning and validation

Handling null values and standardizing formats

Data prepared for analytics

🔹 Gold Layer

Business-level aggregations

Metrics created:

Total Orders

Total Revenue

Average Order Value

Optimized for reporting and KPIs

📊 Power BI Dashboard Features :

KPI Cards:

Total Customers

Total Orders

Total Revenue

Customer-wise analytics

City-wise distribution

Interactive filters and slicers

Clean, professional color theme

Business-friendly layout

 Key Learnings :

End-to-end Microsoft Fabric workflow

Enterprise data modeling concepts

Spark-based transformations

Semantic model creation

Dashboard storytelling with Power BI

Real-world data engineering practices

 Use Case :

This project simulates how enterprises:

Maintain data quality

Build scalable analytics platforms

Enable self-service BI

Support business decision-making


