<div align="center">
  <img src="https://img.shields.io/badge/Celebal%20Technologies-Excellence%20Internship-2A6E9B?style=for-the-badge" alt="Celebal Technologies">
  <h1>🗄️ Week 02 — SQL Basics</h1>
  <p><strong>E-Commerce Sales Database — Schema Design, Queries & Transactions</strong></p>
  <p>
    <img src="https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white" alt="MySQL">
    <img src="https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white" alt="Jupyter">
    <img src="https://img.shields.io/badge/Python-3.14-3776AB?logo=python&logoColor=white" alt="Python 3.14">
    <img src="https://img.shields.io/badge/Status-Complete-success" alt="Status">
  </p>
  <p>
    <a href="#-database-schema">Schema</a> •
    <a href="#-notebooks-breakdown">Notebooks</a> •
    <a href="#-assignment-questions">Questions</a> •
    <a href="#-how-to-run">How to Run</a>
  </p>
</div>

---

## 📌 Overview

This week focuses on **relational database design** and **SQL fundamentals** using MySQL. A fully normalized e-commerce database (`celebal_sql`) with 4 tables is built from scratch, populated with sample data, and queried across 5 sections covering the complete SQL spectrum — from basic `SELECT` statements to advanced transactions and ACID properties.

---

## 🏛️ Database Schema

### Entity Relationship

```
customers ──1:N──> orders ──1:N──> order_items
                                          ▲
products ──────────1:N────────────────────┘
```

### Tables

<details>
<summary><strong>📋 customers</strong> — 8 records</summary>

| Column | Type | Constraints |
|--------|------|-------------|
| `customer_id` | `INT` | `PRIMARY KEY` |
| `first_name` | `VARCHAR(50)` | `NOT NULL` |
| `last_name` | `VARCHAR(50)` | `NOT NULL` |
| `email` | `VARCHAR(100)` | `UNIQUE`, `NOT NULL` |
| `city` | `VARCHAR(50)` | `NOT NULL` |
| `state` | `VARCHAR(50)` | `NOT NULL` |
| `join_date` | `DATE` | `NOT NULL` |
| `is_premium` | `BOOLEAN` | `DEFAULT FALSE` |

*Indexes:* `idx_customers_city`, `idx_customers_state`
</details>

<details>
<summary><strong>📦 products</strong> — 8 records</summary>

| Column | Type | Constraints |
|--------|------|-------------|
| `product_id` | `INT` | `PRIMARY KEY` |
| `product_name` | `VARCHAR(100)` | `NOT NULL` |
| `category` | `VARCHAR(50)` | `NOT NULL` |
| `brand` | `VARCHAR(50)` | `NOT NULL` |
| `unit_price` | `DECIMAL(10,2)` | `NOT NULL`, `CHECK (unit_price > 0)` |
| `stock_qty` | `INT` | `NOT NULL DEFAULT 0`, `CHECK (stock_qty >= 0)` |

*Indexes:* `idx_products_category`
</details>

<details>
<summary><strong>📄 orders</strong> — 10 records</summary>

| Column | Type | Constraints |
|--------|------|-------------|
| `order_id` | `INT` | `PRIMARY KEY` |
| `customer_id` | `INT` | `NOT NULL`, `FOREIGN KEY → customers` |
| `order_date` | `DATE` | `NOT NULL` |
| `status` | `VARCHAR(20)` | `NOT NULL DEFAULT 'Pending'`, `CHECK (IN ('Pending','Shipped','Delivered','Cancelled'))` |
| `total_amount` | `DECIMAL(12,2)` | `NOT NULL`, `CHECK (total_amount >= 0)` |

*Indexes:* `idx_orders_date`, `idx_orders_status`
</details>

<details>
<summary><strong>🛒 order_items</strong> — 15 records</summary>

| Column | Type | Constraints |
|--------|------|-------------|
| `item_id` | `INT` | `PRIMARY KEY` |
| `order_id` | `INT` | `NOT NULL`, `FOREIGN KEY → orders` |
| `product_id` | `INT` | `NOT NULL`, `FOREIGN KEY → products` |
| `quantity` | `INT` | `NOT NULL`, `CHECK (quantity > 0)` |
| `unit_price` | `DECIMAL(10,2)` | `NOT NULL`, `CHECK (unit_price > 0)` |
| `discount_pct` | `DECIMAL(5,2)` | `DEFAULT 0`, `CHECK (0–100)` |
</details>

