# Retail_sales_Analysis

# Project Report: Retail Sales Analysis
________________________________________
#  Project Title:
## Retail Sales Analysis
________________________________________
# Problem Statement:
To analyze retail sales data to gain insights into customer behavior, product performance, and sales trends using SQL while addressing specific business questions to guide decision-making.
________________________________________
# Objectives:
1.	Set up a retail sales database: Create and populate a retail sales database.
2.	Data Cleaning: Identify and remove records with missing or null values.
3.	Exploratory Data Analysis (EDA): Perform basic analysis to understand the dataset.
4.	Business Analysis: Address specific business questions using SQL queries to derive actionable insights.
________________________________________
# Tools and Technologies:
1.	Database Management System: MySQL
2.	Programming Language: SQL
3.	Database Design Tools: SQL client (e.g., pgAdmin)
________________________________________
# Description:
This project uses a retail sales dataset to build SQL skills, focusing on data cleaning, exploration, and business-driven analysis. The dataset includes transaction details, customer demographics, product categories, and sales metrics.
________________________________________
# Methodology:
1.	Database Setup:
o	Created a database named retail_sales.
o	Created a table retail_sales with columns for transaction ID, sale details, customer demographics, product category, and sales metrics.
2.	Data Cleaning and Exploration:
o	Checked for missing/null values and removed records with incomplete data.
o	Counted total records, unique customers, and product categories.
3.	Business Analysis:
Addressed the following business questions using SQL:
________________________________________
Business Questions and Queries:
1.	Retrieve all columns for sales made on '2022-11-05':
SELECT * FROM retail_sales WHERE sale_date = '2022-11-05';
 
2.	Retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in November 2022:
SELECT * 
FROM retail_sales 
WHERE category = 'Clothing' 
  AND TO_CHAR(sale_date, 'YYYY-MM') = '2022-11' 
  AND quantity > 4;
 
3.	Calculate the total sales (total_sale) for each category:
SELECT category, SUM(total_sale) AS net_sale, COUNT(*) AS total_orders 
FROM retail_sales 
GROUP BY category;
 
4.	Find the average age of customers who purchased items from the 'Beauty' category:
SELECT ROUND(AVG(age), 2) AS avg_age 
FROM retail_sales 
WHERE category = 'Beauty';

 
5.	Find all transactions where the total_sale is greater than 1000:
SELECT * 
FROM retail_sales 
WHERE total_sale > 1000;
 
6.	Find the total number of transactions (transaction_id) made by each gender in each category:
SELECT category, gender, COUNT(*) AS total_trans 
FROM retail_sales 
GROUP BY category, gender 
ORDER BY category;

 
7.	Calculate the average sale for each month and find the best-selling month in each year:
SELECT year, month, avg_sale 
FROM ( 
    SELECT EXTRACT(YEAR FROM sale_date) AS year, 
           EXTRACT(MONTH FROM sale_date) AS month, 
           AVG(total_sale) AS avg_sale, 
           RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) AS rank 
    FROM retail_sales 
    GROUP BY year, month
) AS t1 
WHERE rank = 1;

 
8.	Find the top 5 customers based on the highest total sales:
SELECT customer_id, SUM(total_sale) AS total_sales 
FROM retail_sales 
GROUP BY customer_id 
ORDER BY total_sales DESC 
LIMIT 5;

 
9.	Find the number of unique customers who purchased items from each category:
SELECT category, COUNT(DISTINCT customer_id) AS cnt_unique_cs 
FROM retail_sales 
GROUP BY category;

10.	Create each shift and count the number of orders per shift (Morning <12, Afternoon 12–17, Evening >17):
WITH hourly_sale AS (
    SELECT *, 
           CASE 
               WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning' 
               WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon' 
               ELSE 'Evening' 
           END AS shift 
    FROM retail_sales
) 
SELECT shift, COUNT(*) AS total_orders 
FROM hourly_sale 
GROUP BY shift;

 
________________________________________
# Findings:
# 1.	Customer Demographics:
Sales span various age groups, with notable purchases in categories like "Clothing" and "Beauty."
# 2.	High-Value Transactions:
Several transactions exceeded $1000, indicating premium purchases.
# 3.	Sales Trends:
The monthly and shift-wise analysis provided insights into customer shopping habits and peak periods.
# 4.	Customer Insights:
Identified top-spending customers and unique buyers per category.
________________________________________
# Insights 
# 1. Customer Demographics
•	Age-Based Preferences: Customers from various age groups actively purchase items. Notably, categories like "Clothing" and "Beauty" see significant engagement, which suggests these categories are universally appealing.
•	Gender Trends: Sales data segmented by gender for each category reveal potential areas for targeted marketing and promotions.
________________________________________
# 2. High-Value Transactions
•	Premium Buyers: Several transactions exceeded $1,000, indicating the presence of a premium customer base. Products associated with these high-value purchases can be analyzed further to design exclusive offers or personalized experiences.
________________________________________
# 3. Sales Trends
•	Seasonality and Peaks: The analysis of monthly average sales and identification of the best-selling month in each year provide insights into seasonality, enabling better inventory and marketing strategies.
•	Shift Analysis: Sales are distributed across morning, afternoon, and evening shifts, with peak periods identified. Retailers can allocate resources such as staff or promotional offers accordingly.
________________________________________
# 4. Product Performance
•	Category Performance: Categories with the highest net sales (e.g., "Clothing," "Beauty") indicate strong market demand. These categories should remain a priority for inventory management and promotional campaigns.
•	Customer Engagement by Category: A count of unique buyers per category highlights customer engagement, helping in identifying underperforming or niche categories.
________________________________________
# 5. Customer Insights
•	Top-Spending Customers: The top 5 customers based on total sales represent a valuable segment. Personalizing their experience with loyalty programs or exclusive offers can increase retention and lifetime value.
•	Unique Buyers per Category: Tracking the number of distinct buyers in each category helps measure customer penetration and category appeal.
________________________________________
# 6. Operational Efficiency
•	Order Distribution by Shift: Morning, afternoon, and evening order data indicate when most transactions occur, enabling optimized staffing and operations during peak hours.
________________________________________
# Recommendations:
# 1.	Targeted Marketing Campaigns:
•	Focus marketing efforts on high-performing categories like "Clothing" and "Beauty."
•	Design campaigns tailored to specific demographics based on age and gender trends.
# 2.	Customer Retention Strategies:
•	Implement loyalty programs for high-spending customers.
•	Offer targeted discounts or promotions to unique buyers in underperforming categories.
#  3.	Seasonal and Peak Planning:
•	Align inventory and promotional activities with peak sales months and times of the day.
•	Prepare for seasonal variations to maximize sales opportunities.
# 4.	Operational Improvements:
•	Optimize staffing and logistics during identified peak hours.
•	Evaluate shift-based performance to streamline customer service and reduce wait times.
# 5.	Future Analysis:
•	Integrate promotional data and customer feedback to understand the drivers of high-value transactions and underperforming categories.
•	Leverage advanced analytics to predict future sales trends and customer preferences.
________________________________________
# Conclusion:
This project provided hands-on experience with SQL for database creation, cleaning, and analysis. The queries addressed business questions that offer actionable insights into customer behavior, sales patterns, and product performance.
________________________________________
Future Scope:
1.	Integrate additional datasets (e.g., promotions, feedback) for deeper analysis.
2.	Automate reporting using visualization tools like Power BI or Tableau.
3.	Apply advanced analytics for predictive sales forecasting.

