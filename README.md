<h1 align="center">🛒 Retail Sales Analysis using SQL (PostgreSQL)</h1>

<p align="center">
  <b>Beginner-Friendly SQL Data Analysis Project</b><br>
  Demonstrating Data Cleaning, EDA & Business Insights using PostgreSQL
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SQL-PostgreSQL-blue?style=for-the-badge&logo=postgresql">
  <img src="https://img.shields.io/badge/Level-Beginner-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Focus-Data%20Analysis-orange?style=for-the-badge">
</p>

---

## 📌 Project Overview

This project analyzes retail sales data using **PostgreSQL**.  
The objective is to demonstrate practical SQL skills including:

- Database Creation  
- Table Design  
- Data Import using COPY  
- Data Cleaning & NULL Handling  
- Exploratory Data Analysis (EDA)  
- Business Problem Solving using SQL  
- Window Functions & CTE  

---

## 🎯 Project Objectives

-  Database Setup  
-  Table Creation  
-  Data Cleaning  
-  Sales Trend Analysis  
-  Customer Analysis  
-  Category Performance Analysis  
-  Advanced SQL Queries  

---

## 🗄️ Database Details

| Component | Details |
|-----------|----------|
| Database Name | `sql_project_p1` |
| Table Name | `retail_sales` |
| Database System | PostgreSQL |

---

## 🧱 Table Structure

```sql
CREATE TABLE retail_sales(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(15),
    age INT,
    category VARCHAR(15),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);

```

---

## 📂 Data Import

```sql
COPY retail_sales
FROM 'D:\SQL_Projects\Retail_Sales_Analysis_Project_P1\Retail_Sales.csv'
DELIMITER ','
CSV HEADER;
```

---

## 🧹 Data Cleaning Process

- Checked total record count  
- Identified NULL values  
- Calculated median age using `PERCENTILE_CONT()`  
- Updated NULL age values  
- Deleted rows with critical NULL values  

### 🔎 Example (Median Age Calculation)

```sql
SELECT
  PERCENTILE_CONT(0.5)
  WITHIN GROUP (ORDER BY age) AS median_age
FROM retail_sales;
```

---

## 📊 Exploratory Data Analysis (EDA)

- Total number of sales  
- Unique customers  
- Category distribution  
- Monthly sales trends  
- Gender-wise transactions  
- Shift-wise order analysis  

---

## 📈 Business Questions Solved

### 1️⃣ Sales on Specific Date

```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

---

### 2️⃣ Clothing Sales in November 2022

```sql
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
AND quantity >= 4;
```

---

### 3️⃣ Category-wise Total Sales

```sql
SELECT category,
       SUM(total_sale) AS net_sale,
       COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

---

### 4️⃣ High-Value Transactions (>1000)

```sql
SELECT *
FROM retail_sales
WHERE total_sale > 1000;
```

---

### 5️⃣ Top 5 Customers by Total Sales

```sql
SELECT customer_id,
       SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

---

### 6️⃣ Shift-wise Order Analysis

```sql
WITH hourly_sale AS (
    SELECT *,
        CASE
            WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
            WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
            ELSE 'Evening'
        END AS shift
    FROM retail_sales
)
SELECT shift,
       COUNT(*) AS total_orders
FROM hourly_sale
GROUP BY shift;
```

---

## 🛠️ SQL Concepts Used

- Aggregate Functions (`SUM`, `AVG`, `COUNT`)  
- Window Functions (`RANK`)  
- Date Functions (`EXTRACT`, `TO_CHAR`)  
- Conditional Logic (`CASE WHEN`)  
- CTE (Common Table Expression)  
- NULL Handling  
- Data Cleaning Techniques  

---

## 📊 Key Insights

- Identified peak sales months  
- Found top spending customers  
- Analyzed category performance  
- Determined shift-wise order distribution  
- Improved overall data quality  

---

## 📂 Project Structure

```
Retail-Sales-SQL-Project/
│── README.md
│── sql_query.sql
│── Retail_Sales.csv
```

---

## ▶️ How to Run This Project

1. Install PostgreSQL  
2. Create database:

```sql
CREATE DATABASE sql_project_p1;
```

3. Create table using provided SQL  
4. Import CSV using COPY command  
5. Run analysis queries  

---

## 📷 Project Preview

(Add screenshots here)

- Table preview  
- Query outputs  
- Top 5 customers  
- Monthly sales analysis  

---

## 🚀 Skills Demonstrated

- SQL Query Writing  
- Data Cleaning  
- Exploratory Data Analysis  
- Window Functions  
- PostgreSQL  
- Business Analytics  

---

## 👤 Author

**Navneet Prajapati**  
Aspiring Data Analyst  

🔗 LinkedIn: https://www.linkedin.com/in/navneet-prajapati-delhi  

---



