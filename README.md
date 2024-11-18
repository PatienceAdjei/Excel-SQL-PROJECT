PIZZA SALES SQL QUERIES
A KPI’s

1.	Total Revenue:
select SUM(total_price)AS Total_Revenue from pizza_sales

 


2.	Average Order Value :
select * from pizza_sales

select SUM(total_price)/ COUNT(DISTINCT order_id) as Avg_Order_Value from pizza_sales

 

3.	Total Pizza Sold
select SUM(quantity) AS Total_Pizza_Sold from pizza_sales

 

4.	Total Orders:
 
select COUNT(DISTINCT order_id) from pizza_sales

 
5.	Average Pizza per Order:
select  CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) /
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) AS Avg_Pizza_Per_Order from pizza_sales

 


CHARTS

1.	--Daily Trend
select DATENAME(DW, order_date) as order_day, COUNT(DISTINCT order_id) AS Total_orders
from pizza_sales
GROUP BY DATENAME(DW, order_date)

2.	--Hourly Trend
select DATEPART(HOUR, order_time) AS order_hours, COUNT(DISTINCT order_id) AS Total_orders
from pizza_sales
GROUP BY DATEPART(HOUR, order_time)
ORDER BY DATEPART(HOUR, order_time)

3.	Percentage of sales by Pizza Category

SELECT pizza_category, sum(total_price) as Total_Sales, sum(total_price) * 100 / 
(SELECT sum(total_price) from pizza_sales WHERE MONTH(order_date) = 1) AS Percentage_of_Sales
from pizza_sales 
WHERE MONTH(order_date) = 1
GROUP BY pizza_category

4.	Percentage of sales by Pizza Size
SELECT pizza_size, CAST(sum(total_price) AS DECIMAL (10,2)) as Total_Sales, CAST(sum(total_price) * 100 / 
(SELECT sum(total_price) from pizza_sales WHERE DATEPART(quarter, order_date) = 1) AS DECIMAL (10,2)) AS PCT
from pizza_sales 
WHERE DATEPART(quarter, order_date)=1
GROUP BY pizza_size
ORDER BY PCT DESC

5.	Total Pizzas Sold by Pizza Category
SELECT pizza_category, sum(quantity) as Total_pizzas_sold
from pizza_sales
Group by pizza_category
6.	Top 5 Best Sellers by Total Pizzas Sold:

SELECT TOP 5 pizza_name, sum(quantity) as Total_Pizzas
from pizza_sales
GROUP BY pizza_name
ORDER BY sum(quantity) DESC


7.	Bottom 5 Worst Sellers by Total Pizzas Sold:

SELECT TOP 5 pizza_name, sum(quantity) as Total_Pizzas
from pizza_sales
GROUP BY pizza_name
ORDER BY sum(quantity) ASC





