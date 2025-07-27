# 🏦 Bankind EDA & Power BI Dashboard Project

<img src="https://img.freepik.com/premium-vector/banking-logo-blue-color_448156-390.jpg" alt="Banking Logo" width="450"/>

> 🔍 A complete exploratory data analysis and visualization project on a fictional banking dataset using **Python (pandas, seaborn, matplotlib)** and **Power BI**. It combines SQL-based data retrieval, statistical exploration, feature engineering, and rich visual storytelling via dashboards.

---

## 📊 Power BI Dashboard Overview

The Power BI report (`Banker_case.pbix`) is an interactive dashboard designed to summarize key metrics from 3,000+ banking customer records and uncover patterns in financial behavior, risk classification, and product holdings.

### ✅ Key Power BI Pages

- **Customer Overview**
  - Total Customers, Average Age, Total Deposits, Avg Estimated Income
  - Filters: Gender, Region, Occupation, Risk Weighting

- **Product & Service Adoption**
  - Distribution of customers with:
    - Credit Cards
    - Savings / Checking Accounts
    - Foreign Currency Accounts
    - Superannuation Savings
    - Business Lending

- **Loyalty & Fee Structure**
  - Most common fee types: High > Mid > Low
  - Loyalty levels: Jade, Silver, Gold, Platinum
  - Pie & bar charts to visualize fee/loyalty segments

- **Risk Weighting vs Lending**
  - Boxplots comparing business lending by risk class
  - Heatmap of financial KPIs by risk segment

- **Income & Deposit Analysis**
  - Income Band segmentation (Low, Medium, High)
  - Correlation between deposit amount and account holdings

---

## 🧪 Python EDA Summary

The dataset (`banking_case.customer`) was accessed via **MySQL**, cleaned and analyzed in **Python**.

### 🧷 Dataset Overview

- **Records**: 3,000 customers
- **Columns**: 25
- **Nulls**: None
- **Types**: 8 object, 8 int, 9 float

### 🔸 Major Fields:

- `Client ID`, `Name`, `Age`, `GenderId`, `Nationality`, `Occupation`
- Financials: `Estimated Income`, `Credit Card Balance`, `Superannuation Savings`, `Bank Loans`, `Bank Deposits`
- Accounts: `Saving Accounts`, `Checking Accounts`, `Foreign Currency Account`, `Business Lending`
- Categorical: `Fee Structure`, `Loyalty Classification`, `Risk Weighting`, `Properties Owned`, `BRId`, `IAId`

---

## 🧠 Key Feature Engineering

### 📌 Income Band Classification

```python
bins = [0, 100000, 300000, float('inf')]
labels = ['Low', 'Med', 'High']
df['Income Band'] = pd.cut(df['Estimated Income'], bins=bins, labels=labels, right=False)
```

| Income Band | Count |
|-------------|-------|
| Low         | 1,027 |
| Medium      | 1,517 |
| High        | 456   |

---

## 📈 Visual Explorations in Python

### ✅ Correlation Heatmap

- `Bank Deposits` ↔ `Checking Accounts`: 0.96
- `Checking Accounts` ↔ `Saving Accounts`: 0.91
- `Bank Deposits` ↔ `Saving Accounts`: 0.94

These show strong positive relationships — customers tend to maintain balanced portfolios across account types.

### ✅ Boxplot: Business Lending vs Risk Weighting

```python
sns.boxplot(x='Risk Weighting', y='Business Lending', data=df)
```

💡 Higher risk classes tend to have lower lending approvals.

---

## 🪄 Insights Derived (Power BI + Python)

- **High-Fee Plan** is most popular; tied closely with **Jade loyalty** class.
- Most customers are in the **medium-income band**.
- Strong relationship between different account holdings and deposit behavior.
- Balanced **gender distribution**, slight male skew in high-fee categories.
- Business lending and risk rating show clear correlation.
- Few customers hold **foreign currency accounts** or **business lending products** — potential cross-sell opportunity.

---

## ⚙️ Tech Stack

| Tool/Platform         | Purpose                        |
|-----------------------|--------------------------------|
| 🐍 Python (pandas, seaborn, matplotlib) | EDA, plots, feature engineering |
| 💽 MySQL              | Data retrieval and querying    |
| 📊 Power BI           | Interactive dashboards         |
| 📝 Jupyter Notebook   | Analysis environment           |

---

## 📁 Files in This Repo

| File Name              | Description                                   |
|------------------------|-----------------------------------------------|
| `Banking.csv`          | Cleaned dataset (exported from MySQL)         |
| `Bankind_EDA_Project.pdf` | Full Jupyter Notebook in PDF format           |
| `Banker_case.pbix`     | Final Power BI report with dashboard visuals  |

---

## ✅ How to Use

1. Clone or download this repository
2. Use MySQL or open `Banking.csv` to view the data
3. Open `Banker_case.pbix` in Power BI Desktop to explore interactive insights
4. Review `.pdf` or notebook for step-by-step EDA and analysis

---

## 📌 Final Thoughts

This project combines data engineering, EDA, and BI visualization to simulate real-world banking analytics. It provides foundational insights for:

- Customer segmentation  
- Risk-based lending strategies  
- Fee optimization  
- Product targeting for cross-sell and up-sell

---

⭐️ Feel free to **fork**, **star**, or **explore** the repo.  
For feedback or collaborations, reach out via GitHub!