---

## 📓 Notebooks Breakdown

| Notebook | Focus | Questions |
|:--------:|-------|:---------:|
| [`DB-setup.ipynb`](DB-setup.ipynb) | Database creation, table DDL, indexes, sample data insertion | — |
| [`Section-A-SQL-Basics.ipynb`](Section-A-SQL-Basics.ipynb) | `SELECT`, `DISTINCT`, Primary Keys, `UNIQUE`, `NOT NULL`, `CHECK` constraints | Q1–Q6 |
| [`Section-B-Filtering & Optimization.ipynb`](Section-B-Filtering%20%26%20Optimization.ipynb) | `WHERE`, comparison/logical operators, `BETWEEN`, date filtering, indexes, SARGable queries | Q7–Q12 |
| [`Section-C -Aggregation.ipynb`](Section-C%20-Aggregation.ipynb) | `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `GROUP BY`, `HAVING` | Q13–Q19 |
| [`Section-D -Joins & Relationships.ipynb`](Section-D%20-Joins%20%26%20Relationships.ipynb) | `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, Foreign Keys, multi-table queries | Q20–Q23 |
| [`Section-E-Advanced-Concepts.ipynb`](Section-E-Advanced-Concepts.ipynb) | `CASE` statement, Transactions, `COMMIT`, `ROLLBACK`, ACID properties | Q24–Q27 |

---

## 🔍 Sample Queries

### Q1 — Retrieve all customers
```sql
SELECT * FROM customers;
```

### Q3 — List unique product categories
```sql
SELECT DISTINCT category FROM products;
```

### Q11 — Orders placed in August 2024
```sql
SELECT * FROM orders
WHERE order_date BETWEEN '2024-08-01' AND '2024-08-31';
```

### Q16 — Total revenue by status
```sql
SELECT status, SUM(total_amount) AS total_revenue
FROM orders
GROUP BY status;
```

### Q20 — Customer orders with INNER JOIN
```sql
SELECT c.first_name, c.last_name, o.order_id, o.total_amount
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id;
```

### Q24 — Product price tiers with CASE
```sql
SELECT product_name, unit_price,
  CASE
    WHEN unit_price < 1000   THEN 'Budget'
    WHEN unit_price <= 3000  THEN 'Mid-Range'
    ELSE                          'Premium'
  END AS price_tier
FROM products;
```

---

## ✅ Key Learnings

| Topic | Skills Acquired |
|-------|----------------|
| **DDL** | `CREATE TABLE`, `ALTER TABLE`, constraints (`PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`, `DEFAULT`) |
| **Indexing** | Creating indexes (`CREATE INDEX`) for query performance |
| **CRUD** | `INSERT`, `SELECT`, filtering with `WHERE`, `DISTINCT` |
| **Filtering** | Comparison operators, `BETWEEN`, `IN`, `LIKE`, date operations, SARGable query patterns |
| **Aggregation** | `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`, `GROUP BY`, `HAVING` |
| **Joins** | `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, Foreign Key relationships |
| **Conditional Logic** | `CASE` expressions for data categorization |
| **Transactions** | `START TRANSACTION`, `COMMIT`, `ROLLBACK` |
| **ACID** | Atomicity, Consistency, Isolation, Durability |

---

## 🚀 How to Run

```bash
# 1. Ensure MySQL is running locally

# 2. Activate the virtual environment
# Windows:
..\venv\Scripts\Activate.ps1
# macOS / Linux:
source ../venv/bin/activate

# 3. Launch Jupyter Notebook
jupyter notebook
```

Then open the notebooks in this order:
1. `DB-setup.ipynb` — creates the database, tables, and inserts sample data
2. `Section-A-SQL-Basics.ipynb` through `Section-E-Advanced-Concepts.ipynb` — in sequence

> **Note:** Update the MySQL connection string (`mysql://root:1234@localhost/celebal_sql`) in each notebook if your credentials differ.

---

<div align="center">
  <sub>Built with ❤️ by <a href="https://github.com/KumarGaurav007">Gaurav Kumar</a> for the Celebal Technologies Excellence Internship</sub>
</div>
