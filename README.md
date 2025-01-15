# Pizza Sales Analysis Using SQL

## Overview
This project explores the dynamic world of pizza sales through data analysis using SQL. By harnessing the power of structured queries, we aim to uncover valuable insights into sales patterns, customer preferences, and operational efficiencies in the pizza industry.

## Objective
The main goal is to analyze pizza sales data to extract actionable insights, optimize business processes, and improve decision-making. This includes exploring trends in revenue, customer preferences, and pizza performance across various dimensions.

## Features
**Basic Analysis:z**

⒈ Retrieve the total number of orders placed.

⒉ Calculate total revenue from pizza sales.

⒊ Identify the highest-priced pizza.

⒋ Determine the most commonly ordered pizza size.

⒌ List the top 5 most ordered pizza types along with their quantities.

**Intermediate Analysis:**

⒈ Perform table joins to determine the total quantity ordered for each pizza category.

⒉ Analyze order distribution across different hours of the day.

⒊ Discover category-wise pizza distribution.

⒋ Group data by date to calculate the daily average number of pizzas ordered.

⒌ Identify the top 3 pizza types based on revenue.

**Advanced Analysis:**

⒈ Calculate the percentage contribution of each pizza type to total revenue.

⒉ Examine cumulative revenue over time.

⒊ Identify the top 3 pizza types contributing to revenue within each category.

## SQL Techniques Used
**Aggregate Functions:** SUM, AVG, COUNT, etc., for deriving totals and averages.

**Joins:** To combine data from multiple tables and create meaningful relationships.

**Group By:** For segmenting data by time, categories, and other dimensions.

**Window Functions:** For cumulative calculations and ranking.

**Filtering and Sorting:** Using WHERE, HAVING, and ORDER BY clauses for precise querying.

## Key Outcomes

**This project enables businesses to:**
⦁ Gain deeper insight into customer preferences and purchasing behaviors.

⦁ Optimize inventory and resource management.

⦁ Improve overall operational efficiency and profitability.

## Technology Stack
⦁ **Database Management System (DBMS):** SQL-based relational database.

⦁ **Query Language:** SQL (Structured Query Language).

## Future Enhancements
⦁ Integration with visualization tools like Tableau or Power BI for graphical insights.

⦁ Automation of queries for real-time reporting.

⦁ Extension to include forecasting models using SQL and machine learning integration.

## 
**Project Title**: Pizza Sales Analysis

**Level**: Beginner  

**Database**: `pizzahut`

## 
This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze pizza sales data. The project involves setting up a pizza sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.


## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `pizzahut`.
- **Table Creation**: A table named `order_details`` is created to store the sales data. The table structure includes columns for

```sql
CREATE DATABASE pizzahut;

USE pizzahut;

CREATE TABLE order_details (
    order_details_id INT NOT NULL,
    order_id INT NOT NULL,
    pizza_id TEXT NOT NULL,
    quantity INT NOT NULL,
    PRIMARY KEY (order_details_id)
);
```


### 2. Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Retrieve the total number of orders placed.**:
```sql
SELECT 
    COUNT(order_id) AS total_order
FROM
    orders;
```

2. **Calculate the total revenue generated from pizza sales.**:
```sql
SELECT 
    ROUND(SUM(order_details.quantity * pizzas.price),
            2) AS total_sales
FROM
    order_details
        JOIN
    pizzas ON pizzas.pizza_id = order_details.pizza_id;
```

3. **Write a SQL query to calculate the total sales (total_sale) for each category.**:
```sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
```

4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
```

5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000
```

6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
```sql
SELECT 
    category,
    gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP 
    BY 
    category,
    gender
ORDER BY 1
```

7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**:
```sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
```

8. **Write a SQL query to find the top 5 customers based on the highest total sales **:
```sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
```

9. **Write a SQL query to find the number of unique customers who purchased items from each category.**:
```sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
```

10. **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**:
```sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
```

## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **High-Value Transactions**: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.

## Reports

- **Sales Summary**: A detailed report summarizing total sales, customer demographics, and category performance.
- **Trend Analysis**: Insights into sales trends across different months and shifts.
- **Customer Insights**: Reports on top customers and unique customer counts per category.

## Conclusion

This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

## How to Use

1. **Clone the Repository**: Clone this project repository from GitHub.
2. **Set Up the Database**: Run the SQL scripts provided in the `database_setup.sql` file to create and populate the database.
3. **Run the Queries**: Use the SQL queries provided in the `analysis_queries.sql` file to perform your analysis.
4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.

## Author - Zero Analyst

This project is part of my portfolio, showcasing the SQL skills essential for data analyst roles. If you have any questions, feedback, or would like to collaborate, feel free to get in touch!

### Stay Updated and Join the Community

For more content on SQL, data analysis, and other data-related topics, make sure to follow me on social media and join our community:

- **YouTube**: [Subscribe to my channel for tutorials and insights](https://www.youtube.com/@zero_analyst)
- **Instagram**: [Follow me for daily tips and updates](https://www.instagram.com/zero_analyst/)
- **LinkedIn**: [Connect with me professionally](https://www.linkedin.com/in/najirr)
- **Discord**: [Join our community to learn and grow together](https://discord.gg/36h5f2Z5PK)

Thank you for your support, and I look forward to connecting with you!
