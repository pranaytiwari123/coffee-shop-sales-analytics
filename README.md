# ☕ Coffee Shop Sales Analytics — MySQL & Power BI

> **End-to-End Data Analytics Project | SQL • MySQL • Power BI • Business Intelligence**

An end-to-end Coffee Shop Sales Analytics project built using **MySQL and Power BI** to transform raw transactional data into meaningful business insights.

The project covers the complete analytics workflow — from **data cleaning and transformation** to **SQL-based KPI analysis**, followed by an **interactive Power BI dashboard** for business decision-making.

---

## 📌 Project Objective

The main objective of this project is to analyze coffee shop transaction data and understand sales performance across different dimensions such as:

- Total Sales
- Total Orders
- Total Quantity Sold
- Month-over-Month (MoM) Performance
- Daily Sales Trends
- Weekday vs Weekend Performance
- Store Location Performance
- Product Category Performance
- Top 10 Products
- Sales by Day and Hour

The analysis helps convert raw transactional data into actionable insights for understanding **revenue, demand patterns, product performance and business performance**.

---

## 🔄 Project Workflow

Raw Transaction Data  
↓  
Data Understanding  
↓  
Data Cleaning & Preparation  
↓  
MySQL Database  
↓  
SQL Transformations & Analysis  
↓  
KPI Calculation  
↓  
Trend & Performance Analysis  
↓  
Power BI Dashboard  
↓  
Business Insights

---

## 🛠️ Tools & Technologies

- **MySQL** — Database management, data cleaning and analysis
- **SQL** — Data transformation, aggregation and KPI calculations
- **Power BI** — Interactive dashboards and data visualization
- **CSV** — Source transaction data

### SQL Concepts Used

`SELECT`  
`WHERE`  
`GROUP BY`  
`ORDER BY`  
`LIMIT`  
`SUM()`  
`COUNT()`  
`AVG()`  
`ROUND()`  
`CASE`  
`LAG()`  
`Window Functions`  
`Subqueries`  
`STR_TO_DATE()`  
`MONTH()`  
`DAY()`  
`DAYOFWEEK()`  
`HOUR()`  
`ALTER TABLE`  
`UPDATE`

---

## 🧹 Data Cleaning & Preparation

Before analysis, the raw dataset was cleaned and standardized in MySQL.

### Date Conversion

The transaction date was converted into a proper SQL `DATE` format:

## ```sql
(UPDATE coffee_shop_sales
SET transaction_date = STR_TO_DATE(transaction_date, '%d-%m-%Y');

ALTER TABLE coffee_shop_sales
MODIFY COLUMN transaction_date DATE;


###  1.Data Cleaning & Preparation

Before performing analysis, the raw dataset was prepared for reliable SQL analysis.

The transaction date was converted into a proper SQL date format:

UPDATE coffee_shop_sales
SET transaction_date =
STR_TO_DATE(transaction_date, '%d-%m-%Y');

The column was then converted to the DATE data type.

Time Transformation

Similarly, transaction time was converted into a proper SQL time format:

UPDATE coffee_shop_sales
SET transaction_time =
STR_TO_DATE(transaction_time, '%H:%i:%s');

The column was then converted to the TIME data type.

Schema Validation

The database structure was checked using:

DESCRIBE coffee_shop_sales;

An imported transaction ID column name was also corrected before analysis.

### 📊 2. Key Performance Indicators

The project focuses on three primary KPIs:

💰 Total Sales
SELECT
    ROUND(SUM(unit_price * transaction_qty)) AS Total_Sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5;

Sales = Unit Price × Transaction Quantity

The project uses the aggregation of this value to calculate total sales.

🧾 Total Orders
SELECT
    COUNT(transaction_id) AS Total_Orders
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5;
📦 Total Quantity Sold
SELECT
    SUM(transaction_qty) AS Total_Quantity_Sold
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5;

The project also extends quantity analysis to month-over-month performance using LAG().

### 📈 3. Month-over-Month (MoM) Analysis

One of the key analytical requirements was to understand whether performance was increasing or decreasing compared with the previous month.

The project uses the SQL window function:

LAG()

Example:

LAG(
    SUM(unit_price * transaction_qty), 1
) OVER (
    ORDER BY MONTH(transaction_date)
)

This allows the current month's performance to be compared with the previous month's performance.

MoM Growth Formula
(Current Month - Previous Month)
-------------------------------- × 100
       Previous Month

This approach was also applied to quantity sold.

### 📅 4. Daily Sales Analysis

Daily sales were calculated by grouping transactions according to the day of the month.

SELECT
    DAY(transaction_date) AS day_of_month,
    ROUND(
        SUM(unit_price * transaction_qty), 1
    ) AS total_sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5
GROUP BY DAY(transaction_date)
ORDER BY DAY(transaction_date);

This helps identify daily sales trends and high/low-performing days.

### 📊 5. Daily Sales vs Average

The project compares individual daily sales against the average daily sales.

A CASE statement categorizes each day as:

Above Average
Below Average
Average

Example logic:

CASE
    WHEN total_sales > avg_sales
        THEN 'Above Average'

    WHEN total_sales < avg_sales
        THEN 'Below Average'

    ELSE 'Average'
END AS sales_status

This provides a simple way to identify unusually strong or weak sales days.

### 🗓️ 6. Weekday vs Weekend Analysis

Sales were divided into:

Weekdays
Weekends

using DAYOFWEEK().

CASE
    WHEN DAYOFWEEK(transaction_date) IN (1,7)
        THEN 'Weekends'
    ELSE 'Weekdays'
END AS day_type

Sales were then aggregated for each group.

This helps understand recurring customer purchasing patterns.

### 🏪 7. Store Location Analysis

Sales performance was compared across different store locations.

SELECT
    store_location,
    SUM(unit_price * transaction_qty) AS Total_Sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5
GROUP BY store_location
ORDER BY SUM(unit_price * transaction_qty) DESC;

This allows high-performing and lower-performing locations to be identified.

### ☕ 8. Product Category Analysis

Sales were also analyzed by product category.

SELECT
    product_category,
    ROUND(
        SUM(unit_price * transaction_qty), 1
    ) AS Total_Sales
FROM coffee_shop_sales
WHERE MONTH(transaction_date) = 5
GROUP BY product_category
ORDER BY SUM(unit_price * transaction_qty) DESC;

This helps determine which categories contribute most to overall sales.



### Dashboard Components

## KPI Cards

Total Sales
Total Orders
Total Quantity Sold



Power BI converts SQL results into an interactive dashboard that allows users to explore performance quickly.

## Made by 
PRANAY NATH TIWARI
