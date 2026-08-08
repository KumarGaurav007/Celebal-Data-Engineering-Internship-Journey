<div align="center">
  <h1>🚀 Celebal Data Engineering Internship Journey</h1>
  <p><strong>8 Weeks of Hands-On Data Engineering — From Python to Cloud & Big Data</strong></p>
  <p>
    <img src="https://img.shields.io/badge/Celebal%20Technologies-Excellence%20Internship-2A6E9B?style=for-the-badge" alt="Celebal Technologies">
  </p>
  <p>
    <img src="https://img.shields.io/badge/Python-3.12+-3776AB?logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white" alt="MySQL">
    <img src="https://img.shields.io/badge/Azure-Data%20Factory-0078D4?logo=microsoftazure&logoColor=white" alt="Azure">
    <img src="https://img.shields.io/badge/Spark-3.x-E25A1C?logo=apachespark&logoColor=white" alt="Spark">
    <img src="https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white" alt="Jupyter">
    <img src="https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white" alt="Pandas">
  </p>
  <p>
    <a href="#-about">About</a> •
    <a href="#-weekly-breakdown">Weekly Breakdown</a> •
    <a href="#-tech-stack">Tech Stack</a> •
    <a href="#-repo-structure">Structure</a> •
    <a href="#-quick-start">Quick Start</a>
  </p>
</div>

---

## 📌 About

