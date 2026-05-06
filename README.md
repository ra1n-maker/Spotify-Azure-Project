# 🎵 Spotify Azure Data Engineering Pipeline

## 📖 Overview
This project illustrates a modern, scalable Medallion Architecture (Bronze, Silver, and Gold) built entirely on the Microsoft Azure and Databricks stack. It is designed to automatically ingest raw Spotify data, process it through a series of refining transformations, and organize it into a high-quality Star Schema for business intelligence and reporting.

## 🏗️ Architecture
1. **Data Ingestion (Bronze Layer):** Azure Data Factory (ADF) orchestrates the movement of raw data from external sources and SQL databases into the initial Data Lake storage container.
2. **Data Cleansing (Silver Layer):** Apache Spark on Databricks processes the raw data, applying filters and normalization logic to ensure data quality and consistency.
3. **Curated Analytics (Gold Layer):** Delta Live Tables (DLT) apply complex business logic, transforming the cleansed data into an optimized Star Schema.
4. **Serving & Security:** Curated data is loaded into Azure Synapse Analytics for high-performance dashboarding. Azure Key Vault is integrated across the pipeline to securely manage all credentials.

## 🎯 Core Requirements & Capabilities
*   **Incremental & Stream Processing:** Processes only new or changed data and natively handles real-time data flows.
*   **Historical Backfilling:** Fully equipped to re-process past dates or ingest historical data on demand.
*   **Metadata-Driven & Dynamic Code:** Utilizes Jinja templating and configuration files to drive pipeline logic, ensuring high scalability without hardcoding.
*   **DevOps & CI/CD:** Leverages Databricks Asset Bundles and Terraform for automated infrastructure deployment and strict version control.

## 🗄️ Data Model (Star Schema)
The Gold layer is structured for fast analytical queries:
*   **Fact Table:** `FactStream` (Tracks individual streams, durations, and device types).
*   **Dimension Tables:** `DimUser`, `DimArtist`, `DimTrack`, and `DimDate` (Provides descriptive attributes for aggregations).

## 📂 Repository Structure
The project is organized to separate infrastructure configuration, source code, and control files:

*   **`Databricks Code/`**: Contains the core logic executed on Databricks clusters. This includes PySpark notebooks and Python scripts for transforming data across the Bronze, Silver, and Gold layers (e.g., Delta Live Tables configurations, exploratory notebooks).
*   **`source_scripts/`**: Houses utility scripts, infrastructure definitions (such as Terraform files for Databricks Asset Bundles), or initial SQL load scripts required to set up external systems or seed data.
*   **`cdc.json`**: Configuration file managing Change Data Capture (CDC) watermarks or state, essential for enabling the incremental processing requirement.
*   **`empty.json`**: A placeholder or schema-definition file used in testing or initializing pipeline metadata structures.
*   **`loop_input`**: A control file or parameter list utilized by metadata-driven loops (e.g., in Azure Data Factory) to dynamically process multiple tables or endpoints without hardcoding logic.
