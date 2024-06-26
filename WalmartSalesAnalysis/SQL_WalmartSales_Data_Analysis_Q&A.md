

The major aim of thie project is to gain insight into the sales data of Walmart to understand the different factors that affect sales of the different branches.


 Create database
````sql
CREATE DATABASE IF NOT EXISTS walmartSales;
````

 Create table
````sql
CREATE TABLE IF NOT EXISTS sales(
	invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
    branch VARCHAR(5) NOT NULL,
    city VARCHAR(30) NOT NULL,
    customer_type VARCHAR(30) NOT NULL,
    gender VARCHAR(30) NOT NULL,
    product_line VARCHAR(100) NOT NULL,
    unit_price DECIMAL(10,2) NOT NULL,
    quantity INT NOT NULL,
    tax_pct FLOAT(6,4) NOT NULL,
    total DECIMAL(12, 4) NOT NULL,
    date DATETIME NOT NULL,
    time TIME NOT NULL,
    payment VARCHAR(15) NOT NULL,
    cogs DECIMAL(10,2) NOT NULL,
    gross_margin_pct FLOAT(11,9),
    gross_income DECIMAL(12, 4),
    rating FLOAT(2, 1)
);
````
---------------------------------------------------------------------------------------------
````sql
SELECT
	*
FROM sales;
````
---------------------------------------------------------------------------------------------
Add the "time_of_day" column
````sql

````sql
ALTER TABLE sales ADD COLUMN time_of_day VARCHAR(20);

UPDATE sales
SET time_of_day = (
	CASE
		WHEN `time` BETWEEN "00:00:00" AND "12:00:00" THEN "Morning"
        WHEN `time` BETWEEN "12:01:00" AND "16:00:00" THEN "Afternoon"
        ELSE "Evening"
    END
);
````
---------------------------------------------------------------------------------------------
Add "day_name" column
````sql
SELECT
	date,
	DAYNAME(date)
FROM sales;

ALTER TABLE sales ADD COLUMN day_name VARCHAR(10);

UPDATE sales
SET day_name = DAYNAME(date);
````

Add "Month_name" column

````sql
SELECT
	date,
	MONTHNAME(date)
FROM sales;

ALTER TABLE sales ADD COLUMN month_name VARCHAR(10);

UPDATE sales
SET month_name = MONTHNAME(date);
````
---------------------------------------------------------------------------------------------




---------------------------- Generic ------------------------------ -->

Q1 : How many unique cities does the data have? -->
````sql
SELECT 
	DISTINCT city
FROM sales;
````
Q2 : In which city is each branch?
````sql
SELECT 
	DISTINCT city,
    branch
FROM sales;
````
------------------------------ Product -------------------------------

Q3 How many unique product lines does the data have?

````sql
SELECT
	DISTINCT product_line
FROM sales;
````

Q4 What is the most selling product line

````sql
SELECT
	SUM(quantity) as qty,
    product_line
FROM sales
GROUP BY product_line
ORDER BY qty DESC;
````
--------------------------------------------------------------------------------------------
Q5 : What is the most selling product line

````sql
SELECT
	SUM(quantity) as qty,
    product_line
FROM sales
GROUP BY product_line
ORDER BY qty DESC;
````
--------------------------------------------------------------------------------------------
Q6 : What is the total revenue by month

````sql
SELECT
	month_name AS month,
	SUM(total) AS total_revenue
FROM sales
GROUP BY month_name 
ORDER BY total_revenue;
````
--------------------------------------------------------------------------------------------
Q7 : What month had the largest COGS?
````sql
SELECT
	month_name AS month,
	SUM(cogs) AS cogs
FROM sales
GROUP BY month_name 
ORDER BY cogs;
````
--------------------------------------------------------------------------------------------
Q8  What product line had the largest revenue?

````sql
SELECT
	product_line,
	SUM(total) as total_revenue
FROM sales
GROUP BY product_line
ORDER BY total_revenue DESC;
````
--------------------------------------------------------------------------------------------
Q9 What is the city with the largest revenue?

````sql
SELECT
	branch,
	city,
	SUM(total) AS total_revenue
FROM sales
GROUP BY city, branch 
ORDER BY total_revenue;
````
--------------------------------------------------------------------------------------------
Q10 What product line had the largest VAT?

````sql
SELECT
	product_line,
	AVG(tax_pct) as avg_tax
FROM sales
GROUP BY product_line
ORDER BY avg_tax DESC;
````

--------------------------------------------------------------------------------------------
Q11 : Fetch each product line and add a column to those product 
-- line showing "Good", "Bad". Good if its greater than average sales

