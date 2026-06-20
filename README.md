# 📊 Tech Hardware Sales Analysis (SQL Server)

## 📌 Project Overview
This project focuses on a comprehensive Data Audit and Sales Analysis using **SQL Server (T-SQL)**. The dataset contains over 10,000 records of tech hardware sales (including Laptops, Headphones, Tablets, and Smartphones). The main goal was to perform data cleaning, examine key business metrics, evaluate category performance, and provide actionable business insights to upper management to optimize sales and inventory strategy.

---

## 🛠️ Tech Stack & Concepts Covered
* **Database Management System:** Microsoft SQL Server (SSMS)
* **SQL Techniques:** Data Aggregations (`SUM`, `AVG`, `COUNT`), Grouping (`GROUP BY`, `HAVING`), Filtering (`WHERE`), Subqueries, and Analytical Sorting (`TOP`, `ORDER BY DESC`).
* **Data Visualization:** Advanced Data Analysis & Charts.

---

## 📋 Business Questions Addressed

### 1. Category Performance Analysis
* **Question:** Which product categories generate the highest revenue, and what is the total quantity sold for each?
* **Objective:** Help inventory and marketing teams understand core revenue drivers.

### 2. High-Ticket Items Analysis
* **Question:** List all orders where the unit price (`price_per_unit`) is strictly above the average unit price across the entire store.
* **Objective:** Identify premium/luxury product trends and customer demand.

### 3. Bulk & Wholesale Orders Detection
* **Question:** Identify large transactions where the `total_sales` value exceeds the overall average order value of the store.
* **Objective:** Spot wholesale clients or bulk buyers for potential loyalty programs.

### 4. Pricing vs. Volume Matrix
* **Question:** What is the average quantity and average unit price per transaction for each specific product?
* **Objective:** Analyze customer behavior regarding price elasticity.

### 5. Product Popularity vs. Profitability
* **Question:** What are the top 5 products by total volume sold (popularity), and what is their corresponding total revenue (profitability)?
* **Objective:** Cross-examine if high-volume products always yield the highest profits.

---

## 💻 SQL Script & Queries

```sql
-- 1. Database Context Selection & Preview
USE SalesProject;
GO
SELECT TOP 10 * FROM [sales project];

-- 2. Data Cleaning: Duplicate Checking
SELECT Order_ID, COUNT(*) AS Times_Repeated
FROM [sales project]
GROUP BY Order_ID
HAVING COUNT(*) > 1;

-- 3. Category Performance
SELECT category, 
       SUM(total_sales) AS sales_per_category, 
       SUM(Quantity) AS qty_per_category 
FROM [sales project] 
GROUP BY category;

-- 4. High-Ticket Items (Subquery)
SELECT order_id, Product, price_per_unit 
FROM [sales project]
WHERE price_per_unit > (SELECT AVG(price_per_unit) FROM [sales project]);

-- 5. Bulk Orders Identification (Subquery)
SELECT order_id, Product, Quantity, total_sales  
FROM [sales project]
WHERE total_sales > (SELECT AVG(total_sales) FROM [sales project]);

-- 6. Pricing vs. Volume Matrix
SELECT product, 
       AVG(quantity) AS avg_quantity, 
       AVG(price_per_unit) AS avg_price 
FROM [sales project]
GROUP BY product;

-- 7. Top Products by Volume & Revenue
SELECT TOP 5 product, 
             SUM(quantity) AS total_qty, 
             SUM(total_sales) AS total_revenue 
FROM [sales project] 
GROUP BY product 
ORDER BY SUM(quantity) DESC;
---

## 📊 Executive Insights & Sales Report

### 1. Overall Store Performance (Key KPIs)
* **Total Revenue:** The store generated a total of **$512,383** in sales.
* **Total Volume Sold:** A total of **477 units** were successfully sold across all product lines.

### 2. Product-Level Performance
* 💻 **The Star Product (Laptop):** Laptops are the absolute leader in both volume and value, driving **$162,098** in revenue through **150 units** sold. This indicates strong market demand and high profitability.
* 🎧 **High-Efficiency Driver (Headphones):** Headphones showed outstanding performance, securing the second spot with **129 units** sold and generating **$155,194**. Despite a lower unit price compared to Tablets, its high sales volume makes it a critical revenue driver.
* 📱 **Steady Contributor (Tablet):** Tablets maintained a balanced performance, bringing in **$113,347** in total sales with **103 units** sold.
* 📞 **Underperforming Asset (Smartphone):** Smartphones sit at the bottom of the matrix, recording the lowest volume (**95 units**) and the lowest revenue (**$81,744**).

### 3. Strategic Recommendations
* **Marketing Focus:** Maintain aggressive advertising campaigns for Laptops and Headphones, as they represent the core profit engines of the business.
* **Pricing & Promotion Review:** It is highly recommended to review the pricing strategy or introduce bundled offers/discounts for Smartphones to stimulate demand and clear inventory.

---

## 📈 Dashboard Visualization
*(Below is the visual dashboard comparing sales performance against quantities sold, utilizing a professional minimalist aesthetic)*

<img width="1692" height="929" alt="image" src="https://github.com/user-attachments/assets/f62ccfc7-6353-4816-b8f6-0be10dc0b010" />


