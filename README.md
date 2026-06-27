# E-commerce Data Analytics Pipeline

An end-to-end analytics project covering data cleaning, feature engineering, Python-based business analysis, and SQL querying on a PostgreSQL database.

> **Note:** The dataset used in this project is synthetically generated for learning and portfolio purposes. It does not represent real-world transaction data.

---

## Project Overview

This project simulates a realistic analytics workflow for an e-commerce business. Starting from raw CSV files, it builds a clean, enriched master dataset and answers business questions using both Python and SQL.

**Dataset:** 5,000 orders | 200 customers | 3 source tables (customers, products, orders)

---

## Tech Stack

- Python (Pandas, NumPy, Matplotlib, Seaborn)
- Jupyter Notebooks
- PostgreSQL (Neon) via psycopg2 and SQLAlchemy

---

## Repository Structure

```
data/
  raw/              # Original CSV files
  processed/        # Cleaned and enriched outputs
notebooks/
  clean_customers.ipynb
  clean_products.ipynb
  clean_orders.ipynb
  analytics.ipynb
  sql_analysis.ipynb
requirements.txt
```

---

## Pipeline

```
Raw CSVs  →  Data Cleaning  →  Feature Engineering  →  Master Dataset  →  Python Analysis  →  SQL Analysis (PostgreSQL)
```

Each source table is cleaned separately, then merged into a single `orders_master` table used for all downstream analysis.

---

## Key Findings

| Area | Finding |
|---|---|
| Total Revenue | 620,007.31 |
| Top Revenue Category | Electronics |
| Overall Return Rate | 8.10% |
| Highest LTV Segment | Gold membership tier |
| Avg. Days to Second Purchase | 37 days |

---

## What Each Notebook Does

**clean_customers.ipynb** : Validates age, signup dates, and categorical fields. Engineers `tenure_days`, `tenure_months`, `age_group`, and `signup_year`.

**clean_products.ipynb** : Computes product economics including `profit`, `margin`, `inventory_cost`, `inventory_risk`, and `price_bucket`.

**clean_orders.ipynb** : Cleans order records, imputes missing discounts, and derives `revenue = quantity × unit_price × (1 - discount)`.

**analytics.ipynb** : Merges all three datasets into `orders_master`. Analyzes revenue by category, membership tier value, region performance, return impact, and customer lifetime value.

**sql_analysis.ipynb** : Loads data into PostgreSQL and runs business queries: top customers by LTV, month-over-month revenue growth, high return-rate products, repeat purchase rate by tier, average days to second purchase, best-selling product by region, and cohort analysis by signup month.

---

## Business Questions Answered

- Which customer segments generate the most lifetime value?
- How does revenue trend month-over-month?
- Which product categories have the highest return rates?
- Which regions contribute most to revenue?
- How quickly do customers make a second purchase?
- Do older customer cohorts produce stronger cumulative revenue?

---

## How to Run

```bash
git clone https://github.com/Gurpreet0022/Ecommerce-Analytics.git
cd Ecommerce-Analytics
python -m venv venv
.\venv\Scripts\Activate.ps1        # Windows
pip install -r requirements.txt
```

Run notebooks in this order:

1. `notebooks/clean_customers.ipynb`
2. `notebooks/clean_products.ipynb`
3. `notebooks/clean_orders.ipynb`
4. `notebooks/analytics.ipynb`
5. `notebooks/sql_analysis.ipynb`

---

## Skills Demonstrated

- Data cleaning and validation across multiple source tables
- Feature engineering for business metrics (margin, inventory risk, tenure, LTV)
- Multi-table merging and master dataset creation
- Exploratory and descriptive analytics with Python
- SQL window functions, cohort analysis, and MoM growth queries on PostgreSQL
