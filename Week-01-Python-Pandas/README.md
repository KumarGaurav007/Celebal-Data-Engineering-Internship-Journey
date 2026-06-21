# Week 01: Python Pandas — Shopping Data Analysis

[![Python](https://img.shields.io/badge/Python-3.12+-blue?logo=python&logoColor=white)](https://python.org)
[![Pandas](https://img.shields.io/badge/Pandas-2.0+-150458?logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![NumPy](https://img.shields.io/badge/NumPy-1.24+-013243?logo=numpy&logoColor=white)](https://numpy.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)](https://jupyter.org)

> **Celebal Data Engineering Internship — Week 1 Assignment**  
> Basic data exploration, cleaning, and transformation of an e-commerce shopping dataset using Pandas.

---

## 📁 Project Structure

```
Week-01-Python-Pandas/
├── data/
│   └── Combined_dataset.csv          # Raw multi-category product data
├── cleaned-data/
│   └── cleaned_shopping_data.csv     # Cleaned output after preprocessing
├── shopping_analysis.ipynb           # Jupyter Notebook with full analysis
└── README.md                         # You are here
```

---

## 📊 Dataset Overview

The dataset contains **e-commerce product listings** with **24 columns** covering product details, pricing, seller info, customer reviews, and more.

| Column                 | Description                              |
|------------------------|------------------------------------------|
| `product_id`           | Unique product identifier                |
| `title`                | Product title                            |
| `product_description`  | Detailed product description             |
| `rating`               | Average customer rating (float)          |
| `ratings_count`        | Number of ratings received               |
| `initial_price`        | Original price before discount           |
| `discount`             | Discount percentage / value              |
| `final_price`          | Final price after discount (string with ₹) |
| `currency`             | Currency code                            |
| `category`             | Product category                         |
| *(and 14 more fields)* | Images, delivery, reviews, sellers, etc. |

---

## 🔍 Analysis Performed

### 1️⃣ Data Exploration
- Loaded CSV with `pd.read_csv()`
- Inspected first / last 5 records (`head()` / `tail()`)
- Reviewed shape, column names, data types, and memory usage (`info()`)
- Generated statistical summary (`describe()`)

### 2️⃣ Missing Value Treatment
| Column                | Strategy            | Fill Value           |
|-----------------------|---------------------|----------------------|
| `discount`            | Fill with `0`       | `0`                  |
| `seller_name`         | Fill with "Unknown" | `"Unknown"`          |
| `seller_information`  | Fill with "Not Available" | `"Not Available"` |
| `videos`              | Fill with "No Video" | `"No Video"`        |
| `what_customers_said` | Fill with "No Customer Review" | `"No Customer Review"` |
| `variations`          | Fill with "No Variations" | `"No Variations"` |

### 3️⃣ Duplicate Check
- Verified **zero duplicate records** in the dataset.

### 4️⃣ Data Type Conversion
- `final_price` was stored as a string (e.g., `₹1,299`).  
  Converted to **float** by removing the ₹ symbol and commas:

```python
df["final_price"] = (
    df["final_price"]
    .str.replace("₹", "", regex=False)
    .str.replace(",", "", regex=False)
    .astype(float)
)
```

### 5️⃣ Feature Engineering
- Created **`discount_amount`** — the difference between initial and final price:

```python
df["discount_amount"] = df["initial_price"] - df["final_price"]
```

### 6️⃣ Filtering & Selection
- **Highly rated products** — filtered records where `rating > 4`
- **Column selection** — extracted key columns: `title`, `rating`, `initial_price`, `final_price`, `category`

### 7️⃣ Export
- Cleaned dataset saved to `cleaned-data/cleaned_shopping_data.csv`

---

## 🚀 How to Run

```bash
# 1. Activate virtual environment (recommended)
python -m venv venv
# Windows:
.\venv\Scripts\Activate.ps1

# 2. Install dependencies
pip install pandas numpy jupyter

# 3. Launch the notebook
jupyter notebook shopping_analysis.ipynb
```

---

## ✅ Key Takeaways

- 📥 **Loading & Inspecting** — Using `read_csv()`, `head()`, `info()`, `describe()` to understand data shape and quality.
- 🧹 **Cleaning** — Handling missing values, checking duplicates, and converting data types.
- 🛠️ **Transformation** — Creating derived columns with vectorized operations.
- 🔎 **Filtering** — Slicing DataFrames with boolean masks and column selection.
- 💾 **Export** — Writing cleaned data back to CSV.

---

<div align="center">
  <sub>Built with ❤️ for the Celebal Data Engineering Internship</sub>
</div>
