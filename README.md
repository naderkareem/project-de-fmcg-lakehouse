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

The solution is built using a Lakehouse architecture implemented on Databricks, following the Medallion Architecture design pattern. Data flows from cloud storage into progressively refined layers to ensure data quality, scalability, and analytical performance.

![Medallion Architecture](architecture/medallion_architecture.png)

At a high level:
- Raw data from both the parent and acquired companies is ingested into the Bronze layer.
- The Silver layer applies data cleansing, standardization, and business rules.
- The Gold layer exposes analytics-ready datasets modeled for reporting and decision-making.

This layered approach enables reliable incremental processing, clear separation of concerns, and simplified debugging while supporting future scalability.

## Data Sources

The project integrates data from two distinct organizations to simulate a real-world acquisition scenario.

**Parent Company (Atlon):**
- Provides structured, historical data at a monthly grain.
- Data includes customers, products, gross pricing, and order transactions.
- Designed for enterprise reporting with stable schemas.

**Acquired Company (Sports Bar):**
- Provides operational data as daily CSV file drops.
- Data is ingested from an S3 landing zone to simulate batch ingestion.
- Data quality issues include inconsistent naming, unreliable identifiers, and varying pricing structures.

This dual-source setup reflects common challenges encountered during mergers and acquisitions, including schema mismatches, grain differences, and data quality inconsistencies.

## Data Modeling

The analytics layer is designed using a Star Schema to support efficient querying and reporting. A centralized fact table captures transactional metrics and is linked to multiple dimension tables that provide descriptive context.

**Fact Table:**
- `fact_orders` – Stores order-level and aggregated sales metrics such as quantity sold and revenue.

**Dimension Tables:**
- `dim_customers` – Customer attributes standardized across both companies.
- `dim_products` – Product details with surrogate keys to resolve unreliable source identifiers.
- `dim_gross_price` – Standardized pricing information aligned to reporting periods.
- `dim_date` – Calendar dimension to support time-based analysis.

This modeling approach ensures compatibility with BI tools, simplifies analytical queries, and enables consistent business metrics across the merged organization.

## ETL Pipeline Design
### Bronze Layer

The Bronze layer is responsible for raw data ingestion from AWS S3 into Databricks. Data is ingested with minimal transformation to preserve the original structure and ensure traceability.

Key characteristics:
- Raw CSV files are ingested as-is from landing locations.
- Metadata columns such as ingestion timestamp and source file name are added.
- No business rules or data cleansing is applied at this stage.

This layer serves as an immutable source of truth and enables reprocessing in case of downstream logic changes.

### Silver Layer

The Silver layer focuses on data cleansing, standardization, and application of business rules to create reliable, analytics-ready datasets.

Key transformations include:
- Deduplication of customer and product records.
- Standardization of categorical fields and correction of common spelling inconsistencies.
- Generation of surrogate keys for products using hashing techniques due to unreliable source identifiers.
- Validation and normalization of pricing and quantity values.

The Silver layer ensures consistent definitions and data quality across datasets originating from different systems.

### Gold Layer

The Gold layer contains curated, business-ready datasets optimized for reporting and analytics. Data from both companies is consolidated and aligned to a common reporting grain.

Key outputs:
- Aggregated fact tables aligned to monthly reporting requirements.
- Conformed dimension tables shared across the organization.
- Star Schema-based datasets designed for BI and dashboard consumption.

This layer represents the single source of truth for analytical and decision-support workloads.

## Incremental Loading Strategy

The pipeline is designed to support incremental data processing to simulate real-world production behavior. Instead of reprocessing the entire dataset, only newly arrived data is ingested and transformed during each run.

Key aspects of the incremental strategy:
- New data files are ingested from an S3 landing directory on a daily basis.
- A staging-based approach is used to process only unprocessed files.
- Processed files are logically separated to prevent duplicate ingestion.
- Incremental fact data is appended to existing tables while preserving historical records.

This approach improves scalability, reduces processing time, and ensures data consistency as data volumes grow over time.

## Orchestration & Scheduling

## Analytics & Reporting

## Business Impact

## Repository Structure

## How to Run This Project

## Future Enhancements
