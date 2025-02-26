# 🛍 Retail Sales Analysis

## 📌 Project Overview
**Project Title:** Retail Sales Analysis  
**Level:** Beginner  
**Database:** `p1_retail_db`

This project demonstrates SQL skills and techniques typically used by data analysts to **explore, clean, and analyze** retail sales data. The project involves setting up a retail sales database, performing **exploratory data analysis (EDA)**, and answering **business-related** questions through SQL queries.

This project is ideal for **beginners** who want to **build a strong foundation in SQL** and understand how to derive business insights from data.

---

## 🎯 Objectives
✅ **Set up a Retail Sales Database**: Create and populate a retail sales database with provided sales data.  
✅ **Data Cleaning**: Identify and remove any records with missing or null values.  
✅ **Exploratory Data Analysis (EDA)**: Perform basic EDA to understand the dataset.  
✅ **Business Analysis**: Use SQL queries to answer specific business questions and generate insights from the sales data.  

---

## 📂 Project Structure
```
📁 SQL-Retail-Sales-Analysis
│── 📜 README.md                # Project documentation
│── 📜 retail_sales_analysis.sql  # SQL queries for analysis
│── 📜 p1_retail_db_schema.sql   # SQL script to create tables
│── 📜 sample_data.csv           # Sample dataset (if allowed to share)
│── 📁 reports
│    ├── sales_summary.pdf       # Business insights (if generated)
│    ├── trend_analysis.pdf
│── 📁 images
│    ├── sales_trends.png        # Any visualizations from SQL results
│    ├── customer_insights.png
```

---

## 🛠 Database Setup
### **1️⃣ Database Creation**
```sql
CREATE DATABASE p1_retail_db;
```

### **2️⃣ Table Creation**
```sql
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

---

## 🔍 Data Exploration & Cleaning
### **Record Count**
```sql
SELECT COUNT(*) FROM retail_sales;
```

### **Unique Customers**
```sql
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
```

### **Unique Product Categories**
```sql
SELECT DISTINCT category FROM retail_sales;
```

### **Check for NULL Values**
```sql
SELECT * FROM retail_sales
WHERE
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

### **Delete Records with NULL Values**
```sql
DELETE FROM retail_sales
WHERE
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR
    gender IS NULL OR age IS NULL OR category IS NULL OR
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```

---

## 📊 Data Analysis & Business Insights

### **1️⃣ Retrieve All Sales for a Specific Date**
```sql
SELECT * FROM retail_sales WHERE sale_date = '2022-11-05';
```

### **2️⃣ Retrieve All Transactions for 'Clothing' Category with Quantity > 4 in Nov 2022**
```sql
SELECT * FROM retail_sales
WHERE category = 'Clothing'
AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
AND quantity >= 4;
```

### **3️⃣ Calculate Total Sales per Category**
```sql
SELECT category, SUM(total_sale) AS net_sale, COUNT(*) AS total_orders
FROM retail_sales
GROUP BY category;
```

### **4️⃣ Find Average Age of Customers Who Purchased 'Beauty' Products**
```sql
SELECT ROUND(AVG(age), 2) AS avg_age FROM retail_sales WHERE category = 'Beauty';
```

### **5️⃣ Find Transactions with Total Sale > 1000**
```sql
SELECT * FROM retail_sales WHERE total_sale > 1000;
```

### **6️⃣ Find Total Transactions by Gender in Each Category**
```sql
SELECT category, gender, COUNT(*) AS total_trans
FROM retail_sales
GROUP BY category, gender
ORDER BY category;
```

### **7️⃣ Find Best-Selling Month in Each Year**
```sql
SELECT year, month, avg_sale FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) AS year,
        EXTRACT(MONTH FROM sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) AS rank
    FROM retail_sales
    GROUP BY 1, 2
) AS t1
WHERE rank = 1;
```

### **8️⃣ Find Top 5 Customers Based on Highest Total Sales**
```sql
SELECT customer_id, SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
```

### **9️⃣ Find Unique Customers per Category**
```sql
SELECT category, COUNT(DISTINCT customer_id) AS cnt_unique_cs
FROM retail_sales
GROUP BY category;
```

### **🔟 Find Number of Orders per Shift (Morning, Afternoon, Evening)**
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
SELECT shift, COUNT(*) AS total_orders FROM hourly_sale GROUP BY shift;
```

---

## 📈 Findings
✅ **Customer Demographics**: Sales are distributed across different age groups and categories.  
✅ **High-Value Transactions**: Some transactions exceed ₹1000, indicating premium purchases.  
✅ **Sales Trends**: Monthly sales analysis helps identify peak seasons.  
✅ **Customer Insights**: Identified **top-spending customers** and **most popular product categories**.  

---

## 📊 Reports
📌 **Sales Summary**: Overview of total sales, customer demographics, and product performance.  
📌 **Trend Analysis**: Sales trends across months and shifts.  
📌 **Customer Insights**: Top customers and unique customer counts per category.  

---

## 🏁 Conclusion
This project is a **beginner-friendly SQL analysis** covering:
- **Database setup**
- **Data cleaning**
- **Exploratory data analysis (EDA)**
- **Business-driven SQL queries**

The insights from this project help in understanding **sales patterns, customer behavior, and product performance**, providing valuable business insights. 🚀

---

