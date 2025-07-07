What issues will you address by cleaning the data?


--1. Duplicate Records
Removed exact duplicate rows in all tables using DISTINCT and created tables with the queries listed below. 

--2. Inconsistent Formatting
Trimmed and standardized text fields like city, country, product names, categories, and gender.

--3. Revenue Scaling
 For tables with monetary fields (like all_sessions and transactions), divided values by 1,000,000.

--4. Missing or Null Values
Identified NULLs in user, location, and transaction fields to reduce grouping issues.



Queries:
Below, provide the SQL queries you used to clean your data.

-- 1. Create a cleaned version of the table using DISTINCT
CREATE TABLE all_sessions_cleaned AS
SELECT DISTINCT *
FROM all_sessions;

-- 2. Normalize city names
SELECT DISTINCT INITCAP(TRIM(city)) AS cleaned_city FROM all_sessions;

-- 3. Normalize country names
SELECT DISTINCT INITCAP(TRIM(country)) AS cleaned_country FROM all_sessions;

-- 4. Preview cleaned table
SELECT * FROM all_sessions_cleaned;

--I also did the same steps for Products as there were many repeated ones there as well.