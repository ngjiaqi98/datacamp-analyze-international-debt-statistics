# datacamp-analyze-international-debt-statistics

Three SQL cells have been created for you in the workbook, please write SQL queries in each of these cells to answer the following:

What is the number of distinct countries present in the database? The output should be single row and column aliased as total_distinct_countries. Save the query as num_distinct_countries.
What country has the highest amount of debt? Your output should contain two columns: country_name and total_debt and one row. Save the query as highest_debt_country.
What country has the lowest amount of principal repayments (indicated by the "DT.AMT.DLXF.CD" indicator code)? The output table should contain three columns: country_name, indicator_name, and lowest_repayment and one row, saved in the query lowest_principal_repayment.
Note: Creating new cells in the workbook will rename the DataFrames. Make sure that your final solution uses the names provided above.

-- num_distinct_countries 
-- Write your query here... 
SELECT COUNT(DISTINCT country_name) AS total_distinct_countries
FROM international_debt;

-- highest_debt_country 
-- Write your query here... 
SELECT 
    country_name,
    SUM(debt) as total_debt
FROM international_debt
GROUP BY country_name
ORDER BY total_debt DESC
LIMIT 1;

-- lowest_principal_repayment 
-- Write your query here... 
SELECT 
    country_name, 
    indicator_name,
    debt AS lowest_repayment
FROM international_debt
WHERE indicator_code = 'DT.AMT.DLXF.CD'
  AND debt = (
    SELECT MIN(debt)
    FROM international_debt
    WHERE indicator_code = 'DT.AMT.DLXF.CD'
);

