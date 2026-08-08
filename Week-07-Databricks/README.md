<div align="center">
  <h1>🐍 Week 07 — Python Basics & Data Cleaning</h1>
  <p><strong>Python Fundamentals, Pandas & End-to-End Data Cleaning Pipeline</strong></p>
  <p>
    <img src="https://img.shields.io/badge/Python-3.14-3776AB?logo=python&logoColor=white" alt="Python">
    <img src="https://img.shields.io/badge/Pandas-2.x-150458?logo=pandas&logoColor=white" alt="Pandas">
    <img src="https://img.shields.io/badge/NumPy-1.24+-013243?logo=numpy&logoColor=white" alt="NumPy">
    <img src="https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white" alt="Jupyter">
    <img src="https://img.shields.io/badge/Status-Completed-success" alt="Status">
  </p>
  <p>
    <a href="#-overview">Overview</a> •
    <a href="#-dataset">Dataset</a> •
    <a href="#-pipeline-steps">Pipeline Steps</a> •
    <a href="#-key-concepts">Key Concepts</a> •
    <a href="#-how-to-run">How to Run</a>
  </p>
</div>

---

## 📌 Overview

This week delivers a hands-on foundation in **Python basics and data cleaning** by working
through the classic **Tableau *Sample – Superstore*** retail dataset. The notebook implements
a complete 7-step data-cleaning workflow — from loading a "messy" CSV into a Pandas
DataFrame to exporting a fully cleaned, analysis-ready dataset.

**Objective:** Build a reusable, industry-style cleaning pipeline using Pandas and NumPy,
covering exploration, missing-value treatment, filtering, deduplication, and feature
engineering.

---

## 📊 Dataset

| Detail | Value |
|--------|-------|
| **File** | [`sample.csv`](sample.csv) |
| **Format** | Tableau Sample – Superstore retail transactions |
| **Raw Records** | 9,994 |
| **Raw Columns** | 21 |
| **Cleaned Output** | [`superstore_cleaned.csv`](superstore_cleaned.csv) — **9,994 rows × 23 cols** |

| Column | Example |
|--------|---------|
| `Order ID` | Order identifier |
| `Order Date` / `Ship Date` | Order & shipment timestamps |
| `Segment` | Consumer, Corporate, Home Office |
| `Category` / `Sub-Category` | Product taxonomy |
| `Region` / `State` / `City` | Geography |
| `Sales`, `Quantity`, `Discount`, `Profit` | Financial metrics |
| `Unit_Price` / `total_amount` | ➕ Added during cleaning |

> **Cleanliness before→after:** missing values `295 → 0` · duplicate rows `10 → 0`.

---

## 🔁 Pipeline Steps

| Step | What We Did | Before → After |
|------|-------------|----------------|
| **1. Load** | `pd.read_csv()` into a DataFrame | 10,004 rows × 21 cols |
| **2. Explore** | `head/tail/shape/columns/dtypes/info/describe` | Understood the data |
| **3. Handle missing values** | Identified, filled (`mode` / `median`), `dropna` demo | 295 missing → 0 |
| **4. Basic operations** | Filtered rows, selected columns (`loc` / `iloc`) | — |
| **5. Remove duplicates** | `drop_duplicates()` | 10 → 0 |
| **6. Derived column** | `Unit_Price` & `total_amount = price × quantity` | +2 columns |
| **7. Save** | `to_csv()` + reload verification | `superstore_cleaned.csv` |

---

## 🧹 Data Cleaning Highlights

### Step 3 — Missing Value Strategy

Smart, column-aware filling instead of a blanket approach:

```python
df["Postal Code"] = df["Postal Code"].fillna(df["Postal Code"].mode()[0])  # identifier → mode
df["Region"]      = df["Region"].fillna(df["Region"].mode()[0])            # category → mode
df["Sales"]       = df["Sales"].fillna(df["Sales"].median())               # numeric  → median
```

