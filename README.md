# 🏦 Bankind EDA Project

![Bankind Logo](https://github.com/user-attachments/assets/ce464601-e6ed-4216-b902-756bfa258e4c/logo.png)


---

## 📁 Dataset Description

This project involves exploratory data analysis on a fictional banking dataset from **Bankind**, containing **3,000 customer records** and **25 columns**. The data was retrieved using MySQL and analyzed with Python libraries like `pandas`, `matplotlib`, `seaborn`, and `numpy`.

### 🔸 Features Include:

- Customer Details: `Client ID`, `Name`, `Age`, `Location ID`, `Joined Bank`
- Demographics: `GenderId`, `Nationality`
- Financial Information: `Estimated Income`, `Credit Card Balance`, `Bank Loans`, `Bank Deposits`
- Banking Behavior: `Fee Structure`, `Loyalty Classification`, `Superannuation Savings`
- Product Holdings: `Checking Accounts`, `Saving Accounts`, `Foreign Currency Account`, `Business Lending`
- Categorical Identifiers: `BRId`, `IAId`, `Risk Weighting`, `Properties Owned`

---

## 🔍 Step-by-Step EDA Process

---

### ✅ Step 1: Connecting to MySQL & Loading Data

We started by connecting to a local MySQL database using `mysql-connector-python` and executed a simple `SELECT * FROM banking_case.customer` query.

```python
import mysql.connector
import pandas as pd

# connect to server
cnx = mysql.connector.connect(
    host="127.0.0.1",
    port=3306,
    user="root",
    password="SAP@123#suj"
)

query = "SELECT * FROM banking_case.customer"
df = pd.read_sql(query, cnx)
cnx.close()
```

---

### 📏 Step 2: Initial Exploration

```python
df.shape  # (3000, 25)
df.info()
df.head()
```

- Total rows: **3000**
- Total columns: **25**
- No null/missing values.
- Data types: 8 object, 8 int64, 9 float64

---

### 📋 Step 3: Feature Engineering – Income Band

To group customers by income levels, we created a new categorical column `Income Band`:

```python
bins = [0, 100000, 300000, float('inf')]
labels = ['Low', 'Med', 'High']
df['Income Band'] = pd.cut(df['Estimated Income'], bins=bins, labels=labels, right=False)
```

📊 **Value counts:**

- Low: 1,027 customers
- Med: 1,517 customers
- High: 456 customers

---

### 📉 Step 4: Descriptive Statistics

```python
df.describe()
```

Key insights:

- **Age**: Min = 17, Max = 85, Mean = 51
- **Estimated Income**: Min = ₹15,919, Max = ₹5,22,330
- **Credit Card Balance**: Avg ≈ ₹3,176; Max = ₹13,991
- **Bank Deposits**: Up to ₹38 Lakhs
- **Superannuation Savings**: Avg ≈ ₹25K

---

### 🔢 Step 5: Categorical Variable Distribution

We explored these categorical columns:

```python
categorical_cols = ['BRId','GenderId','IAId','Amount of Credit Cards','Nationality',
                    'Occupation','Fee Structure','Loyalty Classification',
                    'Properties Owned','Risk Weighting','Income Band']
```

**Examples:**

- `Nationality`: European > Asian > American > Australian > African
- `Fee Structure`: High (1476), Mid (962), Low (562)
- `Loyalty Classification`: Jade (1331), Silver (767), Gold (585), Platinum (317)
- `Amount of Credit Cards`: Mostly 1 or 2

```python
for col in categorical_cols:
    sns.countplot(data=df, x=col, hue='GenderId')
    plt.xticks(rotation=45)
    plt.show()
```

---

### 📊 Step 6: Numerical Analysis (Univariate)

Selected numerical columns:

```python
numerical_cols = ['Estimated Income','Superannuation Savings','Credit Card Balance',
                  'Bank Loans','Bank Deposits','Checking Accounts',
                  'Saving Accounts','Foreign Currency Account','Business Lending']
```

We plotted histograms to observe distributions:

```python
plt.figure(figsize=(15, 8))
for i, col in enumerate(numerical_cols):
    plt.subplot(3, 3, i+1)
    sns.histplot(df[col], kde=True)
    plt.title(col)
plt.tight_layout()
plt.show()
```

🔍 Observation:

- Strong right skew in most financial fields (few customers have very high balances).

---

### ♨️ Step 7: Correlation Heatmap

To understand relationships between financial variables:

```python
correlation_matrix = df[numerical_cols].corr()
plt.figure(figsize=(12, 12))
sns.heatmap(correlation_matrix, annot=True, cmap="crest", fmt=".2f")
plt.title("Correlation Matrix")
plt.show()
```

📌 Top correlations:

- `Bank Deposits` ↔ `Checking Accounts`: 0.96
- `Bank Deposits` ↔ `Saving Accounts`: 0.94
- `Checking Accounts` ↔ `Saving Accounts`: 0.91

These suggest that customers with large amounts in one account type tend to hold high balances across others as well.

---

### 📈 Step 8: Pie Chart – Fee Structure

```python
fee_counts = df['Fee Structure'].value_counts()
plt.pie(fee_counts, labels=fee_counts.index, autopct='%1.1f%%', startangle=90,
        colors=['#ff9999', '#66b3ff', '#99ff99'])
plt.axis('equal')
plt.title("Distribution of Fee Structure")
plt.show()
```

📝 High Fee Plan is the most common.

---

### 📦 Step 9: Boxplot – Business Lending vs Risk Weighting

```python
sns.boxplot(x='Risk Weighting', y='Business Lending', data=df, palette='viridis')
plt.title('Business Lending Distribution by Risk Weighting')
plt.xlabel('Risk Weighting')
plt.ylabel('Business Lending ($)')
plt.show()
```

💡 Shows clear variance in lending amounts across different risk profiles.

---

## 💡 Key Insights

- Strong correlation between various types of account balances.
- High-fee structure and Jade loyalty dominate the customer base.
- Medium-income customers form the majority segment.
- Gender distribution is nearly even.
- Business lending varies significantly by risk level.

---

## ⚙️ Technologies Used

- Python 3.x
- Jupyter Notebook
- Libraries: `pandas`, `matplotlib`, `seaborn`, `mysql-connector-python`
- MySQL (local server connection)

---

## 📁 Files Included

- `Banking.csv` – Raw dataset.
- `Bankind_EDA_Project.pdf` – Full notebook with code, visualizations, and insights.

---

## ✅ Final Notes

This EDA process offers a foundation for deeper analytics like customer segmentation, credit scoring, churn prediction, and cross-sell/up-sell strategies for financial products.

Feel free to fork, star, or clone this repository to explore more!
