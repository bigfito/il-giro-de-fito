# 🍝 Il Giro de Fito - Snowflake Platform Demo

<p align="center">
  <img src="https://img.shields.io/badge/Snowflake-29B5E8?style=for-the-badge&logo=snowflake&logoColor=white" alt="Snowflake"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white" alt="Jupyter"/>
</p>

A comprehensive Snowflake demonstration showcasing the full breadth of platform capabilities through a fictional Italian restaurant scenario. **Il Giro de Fito** is an authentic Tuscan restaurant specializing in traditional pizza, handmade pasta, fine wines, and Alpine spring water.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features Demonstrated](#-features-demonstrated)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [Demo Sections](#-demo-sections)
- [Sample Data](#-sample-data)
- [RBAC Model](#-rbac-model)
- [Cleanup](#-cleanup)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

This demo provides a hands-on exploration of Snowflake's modern data platform using a realistic restaurant business scenario. The notebook creates a complete data environment including:

- **4 restaurant locations** across Tuscany (Firenze, Siena, Lucca, Pisa)
- **Full menu system** with categories, items, and dietary information
- **Wine inventory** featuring authentic Tuscan wines
- **Alpine spring water** products with mineral content analysis
- **Customer loyalty program** with tiered memberships
- **Order processing** with CDC pipelines and real-time analytics

---

## ✨ Features Demonstrated

| Category | Snowflake Features |
|----------|-------------------|
| **Table Types** | Permanent, Transient, Temporary, Hybrid |
| **View Types** | Standard, Secure, Materialized |
| **Open Formats** | Apache Iceberg Tables (Internal Catalog) |
| **Data Loading** | Internal Stages, File Formats (CSV, JSON, Parquet), COPY INTO |
| **Programmability** | Java Stored Procedures, Python Stored Procedures |
| **Extensibility** | Python User Defined Functions (UDFs) |
| **CDC & Automation** | Streams, Tasks, Scheduled Jobs |
| **Real-time Analytics** | Dynamic Tables with configurable lag |
| **Security** | Role-Based Access Control (RBAC) |

---

## 📦 Prerequisites

### Snowflake Account Requirements

- Snowflake account with `ACCOUNTADMIN` role access
- Enterprise Edition or higher (for some features like Hybrid Tables)
- Sufficient credits for warehouse usage

### Optional: External Volume for Iceberg

For full Apache Iceberg functionality, configure an external volume. The demo includes alternative standard table syntax if external volumes are not available.

### Recommended Tools

- [Snowflake Web UI](https://app.snowflake.com) (Snowsight)
- [VS Code](https://code.visualstudio.com/) with Snowflake Extension
- Jupyter Notebook / JupyterLab

---

## 🚀 Quick Start

### Option 1: Snowflake Notebooks (Recommended)

1. Log into your Snowflake account
2. Navigate to **Notebooks** in Snowsight
3. Click **Import from file**
4. Upload `il_giro_de_fito_snowflake_demo.ipynb`
5. Run cells sequentially from the beginning

### Option 2: SQL Worksheets

1. Open Snowsight and create a new SQL Worksheet
2. Copy and paste SQL code from each notebook cell
3. Execute in order, starting with infrastructure setup

### Option 3: Local Jupyter

```bash
# Clone the repository
git clone https://github.com/your-username/il-giro-de-fito-snowflake-demo.git
cd il-giro-de-fito-snowflake-demo

# Install Snowflake connector (optional, for local execution)
pip install snowflake-connector-python snowflake-snowpark-python

# Open the notebook
jupyter notebook il_giro_de_fito_snowflake_demo.ipynb
```

---

## 📁 Project Structure

```
il-giro-de-fito-snowflake-demo/
│
├── README.md                              # This file
├── il_giro_de_fito_snowflake_demo.ipynb   # Main demo notebook
└── LICENSE                                # License file (optional)
```

### Snowflake Objects Created

```
GIRODEFITO (Database)
└── PROD (Schema)
    ├── Tables
    │   ├── LOCATIONS                    [Permanent]
    │   ├── MENU_CATEGORIES              [Permanent]
    │   ├── MENU_ITEMS                   [Permanent]
    │   ├── CUSTOMERS                    [Permanent]
    │   ├── STAFF                        [Permanent]
    │   ├── ORDERS                       [Permanent]
    │   ├── ORDER_ITEMS                  [Permanent]
    │   ├── WINE_INVENTORY               [Permanent]
    │   ├── SPRING_WATER_PRODUCTS        [Permanent]
    │   ├── ORDERS_FROM_STAGE            [Permanent]
    │   ├── ORDERS_STAGING               [Transient]
    │   ├── DAILY_METRICS_STAGING        [Transient]
    │   ├── ETL_CONTROL_LOG              [Transient]
    │   ├── RESERVATIONS                 [Hybrid]
    │   ├── KITCHEN_QUEUE                [Hybrid]
    │   ├── ACTIVE_PAYMENT_SESSIONS      [Hybrid]
    │   ├── ORDER_CHANGE_HISTORY         [Permanent]
    │   ├── INVENTORY_ALERTS             [Permanent]
    │   └── ICE_*_READY                  [Iceberg-ready]
    │
    ├── Views
    │   ├── V_MENU_COMPLETE              [Standard]
    │   ├── V_LOCATION_SUMMARY           [Standard]
    │   ├── V_WINE_LIST                  [Standard]
    │   ├── V_CUSTOMER_LOYALTY           [Standard]
    │   ├── V_SECURE_REVENUE_REPORT      [Secure]
    │   ├── V_SECURE_CUSTOMER_ANALYTICS  [Secure]
    │   ├── V_SECURE_MENU_PRICING        [Secure]
    │   ├── MV_DAILY_SALES_SUMMARY       [Materialized]
    │   ├── MV_MENU_ITEM_PERFORMANCE     [Materialized]
    │   └── MV_INVENTORY_STATUS          [Materialized]
    │
    ├── Dynamic Tables
    │   ├── DT_SALES_DASHBOARD           [5 min lag]
    │   ├── DT_MENU_RANKINGS             [10 min lag]
    │   ├── DT_CUSTOMER_LTV              [30 min lag]
    │   └── DT_WINE_INVENTORY_STATUS     [15 min lag]
    │
    ├── Streams
    │   ├── STREAM_ORDERS_CDC
    │   ├── STREAM_CUSTOMERS_CDC
    │   └── STREAM_WINE_INVENTORY_CDC
    │
    ├── Tasks
    │   ├── TASK_PROCESS_ORDER_CHANGES   [5 min]
    │   └── TASK_CHECK_WINE_INVENTORY    [30 min]
    │
    ├── Stages
    │   ├── STG_DATA_LOAD
    │   ├── STG_JSON_DATA
    │   └── STG_CSV_DATA
    │
    ├── File Formats
    │   ├── FF_CSV
    │   ├── FF_JSON
    │   └── FF_PARQUET
    │
    ├── Stored Procedures
    │   ├── SP_CALCULATE_ORDER_STATS_JAVA      [Java]
    │   ├── SP_GENERATE_DAILY_REPORT_PYTHON    [Python]
    │   └── SP_WINE_REORDER_ALERT_PYTHON       [Python]
    │
    └── User Defined Functions
        ├── UDF_CALCULATE_LOYALTY_POINTS       [Python]
        ├── UDF_WINE_PAIRING                   [Python]
        ├── UDF_FORMAT_CURRENCY_IT             [Python]
        └── UDF_SEASONAL_MENU_FLAG             [Python]

GIRODEFITO_WH (Warehouse - SMALL)

Roles
├── GIRODEFITO_ADMIN
└── GIRODEFITO_USER
```

---

## 📖 Demo Sections

### 1️⃣ Environment Setup
Creates the database (`GIRODEFITO`), schema (`PROD`), and virtual warehouse (`GIRODEFITO_WH` - SMALL size).

### 2️⃣ RBAC Configuration
Implements two roles with distinct privilege levels:
- **GIRODEFITO_ADMIN**: Full DDL/DML access, warehouse control
- **GIRODEFITO_USER**: Read-only access for reporting

### 3️⃣ Native Tables
Demonstrates all four Snowflake table types:
- **Permanent**: Core business entities with full Time Travel and Fail-safe
- **Transient**: ETL staging tables with reduced storage costs
- **Temporary**: Session-scoped working tables
- **Hybrid**: OLTP-optimized tables with row-level locking

### 4️⃣ Native Views
Showcases all three view types:
- **Standard**: Regular views with visible definitions
- **Secure**: Views with hidden definitions for data sharing
- **Materialized**: Pre-computed results for performance

### 5️⃣ Apache Iceberg Tables
Creates Iceberg-compatible table structures for open format interoperability.

### 6️⃣ Internal Stages & COPY INTO
Demonstrates bulk data loading:
- Stage creation with directory tables
- File format definitions (CSV, JSON, Parquet)
- Data export and import via COPY INTO

### 7️⃣ Stored Procedures
Server-side logic implementation:
- **Java**: Order statistics calculation
- **Python**: Daily report generation, wine reorder alerts

### 8️⃣ User Defined Functions
Custom Python UDFs:
- Loyalty points calculator with tier multipliers
- Wine pairing recommendations
- Italian currency formatting
- Seasonal menu flagging

### 9️⃣ Streams and Tasks
CDC and automation:
- Streams capture INSERT/UPDATE/DELETE on key tables
- Tasks process changes on schedule or when data arrives

### 🔟 Dynamic Tables
Declarative data pipelines:
- Sales dashboard (5-minute refresh)
- Menu rankings (10-minute refresh)
- Customer LTV (30-minute refresh)
- Wine inventory status (15-minute refresh)

### 1️⃣1️⃣ Demo Queries
Sample analytical queries demonstrating:
- Executive dashboard metrics
- Menu with wine pairings
- Spring water mineral analysis

### 1️⃣2️⃣ Cleanup
Optional section to remove all demo objects.

---

## 🗃️ Sample Data

The demo includes realistic Italian restaurant data:

### 🏪 Locations (4)
| Location | City | Capacity |
|----------|------|----------|
| Il Giro de Fito - Firenze | Florence | 80 seats |
| Il Giro de Fito - Siena | Siena | 60 seats |
| Il Giro de Fito - Lucca | Lucca | 50 seats |
| Il Giro de Fito - Pisa | Pisa | 70 seats |

### 🍝 Menu Categories (8)
Antipasti, Primi - Pasta, Primi - Risotto, Pizza, Secondi, Contorni, Dolci, Bevande

### 🍷 Wine Selection
| Wine | Type | Region | Vintage |
|------|------|--------|---------|
| Brunello di Montalcino Riserva | Red | Toscana | 2016 |
| Chianti Classico Gran Selezione | Red | Toscana | 2018 |
| Vernaccia di San Gimignano | White | Toscana | 2022 |
| Vin Santo del Chianti | Dessert | Toscana | 2015 |
| Prosecco Superiore DOCG | Sparkling | Veneto | 2022 |

### 💧 Alpine Spring Water
Sourced from the Dolomites with detailed mineral content (calcium, magnesium, sodium).

### 👥 Customer Loyalty Tiers
| Tier | Points Required | Multiplier |
|------|-----------------|------------|
| Bronze | 0 - 999 | 1.0x |
| Silver | 1,000 - 2,499 | 1.25x |
| Gold | 2,500 - 4,999 | 1.5x |
| Platinum | 5,000+ | 2.0x |

---

## 🔐 RBAC Model

```
ACCOUNTADMIN
    │
    └── SYSADMIN
            │
            └── GIRODEFITO_ADMIN
                    │
                    ├── Full warehouse control (USAGE, OPERATE, MODIFY)
                    ├── All DDL operations (CREATE, ALTER, DROP)
                    ├── All DML operations (SELECT, INSERT, UPDATE, DELETE)
                    ├── Execute stored procedures
                    └── GIRODEFITO_USER (inherited)
                            │
                            ├── Warehouse USAGE only
                            ├── SELECT on all tables
                            ├── SELECT on all views
                            └── SELECT on all dynamic tables
```

---

## 🧹 Cleanup

To remove all demo objects, uncomment and run the cleanup section in the notebook:

```sql
USE ROLE ACCOUNTADMIN;

-- Suspend tasks first
ALTER TASK GIRODEFITO.PROD.TASK_PROCESS_ORDER_CHANGES SUSPEND;
ALTER TASK GIRODEFITO.PROD.TASK_CHECK_WINE_INVENTORY SUSPEND;

-- Drop database (cascades all objects)
DROP DATABASE IF EXISTS GIRODEFITO CASCADE;

-- Drop warehouse
DROP WAREHOUSE IF EXISTS GIRODEFITO_WH;

-- Drop roles
DROP ROLE IF EXISTS GIRODEFITO_ADMIN;
DROP ROLE IF EXISTS GIRODEFITO_USER;
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Snowflake Documentation and Community
- Authentic Italian culinary traditions from Tuscany
- The beautiful wines of the Chianti and Montalcino regions

---

<p align="center">
  <strong>🍝 Buon appetito e buon lavoro con Snowflake! 🍷</strong>
  <br>
  <em>Il Giro de Fito - Tradizione Toscana dal 2018</em>
</p>
