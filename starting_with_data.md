Question 1: Which date had the highest number of sessions?
SQL Queries:
SELECT date, COUNT(*) AS session_count
FROM all_sessions_cleaned
GROUP BY date
ORDER BY session_count DESC
LIMIT 1;


Answer: 
 Aug 15 2016


Question 2: What are the most active users that have the most number of sessions

SQL Queries:
SELECT 
  full_visitor_id,
  COUNT(DISTINCT visit_id) AS total_sessions
FROM all_sessions_cleaned
GROUP BY full_visitor_id
ORDER BY total_sessions DESC
LIMIT 10;

Answer:
 User "3608475193341679870" with 9


Question 3: What product category appears in the most transactions? 

SQL Queries:
SELECT 
  v2product_category,
  COUNT(*) AS category_appearance_count
FROM all_sessions_cleaned
WHERE v2product_category IS NOT NULL
GROUP BY v2product_category
ORDER BY category_appearance_count DESC
LIMIT 10;


Answer:

Youtube promoted brands in home, menswear and electronics.


Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
