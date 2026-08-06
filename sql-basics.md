# Introduction to SQL for Data Analysis
 1. SELECT: Retrieve specific columns
SELECT user_id, platform, focus_mins, habits_completed
FROM user_activity_logs;

 2. WHERE & ORDER BY: Filter active users on macOS and sort by focus duration
SELECT user_id, focus_mins, habits_completed
FROM user_activity_logs
WHERE platform = 'macOS' 
  AND focus_mins >= 30
ORDER BY focus_mins DESC;

 3. GROUP BY & HAVING: Aggregate metrics per platform and filter active platforms
SELECT 
    platform,
    COUNT(user_id) AS total_sessions,
    ROUND(AVG(focus_mins), 2) AS avg_focus_mins,
    SUM(habits_completed) AS total_habits
FROM user_activity_logs
WHERE status = 'active'
GROUP BY platform
HAVING COUNT(user_id) >= 5
ORDER BY avg_focus_mins DESC;

## Reflection

1. How does SQL help in data analysis?
- Direct Primary Source Access: Interacts directly with production databases and enterprise data warehouses without needing static file exports.
- Server-Side Scalability: Executes heavy data transformations, joins, and filtering on database engines designed to process multi-gigabyte or terabyte datasets in seconds.
- Universal Analytics Standard: Serves as the universal language across virtually all database systems (PostgreSQL, MySQL) and cloud warehouses (Snowflake, BigQuery).

2. What is the difference between filtering (WHERE) and aggregation (GROUP BY)?
- Filtering (`WHERE`): Evaluates individual row-level records *before* any grouping occurs, discarding rows that do not meet specific logical criteria.
- Aggregation (`GROUP BY`): Collapses multiple individual rows sharing common categorical values into single summary rows and computes aggregate metrics (`SUM`, `AVG`, `COUNT`) across those buckets.

3. How would you retrieve and analyze user activity data in Focus Bear’s database?
- Extract & Join: Join user account tables with activity logs on `user_id` to link demographic data (e.g., operating system) with engagement logs.
- Filter Active Contexts: Use `WHERE` clauses to isolate specific timeframes (e.g., `created_at >= CURRENT_DATE - INTERVAL '30 days'`) and valid focus sessions.
- Summarize Engagement: Apply `GROUP BY platform` along with `AVG(focus_mins)` and `SUM(habits_completed)` to identify which platform drives the highest user retention and habit completion rates.

4. Why is learning SQL important even if you primarily use Python for analytics?
- Memory & Computational Efficiency: Loading raw, unmanaged database dumps into Python causes memory overload (`MemoryError`). SQL filters and pre-aggregates massive datasets so Pandas receives clean, manageable DataFrames via `pd.read_sql()`.
- Database Interoperability: Production enterprise data lives in SQL databases. SQL is necessary to extract, clean, and model data at the storage layer before Python handles advanced statistical modeling or visualization.