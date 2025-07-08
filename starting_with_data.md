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


Question 4: What was the average time spent on the site between those that made and did not make a purchase? 

SQL Queries:

SELECT 
  CASE 
    WHEN s.transaction_revenue IS NOT NULL THEN 'Purchasers' 
    ELSE 'Non-Purchasers' 
  END AS visitor_type,
  ROUND(AVG(a.time_on_site), 2) AS avg_time_on_site_seconds
FROM analytics a
LEFT JOIN all_sessions_cleaned s
  ON a.full_visitor_id = s.full_visitor_id
GROUP BY visitor_type;

Answer:

Non-purchasers: 709 seconds or 11.78 minutes
Purchasers: 212.5 seconds or 3.54 minutes

This suggests that non purchasers were not converting as they did not find what they wanted or possibly only browsing. Would be interesting to if there is a pattern in what products they were investigating and if there are ways the marketing department could use that in their next targeted campaign. 

Other suggestions could also be if there are problems or friction at checkout. 



Question 5: 

SQL Queries:

Answer:
