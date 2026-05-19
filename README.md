# 🚴 Databricks Bike Lakehouse 2026

<div align="center">

![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-003366?style=for-the-badge&logo=delta&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)

**A comprehensive data lakehouse solution implementing the medallion architecture for customer information processing**

</div>

---

## 🎥 Video Tutorial

📹 **Watch the Complete Guide:** [Data LakeHouse using Databricks](https://youtu.be/tROyARdT56g)

---

## 📋 Overview

This repository contains a **Databricks Lakehouse** project that processes and transforms customer relationship management (CRM) data for bike rental operations. The project follows the industry-standard **medallion architecture** (Bronze → Silver → Gold) for progressive data refinement and quality improvement.

---

## 🏗️ Architecture

### Medallion Layers

```
📊 DATABRICKS LAKEHOUSE
│
├─── 🥉 BRONZE LAYER
│    └─ Raw Data Ingestion
│       • CSV files from source systems
│       • Minimal transformation
│       • Historical data preservation
│
├─── 🥈 SILVER LAYER
│    └─ Data Cleaning & Transformation
│       • Data quality improvements
│       • Standardization & normalization
│       • Column renaming & formatting
│
└─── 🥇 GOLD LAYER
     └─ Business-Ready Analytics
        • Dimensional models
        • Fact tables
        • Optimized for BI/Analytics
```

---

## 📁 Project Structure

```
bike_lakehouse_2026/
├── 🔴 Bronze.ipynb              # Layer 1: Raw data ingestion
├── ⚪ Silver_crm_cust_infor.ipynb  # Layer 2: Data transformation & cleaning
└── 🟡 Gold_Customers.ipynb      # Layer 3: Business-ready customer dimension
```

---

## 📓 Notebooks Description

### 1️⃣ **Bronze.ipynb** - Raw Data Ingestion
   
   **Purpose:** 🔴 Ingests raw CSV files into the Bronze layer
   
   **Key Operations:**
   - ✅ Reads CSV files from source systems (`/Volumes/workspace/bronze/source_systems/`)
   - ✅ Infers schema automatically
   - ✅ Loads data with minimal transformation
   - ✅ Persists raw tables for historical tracking
   
   **Tables Created:**
   - `workspace.bronze.crm_cust_info` - Customer information
   - `workspace.bronze.crm_prd_info` - Product information
   
   **Tech Stack:** PySpark SQL, Apache Spark

---

### 2️⃣ **Silver_crm_cust_infor.ipynb** - Data Transformation

   **Purpose:** ⚪ Transforms and standardizes Bronze data to Silver layer
   
   **Key Operations:**
   - 🧹 String trimming to remove whitespace
   - 🔄 Column renaming for clarity (`cst_id` → `customer_id`, etc.)
   - 📊 Data normalization (marital status, gender codes)
   - ✅ Data quality validation
   - 🔍 Standardization of categorical values
   
   **Transformations Include:**
   - Trim whitespace from string columns
   - Normalize marital status: `S` → `Single`, `M` → `Married`
   - Normalize gender codes
   - Standardize date formats
   
   **Output Table:** `silver.crm_customer`
   
   **Tech Stack:** PySpark SQL, PySpark Functions

---

### 3️⃣ **Gold_Customers.ipynb** - Business Analytics Layer

   **Purpose:** 🟡 Creates dimensional models for analytics and BI tools
   
   **Key Operations:**
   - 📈 Builds customer dimension table
   - 🔑 Generates surrogate keys using `ROW_NUMBER()`
   - 🎯 Optimizes for analytical queries
   - 💾 Persists in Delta format for ACID compliance
   
   **Features:**
   - Customer Key (surrogate)
   - Customer ID (business key)
   - Customer Name (first & last)
   - Ready for join with fact tables
   
   **Output Table:** `gold.dim_customers`
   
   **Tech Stack:** PySpark SQL, Delta Lake

---

## 🔄 Data Flow

```
SOURCE DATA
    ↓
📥 CSV Files
    ↓
🔴 BRONZE LAYER (Bronze.ipynb)
    │ Raw ingestion, minimal processing
    ↓
⚪ SILVER LAYER (Silver_crm_cust_infor.ipynb)
    │ Cleaning, transformation, standardization
    ↓
🟡 GOLD LAYER (Gold_Customers.ipynb)
    │ Business-ready dimensions & facts
    ↓
📊 ANALYTICS & BI TOOLS
```

---

## 🚀 Quick Start

### Prerequisites
- ✅ Databricks Workspace access
- ✅ Apache Spark environment
- ✅ Delta Lake enabled
- ✅ Source data in `/Volumes/workspace/bronze/source_systems/`

### Execution Order

1. **Run Bronze Layer First**
   ```
   Open and execute: Bronze.ipynb
   ```
   This creates raw tables from CSV files.

2. **Run Silver Layer Second**
   ```
   Open and execute: Silver_crm_cust_infor.ipynb
   ```
   This cleans and transforms the Bronze data.

3. **Run Gold Layer Last**
   ```
   Open and execute: Gold_Customers.ipynb
   ```
   This creates the final dimensional model.

---

## 🎯 Key Features

| Feature | Description |
|---------|-------------|
| 🏛️ **Medallion Architecture** | Industry-standard data warehouse pattern |
| 🧹 **Data Quality** | Automated cleaning, normalization, and validation |
| 📊 **Delta Lake** | ACID compliance, time travel, schema enforcement |
| 🔍 **Scalability** | Distributed processing with Apache Spark |
| 🔐 **Version Control** | Delta Lake maintains data versions |
| 🎨 **Standardization** | Consistent naming conventions and data types |

---

## 📊 Data Transformations

### Column Mappings (Bronze → Silver)

| Bronze Column | Silver Column | Transformation |
|---------------|---------------|-----------------|
| `cst_id` | `customer_id` | Renamed |
| `cst_key` | `customer_key` | Renamed |
| `cst_firstname` | `customer_firstname` | Trimmed, standardized |
| `cst_lastname` | `customer_lastname` | Trimmed, standardized |
| `cst_marital_status` | `marital_status` | Normalized (S/M → Single/Married) |
| `cst_gndr` | `gender` | Normalized |
| `cst_create_date` | `create_date` | Standardized format |

---

## 🛠️ Technologies & Tools

- **🔷 Databricks** - Unified analytics platform
- **⚡ Apache Spark** - Distributed computing framework
- **🗄️ Delta Lake** - Open-source storage layer
- **🐍 Python / PySpark** - Data processing
- **📝 SQL** - Data querying and transformation
- **📓 Jupyter Notebooks** - Interactive development

---

## 📈 Performance Considerations

- ✅ Use `%sql` for complex queries (optimized execution)
- ✅ Leverage Spark caching for repeated operations
- ✅ Partition tables by date for faster queries
- ✅ Use Delta file statistics for query optimization
- ✅ Monitor cluster resources during large transformations

---

## 📚 Best Practices Implemented

- 📋 Clear cell documentation with markdown
- 🔄 Idempotent operations (safe to re-run)
- 🎯 Single responsibility per notebook
- 🏷️ Consistent naming conventions
- ✅ Data validation at each layer
- 📊 Display results for verification

---

## 🔮 Future Enhancements

- 🎨 Add more dimension tables (products, locations)
- 📉 Create fact tables for transactions
- 📊 Implement aggregation tables for performance
- 🔔 Add data quality monitoring & alerts
- 📈 Build dashboards for business metrics
- 🤖 Implement incremental load patterns (CDC)

---

## 📞 Support & Documentation

For more information about:
- **Databricks:** https://docs.databricks.com
- **Apache Spark:** https://spark.apache.org/docs/latest/
- **Delta Lake:** https://docs.delta.io
- **Medallion Architecture:** https://www.databricks.com/blog/2022/06/24/simplify-data-pipelines-with-delta-lake.html

---

## 📝 License

This project is part of the **Databricks Bootcamp 2026** training program.

---

<div align="center">

**Built with ❤️ using Databricks | 2026**

*Transforming raw data into actionable insights through advanced data engineering practices*

</div>
