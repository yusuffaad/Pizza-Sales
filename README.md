# Pizza-Sales

## Overview
This project analyses key indicators for pizza sales data to gain insight into the pizza business's performance.The dataset was used for in-depth exploratory analysis using MS SQL Server and data visualization in Tableau. The analysis aimed to understand pizza sales trends, customer preferences, and popular pizza categories.

## Data Sources
The primary data source for this analysis is the [pizza_sales.csv](pizza_sales.csv) containing different information about the business in columns.

## Tools Used
- MS SQL Server: Import data, create database, write queries and create reports.
- Tableau: Connect to MS SQL Server, data processing and data visualisation

## Exploratory Data Analysis
EDA involved exploring the pizza sales data to answer the following key problem statements;
1. What are the busiest days and hours for orders?
2. Which pizza category generates the highest and least revenue?
3. Which pizza category are the most and least sold?
4. Which pizza category accounts for the largest share of sales and orders?

## Data Analysis (SQL Queries)
```sql
--The sum of the total price of all pizza orders.
SELECT SUM(total_price) as Total_Revenue 
FROM pizza_sales

--Average Pizzas Order
SELECT SUM(total_price)/COUNT(DISTINCT order_id) as Avg_Order_Value
FROM pizza_sales

--Total Pizza Sold
SELECT SUM(quantity) as Total_Pizza_Sold
FROM pizza_sales

--The total number of orders placed
SELECT COUNT(DISTINCT order_id) as Total_Orders
FROM pizza_sales

-- Average Pizza Sold per Order
SELECT CAST(CAST(SUM(quantity)as DECIMAL(10,2)) /CAST(COUNT(DISTINCT order_id) as DECIMAL(10,2)) as DECIMAL(10,2)) as Avg_Pizza_per_Order
FROM pizza_sales

-- Hourly Trend for Total Orders
SELECT DATEPART(HOUR, order_time) as order_hour, SUM(quantity) as Total_Pizzas_Sold 
FROM pizza_sales
GROUP BY DATEPART(HOUR, order_time)
ORDER BY DATEPART(HOUR, order_time)

-- Weekly Trend for Total Orders
SELECT DATEPART(ISO_WEEK, order_date) as week_number, YEAR(order_date) as Order_Year, COUNT(DISTINCT order_id) as Total_Orders
FROM pizza_sales
GROUP BY DATEPART(ISO_WEEK, order_date), YEAR(order_date) 
ORDER BY DATEPART(ISO_WEEK, order_date), YEAR(order_date) 

-- Percentage of Sales by Pizza Category
SELECT pizza_category, CAST(SUM(total_price)*100/(SELECT sum(total_price) from pizza_sales)as DECIMAL(10,2)) as Percent_Total_Sales
FROM pizza_sales
GROUP BY pizza_category

-- Percentage of Sales by Pizza Size
SELECT pizza_size, CAST(SUM(total_price)*100/(SELECT SUM(total_price) from pizza_sales) as DECIMAL(10,2)) as Percent_Total_Sales
FROM pizza_sales
GROUP BY pizza_size

-- Total pizza Sold by Pizza Category
SELECT pizza_category, SUM(quantity) as Total_Sold
FROM pizza_sales
GROUP BY pizza_category

-- Top 5 Best Sellers by Revenue 
SELECT TOP 5 pizza_name, SUM(total_price) as Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC

-- Bottom 5 Sellers by Revenue
SELECT TOP 5 pizza_name, SUM(total_price) as Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue

-- Top 5 Best Sellers by Total Quantity
SELECT TOP 5 pizza_name, SUM(quantity) as Total_Quantity
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity DESC

-- Bottom 5 Sellers by Total Quantity
SELECT TOP 5 pizza_name, SUM(quantity) as Total_Quantity
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Quantity
 
-- Top 5 Sellers by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id)  as Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC
 
-- Bottom 5 Sellers by Total Orders
SELECT TOP 5 pizza_name, COUNT(DISTINCT order_id)  as Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders
```
## Data Visualisation Tableau
 






 






 


