# 📊 Sales Insights Data Analysis Project

An end‑to‑end **data analytics project** that transforms raw sales transaction data into **actionable business insights** using **SQL for data exploration** and **Power BI for interactive visualization**.

---

## 🚀 Project Overview

This project focuses on analyzing company sales performance across **markets, customers, products, and time periods**.
The workflow includes:

* Importing a **SQL database dump**
* Performing **exploratory data analysis using SQL queries**
* Cleaning and transforming data
* Building an **interactive Power BI dashboard** for decision‑making

The goal is to help stakeholders understand **revenue trends, customer distribution, and market performance**.

---

## 🗂 Dataset & Setup

* Source file: `db_dump.sql`
* Import the SQL dump into **MySQL / SQL Server** following the tutorial instructions
* Tables used in analysis:

  * `customers`
  * `transactions`
  * `date`

---

## 🧠 Data Analysis Using SQL

Key business questions answered using SQL:

* View all customer records

```sql
SELECT * FROM customers;
```

* Count total customers

```sql
SELECT COUNT(*) FROM customers;
```

* Transactions in **Chennai market (Mark001)**

```sql
SELECT * FROM transactions WHERE market_code = 'Mark001';
```

* Distinct products sold in Chennai

```sql
SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
```

* Transactions in **USD currency**

```sql
SELECT * FROM transactions WHERE currency = 'USD';
```

* Transactions in **year 2020** (joined with date table)

```sql
SELECT transactions.*, date.*
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020;
```

* **Total revenue in 2020**

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020
AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');
```

* **Total revenue in January 2020**

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020
AND date.month_name = 'January'
AND (transactions.currency = 'INR\r' OR transactions.currency = 'USD\r');
```

* **Total revenue in Chennai (2020)**

```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020
AND transactions.market_code = 'Mark001';
```

---

## 📈 Data Analysis Using Power BI

### Data Transformation

A normalized revenue column (`norm_amount`) is created to convert **USD to INR**:

```powerbi
= Table.AddColumn(#"Filtered Rows", "norm_amount",
    each if [currency] = "USD" or [currency] = "USD#(cr)"
    then [sales_amount] * 75
    else [sales_amount],
    type any)
```

### Dashboard Insights

The Power BI dashboard provides:

* **Total revenue trends over time**
* **Market‑wise sales performance**
* **Top customers and products**
* **Year‑wise and month‑wise revenue analysis**

These insights support **data‑driven business decisions** and performance monitoring.

---

## ⚙️ Tech Stack

* **SQL** – Data extraction, joins, aggregations, and filtering
* **Power BI** – Data cleaning, modeling, and interactive dashboards
* **Data Modeling Concepts** – Star schema, measures, KPIs, and time intelligence

---

## ▶️ How to Use This Project

1. Import `db_dump.sql` into your SQL database
2. Run the provided **analysis queries**
3. Load tables into **Power BI**
4. Apply transformations and build the **dashboard visuals**

---

## 🎯 Business Value

* Identifies **high‑revenue markets and customers**
* Tracks **sales growth trends**
* Enables **strategic decision‑making using data**
* Demonstrates real‑world **data analyst workflow**

---

## 🔮 Future Improvements

* Automate **ETL pipeline** using Python
* Add **forecasting models for revenue prediction**
* Deploy dashboard to **Power BI Service** for live monitoring

---

## 🤝 Contribution

Contributions and suggestions are welcome. Feel free to fork and improve the project.

---

## ⭐ Support

If you found this project useful, consider **starring the repository** and sharing feed
