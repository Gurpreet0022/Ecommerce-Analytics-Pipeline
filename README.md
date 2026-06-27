# E-commerce Data Analytics Project

This project builds an end-to-end analytics workflow for an e-commerce dataset.
It starts from raw CSV files, performs data cleaning and feature engineering, creates a combined master dataset, and then runs both Python and SQL-based business analysis.

## Project Goals

- Clean and validate customer, product, and order data.
- Engineer business-ready features for analytics.
- Build a single integrated dataset for reporting.
- Generate insights on revenue, profit, returns, customer value, and retention.
- Perform advanced SQL analysis, including cohort-style analysis.

## Tech Stack

- Python (Pandas, NumPy, Matplotlib, Seaborn)
- Jupyter Notebooks
- PostgreSQL (Neon) via psycopg2 and SQLAlchemy

## Repository Structure

```text
requirements.txt
data/
  raw/
    customers.csv
    orders.csv
    products.csv
  processed/
    customers_enriched.csv
    orders_enriched.csv
    products_enriched.csv
    orders_master.csv
notebooks/
  clean_customers.ipynb
  clean_products.ipynb
  clean_orders.ipynb
  analytics.ipynb
  sql_analysis.ipynb
```

## Data Pipeline Overview

1. Clean each source dataset separately:
   - customers
   - products
   - orders
2. Engineer useful business columns in each cleaned dataset.
3. Save cleaned outputs to data/processed.
4. Merge datasets into orders_master.
5. Run descriptive analytics in Python notebooks.
6. Run SQL business queries in PostgreSQL.

## Notebook-by-Notebook Summary

### 1) clean_customers.ipynb

Main work done:
- Loads raw customer data.
- Performs null/duplicate checks and validation for age and signup_date.
- Validates categorical consistency (gender, membership_tier, city, region).
- Creates features:
  - signup_year
  - tenure_days
  - tenure_months
  - age_group
- Adds visual analysis and numeric summaries for:
  - age-group distribution
  - membership-tier distribution
  - yearly signup growth
  - tenure distribution

Output:
- data/processed/customers_enriched.csv

### 2) clean_products.ipynb

Main work done:
- Loads raw products data.
- Checks nulls, duplicates, and value consistency.
- Creates product economics features:
  - profit
  - margin
  - inventory_cost
  - inventory_revenue
  - inventory_risk
  - inventory_risk_label
  - price_bucket
- Adds category-level insights and charts for:
  - profit concentration
  - pricing power
  - inventory capital allocation
  - risky inventory exposure

Output:
- data/processed/products_enriched.csv

### 3) clean_orders.ipynb

Main work done:
- Loads raw orders data.
- Converts order_date to datetime.
- Removes duplicates.
- Imputes missing discount values with 0.
- Validates status, region, and quantity consistency.
- Creates revenue feature:
  - revenue = quantity * unit_price * (1 - discount)
- Adds charts and metrics for:
  - return rate
  - region-wise revenue
  - order status distribution
  - top products by revenue

Output:
- data/processed/orders_enriched.csv

### 4) analytics.ipynb

Main work done:
- Loads the three enriched datasets.
- Merges them into one analytical dataset.
- Performs quality checks after merge.
- Builds business analysis with charts + numeric interpretation:
  - revenue and profit by category
  - membership tier value
  - region performance
  - return impact by category
  - top products by revenue
  - inventory risk vs revenue
  - price sensitivity by price_bucket
  - customer lifetime value table

Output:
- data/processed/orders_master.csv

### 5) sql_analysis.ipynb

Main work done:
- Connects to PostgreSQL (Neon).
- Creates customers, products, and orders tables.
- Inserts data from processed CSVs.
- Executes SQL business queries such as:
  - top customers by lifetime value
  - month-over-month revenue growth
  - high return-rate products
  - repeat purchase rate by membership tier
  - average days to second purchase
  - best-selling product by region
  - cohort summary by signup month and order month
- Documents findings in markdown after query outputs.

## How to Run

## 1) Clone and enter project

```bash
git clone <your-repo-url>
cd Ecommerce
```

## 2) Create and activate virtual environment

Windows PowerShell:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

## 3) Install dependencies

```bash
pip install -r requirements.txt
```

## 4) Run notebooks in this order

1. notebooks/clean_customers.ipynb
2. notebooks/clean_products.ipynb
3. notebooks/clean_orders.ipynb
4. notebooks/analytics.ipynb
5. notebooks/sql_analysis.ipynb

This ensures processed files exist before downstream notebooks are executed.

## Key Engineered Columns

- Customers:
  - signup_year
  - tenure_days
  - tenure_months
  - age_group
- Products:
  - profit
  - margin
  - inventory_cost
  - inventory_revenue
  - inventory_risk
  - inventory_risk_label
  - price_bucket
- Orders:
  - revenue

## Business Questions Answered

- Which customer segments generate the most lifetime value?
- How does revenue trend month-over-month?
- Which products have high return rates?
- Which regions contribute most to revenue and profit?
- How quickly do customers make a second purchase?
- Do older customer cohorts produce stronger cumulative revenue?

## Outcome

This project demonstrates a full analytics lifecycle:
- data wrangling,
- feature engineering,
- integrated dataset creation,
- exploratory and business analytics,
- SQL-based decision support.