````sql
SELECT 
	AVG(quantity) AS avg_qnty
FROM sales;

SELECT
	product_line,
	CASE
		WHEN AVG(quantity) > 6 THEN "Good"
        ELSE "Bad"
    END AS remark
FROM sales
GROUP BY product_line;
````


````sql
-- Which branch sold more products than average product sold?
SELECT 
	branch, 
    SUM(quantity) AS qnty
FROM sales
GROUP BY branch
HAVING SUM(quantity) > (SELECT AVG(quantity) FROM sales);
````
--------------------------------------------------------------------------------------------
Q 11 What is the most common product line by gender
````sql
SELECT
	gender,
    product_line,
    COUNT(gender) AS total_cnt
FROM sales
GROUP BY gender, product_line
ORDER BY total_cnt DESC;
````

--------------------------------------------------------------------------------------------
Q 12 What is the average rating of each product line

````sql
SELECT
	ROUND(AVG(rating), 2) as avg_rating,
    product_line
FROM sales
GROUP BY product_line
ORDER BY avg_rating DESC;

````

--------------------------------------------------------------------
-------------------------- Customers -------------------------------
-------------------------------------------------------------------- 



How many unique customer types does the data have?

````sql
SELECT
	DISTINCT customer_type
FROM sales;
````
--------------------------------------------------------------------------------------------
 How many unique payment methods does the data have?

````sql
SELECT
	DISTINCT payment
FROM sales;
````
--------------------------------------------------------------------------------------------

What is the most common customer type?

````sql
SELECT
	customer_type,
	count(*) as count
FROM sales
GROUP BY customer_type
ORDER BY count DESC;
````
--------------------------------------------------------------------------------------------

Which customer type buys the most?

````sql
SELECT
	customer_type,
    COUNT(*)
FROM sales
GROUP BY customer_type;
````
--------------------------------------------------------------------------------------------
What is the gender of most of the customers?
````sql
SELECT
	gender,
	COUNT(*) as gender_cnt
FROM sales
GROUP BY gender
ORDER BY gender_cnt DESC;
````

--------------------------------------------------------------------------------------------
What is the gender distribution per branch?

````sql
SELECT
	gender,
	COUNT(*) as gender_cnt
FROM sales
WHERE branch = "C"
GROUP BY gender
ORDER BY gender_cnt DESC;
````

--------------------------------------------------------------------------------------------

Which time of the day do customers give most ratings? 

````sql
SELECT
	time_of_day,
	AVG(rating) AS avg_rating
FROM sales
GROUP BY time_of_day
ORDER BY avg_rating DESC;
````



Which time of the day do customers give most ratings per branch? 

````sql
SELECT
	time_of_day,
	AVG(rating) AS avg_rating
FROM sales
WHERE branch = "A"
GROUP BY time_of_day
ORDER BY avg_rating DESC;

````

--------------------------------------------------------------------------------------------

Which day fo the week has the best avg ratings? -->

````sql
SELECT
	day_name,
	AVG(rating) AS avg_rating
FROM sales
GROUP BY day_name 
ORDER BY avg_rating DESC;
````

--------------------------------------------------------------------------------------------
why is that the case, how many sales are made on these days? 

````sql
SELECT 
	day_name,
	COUNT(day_name) total_sales
FROM sales
WHERE branch = "C"
GROUP BY day_name
ORDER BY total_sales DESC;
````



 -- ---------------------------- Sales ---------------------------------
-- -------------------------------------------------------------------- -->

 Number of sales made in each time of the day per weekday

````sql
SELECT
	time_of_day,
	COUNT(*) AS total_sales
FROM sales
WHERE day_name = "Sunday"
GROUP BY time_of_day 
ORDER BY total_sales DESC;
 Evenings experience most sales, the stores are 
filled during the evening hours

````

--------------------------------------------------------------------------------------------

Which of the customer types brings the most revenue?

````sql
SELECT
	customer_type,
	SUM(total) AS total_revenue
FROM sales
GROUP BY customer_type
ORDER BY total_revenue;
````
--------------------------------------------------------------------------------------------
Which city has the largest tax/VAT percent?
````sql
SELECT
	city,
    ROUND(AVG(tax_pct), 2) AS avg_tax_pct
FROM sales
GROUP BY city 
ORDER BY avg_tax_pct DESC;
````
--------------------------------------------------------------------------------------------
Which customer type pays the most in VAT? 
````sql
SELECT
	customer_type,
	AVG(tax_pct) AS total_tax
FROM sales
GROUP BY customer_type
ORDER BY total_tax;
````
-- --------------------------------------------------------------------
