<div align="center">
  <h1>📊 Procurement Analytics — Medallion Architecture</h1>
  <p><strong>End-to-End Data Engineering Pipeline with PySpark · SCD Type 2 · Business Intelligence</strong></p>
  <p>
    <img src="https://img.shields.io/badge/PySpark-4.2.0-E25A1C?logo=apachespark&logoColor=white" alt="PySpark">
    <img src="https://img.shields.io/badge/Python-3.14-3776AB?logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white" alt="Pandas">
    <img src="https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white" alt="Jupyter">
    <img src="https://img.shields.io/badge/Power%20BI-Ready-F2C811?logo=powerbi&logoColor=black" alt="Power BI">
  </p>
  <p>
    <a href="#-overview">Overview</a> •
    <a href="#-architecture">Architecture</a> •
    <a href="#-pipeline-stages">Pipeline Stages</a> •
    <a href="#-key-insights">Key Insights</a> •
    <a href="#-getting-started">Getting Started</a>
  </p>
</div>

---

## 🧭 Overview

This is the **Capstone Final Project** for the Celebal Technologies Data Engineering Excellence Internship. It demonstrates a complete, production-style **procurement analytics pipeline** built on the **Medallion Architecture** (Bronze → Silver → Gold) using **Apache Spark (PySpark)**.

Starting from raw procurement CSVs, the pipeline ingests source data, cleans and standardizes it, tracks historical contract changes with **Slowly Changing Dimension (SCD) Type 2**, and finally produces **business-ready analytical datasets** designed to be dropped straight into **Power BI**.

| Detail | Info |
|--------|------|
| **Project Type** | End-to-End Data Engineering Pipeline |
| **Pattern** | Medallion Architecture (Bronze · Silver · Gold) |
| **Compute** | Apache Spark 4.2.0 (local) |
| **Business Focus** | Procurement spend, vendor risk & price compliance |
| **Final Output** | 5 analytical datasets ready for Power BI |

---

## 🏗️ Architecture

```
                       ┌──────────────────────────────────────────────────────────────┐
                       │                     MEDALLION ARCHITECTURE                    │
                       └──────────────────────────────────────────────────────────────┘

  Raw Source CSVs                     Bronze                                Silver
  ────────────────                     ──────                                ──────
  vendors_1.csv   ─┐
  orders_1.csv    ─┤  ┌──────────────────────┐   ┌────────────────────────────────┐
  invoices_1.csv  ─┼─►│  RAW ingestion        │──►│  Cleaned · Standardized       │
  contracts_1.csv ─┘  │  • No transformation  │   │  • Missing values handled     │
                      │  • + ingestion_ts     │   │  • Duplicates removed         │
                      │  • Full traceability  │   │  • Timestamps standardized    │
                      └──────────────────────┘   └────────────────────────────────┘
                                                                        │
                                               ┌────────────────────────┴────────────────────────┐
                                               │             SCD TYPE 2 – CONTRACTS                │
                                               │  version_number · effective_start/end · is_current│
                                               └──────────────────────────────────────────────────┘
                                                                        │
                                                                        ▼
                       Gold                                          Power BI
                       ────                                          ────────
        ┌──────────────────────────────┐        ┌──────────────────────────────┐
        │ vendor_spend                 │        │ • Bar Chart — Top Vendors    │
        │ price_variance               │───────►│ • Variance by Vendor         │
        │ vendor_risk                  │        │ • Risk Distribution (Pie)    │
        │ region_spend                 │        │ • Region Spend (Map/Bar)     │
        │ monthly_spend                │        │ • Monthly Spend Trend (Line) │
        └──────────────────────────────┘        └──────────────────────────────┘
```

---

## 🧩 Pipeline Stages

The project is split into **6 sequential notebooks**, each building on the last.

