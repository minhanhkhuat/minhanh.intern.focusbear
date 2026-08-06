# Using PostgreSQL for Analytics
1. SQL Query with JOIN & CASE Statements
SELECT 
    u.user_id,
    u.platform,
    COUNT(s.session_id) AS total_sessions,
    COALESCE(SUM(s.focus_mins), 0) AS total_focus_mins,
    CASE 
        WHEN SUM(s.focus_mins) >= 300 THEN 'High Engagement'
        WHEN SUM(s.focus_mins) BETWEEN 100 AND 299 THEN 'Moderate Engagement'
        ELSE 'Low / At Risk'
    END AS engagement_category
FROM users u
LEFT JOIN focus_sessions s 
    ON u.user_id = s.user_id 
   AND s.created_at >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY u.user_id, u.platform
ORDER BY total_focus_mins DESC;

2. Query Performance Tuning with EXPLAIN ANALYZE
EXPLAIN (ANALYZE, BUFFERS)
SELECT u.user_id, SUM(s.focus_mins)
FROM users u
JOIN focus_sessions s ON u.user_id = s.user_id
WHERE s.created_at >= '2026-01-01'
GROUP BY u.user_id;

3. Advanced PostgreSQL Analytics Features
-- Calculate a 7-day moving average of focus duration per user
SELECT 
    user_id,
    created_at,
    focus_mins,
    AVG(focus_mins) OVER (
        PARTITION BY user_id 
        ORDER BY created_at 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) AS rolling_7day_avg
FROM focus_sessions;

4. Native JSONB Support

-- Query nested JSON data and check key containment using JSONB operators
SELECT 
    user_id,
    settings->>'theme' AS selected_theme,
    settings->'notifications'->>'email' AS email_notifications_enabled
FROM user_profiles
WHERE settings @> '{"beta_tester": true}';

## Reflection

1. What makes PostgreSQL a good choice for data analytics?
- Advanced Analytics Toolkit: Supports window functions, Common Table Expressions (CTEs), rollup sets, and native JSONB indexing for semi-structured data.
- Extensibility & Ecosystem: Integrates seamlessly with Python/Pandas data pipelines and supports extensions like `pgvector` for AI vector embeddings and `PostGIS` for spatial analytics.
- ACID Compliance & Concurrency: Multi-Version Concurrency Control (MVCC) allows running complex analytical read queries in parallel without locking write operations.
- Sophisticated Indexing: Offers diverse index types (B-Tree, GIN, GiST, BRIN) to accelerate high-volume range and JSON field filtering.

2. How do JOIN operations help in analyzing relational data?
- Contextual Data Merging: Connects normalized, isolated tables (e.g., joining a `users` table with a `focus_sessions` table) to build a unified analytical view.
- Multi-Dimensional Segmentation: Allows slicing user behavior metrics across relational attributes such as subscription tiers, signup dates, and operating systems.
- Data Integrity Maintenance: Enables normalized storage to prevent data duplication while allowing flexible, ad-hoc relationships during query execution.

3. What are window functions, and how can they be used for user trend analysis?
Window functions compute calculations across a specific set of rows (a frame) related to the current row without collapsing the result set into a single aggregated row like `GROUP BY` does.
- Rolling Averages: Calculating 7-day or 30-day moving averages of daily focus duration to smooth out weekly volatility.
- Lag & Lead Analysis: Using `LAG()` or `LEAD()` to compare current session performance against a user's previous session to measure improvement.
- User Ranking & Retention: Employing `ROW_NUMBER()` or `DENSE_RANK()` to identify top active users or trace user activity sequences over time.

4. Why is query optimization important, and how does EXPLAIN ANALYZE help?
Query optimization prevents server resource exhaustion, cuts execution time, and keeps analytical dashboards responsive when querying large datasets.
- `EXPLAIN ANALYZE` Mechanics: Executes the query and returns the database optimizer's exact execution tree along with actual time elapsed, row counts, and memory buffer usage.
- Bottleneck Identification: Highlights inefficient Sequential Scans (`Seq Scan`) where an Index Scan should be applied.
- Join & Sorting Inspection: Exposes expensive disk-based sorting and sub-optimal join algorithms (e.g., Nested Loops on high-cardinality tables) so engineers can refine query structure or indexing.