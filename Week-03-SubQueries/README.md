# Week 3 — SQL Subqueries & Advanced Analytics

<p align="center">
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Database-MySQL-blue?style=for-the-badge&logo=mysql"/>
  <img src="https://img.shields.io/badge/Domain-Data_Engineering-ff6f00?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Internship-Celebal_Technologies-purple?style=for-the-badge"/>
</p>

---

##  Project Overview

This week focuses on mastering **SQL Subqueries**, **Common Table Expressions (CTEs)**, and **Window Functions** using the **Superstore E-Commerce Dataset**. The dataset is normalized into a relational schema and analyzed to extract actionable business insights.

---

##  Dataset

| Detail | Value |
|--------|-------|
| **Source** | Sample Superstore (CSV) |
| **Rows** | 9,994 |
| **Period** | 2014 – 2017 |
| **Geography** | United States |

---

##  Database Schema

The raw data was normalized into **4 tables** inside `subqueries_sql`:

```
subqueries_sql/
├── superstore_raw      # Raw denormalized import
├── customers           # Customer details (PK: customer_id)
├── orders              # Order transactions (PK: order_id, FK: customer_id)
└── products            # Product catalog (PK: product_id)
```

---

##  Notebooks

### 1. `DB-setup.ipynb` — Database Setup
- Creates MySQL database and imports CSV via Pandas + SQLAlchemy
- Normalizes data into `customers`, `orders`, and `products` tables

### 2. `Queries.ipynb` — SQL Concepts & Queries

| Query | Concept |
|-------|---------|
| Orders with sales > average | **Scalar Subquery** |
| Highest-sales order per customer | **Correlated Subquery** |
| Total sales per customer | **CTE** |
| Customers with above-avg sales | **CTE + Subquery** |
| Rank customers by total sales | **Window Function (RANK)** |
| Row numbers per customer orders | **Window Function (ROW_NUMBER + PARTITION BY)** |
| Top 3 customers by sales | **CTE + Window Function + Filter** |

### 3. `Customer-Sales-Insight.ipynb` — Mini Project

| Business Question | Technique |
|-------------------|-----------|
| Who are the **Top 5** customers? | CTE + LIMIT |
| Who are the **Bottom 5** customers? | CTE + ASC LIMIT |
| Which customers placed **only one** order? | GROUP BY + HAVING |
| Which customers have **above-average** sales? | CTE + Subquery |
| What is the **highest order value** per customer? | GROUP BY + MAX() |

---

##  Key Findings

| Insight | Value |
|---------|-------|
|  ️ **Top Customer** | Sean Miller ($25,043) |
|   **Bottom Customer** | Thais Sissman ($4.83) |
|   **Single-Order Customers** | 12 identified |
|   **Above-Average Customers** | 294 out of 793 |
|   **Avg Sales per Customer** | ~$2,889 |

---

##  Technologies Used

| Tool | Purpose |
|------|---------|
| **MySQL** | Relational database |
| **Python (Pandas, SQLAlchemy)** | Data import & connection |
| **Jupyter Notebook (ipython-sql)** | Interactive SQL execution |
| **JupySQL** | SQL magic in notebooks |

---

##  How to Run

```bash
# 1. Install dependencies
pip install pandas sqlalchemy pymysql ipython-sql jupysql

# 2. Start MySQL server and create the database
mysql -u root -p -e "CREATE DATABASE subqueries_sql;"

# 3. Run notebooks in order:
#    DB-setup.ipynb → Queries.ipynb → Customer-Sales-Insight.ipynb
```

---

<p align="center">
  <b>Celebal Technologies — Data Engineering Excellence Internship</b><br>
  <i>Author: Gaurav Kumar</i>
</p>