| # | Notebook | Layer | Purpose |
|---|----------|-------|---------|
| 00 | [`00-Project-Setup.ipynb`](00-Project-Setup.ipynb) | — | Initialize Spark, validate datasets & structure |
| 01 | [`01-Bronze-Ingestion.ipynb`](01-Bronze-Ingestion.ipynb) | 🥉 Bronze | Ingest raw CSVs, add `ingestion_timestamp`, preserve source data |
| 02 | [`02-Silver-Transformation.ipynb`](02-Silver-Transformation.ipynb) | 🥈 Silver | Clean, deduplicate & standardize; prepare SCD columns |
| 03 | [`03-SCD-Type2-Vendor-Contracts.ipynb`](03-SCD-Type2-Vendor-Contracts.ipynb) | 🥈 Silver | Track contract history with **SCD Type 2** |
| 04 | [`04-Gold-Business-Analytics.ipynb`](04-Gold-Business-Analytics.ipynb) | 🥇 Gold | Compute 5 business analytical datasets |
| 05 | [`05-PowerBI-Export.ipynb`](05-PowerBI-Export.ipynb) | 📊 Export | Validate exports & recommend dashboard visuals |

---

## 🥉 01 — Bronze Layer

> **"Data as it is."** Source files are ingested exactly as received — no transformations.

- Read raw CSVs (`header=True`, `inferSchema=True`)
- Added `ingestion_timestamp` to every record for traceability
- Preserved original records for re-processing & audit

| Dataset | Source Rows |
|---------|-------------|
| Purchase Orders | 5,000 |
| Invoices | 5,000 |
| Vendors | 5,100 |
| Contracts | 5,100 |

📁 Output: `output/bronze/`

---

## 🥈 02 — Silver Layer

> **"Data cleaned & trusted."** Applies data-quality rules to produce curated datasets.

| Dataset | Bronze → Silver | Transformation |
|---------|-----------------|----------------|
| Orders | 5,000 → 4,618 | Removed invalid `N/A` timestamps & null items |
| Invoices | 5,000 → 5,000 | Deduplicated, timestamp cast |
| Vendors | 5,100 → 5,000 | 100 duplicates removed, names trimmed |
| Contracts | 5,050 → 5,000 | 50 duplicates removed, robust date parsing (`coalesce` + `try_to_timestamp`) |

✔ **Validation:** `0` duplicate vendors · `0` duplicate contracts remaining.

📁 Output: `output/silver/`

---

## 🕘 03 — SCD Type 2 for Vendor Contracts

> **"Full history, one current truth."** Tracks every negotiated-price / validity change over time.

Contracts are versioned per `(vendor_id, item_name)` using `ROW_NUMBER()` and `LEAD()` window functions.

| SCD Column | Purpose |
|------------|---------|
| `version_number` | Sequential version of a vendor-item contract |
| `effective_start_date` | When the version becomes active |
| `effective_end_date` | When the version is superseded (`NULL` = current) |
| `is_current` | Flag for the latest active contract |

| Metric | Count |
|--------|-------|
| Current active contracts | **4,897** |
| Historical contract versions | **103** |
| Total versioned records | **5,000** |

📁 Output: `output/silver/scd/`

---

## 🥇 04 — Gold Layer & Business Insights

> **"Analytics for decision makers."** Joins orders × invoices × vendors × current contracts to derive metrics: `invoice_amount`, `contract_amount`, `price_variance`.

### 💰 Insight 1 — Total Vendor Spend
| Rank | Vendor | Total Spend |
|------|--------|-------------|
| 1 | Price-Dominguez | **$25.6 M** |
| 2 | Perez Ltd | $22.7 M |
| 3 | English-Dominguez | $21.9 M |

### ⚖️ Insight 2 — Invoice vs Contract Price Variance
Vendors billing above negotiated contract prices (top: **Edwards Ltd, $22.9 M** variance) — key for contract compliance.

