What are your risk areas? Identify and describe them.

-- 1. Duplicate Rows
-- If we don’t remove exact or near-duplicate records, we might double-count transactions, visitors, or products.

-- 2. Missing Data
-- Some sessions may have missing 'city', 'country', or 'transaction_revenue' values.
-- This could cause underreporting in revenue or geography-based analysis.

-- 3. Sparse Purchase Events
-- The vast majority of sessions may not include purchases.
-- If we only analyze revenue rows, we risk ignoring important context.

-- 4. Inconsistent Formatting
-- City or country names might be written differently (e.g., 'US' vs 'United States').
-- This could cause incorrect grouping and misleading totals.
-- This has been the most problematic risk under my observations and what I would spend the most  time going over.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

-- Quality Assurance for all_sessions table

-- 1. Check total row count
SELECT COUNT(*) AS total_rows 
FROM all_sessions;

-- 2. Check for exact duplicates
SELECT COUNT(*) AS unique_rows 
FROM (SELECT DISTINCT * 
FROM all_sessions) sub;

-- 3. Check for NULLs in important columns
SELECT 
  COUNT(*) FILTER (WHERE full_visitor_id IS NULL) AS null_visitors,
  COUNT(*) FILTER (WHERE country IS NULL) AS null_countries,
  COUNT(*) FILTER (WHERE city IS NULL) AS null_cities,
  COUNT(*) FILTER (WHERE transaction_revenue IS NULL) AS null_revenue
FROM all_sessions;

-- 4. See how many cities/countries have revenue
SELECT DISTINCT country, city 
FROM all_sessions
WHERE transaction_revenue IS NOT NULL;

-- 5. Count distinct visitors
SELECT COUNT(DISTINCT full_visitor_id) AS unique_visitors 
FROM all_sessions;

