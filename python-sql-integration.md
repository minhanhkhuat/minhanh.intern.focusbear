# Connecting Python & Pandas to a SQL Database
import os
import pandas as pd
from dotenv import load_dotenv
from sqlalchemy import create_engine

#Load credentials from .env
load_dotenv()

user = os.getenv("DB_USER", "postgres")
password = os.getenv("DB_PASSWORD", "admin")
host = os.getenv("DB_HOST", "localhost")
port = os.getenv("DB_PORT", "5432")
db_name = os.getenv("DB_NAME", "focus_bear_db")

#1. Create connection engine using psycopg2
connection_uri = f"postgresql+psycopg2://{user}:{password}@{host}:{port}/{db_name}"
engine = create_engine(connection_uri)

#2. Fetch data directly into a Pandas DataFrame
sql_query = """
    SELECT user_id, platform, focus_mins, habits_completed, created_at
    FROM user_activity_logs;
"""
df = pd.read_sql(sql_query, con=engine)

#3. Perform Data Transformations
#- Handle missing values in numerical columns
df["focus_mins"] = df["focus_mins"].fillna(0)

#- Derived Column: Convert duration to hours
df["focus_hours"] = (df["focus_mins"] / 60).round(2)

#- Conditional Filtering & Categorization
df["engagement_level"] = df["focus_hours"].apply(lambda h: "High" if h >= 1.5 else "Standard")

#- Aggregation: Group metrics by platform
summary_df = df.groupby("platform").agg(
    active_users=("user_id", "nunique"),
    avg_focus_hours=("focus_hours", "mean"),
    total_habits=("habits_completed", "sum")
).reset_index()

print("--- Aggregated Platform Summary ---")
print(summary_df)

## Reflections


1. Why is it useful to query databases directly from Python instead of using a SQL client?
- End-to-End Automation: Eliminates manual data exports (CSV/Excel) from SQL clients (like DBeaver or pgAdmin), allowing scripts to execute queries, process data, and generate outputs on scheduled intervals automatically.
- Programmatic Dynamic Queries: Enables developers to build dynamic SQL queries using parameterized variables, loops, and conditional application logic based on user input or automated triggers.
- Seamless Pipeline Integration: Integrates database extraction directly into downstream data workflows—such as machine learning models, API endpoints, or automated notification bots—without human intervention.

2. How does psycopg differ from psycopg2?
- Modern Architecture (`psycopg3` vs `psycopg2`): `psycopg` (v3) is a complete rewrite of `psycopg2`, redesigned for modern Python standards.
- Async IO Support: `psycopg` features native asynchronous concurrency (`asyncio`), making non-blocking database queries much more efficient in high-throughput applications compared to `psycopg2`.
- Improved Type Adaptation: Offers faster, more flexible C-based type casting between Python objects and native PostgreSQL data types (such as JSONB, UUIDs, and Arrays).
- Prepared Statements: Supports server-side prepared statements natively for optimized execution speed and security.

3. How can Pandas help with post-query data transformation?
- Advanced In-Memory Cleansing: Easily handles missing records (`fillna`, `dropna`), standardizes string formats, and strips trailing spaces faster than complex SQL string functions.
- Flexible Reshaping & Pivoting: Allows multi-index grouping, array vectorization, and cross-tabulation (`pivot_table`) that can be cumbersome or slow in pure SQL.
- Rich Ecosystem Compatibility: Converts SQL results into formats compatible with plotting libraries (Matplotlib, Seaborn) or statistical models with zero formatting glue code required.

4. How could this integration be used to generate automated reports for Focus Bear?
- Automated Daily Usage Summaries: Running a background Python cron job every midnight to fetch raw focus logs, compute active user metrics via Pandas, and send daily summary digests to the team Slack or email.
- Weekly Cohort & Retention Reports: Automatically querying habit execution patterns, grouping users into registration cohorts, generating visual heatmaps, and uploading PDF reports directly to Google Drive.
- Anomaly & Churn Detection Alerting: Executing periodic queries to detect sudden drops in active focus session durations and triggering automated re-engagement workflows for at-risk users.