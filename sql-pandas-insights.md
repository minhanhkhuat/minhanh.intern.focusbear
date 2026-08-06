# Combining SQL + Pandas for Deeper Insights
import os
import pandas as pd
from dotenv import load_dotenv
from sqlalchemy import create_engine

load_dotenv()

db_user = os.getenv("DB_USER", "postgres")
db_password = os.getenv("DB_PASSWORD", "admin")
db_host = os.getenv("DB_HOST", "localhost")
db_port = os.getenv("DB_PORT", "5432")
db_name = os.getenv("DB_NAME", "focus_bear_db")

db_url = f"postgresql://{db_user}:{db_password}@{db_host}:{db_port}/{db_name}"
engine = create_engine(db_url)

sql_query = """
SELECT 
    user_id,
    platform,
    focus_mins,
    habits_completed,
    created_at
FROM user_activity_logs
WHERE focus_mins > 0;
"""

df = pd.read_sql(sql_query, con=engine)

print(df.head())

df_filtered = df[df["platform"].isin(["macOS", "Windows"])].copy()

df_filtered["focus_hours"] = df_filtered["focus_mins"] / 60

analytics_summary = df_filtered.groupby("platform").agg(
    avg_focus_hours=("focus_hours", "mean"),
    total_habits_done=("habits_completed", "sum"),
    active_users=("user_id", "nunique")
).reset_index()

print("\n--- 2. Results---")
print(analytics_summary)

## Reflections

- Optimizing Memory Efficiency: Querying millions of raw habit logs directly in Python causes RAM bottlenecks. SQL filters logs by active date ranges first, allowing Pandas to process clean, manageable DataFrames.
- Cohort Retention Analysis: SQL aggregates user sign-up groups, while Pandas transforms the dataset into retention heatmaps using `.pivot_table()` to evaluate habit consistency over time.
- Micro-Break Algorithm Refinement: SQL extracts interrupted focus sessions, and Pandas computes correlation matrices between break frequencies and total productive time to optimize prompt timing.