| Detail | Info |
|--------|------|
| **Organization** | [Celebal Technologies](https://celebaltech.com) |
| **Program** | Excellence Internship Program |
| **Role** | Data Engineering Intern |
| **Duration** | 15 June 2026 – 15 August 2026 |
| **Intern** | [Gaurav Kumar](https://github.com/KumarGaurav007) |

This repository documents my **complete internship journey** — a progressive curriculum covering the entire data engineering stack:

> **Python & Pandas** → **SQL Fundamentals** → **Advanced SQL** → **Azure Cloud** → **Apache Spark** → **Databricks** → **Final Project**

Each week builds on the previous, starting from foundational data manipulation and moving into cloud infrastructure, big data processing, and finally a capstone project.

---

## 📅 Weekly Breakdown

<details>
<summary><strong>✅ Week 1 — Python & Pandas</strong> <code>Shopping Data Analysis</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Data exploration, cleaning & transformation with Pandas |
| **Dataset** | Myntra e-commerce product listings (24 columns) |
| **Notebook** | [`shopping_analysis.ipynb`](Week-01-Python-Pandas/shopping_analysis.ipynb) |

**Key Skills:**
- Data loading & inspection (`read_csv`, `head`, `info`, `describe`)
- Missing value treatment (6 columns filled with defaults)
- Data type conversion (string `₹1,299` → float)
- Feature engineering (`discount_amount = initial_price - final_price`)
- Filtering by rating, column selection, CSV export

🛠️ **Tech:** Python · Pandas · NumPy · Jupyter

</details>

<details>
<summary><strong>✅ Week 2 — SQL Basics</strong> <code>E-Commerce Database</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Relational DB design & SQL from SELECT to transactions |
| **Database** | `celebal_sql` — 4 tables (customers, products, orders, order_items) |
| **Notebooks** | 5 sections covering 27 questions |

**Key Skills:**
- DDL: `CREATE TABLE`, constraints (PK, FK, UNIQUE, CHECK, DEFAULT)
- CRUD: `SELECT`, `INSERT`, `WHERE`, `DISTINCT`
- Filtering: `BETWEEN`, `IN`, `LIKE`, SARGable queries
- Aggregation: `COUNT`, `SUM`, `AVG`, `GROUP BY`, `HAVING`
- Joins: `INNER`, `LEFT`, `RIGHT JOIN`
- Advanced: `CASE`, Transactions, `COMMIT`/`ROLLBACK`, ACID

📊 **Sample Query — Revenue by Status:**
```sql
SELECT status, SUM(total_amount) AS total_revenue
FROM orders
GROUP BY status;
```

🛠️ **Tech:** MySQL · Jupyter · ipython-sql

</details>

<details>
<summary><strong>✅ Week 3 — Advanced SQL & Subqueries</strong> <code>Superstore Analytics</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Subqueries, CTEs, Window Functions & analytical insights |
| **Dataset** | Superstore CSV (9,994 rows, US sales 2014–2017) |
| **Database** | `subqueries_sql` — 4 normalized tables |
| **Notebooks** | DB setup, 7 query concepts, mini project (5 questions) |

**Techniques Mastered:**

| Concept | Example |
|---------|---------|
| Scalar Subquery | Orders with sales > average |
| Correlated Subquery | Highest-sales order per customer |
| CTE | Total sales per customer |
| CTE + Subquery | Customers with above-avg sales |
| Window Function | `RANK()` customers by total sales |
| `ROW_NUMBER` + `PARTITION BY` | Rank orders per customer |
| CTE + Window + Filter | Top 3 customers by sales |

🔑 **Key Insight:** Top customer = *Sean Miller* ($25,043), 294 out of 793 above average.

🛠️ **Tech:** MySQL · Python (Pandas, SQLAlchemy, PyMySQL) · JupySQL

</details>

<details>
<summary><strong>✅ Week 4 — Azure Data Pipeline</strong> <code>Cloud ETL with ADF</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Cloud ETL pipeline using Azure Data Factory |
| **Services** | Resource Group · Storage Account · Blob Storage · ADF · IAM |
| **Activities** | Get Metadata + Copy Data |

**Pipeline Architecture:**
```
CSV File → Blob Storage → Linked Service → Source Dataset
    → Get Metadata → Copy Data → Destination Dataset → Output File
```

**Tasks Completed:**
| # | Task | Status |
|---|------|--------|
| 1 | Create Resource Group | ✅ |
| 2 | Storage Account & Blob Storage | ✅ |
| 3 | ADF Configuration (Linked Service, Datasets) | ✅ |
| 4 | Pipeline Development (Copy Data) | ✅ |
| 5 | Pipeline Execution & Monitoring | ✅ |
| 6 | IAM Role-Based Access Control | ✅ |

📸 17 screenshots documenting every step.

🛠️ **Tech:** Azure Portal · Data Factory · Blob Storage · RBAC

</details>

<details>
<summary><strong>✅ Week 5 — Apache Spark</strong> <code>PySpark Data Processing</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Spark fundamentals, PySpark DataFrames & data cleaning at scale |
| **Dataset** | Synthetic sales dataset (1,000 records, 14 columns) |
| **Notebook** | [`Spark-Questions.ipynb`](Week-05-Spark-Questions/Spark-Questions.ipynb) |
| **Report** | [PySpark Assignment Report](Week-05-Spark-Questions/PySpark-Assignment-report.pdf) |

**15 Questions Covering:**

| # | Concept |
|---|---------|
| Q1–Q2 | MapReduce vs Spark, In-Memory Computing |
| Q3 | `dropDuplicates()` on multiple columns |
| Q4 | Filter + groupBy + aggregation |
| Q5 | `.na.drop()` vs `.na.fill()` null handling |
| Q6 | groupBy + count + filter (cities > 100) |
| Q7 | DataFrame immutability (drop/rename) |
| Q8 | Multi-condition filtering (age 18–30 + Premium) |
| Q9 | Null-safe mathematical aggregations |
| Q10 | Timestamp casting (`raw_timestamp` → `event_time`) |
| Q11 | Shuffle process & Wide Transformations |
| Q12 | Filtering null/empty strings |
| Q13 | `.agg()` for multiple statistics |
| Q14 | `inferSchema=true` risks |
| Q15 | Complete pipeline: dedup → fill nulls → groupBy revenue |

🛠️ **Tech:** PySpark · findspark · Jupyter

</details>

<details>
<summary><strong>✅ Week 6 — PySpark Architecture & Components</strong> <code>Spark Execution Model</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Spark Architecture, Lazy Evaluation, DAG, DataFrame Operations & File Formats |
| **Dataset** | Synthetic sales dataset (1,000 records, 17 columns) |
| **Notebook** | [`Spark-Questions.ipynb`](Week-06-Spark-Assignment/Spark-Questions.ipynb) |

**15 Questions Covering:**

| # | Concept |
|---|---------|
| Q1 | Driver, Cluster Manager & Executor roles |
| Q2 | Lazy Evaluation & DAG optimization |
| Q3 | Reading CSV with `header=True`, `inferSchema=True` |
| Q4 | CSV (row-based) vs Parquet (columnar) storage |
| Q5 | Filter + Select (Electronics category) |
| Q6 | Rename column & cast data type |
| Q7 | Lineage Graph (DAG) fault tolerance |
| Q8 | Multi-condition filter with AND (`status=Completed AND amount>1000`) |
| Q9 | Predicate Pushdown in Parquet |
| Q10 | Add derived column (`final_price = base_price × 1.18`) |
| Q11 | Transformations vs Actions (`filter`/`select` vs `show`/`count`) |
| Q12 | Read Parquet → filter nulls → write CSV (ETL pipeline) |
| Q13 | Client Mode vs Cluster Mode |
| Q14 | Multi-condition filter with OR (`region=North OR priority=High`) |
| Q15 | `.show(5)` vs `.collect()` — memory safety |

🛠️ **Tech:** PySpark · Parquet · CSV · Jupyter

</details>

<details>
<summary><strong>✅ Week 7 — Python & Pandas Data Cleaning</strong> <code>Tableau Superstore</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | Python basics & a complete 7-step data-cleaning pipeline with Pandas/NumPy |
| **Dataset** | Tableau Sample – Superstore (9,994 rows, 21 columns) |
| **Notebook** | [`python_basics_data_cleaning.ipynb`](Week-07-Databricks/python_basics_data_cleaning.ipynb) |
| **Output** | [`superstore_cleaned.csv`](Week-07-Databricks/superstore_cleaned.csv) — 9,994 × 23 · 0 missing · 0 duplicates |

**7-Step Pipeline:**
| Step | Action |
|------|--------|
| 1 | Load CSV into a DataFrame (`read_csv`) |
| 2 | Explore (`head/tail/shape/columns/dtypes/info/describe`) |
| 3 | Handle missing values — `mode()` for categories/IDs, `median()` for `Sales` |
| 4 | Basic ops — boolean filtering (`&`), `loc` / `iloc` selection |
| 5 | Remove duplicates (`drop_duplicates()`) |
| 6 | Feature engineering — `Unit_Price`, `total_amount = price × quantity` |
| 7 | Save & verify (`to_csv` + reload check) |

**Key Numbers:** missing values `295 → 0` · duplicates `10 → 0` · median order ≈ **$54.40** · Consumer = largest segment (**5,191 orders**)

🛠️ **Tech:** Python · Pandas · NumPy · Jupyter

</details>

<details>
<summary><strong>✅ Week 8 — E-Commerce Order Analytics</strong> <code>Final Project</code></summary>
<br>

| Aspect | Details |
|--------|---------|
| **Topic** | End-to-end analytics pipeline: generate → clean → load → SQL → report → test |
| **Database** | SQLite (`ecommerce.db`), 4 tables, 500+ customers/products/orders |
| **Notebooks** | [`DB-Setup`](Week-08-ECommerce-Analytics/DB-Setup.ipynb) + [`Section A–F`](Week-08-ECommerce-Analytics) |
| **Reports** | [`issues_report.csv`](Week-08-ECommerce-Analytics/reports/issues_report.csv) |

**Sections:**
| Section | Focus |
|---------|-------|
| A | Synthetic data generation with intentional quality issues |
| B | Cleaning, normalization & validation |
| C | Basic SQL analytics (revenue, top 10 customers, monthly/status/regional) |
| D | Advanced SQL (CTEs, window functions, `RANK()`, `NTILE()`, `LAG()`) |
| E | Python–SQL integration & executive dashboard |
| F | 7 edge-case / data-quality tests |

**Data Quality Handled:** 12 missing customer IDs · 48 negative-quantity rows · invalid emails flagged.

🛠️ **Tech:** Python · Pandas · SQLite · SQL · Jupyter

</details>

---

## 🛠️ Tech Stack

| Category | Technologies |
|----------|-------------|
| **Languages** | ![Python](https://img.shields.io/badge/Python-3.12+-3776AB?logo=python&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-Standard-4479A1?logo=mysql&logoColor=white) |
| **Data Processing** | ![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458?logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-1.24+-013243?logo=numpy&logoColor=white) ![Spark](https://img.shields.io/badge/Spark-3.x-E25A1C?logo=apachespark&logoColor=white) |
| **Databases** | ![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?logo=mysql&logoColor=white) |
| **Cloud** | ![Azure](https://img.shields.io/badge/Azure-Data%20Factory%20%7C%20Blob%20Storage-0078D4?logo=microsoftazure&logoColor=white) |
| **Tools & Notebooks** | ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white) ![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?logo=visualstudiocode&logoColor=white) |
| **Libraries** | SQLAlchemy · PyMySQL · ipython-sql · JupySQL · findspark |

---

## 📂 Repo Structure

```
📦 Celebal-Data-Engineering-Internship-Journey
├── 📄 README.md                        ← You are here
├── 📄 requirements.txt                 ← Python dependencies
│
├── 📁 Week-01-Python-Pandas/           # Data cleaning & exploration
│   ├── shopping_analysis.ipynb
│   ├── data/Combined_dataset.csv
│   └── cleaned-data/cleaned_shopping_data.csv
│
├── 📁 Week-02-SQL-Basics/              # SQL fundamentals (27 queries)
│   ├── DB-setup.ipynb
│   ├── Section-A to Section-E notebooks
│   └── README.md
│
├── 📁 Week-03-SubQueries/              # Advanced SQL analytics
│   ├── Queries.ipynb
│   ├── Customer-Sales-Insight.ipynb
│   ├── data/Superstore.csv
│   └── README.md
│
├── 📁 Week-04-Azure-Data-Pipeline/     # Cloud ETL pipeline
│   ├── Azure-Data-Pipeline.ipynb
│   ├── data/Sample-Superstore.csv
│   ├── screenshots/ (17 images)
│   └── README.md
│
├── 📁 Week-05-Spark-Questions/         # PySpark big data processing
│   ├── Spark-Questions.ipynb
│   ├── data/sample-dataset.csv
│   ├── PySpark-Assignment-report.pdf
│   └── README.md
│
├── 📁 Week-06-Spark-Assignment/        # PySpark Architecture & DataFrame ops
│   ├── Spark-Questions.ipynb
│   ├── data/
│   └── README.md
│
├── 📁 Week-07-Databricks/              # Python & Pandas data cleaning
│   ├── python_basics_data_cleaning.ipynb
│   ├── sample.csv
│   ├── superstore_cleaned.csv
│   └── README.md
│
└── 📁 Week-08-ECommerce-Analytics/     # Final project — order analytics pipeline
    ├── DB-Setup.ipynb
    ├── Section-A to Section-F notebooks
    ├── data/ · reports/ · ecommerce.db
    └── README.md
```

---

## 🚀 Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/KumarGaurav007/Celebal-Data-Engineering-Internship-Journey.git
cd Celebal-Data-Engineering-Internship-Journey

# 2. Activate the virtual environment
.\venv\Scripts\Activate.ps1     # Windows
source venv/bin/activate         # macOS / Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch Jupyter
jupyter notebook
```

---

## 📈 Progress

```
Week 1 ████████████████████████ 100%  ✅ Python & Pandas
Week 2 ████████████████████████ 100%  ✅ SQL Basics
Week 3 ████████████████████████ 100%  ✅ Advanced SQL & Subqueries
Week 4 ████████████████████████ 100%  ✅ Azure Data Pipeline
Week 5 ████████████████████████ 100%  ✅ Apache Spark
Week 6 ████████████████████████ 100%  ✅ PySpark Architecture & Components
Week 7 ████████████████████████ 100%  ✅ Python & Pandas Data Cleaning
Week 8 ████████████████████████ 100%  ✅ E-Commerce Order Analytics
```

---

<div align="center">
  <p>
    <sub>Built with ❤️ by <a href="https://github.com/KumarGaurav007">Gaurav Kumar</a></sub>
    <br>
    <sub>Celebal Technologies — Data Engineering Excellence Internship</sub>
  </p>
</div>