- **`mode`** for identifiers & categorical text (most common value)
- **`median`** for numeric columns (resistant to outliers)
- **`dropna()`** previewed as the alternative when filling doesn't make sense

### Step 4 — Filter & Select
```python
big_orders    = df[df["Sales"] > 1000]                                          # filter rows
consumers_west = df[(df["Segment"] == "Consumer") & (df["Region"] == "West")]   # multi-condition
df.loc[0:4, ["Order ID", "Sales"]]    # label-based
df.iloc[0:4, [1, 17]]                 # position-based
```

### Step 6 — Feature Engineering
```python
df["Unit_Price"]  = df["Sales"] / df["Quantity"]
df["total_amount"] = df["Unit_Price"] * df["Quantity"]
```

A sanity check confirms `total_amount` matches `Sales` within 1 cent across every row.

### Step 7 — Save & Verify
```python
df.to_csv("superstore_cleaned.csv", index=False)
cleaned = pd.read_csv("superstore_cleaned.csv")   # loads back clean
# → 9,994 rows × 23 cols · 0 missing · 0 duplicates
```

---

## 📈 Bonus Insights

- **`Sales`** ranges from a **$0.44** order up to **~$22,638**; median order ≈ **$54.40**
- **Consumer** is the largest segment (**5,191** orders)
- Majority of orders come from the **West**, **East**, and **Central** US regions

---

## 🧠 Key Concepts

| Concept | Description |
|---------|-------------|
| **DataFrame** | 2-D, labeled tabular structure for all Python data work |
| **Missing Values** | `isnull().sum()` → count; `fillna()` / `dropna()` → resolution |
| **Central Tendency** | `mode()` for categories, `median()` for skewed numerics |
| **Boolean Filtering** | Row selection with conditions; `&` for AND, wrap each in `()` |
| **`loc` vs `iloc`** | Label-based vs integer-position-based indexing |
| **Deduplication** | `duplicated()` / `drop_duplicates()` remove redundant records |
| **Feature Engineering** | Deriving `Unit_Price` & `total_amount` from existing columns |
| **Sanity Checks** | Verify derived math (e.g., within 1 cent of `Sales`) |

---

## 🚀 How to Run

```bash
# 1. Activate virtual environment
.\venv\Scripts\Activate.ps1     # Windows
source venv/bin/activate         # macOS / Linux

# 2. Launch Jupyter
jupyter notebook

# 3. Open python_basics_data_cleaning.ipynb
```

---

## 📁 Files

| File | Description |
|------|-------------|
| [`python_basics_data_cleaning.ipynb`](python_basics_data_cleaning.ipynb) | Main notebook — 7-step cleaning pipeline with explanations |
| [`sample.csv`](sample.csv) | Raw Tableau Superstore dataset (9,994 × 21) |
| [`superstore_cleaned.csv`](superstore_cleaned.csv) | Cleaned output (9,994 × 23, 0 missing, 0 duplicates) |
| [`README.md`](README.md) | You are here |

---

## ✅ Key Takeaways

- 📥 **Load & explore first** — `shape`, `info`, `describe()` reveal the data before any cleaning
- 🧂 **One filling strategy doesn't fit all** — use `mode` for categories, `median` for skewed numbers
- 🔍 **Boolean filtering** with `&` and indexing with `loc`/`iloc` are everyday workhorses
- 🧹 **Deduplicate** with `drop_duplicates()` to avoid inflated statistics
- 🧮 **Feature engineering** adds business value (`total_amount = price × quantity`)
- ✅ **Always verify output** — reload the saved CSV and confirm shape, nulls & duplicates

---

<div align="center">
  <p>
    <sub>Built with ❤️ for the Celebal Data Engineering Internship</sub>
    <br>
    <sub>Author: <a href="https://github.com/KumarGaurav007">Gaurav Kumar</a></sub>
  </p>
</div>