# 🥬 Vegetable Product & Category Master Data Analysis

An exploratory data analysis (EDA) of a retail/wholesale vegetable product catalogue ("Superset"), covering data quality checks, category distribution, and product-naming patterns.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Numerical-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4c72b0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Objectives](#-objectives)
- [Dataset](#-dataset)
- [Tools & Technologies](#-tools--technologies)
- [Project Workflow](#-project-workflow)
- [Getting Started](#-getting-started)
- [Data Cleaning Summary](#-data-cleaning-summary)
- [Key Findings](#-key-findings)
- [Business Insights](#-business-insights)
- [Recommendations](#-recommendations)
- [Challenges Faced](#-challenges-faced)
- [Future Scope](#-future-scope)
- [Project Structure](#-project-structure)
- [References](#-references)
- [Author](#-author)

---

## 📖 Overview

This project analyses a small but well-structured **master dataset** of vegetable products and the categories they belong to. The dataset contains **251 records** and **4 columns**: `Item Code`, `Item Name`, `Category Code`, and `Category Name`.

The goal is to understand how the catalogue is organised, verify its data quality, and generate practical, data-backed insights for catalogue management and category planning.

> **Note:** This is a clean master/reference table, **not** a transactional dataset. It has no prices, quantities, dates, or customer information, so the analysis focuses on data quality, category distribution, and naming patterns rather than sales or revenue trends.

---

## ❓ Problem Statement

Merchandising, procurement, and inventory teams need clear answers to questions such as:

- How many products do we sell, and how are they grouped into categories?
- Are there naming inconsistencies or duplicate-looking entries that could confuse staff or customers?

Without structured analysis of this master data, imbalances between categories and repeated numbered-variant names can go unnoticed and affect how the catalogue is managed, filtered, and displayed.

---

## 🎯 Objectives

- Understand the structure and content of the vegetable product master dataset
- Check for missing values, duplicates, and formatting inconsistencies
- Explore product distribution across the six vegetable categories
- Study naming patterns, including numbered variants such as `Eggplant (1)` and `Eggplant (2)`
- Create simple, meaningful visualisations of category distribution
- Generate business insights and recommendations supported by the data

---

## 📂 Dataset

| Property | Details |
| --- | --- |
| **File** | `cleaned_superset__2_.csv` |
| **Source** | Cleaned CSV export of a retail/wholesale vegetable product catalogue |
| **Rows** | 251 |
| **Columns** | 4 |

### Column Description

| Column | Type | Description |
| --- | --- | --- |
| `Item Code` | Integer (15 digits) | Unique identifier for each product (acts as primary key) |
| `Item Name` | Text | Name of the vegetable product, e.g. "Chinese Cabbage" |
| `Category Code` | Integer (10 digits) | Identifier for the product's category |
| `Category Name` | Text | One of 6 categories, e.g. "Capsicum", "Edible Mushroom" |

---

## 🛠 Tools & Technologies

| Tool | Purpose |
| --- | --- |
| **Python** | Core programming language |
| **Pandas** | Loading, cleaning, and exploring tabular data |
| **NumPy** | Numerical operations supporting Pandas |
| **Matplotlib** | Bar chart visualisation |
| **Seaborn** | Statistical / category-comparison plots |
| **Jupyter Notebook / VS Code** | Interactive development environment |

---

## 🔄 Project Workflow

1. **Problem Statement**: define what to learn from the catalogue
2. **Dataset Collection**: receive the cleaned CSV
3. **Import Libraries**: Pandas, NumPy, Matplotlib, Seaborn
4. **Load Dataset**: read the CSV into a DataFrame
5. **Data Exploration**: shape, columns, data types, sample rows
6. **Data Cleaning**: missing values, duplicates, inconsistent text
7. **Exploratory Data Analysis**: category frequencies and naming patterns
8. **Bivariate Analysis**: Category Code vs Category Name
9. **Feature Engineering**: `base_item_name` and `is_variant` columns
10. **Data Visualisation**: bar and pie charts
11. **Business Insights**
12. **Recommendations**
13. **Conclusion**

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- Jupyter Notebook or VS Code

### Installation

```bash
# Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# Install dependencies
pip install pandas numpy matplotlib seaborn jupyter
```

### Run the Analysis

```bash
jupyter notebook
```

Then open the analysis notebook and run all cells.

### Quick Start

```python
import pandas as pd

df = pd.read_csv("cleaned_superset__2_.csv")

print(df.shape)                            # (251, 4)
print(df["Category Name"].value_counts())
```

---

## 🧹 Data Cleaning Summary

| Check | Method | Result |
| --- | --- | --- |
| Missing values | `df.isnull().sum()` | 0 missing values in all 4 columns |
| Duplicate rows | `df.duplicated().sum()` | 0 fully duplicate rows |
| Data types | `df.dtypes` | IDs read as integers; names as text |
| Code ↔ Name consistency | `df.groupby()` | Each of the 6 category codes maps to exactly one category name, and vice versa |
| Repeated item names | `df['Item Name'].duplicated()` | 8 rows share an exact name with another row |
| Numbered-variant suffixes | Regex `(1)`, `(2)` … | 63 of 251 names (25%) end in a numbered suffix |

No rows needed to be removed or repaired. Outlier handling was not applicable since the dataset has no continuous numeric measurement columns.

---

## 📊 Key Findings

### Category Distribution

| Category Name | Items | Share of Catalogue |
| --- | --- | --- |
| Flower/Leaf Vegetables | 100 | 39.8% |
| Edible Mushroom | 72 | 28.7% |
| Capsicum | 45 | 17.9% |
| Aquatic Tuberous Vegetables | 19 | 7.6% |
| Solanum | 10 | 4.0% |
| Cabbage | 5 | 2.0% |

### Highlights

- **Flower/Leaf Vegetables** and **Edible Mushroom** together make up nearly **69%** of the catalogue
- **Cabbage** is the smallest category with only **5** products
- **247** unique item names across **251** rows
- Item name length ranges from **4 to 49 characters** (average about 18.5)
- Feature engineering reduced the 251 raw listings to **218 unique base products**

### Feature Engineering

```python
# Strip numbered suffixes like "(1)" or "(2)" to get the base product name
df["base_item_name"] = df["Item Name"].str.replace(r"\s*\(\d+\)$", "", regex=True)

# Flag items that use a numbered-variant suffix
df["is_variant"] = df["Item Name"].str.contains(r"\(\d+\)$", regex=True)
```

> The exact regex patterns used in your notebook may differ slightly; adjust as needed.

---

## 💡 Business Insights

- The catalogue is heavily concentrated in two categories, which will require the most shelf space, storage, and supplier coordination.
- The Category Code system is fully consistent, so the master data can be trusted for category-level reporting.
- A quarter of all items are numbered variants of a base product, so the true count of distinct vegetables is closer to **218** than 251.
- The dataset is clean and ready to be joined with transactional data (sales or inventory) using `Item Code` as the key.

---

## ✅ Recommendations

1. **Review the Cabbage and Solanum categories** (5 and 10 products): confirm whether this is intentional or incomplete cataloguing.
2. **Standardise numbered-variant naming**: use attribute-based names (e.g. `Eggplant – Round`) instead of `Eggplant (3)`.
3. **Use this table as a lookup** for future sales or inventory analysis, joining on `Item Code`.
4. **Manually review the 8 exact-duplicate item names** to confirm whether they are different package sizes/batches or accidental double entries.

---

## ⚠️ Challenges Faced

- **Limited dataset scope**: with only 4 columns and no numeric measurements, techniques like correlation matrices, outlier detection, and time-trend analysis could not be applied meaningfully.
- **Genuine vs. accidental duplicates**: an exact-duplicate item name is not automatically an error, so careful judgment was needed.
- **Extracting base product names**: variant suffixes appear in different positions, so a regular expression was required rather than a simple lookup.

---

## 🔮 Future Scope

- Join with a sales/transaction dataset (via `Item Code`) to analyse revenue and demand by category
- Build an interactive dashboard (Power BI / Tableau) for category share and catalogue changes over time
- Apply text-similarity techniques to automatically group numbered-variant product names
- Use `base_item_name` as an input for demand-forecasting or recommendation-system projects
- Automate data-quality checks to run on every catalogue refresh

---

## 🗂 Project Structure

```text
├── data/
│   └── cleaned_superset__2_.csv
├── notebooks/
│   └── vegetable_catalogue_analysis.ipynb
├── reports/
│   └── Vegetable_Catalogue_Data_Analysis_Report.docx
├── images/
│   ├── category_bar_chart.png
│   └── category_pie_chart.png
└── README.md
```

> Adjust the folder and file names to match your actual repository.

---

## 📚 References

- Dataset: `cleaned_superset__2_.csv`
- [Python Documentation](https://docs.python.org/3/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [NumPy Documentation](https://numpy.org/doc/)
- [Matplotlib Documentation](https://matplotlib.org/stable/index.html)
- [Seaborn Documentation](https://seaborn.pydata.org/)

---

## 👤 Author

**Your Name**
Data Analyst (Student / Trainee Project)
📅 August 2026

- GitHub: [@your-username](https://github.com/your-username)
- LinkedIn: [your-profile](https://www.linkedin.com/in/your-profile)

---

⭐ If you found this project useful, consider giving it a star!
