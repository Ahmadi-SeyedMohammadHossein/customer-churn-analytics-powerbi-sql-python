# 📊 Customer Churn Analytics — End-to-End Data Project

> **Tools:** Python · SQL · Power BI · DAX  
> **Domain:** Telecom / CRM  
> **Dataset:** 7,043 customers · 32 features  
> **Type:** End-to-End Personal Portfolio Project

---

## 🎯 Business Problem

In subscription-based businesses, losing customers is more expensive than acquiring new ones.
This project analyzes a real telecom dataset to answer three core business questions:

- **Why** do customers leave?
- **Who** is at highest risk of churning?
- **What** actions can the business take to reduce churn?

---

## 📌 Key Results

| Metric | Value |
|--------|-------|
| 📦 Total Customers | 7,043 |
| ❌ Churned Customers | 1,869 |
| 📉 **Churn Rate** | **26.5%** |
| 💰 Average CLTV | $4,400 |
| ⚠️ Highest Risk Segment | Month-to-month · High charges · New customers |

---

## 🔍 Key Insights

### 1 · Contract Type is the Strongest Churn Predictor
Month-to-month customers churn at dramatically higher rates than one-year or two-year contract holders.
Customers on flexible contracts have no switching cost — making them the highest-risk segment.

### 2 · High Monthly Charges Correlate with Churn
Customers in the **High** charge segment (>$70/month) show the highest churn volume.
Combined with month-to-month contracts, this creates a critical risk profile.

### 3 · New Customers Are Most Vulnerable
Customers in the **New** tenure category churn more than Mid or Long-term customers.
The first 12 months are the most critical window for retention interventions.

### 4 · Electronic Check Users Churn Most
Among payment methods, **Electronic check** users show significantly higher churn —
possibly indicating lower engagement and weaker commitment to the service.

### 5 · Top Churn Reasons (from Churn Reason field)
- Competitor made a better offer
- Competitor had better devices
- Customer moved
- Competitor offered more data / faster speeds

> 💡 **Business Recommendation:** Focus retention budget on Month-to-month + High-charge + New customers.
> A targeted offer in month 3–6 could significantly reduce churn in the highest-risk segment.

---

## 🛠️ Tools & Technologies

| Layer | Tools Used |
|-------|-----------|
| Data Cleaning & EDA | Python · Pandas · NumPy · Matplotlib · Seaborn |
| Data Analysis | SQL (MySQL) |
| Dashboard & KPIs | Power BI · DAX |
| Data Preparation | Excel · Power Query |

---

## 📁 Project Structure

```
customer-churn-analytics-powerbi-sql-python/
│
├── python/
│   ├── churn_analysis1.ipynb        # Data cleaning, EDA, feature engineering
│   └── churn_analysis2.ipynb        # Segmentation analysis & visualizations
│
├── sql/
│   ├── sql_churn_analysis.png       # Contract & segment churn queries
│   └── sql_total_customers.png      # Customer count & churn rate queries
│
├── powerbi/
│   ├── Dashboard.pbix                            # Power BI source file
│   ├── Customer Churn Analysis Dashboard.mp4    # Dashboard walkthrough (30s)
│   ├── dashboard_preview.png                    # Dashboard screenshot
│   ├── Telco_customer_churn_cleaned.csv         # Cleaned dataset (7,043 rows)
│   └── Telco_customer_churn_dashboard.csv       # Dashboard-ready aggregated data
│
└── README.md
```

---

## 📊 Dashboard Preview

![Customer Churn Analysis Dashboard](./powerbi/dashboard_preview.png)

> 🎬 [Watch Dashboard Walkthrough (30s)](./powerbi/Customer%20Churn%20Analysis%20Dashboard.mp4)

**Dashboard includes:**
- KPI Cards: Total Customers · Total Churned · Avg CLTV · Churn Rate %
- Churn by Contract Type (bar chart)
- Churn by Tenure Category (bar chart)
- Churn by Payment Method (bar chart)
- Monthly Charges vs Churn (bar chart)
- Interactive slicers: Gender · Internet Service · Contract Type

---

## 🗄️ SQL Analysis

Key queries used in this project:

```sql
-- Churn Rate
SELECT 
    ROUND(100.0 * SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*), 2) 
    AS churn_rate
FROM customers;

-- Churn by Contract Type
SELECT 
    Contract,
    COUNT(*) AS total_customers,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS churn_rate
FROM customers
GROUP BY Contract
ORDER BY churn_rate DESC;

-- Monthly Charges Segmentation
SELECT 
    CASE 
        WHEN MonthlyCharges < 35 THEN 'Low'
        WHEN MonthlyCharges BETWEEN 35 AND 70 THEN 'Medium'
        ELSE 'High'
    END AS charge_segment,
    COUNT(*) AS total_customers,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned_customers
FROM customers
GROUP BY charge_segment;
```

---

## ⚙️ DAX Measures (Power BI)

```dax
-- Churn Rate
Churn Rate % = 
DIVIDE(
    CALCULATE(COUNTROWS(customers), customers[Churn] = "Yes"),
    COUNTROWS(customers),
    0
) * 100

-- High Risk Customers
High Risk Customers =
CALCULATE(
    COUNTROWS(customers),
    customers[Contract] = "Month-to-month",
    customers[MonthlyCharges] > 70
)

-- Average CLTV
Avg CLTV = AVERAGE(customers[CLTV])
```

---

## 📂 Dataset

| Field | Detail |
|-------|--------|
| Source | IBM Telco Customer Churn Dataset |
| Records | 7,043 customers |
| Features | 32 columns (demographics · services · billing · churn info) |
| Key fields | Contract · MonthlyCharges · Tenure · Churn Reason · CLTV · Churn Score |

---

## 🚀 How to Run

**Python Notebooks:**
```bash
git clone https://github.com/Ahmadi-SeyedMohammadHossein/customer-churn-analytics-powerbi-sql-python
cd customer-churn-analytics-powerbi-sql-python
jupyter notebook python/churn_analysis1.ipynb
```

**Power BI Dashboard:**
- Open `powerbi/Dashboard.pbix` in Power BI Desktop (free)

---

## 👤 Author

**Mohammad Hossein Ahmadi** — Data Analyst | Frankfurt am Main, Deutschland  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin&logoColor=white)](https://linkedin.com/in/seyed-mohammad-hossein-ahmadi)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-black?logo=github)](https://github.com/Ahmadi-SeyedMohammadHossein)
[![Email](https://img.shields.io/badge/Email-Contact-red?logo=microsoft-outlook&logoColor=white)](mailto:s.m.ahmadi@outlook.com)
