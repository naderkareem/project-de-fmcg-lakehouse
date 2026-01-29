# End-to-End FMCG Data Engineering Pipeline (Lakehouse Architecture)

## Project Overview

This project demonstrates an end-to-end data engineering pipeline built using Databricks Free Edition for the FMCG (Fast-Moving Consumer Goods) domain. The solution simulates a real-world acquisition scenario where a large FMCG manufacturer (Atlon) acquires a smaller startup (Sports Bar) and must consolidate data from both organizations into a unified Lakehouse architecture.

The pipeline ingests data from multiple sources, applies standardized transformations using Apache Spark, and organizes the data using the Medallion Architecture (Bronze, Silver, and Gold layers). The final output delivers analytics-ready tables designed using a Star Schema to support scalable reporting, pricing analysis, and business decision-making.

## Business Problem

Following the acquisition of Sports Bar, the parent company Atlon faced significant data integration challenges. Sports Bar’s data was scattered across spreadsheets and flat files with inconsistent schemas, naming conventions, and data quality issues. In contrast, Atlon operated with structured, monthly-grain transactional data designed for enterprise reporting.

Key challenges included:
- Fragmented data sources with no single source of truth
- Mismatched data granularity between parent and child companies
- Inconsistent product naming, pricing, and customer identifiers
- Lack of reliable historical and incremental reporting mechanisms

The business required a scalable and repeatable data engineering solution to unify data from both companies, standardize metrics, and enable consistent reporting across the merged organization.

## Solution Overview

To address the data integration challenges, an end-to-end Lakehouse-based data engineering solution was designed using Databricks and Apache Spark. The pipeline consolidates raw data from both the parent and acquired companies into a unified data platform while preserving historical accuracy and supporting incremental data growth.

The solution follows the Medallion Architecture pattern:
- Raw data is ingested into a Bronze layer with minimal transformations.
- Cleaned and standardized datasets are curated in the Silver layer.
- Business-ready, aggregated datasets are published in the Gold layer for analytics and reporting.

A Star Schema data model is implemented in the Gold layer to ensure high-performance querying and compatibility with BI and dashboarding tools. The pipeline supports both full historical loads and ongoing incremental processing to simulate real-world production behavior.

## Technology Stack

- **Databricks (Free Edition)** – Distributed data processing and orchestration platform  
- **Apache Spark (PySpark & Spark SQL)** – Large-scale data transformations  
- **AWS S3** – Cloud-based data lake storage for raw and processed data  
- **Python** – Transformation logic and pipeline orchestration  
- **SQL** – Data modeling, aggregations, and analytical queries  
- **Medallion Architecture** – Layered data design (Bronze, Silver, Gold)  
- **Star Schema** – Analytical data modeling for reporting and BI workloads  

## High-Level Architecture

## Data Sources

## Data Modeling

## ETL Pipeline Design
### Bronze Layer
### Silver Layer
### Gold Layer

## Incremental Loading Strategy

## Orchestration & Scheduling

## Analytics & Reporting

## Business Impact

## Repository Structure

## How to Run This Project

## Future Enhancements
