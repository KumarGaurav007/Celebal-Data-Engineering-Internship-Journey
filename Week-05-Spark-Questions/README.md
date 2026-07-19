<div align="center">
  <h1>🔥 Week 05 — Apache Spark & PySpark</h1>
  <p><strong>Distributed Data Processing, Data Cleaning & Big Data Analytics</strong></p>
  <p>
    <img src="https://img.shields.io/badge/Spark-3.x-E25A1C?logo=apachespark&logoColor=white" alt="Spark">
    <img src="https://img.shields.io/badge/Python-3.14-3776AB?logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white" alt="Jupyter">
    <img src="https://img.shields.io/badge/Status-Completed-success" alt="Status">
  </p>
  <p>
    <a href="#-overview">Overview</a> •
    <a href="#-dataset">Dataset</a> •
    <a href="#-questions-breakdown">Questions</a> •
    <a href="#-key-concepts">Key Concepts</a> •
    <a href="#-how-to-run">How to Run</a>
  </p>
</div>

---

## 📌 Overview

This week introduces **Apache Spark** — the industry-standard distributed computing engine for big data. Using **PySpark**, 15 hands-on questions are solved covering the complete Spark workflow: from understanding its architecture and advantages over MapReduce, through DataFrame operations, data cleaning, transformations, and aggregations.

**Objective:** Build proficiency in processing large-scale data using Spark's in-memory computing engine and PySpark DataFrame API.

---

## 📊 Dataset

| Detail | Value |
|--------|-------|
| **File** | [`data/sample-dataset.csv`](data/sample-dataset.csv) |
| **Format** | Synthetic sales data |
| **Records** | 1,000 |
| **Columns** | 14 |

| Column | Type | Description |
|--------|------|-------------|
| `user_id` | Integer | Unique user identifier |
| `transaction_date` | String | Date of transaction |
| `region` | String | Geographic region |
| `product_category` | String | Product category |
| `sale_amount` | Float | Transaction amount |
| `price` | Float | Product price |
| `city` | String | Customer city |
| `status` | String | Order status (nullable) |
| `email` | String | Customer email (nullable) |
| `username` | String | Customer username (nullable) |
| `age` | Integer | Customer age |
| `subscription` | String | Subscription plan |
| `store_id` | Integer | Store identifier |
| `raw_timestamp` | String | Raw timestamp string |

---

## ❓ Questions Breakdown

### 🔹 Spark Fundamentals (Q1–Q2)

| # | Question | Key Concept |
|---|----------|-------------|
| **Q1** | Explain MapReduce limitations & how Spark overcomes them | MapReduce vs Spark comparison — disk I/O, DAG, in-memory |
| **Q2** | Why does Spark suit iterative ML algorithms? | In-memory computing avoids repeated disk I/O |

### 🔹 DataFrame Operations (Q3–Q8, Q12)

| # | Question | Technique |
|---|----------|-----------|
| **Q3** | Remove duplicate rows based on `user_id` + `transaction_date` | `dropDuplicates(subset=[...])` |
| **Q4** | For West region, avg `sale_amount` per `product_category` | `filter` → `groupBy` → `agg(avg())` |
| **Q6** | List cities with more than 100 transactions | `groupBy("city")` → `count()` → `filter(count > 100)` |
| **Q7** | Drop `username` column & rename `subscription` → `plan` | `.drop()`, `.withColumnRenamed()` |
| **Q8** | Filter users age 18–30 with Premium subscription | Multi-condition `filter((col1) & (col2))` |
| **Q12** | Remove rows where email is null OR username is empty | `filter(col("email").isNotNull() & (col("username") != ""))` |

### 🔹 Null Handling & Cleanup (Q5, Q9, Q14)

| # | Question | Technique |
|---|----------|-----------|
| **Q5** | Compare `.na.drop()` vs `.na.fill()` — fill null in `status` | `df.na.fill("Unknown", subset=["status"])` |
| **Q9** | Handle nulls before mathematical aggregations | Drop or fill nulls → `groupBy().agg()` |
| **Q14** | Risks of `inferSchema=true` with inconsistent date formats | Schema inference pitfalls with mixed formats |

### 🔹 Advanced Transformations (Q10–Q11, Q13, Q15)

| # | Question | Technique |
|---|----------|-----------|
| **Q10** | Cast `raw_timestamp` to `TimestampType` → rename `event_time` | `.withColumn("event_time", col("raw_timestamp").cast("timestamp"))` |
| **Q11** | Explain Shuffle process & Wide Transformations | Narrow vs Wide transformations, shuffle boundaries |
| **Q13** | Compute min, max, avg of `price` in one go | `.agg(min("price"), max("price"), avg("price"))` |
| **Q15** | Complete pipeline: dedup → fill null prices → groupBy store revenue | End-to-end DataFrame pipeline |

---

## 🧠 Key Concepts

| Concept | Description |
|---------|-------------|
| **In-Memory Computing** | Data cached in memory across nodes — 10–100x faster than disk-based MapReduce |
| **DAG Scheduler** | Directed Acyclic Graph optimizes execution plan, reducing unnecessary I/O |
| **Lazy Evaluation** | Transformations build a logical plan; actions trigger execution |
| **Narrow vs Wide Transformations** | Narrow = no shuffle (map, filter); Wide = shuffle needed (groupBy, join) |
| **Shuffle** | Data redistribution across partitions — expensive but necessary for grouping |
| **DataFrame API** | Higher-level abstraction over RDDs with built-in optimizations (Catalyst, Tungsten) |
| **Schema Inference** | Automatic type detection — convenient but risky with messy data |

---

## 🚀 How to Run

```bash
# 1. Activate virtual environment
.\venv\Scripts\Activate.ps1     # Windows
source venv/bin/activate         # macOS / Linux

# 2. Launch Jupyter
jupyter notebook

# 3. Open Spark-Questions.ipynb
```

> **Note:** PySpark is configured within the virtual environment. Ensure `SPARK_HOME` is set if running outside the provided venv.

---

## 📁 Files

| File | Description |
|------|-------------|
| [`Spark-Questions.ipynb`](Spark-Questions.ipynb) | Main notebook with all 15 questions & solutions |
| [`data/sample-dataset.csv`](data/sample-dataset.csv) | Synthetic dataset (1,000 records, 14 columns) |
| [`PySpark-Assignment-report.pdf`](PySpark-Assignment-report.pdf) | Formatted PDF report of the assignment |
| [`README.md`](README.md) | You are here |

---

## ✅ Key Takeaways

- ⚡ Spark's **in-memory computing** fundamentally outperforms disk-based MapReduce for iterative workloads
- 🧹 PySpark DataFrame API provides **Pandas-like syntax** with distributed execution
- 🚨 **Null handling** is critical before aggregation — missing values silently produce incorrect results
- 🔄 **Wide transformations** trigger expensive shuffles — design queries to minimize data movement
- 🏗️ **End-to-end pipelines** (dedup → clean → aggregate) demonstrate real-world Spark workflows

---

<div align="center">
  <p>
    <sub>Built with ❤️ for the Celebal Data Engineering Internship</sub>
    <br>
    <sub>Author: <a href="https://github.com/KumarGaurav007">Gaurav Kumar</a></sub>
  </p>
</div>
