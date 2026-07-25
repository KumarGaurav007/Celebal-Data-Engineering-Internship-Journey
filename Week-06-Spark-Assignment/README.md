<div align="center">
  <h1>⚡ Week 06 — PySpark Architecture & Components</h1>
  <p><strong>Spark Architecture, Lazy Evaluation, DAG, DataFrame Operations & File Formats</strong></p>
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

This week dives deep into **Apache Spark's internal architecture** and its core components. Through 15 conceptual and practical questions, the assignment explores how Spark achieves distributed computing at scale — covering the Driver-Executor model, Lazy Evaluation, DAG-based fault tolerance, and the difference between CSV and Parquet formats.

**Objective:** Master Spark's execution model and perform efficient DataFrame transformations on large datasets.

---

## 📊 Dataset

| Detail | Value |
|--------|-------|
| **File** | [`data/pyspark-assignment-dataset.csv`](data/pyspark-assignment-dataset.csv) |
| **Format** | Synthetic sales transactions |
| **Records** | 1,000 |
| **Columns** | 17 |

| Column | Type | Description |
|--------|------|-------------|
| `user_id` | Integer | Unique user identifier |
| `transaction_date` | Date | Date of transaction |
| `product_id` | String | Product identifier |
| `category` | String | Product category (Electronics, Books, etc.) |
| `price` | Double | Product price |
| `base_price` | Double | Base price before adjustments |
| `amount` | Double | Total transaction amount |
| `quantity` | Integer | Quantity purchased |
| `status` | String | Order status (Completed, Pending, Cancelled) |
| `priority` | String | Order priority (Low, Medium, High) |
| `region` | String | Geographic region |
| `city` | String | Customer city |
| `email` | String | Customer email |
| `username` | String | Customer username |
| `subscription` | String | Subscription plan (Basic, Standard, Premium) |
| `store_id` | String | Store identifier |
| `raw_timestamp` | Timestamp | Raw timestamp of transaction |

---

## ❓ Questions Breakdown

### 🔹 Spark Architecture & Execution Model (Q1–Q2, Q7, Q11, Q13)

| # | Question | Key Concept |
|---|----------|-------------|
| **Q1** | Explain roles of Driver, Cluster Manager & Executor | Spark distributed architecture — control vs compute |
| **Q2** | How does Lazy Evaluation improve performance? | Delayed execution, DAG optimization, reduced I/O |
| **Q7** | How does the Lineage Graph (DAG) provide fault tolerance? | Recomputes only lost partitions on worker failure |
| **Q11** | Difference between Transformations & Actions | Lazy vs eager — `filter()` vs `show()` |
| **Q13** | Difference between Client Mode & Cluster Mode | Driver location — dev vs production deployment |

### 🔹 DataFrame Operations (Q3, Q5, Q6, Q8, Q10, Q12, Q14)

| # | Question | Technique |
|---|----------|-----------|
| **Q3** | Read CSV with `header=True` & `inferSchema=True` | `spark.read.csv()` |
| **Q5** | Select `product_id`, `price` where category = Electronics | `filter()` + `select()` |
| **Q6** | Rename column & cast price from String to Double | `withColumnRenamed()`, `cast()` |
| **Q8** | Filter: status = Completed AND amount > 1000 | Multi-condition with `&` |
| **Q10** | Add `final_price` = `base_price * 1.18` (18% tax) | `withColumn()` derived column |
| **Q12** | Load Parquet → filter null `user_id` → save as CSV | Read → clean → write ETL pipeline |
| **Q14** | Filter: region = North OR priority = High | Multi-condition with `\|` |

### 🔹 File Formats & Optimization (Q4, Q9, Q15)

| # | Question | Technique |
|---|----------|-----------|
| **Q4** | CSV (row-based) vs Parquet (columnar) — performance impact | Columnar storage, compression, schema |
| **Q9** | Predicate Pushdown in Parquet | Filter pushed to storage layer — less data in memory |
| **Q15** | `.show(5)` vs `.collect()` on multi-terabyte data | Memory safety — preview vs full retrieval |

---

## 🧠 Key Concepts

| Concept | Description |
|---------|-------------|
| **Driver** | Main control process — creates SparkSession, builds DAG, schedules tasks |
| **Cluster Manager** | Allocates resources — launches Executors on worker nodes (Standalone, YARN, Mesos, K8s) |
| **Executor** | Worker process — executes tasks, caches data, returns results to Driver |
| **Lazy Evaluation** | Transformations build a lineage DAG; execution triggers only on Actions |
| **Lineage Graph (DAG)** | Directed Acyclic Graph recording all transformations — enables fault tolerance via recomputation |
| **Predicate Pushdown** | Parquet optimization — filters applied at storage level, reducing data loaded into memory |
| **Client vs Cluster Mode** | Client: Driver runs on submission machine. Cluster: Driver runs inside the cluster |
| **CSV vs Parquet** | CSV: row-based, human-readable, larger. Parquet: columnar, compressed, faster analytics |
| **Transformations** | Lazy operations (`filter`, `select`, `groupBy`) — define processing logic |
| **Actions** | Eager operations (`show`, `count`, `collect`) — trigger execution & return results |

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
| [`Spark-Questions.ipynb`](Spark-Questions.ipynb) | Main notebook — all 15 questions with explanations & code |
| [`data/pyspark-assignment-dataset.csv`](data/pyspark-assignment-dataset.csv) | Synthetic sales dataset (1,000 records, 17 columns) |
| [`README.md`](README.md) | You are here |

---

## ✅ Key Takeaways

- 🏛️ Spark's **Driver–Cluster Manager–Executor** architecture enables distributed, fault-tolerant data processing
- ⏳ **Lazy Evaluation** + **DAG optimization** dramatically reduce unnecessary I/O and compute
- 🔁 **Lineage Graph** provides automatic fault tolerance by recomputing only lost partitions
- 📦 **Parquet** with **Predicate Pushdown** drastically outperforms CSV for large-scale analytics
- 🧪 `.show(5)` is always safer than `.collect()` when exploring large datasets — prevents OOM on Driver
- 🛠️ DataFrame API (`filter`, `select`, `withColumn`, `cast`) enables clean, expressive ETL pipelines

---

<div align="center">
  <p>
    <sub>Built with ❤️ for the Celebal Data Engineering Internship</sub>
    <br>
    <sub>Author: <a href="https://github.com/KumarGaurav007">Gaurav Kumar</a></sub>
  </p>
</div>
