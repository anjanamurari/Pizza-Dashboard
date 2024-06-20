# Pizza-Dashboard
Self Learning Project
MS SQL Server

Import CSV file of the data to the server after creating a new database.

To View the entire Table run below SQL Query.
Select * from pizza_sales;

Run SQL Queries for each KPIs

1. Total Revenue: The sum of the total price of all pizza orders.

         select SUM(total_price) as Total_Revenue from pizza_sales;

		
![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/44525371-c386-410a-baa2-150253026ca7)

2. Average Order Value: The average amount spent per order, calculated by dividing the total revenue by the total number of orders.

	select (SUM(total_price)/COUNT(DISTINCT order_id)) as Average_Order_Value from pizza_sales;

		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/65ce4ace-0152-40b1-9c57-2cce6bf0d13a)


3. Total Pizzas Sold: The sum of the quantities of all pizzas sold.

	select SUM(quantity) as Total_Pizzas_Sold from  pizza_sales;
	
	![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/b3736a5c-7f08-4d75-8a4a-37fd65e8c752)
	
	
4. Total Orders: The total number of orders placed.

	select COUNT(DISTINCT order_id) as Total_Orders from pizza_sales;
	
		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/614f4c8c-7883-4aae-8de1-79b207788dec)

		
5. Average Pizzas Per Order: The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold by the total number of orders.

	select SUM(quantity)/COUNT(DISTINCT order_id) as Average_Pizza_per_Order from pizza_sales;
	
		
	![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/0b53711a-361b-4928-b629-9c3a4198ce07)

	5.1 To convert to decimal use below

	select CAST(CAST(SUM(quantity) AS DECIMAL(10,2))/CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2)) as Average_Pizza_per_Order from pizza_sales;
	
![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/c0012d80-7f75-48e8-a82a-5a5aab5d85b5)

Run SQL queries for chart values.

1. Daily Trend for Total Orders: Create a bar chart that displays the daily trend of total orders over a specific time period. This chart will help us identify any patterns or fluctuations in order volumes on a daily basis.

	SELECT DATENAME(DW,order_date) AS Order_day , COUNT(DISTINCT order_id) as Total_Orders 
	FROM pizza_sales
	GROUP BY DATENAME(DW,order_date);
	
		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/3f40f109-6c03-42d6-ac39-ebab3a6a6601)

	
2. Hourly Trend for Total Orders: Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.

	SELECT DATEPART(HOUR, order_time) AS Order_hours , COUNT(DISTINCT order_id) as Total_Orders
	FROM pizza_sales
	GROUP BY DATEPART(HOUR, order_time)
	ORDER BY DATEPART(HOUR, order_time);
	
		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/377f7965-3cb0-4b80-8656-37aef3fd0095)


3. Percentage of Sales by Pizza Category: Create a pie chart that shows the distribution of sales across different pizza categories. This chart will provide insights into the popularity of various pizza categories and their contribution to overall sales.

	SELECT pizza_category, SUM(total_price)*100/ (SELECT SUM(total_price) from pizza_sales) AS Percentage_of_Sales from pizza_sales
	GROUP BY pizza_category;
	
		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/2f9a3cc5-52da-4eaf-ad4c-ef4c91338b77)

	
4. Percentage of Sales by Pizza Size:
Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. This chart will help us understand customer preferences for pizza sizes and their impact on sales.

	SELECT pizza_size, SUM(total_price)*100/ (SELECT SUM(total_price) from pizza_sales) AS Percentage_of_Sales from pizza_sales
	GROUP BY pizza_size;
	
		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/cc13ff8c-9579-40bc-a90c-8de0bb0eaea9)

	
5. Total Pizzas Sold by Pizza Category:
Create a funnel chart that presents the total number of pizzas sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.

	SELECT pizza_category , SUM(quantity) as Total_Pizza_Sold FROM pizza_sales
	GROUP BY pizza_category;
	![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/dcca0a54-4f08-4d19-a8ca-acd22805ef64)

		


6. Top 5 Best Sellers by Total Pizzas Sold:
Create a bar chart highlighting the top 5 best-selling pizzas based on the total number of pizzas sold. This chart will help us identify the most popular pizza options.

	SELECT TOP 5 pizza_name , SUM(quantity) AS Total_Sold
	from pizza_sales
	GROUP BY pizza_name
	ORDER BY Total_Sold DESC;
	
		![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/3cf40c4a-3d78-4b2c-8299-a01591226efb)

	
7. Bottom 5 Worst Sellers by Total Pizzas Sold:
Create a bar chart showcasing the bottom 5 worst-selling pizzas based on the total number of pizzas sold. This chart will enable us to identify underperforming or less popular pizza options.

	SELECT TOP 5 pizza_name , SUM(quantity) AS Total_Sold
	from pizza_sales
	GROUP BY pizza_name
	ORDER BY Total_Sold ASC;
	
		
	
![image](https://github.com/anjanamurari/Pizza-Dashboard/assets/39182483/9d314ddd-e68e-4726-a511-2eec82e2dca4)
