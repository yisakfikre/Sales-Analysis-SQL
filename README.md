# Sales Analysis for E-commerce Business Using SQL

## Project Overview:
This project involves the analysis of sales data for an e-commerce business. The dataset contains information about customer orders, product details, payment methods, and sales performance. SQL queries were used to extract insights such as the top-selling products, monthly sales trends, highest spending customers, and more.

## Dataset:
The dataset used in this project is a CSV file with 27,000 rows. It contains the following columns:
- Order ID
- Order Date
- Customer ID
- Product ID
- Product Name
- Category
- Quantity
- Price per Unit
- Total Sale Amount
- Payment Method
- Payment Status
- Country
- Continent

## SQL Queries:
The project includes several SQL queries for analysis, such as:
- Finding the top 5 selling products by quantity sold.
- Analyzing monthly sales trends.
- Identifying the highest spending customer.
- Analyzing sales by payment method, country, and continent.
- The SQL Query used for this analysis is shown below

-- Create the database
CREATE DATABASE ecommerce_sales;

-- Create the table
CREATE TABLE ecommerce_data (
    order_id VARCHAR(20),
    order_date DATE,
    customer_id VARCHAR(20),
    product_id VARCHAR(20),
    product_name VARCHAR(100),
    category VARCHAR(50),
    quantity INT,
    price_per_unit DECIMAL(10, 2),
    total_sale_amount DECIMAL(10, 2),
    payment_method VARCHAR(50),
    payment_status VARCHAR(20),
    country VARCHAR(50),
    continent VARCHAR(50)
);
  

-- Use the database
USE ecommerce_sales


-- Import the CSV data into the table via Task > Import Flat File
-- Ensure that the CSV file is stored in a known location (e.g., '/path/to/ecommerce_data.csv')
-- Note: Modify the path and format accordingly for your SQL Server/Environment


-- Total Sales Revenue
SELECT SUM(total_sale_amount) AS total_revenue
FROM ecommerce_data;


--  Sales by Continent
SELECT continent, SUM(total_sale_amount) AS total_sales
FROM ecommerce_data
GROUP BY continent
ORDER BY total_sales DESC;


-- Total Order & Sales BY Payment Methods
SELECT payment_method, COUNT(order_id) AS total_orders, SUM(total_sale_amount) AS total_sales
FROM ecommerce_data
GROUP BY payment_method
ORDER BY total_sales DESC;


-- Number of Transactions BY Payment Methods
SELECT payment_method, COUNT(*) AS number_of_transactions
FROM ecommerce_data
GROUP BY payment_method
ORDER BY number_of_transactions DESC;


  -- Total Quantity Sold By Product Name
SELECT TOP 5 product_name, SUM(quantity) AS total_quantity_sold
FROM ecommerce_data
GROUP BY product_name
ORDER BY total_quantity_sold DESC;


-- Top 5 Customer by Spending
SELECT TOP 5 customer_id, SUM(total_sale_amount) AS total_spent
FROM ecommerce_data
GROUP BY customer_id
ORDER BY total_spent DESC;


-- Total Sale By Category
SELECT category, SUM(total_sale_amount) AS total_sales
FROM ecommerce_data
GROUP BY category
ORDER BY total_sales DESC;


-- Average Sale Value
SELECT AVG(total_sale_amount) AS avg_sale_value
FROM ecommerce_data;


-- Monthly Sales
SELECT 
    CAST(YEAR(date) AS VARCHAR(4)) + '-' + RIGHT('0' + CAST(MONTH(date) AS VARCHAR(2)), 2) AS month,
    SUM(total_sale_amount) AS monthly_sales
FROM ecommerce_data
GROUP BY YEAR(date), MONTH(date)
ORDER BY month;


-- Percentage of Orders by Payment Status
SELECT payment_status, COUNT(*) * 100.0 / (SELECT COUNT(*) FROM ecommerce_data) AS percentage_of_orders
FROM ecommerce_data
GROUP BY payment_status;


## How to Use:
1. Clone this repository.
2. Import the provided CSV data into your SQL database.
3. Run the SQL queries provided in the `sql_queries/` folder to gain insights from the data.
4. Optionally, create visualizations using tools like Power BI, Tableau, or Excel to further analyze the data.
## Download the file
You can download the SQL File and CSV file used for the analysis. Incase you want to try by yourself 

## License:
This project is licensed under the MIT License.
