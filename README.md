# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals  
The raw data in this project revolves around online sessions, product information, and sales reports for an online platform.  
The goal of this project was to review web session data and related datasets to uncover patterns in user behaviour and identify high-value customers and popular product categories.

## Process

Step 1: Data Import and Cleaning  
- Imported all provided datasets into PostgreSQL and created the necessary tables.  
- Removed duplicate rows using SELECT DISTINCT.  
- Normalized city, country, product names, and category fields.  
- Scaled monetary fields such as transaction_revenue from micros to standard USD values.  
- Identified and handled missing or null values to ensure consistency.

Step 2: Data Analysis Using SQL  
- Used SQL to explore user activity and purchasing trends.  
- Answered the following questions using joins, aggregate functions, and window functions:

1. Which cities and countries have the highest levels of transaction revenue?  
2. What is the average number of products ordered from visitors in each city and country?  
3. Is there any pattern in the types of products ordered by region?  
4. What are the top-selling products from each city and country?  
5. Can we summarize the impact of revenue generated from each city and country?

## Results

Menswear and electronics were the most popular product categories across most locations.  
Electronics stood out in several west coast US cities, particularly in California.  
A small number of cities and countries accounted for the majority of the site’s total revenue.  
Most visitors placed small orders, and conversion rates were relatively low overall.

## Challenges

Some major challenges included cleaning messy data, handling null values, and decoding micro-scaled revenue values.  
There were large amounts of duplicate records across multiple tables, and inconsistent formatting made grouping more difficult.  
The data was dense and at times overwhelming, which made staying focused on one task difficult.

## Future Goals

If I had more time, I would:
- Join more tables such as traffic_sources and user_info to explore deeper visitor behavior.  
- Calculate visitor lifetime value across multiple sessions.  
- Build a cleaner product category structure for more reliable analysis.  
- Explore time-based trends in traffic and sales.  
- Visualize the results using a dashboard tool like Tableau 

