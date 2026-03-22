  <img src="https://img.shields.io/badge/Meltano-3A30C3?style=for-the-badge&logo=meltano&logoColor=white" alt="Meltano" />
  <img src="https://img.shields.io/badge/Google_BigQuery-669DF6?style=for-the-badge&logo=google-bigquery&logoColor=white" alt="BigQuery" />
  <img src="https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white" alt="dbt" />
  <img src="https://img.shields.io/badge/DuckDB-FFF044?style=for-the-badge&logo=duckdb&logoColor=black" alt="DuckDB" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas" />

## Project Overview
This project builds an end-to-end analytics pipeline on the Olist Brazilian e-commerce dataset,
transforming raw CSV files into analytics-ready fact and dimension tables using dbt and BigQuery.

The goal is to analyse order growth, customer purchasing behaviour, and delivery performance
using production-style data modelling, testing, and validation.

## Data Source
- **Dataset:** Olist Brazilian E-commerce Dataset (Kaggle)
- **Period:** 2016–2018
- **Size:** ~100k orders, ~99k customers, ~33k products
- **Granularity:** Order-level transactional data
  
## Architecture

```mermaid
flowchart LR
A[Kaggle CSV Files] --> B[Meltano ELT]

subgraph Local_Development
B --> C[DuckDB]
end

subgraph Data_Warehouse
B --> D[BigQuery olist_raw]
D --> E[dbt Staging Models]
E --> F[dbt Snapshots SCD2]
F --> G[dbt Marts Facts Dimensions]
end

G --> H[Python Pandas Analysis]
```

## Data Modelling

### Staging Layer
- One-to-one mappings from raw tables
- Type casting and standardised column names

### Snapshots
- SCD Type 2 tracking for:
  - Customers
  - Products
- Preserves historical attribute changes over time

### Marts
**Dimensions**
- dim_customers
- dim_products
- dim_sellers
- dim_geolocation

**Facts**
- fct_orders
- fct_order_items
- fct_payments
- fct_reviews

## Data Quality & Testing

dbt tests were implemented across staging and mart layers:
- Primary key uniqueness
- Not-null constraints
- Foreign key relationship tests between facts and dimensions

All tests pass successfully, ensuring referential integrity and analytical reliability.

## Analysis Highlights

- Monthly order volume grew steadily from 2016 to late 2017 before plateauing
- Over 90% of customers placed only one order, indicating low repeat purchase behaviour
- Median delivery time was ~10 days, with a long tail of delayed deliveries
- Late deliveries represented a small but significant minority of total orders

## Tech Stack
- **Data Ingestion:** Meltano
- **Data Warehouse:** BigQuery
- **Transformations:** dbt
- **Data Modelling:** Star schema (facts & dimensions)
- **Analysis:** Python, Pandas, Seaborn, Matplotlib
- **Version Control:** Git & GitHub

## 📄 License

This project was developed as a Data Pipeline Project for Data Science & AI certification, in collaboration with Farida, Leslie, Taufiq, and Wilson.