### 🚨 Insight 3 — Vendor Risk Classification
| Risk | Vendors |
|------|---------|
| Medium | 1,607 |
| Low | 1,580 |
| High | 1,566 |
| NULL | 247 |

### 🌍 Insight 4 — Region-wise Spend
| Region | Spend |
|--------|-------|
| AMER | **$1.62 B** |
| EMEA | $1.50 B |
| APAC | $1.49 B |
| LATAM | $1.41 B |

### 📈 Insight 5 — Monthly Spend Trend
Monthly procurement spend tracked across 2024–2025 (peak ≈ **$302.8 M** in Jul 2025), enabling seasonality analysis.

### 📁 Gold Outputs (`output/gold/`)

| File | Insight | Power BI Visual |
|------|---------|-----------------|
| `vendor_spend.csv` | Top vendors by spend | Bar Chart |
| `price_variance.csv` | Contract compliance | Bar Chart |
| `vendor_risk.csv` | Risk distribution | Pie Chart |
| `region_spend.csv` | Regional analysis | Map / Bar Chart |
| `monthly_spend.csv` | Spend trends | Line Chart |

---

## 📁 Project Structure

```
Final-Project-Procurement-Analytics/
├── 📄 README.md
│
├── 📓 00-Project-Setup.ipynb              # Spark init & data validation
├── 📓 01-Bronze-Ingestion.ipynb           # Raw ingestion + metadata
├── 📓 02-Silver-Transformation.ipynb      # Cleaning & standardization
├── 📓 03-SCD-Type2-Vendor-Contracts.ipynb # SCD Type 2 history tracking
├── 📓 04-Gold-Business-Analytics.ipynb    # Business analytical datasets
├── 📓 05-PowerBI-Export.ipynb             # Export validation & dashboards
│
├── 📁 data/                               # Raw source CSVs
│   ├── vendors_1.csv
│   ├── orders_1.csv
│   ├── invoices_1.csv
│   └── contracts_1.csv
│
├── 📁 output/
│   ├── 📁 bronze/                         # Raw + ingestion metadata
│   ├── 📁 silver/                         # Cleaned datasets + SCD history
│   └── 📁 gold/                           # Business-ready analytics
```

---

## 🚀 Getting Started

```bash
# 1. Activate your virtual environment
.\venv\Scripts\Activate.ps1        # Windows
source venv/bin/activate           # macOS / Linux

# 2. Install dependencies
pip install pyspark pandas jupyter

# 3. Launch Jupyter & run notebooks in order 00 → 05
jupyter notebook
```

> ⚠️ **Windows note:** PySpark requires `HADOOP_HOME` (with `winutils.exe`) to be set, e.g. `C:\hadoop`. Installing **PyArrow ≥ 18** removes the Arrow fallback warnings and speeds up `toPandas()`.

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|-----------|
| **Language** | Python 3.14 |
| **Big Data** | Apache Spark (PySpark) 4.2.0 |
| **Data Processing** | Pandas |
| **Environment** | Jupyter Notebook · VS Code |
| **BI / Reporting** | Power BI (export-ready CSVs) |

---

## 🔮 Key Learnings

- **Medallion Architecture** — a scalable, layered pattern for reliable data platforms: raw → trusted → curated.
- **SCD Type 2** — preserving dimension history while keeping a single active record for analytics.
- **Data Quality Rules** — deduplication, null handling, robust multi-format date parsing (`coalesce` + `try_to_timestamp`).
- **Window Functions** — `ROW_NUMBER()` & `LEAD()` for versioning and effective-date chaining.
- **Power BI Readiness** — designing aggregations so analysts can visualize without extra transformation.

---

## 👤 Author

<div align="center">
  <p>
    <strong>Gaurav Kumar</strong> — Data Engineering Intern, Celebal Technologies
    <br>
    <a href="https://github.com/KumarGaurav007">GitHub</a> ·
    <a href="https://celebaltech.com">Celebal Technologies</a>
  </p>
</div>
