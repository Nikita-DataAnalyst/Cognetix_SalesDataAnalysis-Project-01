# 📊 Cognetix Sales Data Analysis Project

This project is completed as a part of the **Cognetix Technology Data Analytics Internship (Foundational Stage - Task 1)**. It performs comprehensive sales data analysis using Python and Pandas to uncover key financial indicators, top-performing product categories, and regional distributions.

## 🛠️ Tech Stack & Libraries Used
- **Language:** Python 3.x
- **Data Manipulation:** Pandas, NumPy
- **Data Visualization:** Matplotlib, Seaborn

## 🚀 Complete Source Code
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load data with Latin-1 encoding for compatibility
df = pd.read_csv("sample_sales_data.csv", encoding="Latin-1")

# Clean Date and extract time features
df['ORDERDATE'] = pd.to_datetime(df['ORDERDATE'])
df['MONTH_NAME'] = df['ORDERDATE'].dt.strftime('%b')
df['MONTH_NUM'] = df['ORDERDATE'].dt.month

# 1. Basic Statistical KPIs Calculation
print(f"💰 Total Revenue: ${df['SALES'].sum():,.2f}")
print(f"📊 Average Sale Value: ${df['SALES'].mean():,.2f}")
print(f"📈 Max Transaction: ${df['SALES'].max():,.2f}")

# 2. Category Performance (Top Productline)
category_totals = df.groupby("PRODUCTLINE")["SALES"].sum().sort_values(ascending=False)
print("\n--- Category-wise Sales ---")
print(category_totals)

# 3. Best Selling Products (Top 10)
top_10 = df.groupby("PRODUCTCODE")["SALES"].sum().sort_values(ascending=False).head(10)

# 4. Top Performing Local Market (City)
top_city = df.groupby("CITY")["SALES"].sum().idxmax()
print(f"\n🏙️ Top Market City: {top_city}")
