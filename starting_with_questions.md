Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 

SELECT 
    country,
    city,
    SUM(transaction_revenue) AS total_revenue
FROM all_sessions
WHERE transaction_revenue IS NOT NULL
GROUP BY country, city
ORDER BY total_revenue DESC;



Answer:

The data shows that only the USA was the only 


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

WITH visitor_product_totals AS (
  SELECT 
    full_visitor_id,
    country,
    city,
    SUM(product_quantity) AS total_quantity
  FROM all_sessions_cleaned
  WHERE product_quantity IS NOT NULL
  GROUP BY full_visitor_id, country, city
)
SELECT 
  country,
  city,
  ROUND(AVG(total_quantity), 2) AS avg_products_per_visitor
FROM visitor_product_totals
GROUP BY country, city
ORDER BY avg_products_per_visitor DESC;

WITH visitor_product_totals AS (
  SELECT 
    full_visitor_id,
    country,
    SUM(product_quantity) AS total_quantity
  FROM all_sessions_cleaned
  WHERE product_quantity IS NOT NULL
  GROUP BY full_visitor_id, country
)
SELECT 
  country,
  ROUND(AVG(total_quantity), 2) AS avg_products_per_visitor
FROM visitor_product_totals
GROUP BY country
ORDER BY avg_products_per_visitor DESC;


Answer:

The top two countries were Spain(10) and the USA (4). The table shows that the average for all other countries was only 1 product per purchase. 



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:

WITH ranked_categories AS (
  SELECT 
    country,
    city,
    v2product_category,
    COUNT(*) AS category_order_count,
    RANK() OVER (
      PARTITION BY country, city
      ORDER BY COUNT(*) DESC
    ) AS category_rank
  FROM all_sessions_cleaned
  WHERE v2product_category IS NOT NULL
  GROUP BY country, city, v2product_category
)
SELECT *
FROM ranked_categories
ORDER BY country, city, category_rank;


Answer:


The pattern indicates that most customers purchase products that are in apparel, specifically menswear and drink ware. 


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

WITH ranked_products AS (
  SELECT 
    country,
    city,
    v2product_name,
    SUM(product_quantity) AS total_quantity,
    ROW_NUMBER() OVER (
      PARTITION BY country, city
      ORDER BY SUM(product_quantity) DESC
    ) AS rn
  FROM all_sessions_cleaned
  WHERE v2product_name IS NOT NULL AND product_quantity IS NOT NULL
  GROUP BY country, city, v2product_name
)
SELECT 
  country,
  city,
  v2product_name AS top_selling_product,
  total_quantity
FROM ranked_products
WHERE rn = 1
ORDER BY country, city;




Answer:

Upon reviewing the list of top products, there are a few patterns that stand out the top two being that security cameras/ products were the top selling product in cities across the west coast of America, predominately in California. T shirts were also very prominent on the list making it seem that they are either not as costly to ship and or produce. 



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT 
  country,
  city,
  COUNT(DISTINCT full_visitor_id) AS unique_visitors,
  SUM(transaction_revenue) / 1000000 AS total_revenue_usd,
  ROUND((SUM(transaction_revenue)::numeric / COUNT(DISTINCT full_visitor_id) / 1000000), 2) AS revenue_per_visitor_usd
FROM all_sessions_cleaned
WHERE transaction_revenue IS NOT NULL
GROUP BY country, city
ORDER BY total_revenue_usd DESC;


Answer:


I am only getting two lines that show the United States 




