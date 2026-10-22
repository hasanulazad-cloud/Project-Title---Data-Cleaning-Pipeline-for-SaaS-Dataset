# 🧹 Data Cleaning Pipeline for SaaS Dataset

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Data%20Cleaning-success)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> A pure-Python pipeline that turns messy SaaS customer records (missing names, mixed date formats, text in numeric fields, duplicates) into a clean dataset, then computes revenue, usage and plan metrics from it.

---

## 📌 Project Overview

Real-world customer data is rarely tidy. This project takes a small, deliberately messy SaaS customer dataset and builds a step-by-step cleaning pipeline using only core Python: dictionaries, lists, sets, functions, a class, `datetime` and file handling. No pandas required.

**What it does**
- 📋 Displays the raw records and accepts a new customer record
- 🏗️ Defines a `SaaSCustomer` class that cleans fields as objects are created
- 🧼 Runs a three-stage cleaning pipeline: missing values, duplicates, date standardisation
- 📊 Computes customer count, average fee, total usage and plan distribution
- 🔎 Flags low-usage customers and lists the unique plans
- 💾 Saves results to `saas_customers_cleaned.csv` and `plan_summary.txt` with error handling

---

## 📂 Repository Contents

| File | Description |
|---|---|
| `Python_Module_End_Assessment_1_Data_Cleaning_Pipeline_for_SaaS_Dataset.ipynb` | Main notebook with all eight tasks |
| `saas_customers_cleaned.csv` | Cleaned customer records (output of Task 8) |
| `plan_summary.txt` | Customers per plan (output of Task 8) |

---

## 🧩 The Data Problems

The raw dataset contains typical quality issues:

| Problem | Example in the data |
|---|---|
| Missing name | Customer 103 has `None` |
| Mixed date formats | `2023-01-10`, `2023/02/15`, `03-01-2023`, `15-04-2023`, `20230520` |
| Text in a numeric field | Monthly fee `forty-nine` |
| Missing usage values | `None` and the string `"NULL"` |
| Blank category | Customer 106 has an empty plan |
| Repeated record | Customer 107 repeats customer 101's details |

---

## 🔧 Pipeline

```
Raw data → Handle missing values → Remove duplicates → Standardise dates → Clean data
```

| Stage | What it does |
|---|---|
| **1. Handle missing values** | Missing name becomes `Unknown Customer.`; `None`, `NULL` and invalid usage hours become `0`; non-numeric fees become `None` |
| **2. Remove duplicates** | Keeps the first row for each `customer_id` |
| **3. Standardise dates** | Tries four formats (`%Y-%m-%d`, `%Y/%m/%d`, `%d-%m-%Y`, `%Y%m%d`) and rewrites every date as `YYYY-MM-DD` |

---

## 📊 Results

Final dataset: **8 customers** (7 original plus 1 added through Task 2).

| Metric | Value |
|---|---|
| Total customers | 8 |
| Average monthly fee | 48.56 (calculated over the 7 customers with a valid fee) |
| Total usage hours | 633 |

**Plan distribution**

| Plan | Customers |
|---|---|
| Pro | 4 |
| Basic | 2 |
| Enterprise | 1 |
| Unknown | 1 |

**Low-usage customers (under 50 hours):** Meena Nair (45 hrs, Basic), A. Kumar (0 hrs, Enterprise) and David (0 hrs, Pro). These are candidates for retention outreach.

**Unique plans (alphabetical):** `Basic`, `Enterprise`, `Pro`, `Unknown`

---

## 🧰 Concepts Demonstrated

`dictionaries` · `lists` · `sets` · `classes (OOP)` · `functions` · `loops` · `datetime parsing` · `try / except / else / finally` · `file I/O` · `data validation`

---

## 🚀 How to Run

```bash
# 1. Clone the repository
git clone https://github.com/hasanulazad-cloud/Project-Title---Data-Cleaning-Pipeline-for-SaaS-Dataset.git
cd Project-Title---Data-Cleaning-Pipeline-for-SaaS-Dataset

# 2. Install Jupyter (the project uses only the Python standard library)
pip install jupyter

# 3. Open the notebook and run all cells in order
jupyter notebook Python_Module_End_Assessment_1_Data_Cleaning_Pipeline_for_SaaS_Dataset.ipynb
```

---

## ⚠️ Known Limitations

- **Duplicate detection uses `customer_id` only.** Customer 107 has the same name, date, plan, fee and usage as customer 101 but a different ID, so it is kept. Comparing the other fields as well would catch it, and the final count would be 7, not 8.
- **Ambiguous dates are read day-first.** `03-01-2023` becomes `2023-01-03`; it could also mean 1 March.
- **The `SaaSCustomer` class is a separate demonstration.** The pipeline works on dictionaries and does not use the class, so plan values are tidied only when metrics are calculated.
- **Output file formatting.** `saas_customers_cleaned.csv` has no header row, and the blank plan for customer 106 is saved empty rather than as `Unknown`. The placeholder name keeps a trailing full stop (`Unknown Customer.`).

---

## 🔮 Future Improvements

- Use pandas for larger datasets
- Detect duplicates on the combination of name, date and plan
- Add a header row to the CSV and use the `csv` module for safe writing
- Standardise plan names inside the pipeline
- Add unit tests for each cleaning function

---

## 👤 Author

**Hasanul H Azad**
Medical billing / RCM professional upskilling in Data Science, AI and Machine Learning
GitHub: [@hasanulazad-cloud](https://github.com/hasanulazad-cloud)

---

⭐ If you found this useful, consider starring the repo.
