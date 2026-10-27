# econ3916-lab11-sql

# SQL for Economists — Joins, Windows and the Cardinality Trap

## Objective
In this lab, I learned how to use SQL with DuckDB to analyze data and compare SQL queries with pandas operations. I also explored how joins and missing values can affect results.

## Methodology
- I translated pandas operations such as filtering, sorting, grouping, and merging into SQL and compared their results.
- I used a `LEFT JOIN` to combine customer and order data, then compared Welch t-tests before and after the join.
- I used window functions, including `AVG() OVER (PARTITION BY ...)` and `RANK()`, to calculate regional averages and rankings without removing individual rows.
- I compared how SQL and pandas handle missing income values.
- I worked with a public NYC taxi Parquet dataset of about 3 million trips using DuckDB queries over HTTP.
- I asked AI to translate three pandas operations into SQL, revised my prompt to be more specific, and checked the expected row counts.

## Key Findings
The one-to-many join increased the data from **600 customers to 3,612 rows** because customers with multiple orders appeared more than once. The Welch t-test changed from **t = 0.07 (p = 0.9413)** before the join to **t = 0.71 (p = 0.4749)** afterward. This showed me that repeating observations can change statistical results even when no new customers are added.

I also learned that window functions can calculate averages and ranks while keeping the original rows. For missing data, `WHERE income != 50000` returned **3 of 5 rows** in SQL because `NULL` comparisons are not true, while the equivalent pandas filter returned **5 rows**. Adding `OR income IS NULL` made the SQL filter match pandas.

Finally, I learned that DuckDB can query a large remote Parquet dataset without first loading the whole file into a pandas DataFrame. Using AI helped me translate pandas into SQL, but I still needed to check the queries carefully, especially for joins and missing values.
