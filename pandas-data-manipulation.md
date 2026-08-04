# Data Manipulation with Pandas

## Reflection 
1. What are the advantages of using Pandas for data manipulation?
- High-Performance Data Structures: Offers `DataFrame` and `Series` objects that allow vectorized operations, making data manipulation significantly faster than standard Python loops.
- Seamless Integration: Works effortlessly with various file formats (CSV, JSON, Excel, SQL databases) and integrates directly with visualization libraries like Matplotlib and Seaborn.
- Comprehensive Data Cleaning Tools: Provides built-in methods for handling missing values, filtering rows, reshaping tables, and performing complex joins.

2. How do you filter and aggregate data in Pandas?
- Filtering: Executed using boolean indexing or query masks. For example, `df[df['focus_mins'] > 30]` filters rows based on explicit logical conditions.
- Aggregation: Performed using the `.groupby()` method paired with aggregation functions like `.sum()`, `.mean()`, or `.agg()`. Additionally, `.pivot_table()` allows multidimensional cross-tabulation of metrics.

3. What techniques help handle missing or incorrect data?
- Detecting Nulls: Using `.isna()` or `.isnull()` to locate missing values across columns.
- Imputation (`fillna`): Replacing missing entries with meaningful statistical values (such as column mean, median, or zero) to preserve data integrity.
- Removal (`dropna`): Dropping rows or columns with missing data when imputation is inappropriate or data quality is severely compromised.
- Correction (`replace` / `map`): Standardizing inconsistent data values, typos, or incorrect category labels using `.replace()`.

4. How would Pandas be useful for analyzing Focus Bear’s user activity data?
- Cleaning Event Logs: Processing raw user activity CSV/JSON exports by removing corrupted log entries and imputing missing duration values.
- Metric Aggregation: Grouping usage data by operating system (macOS, Windows, iOS, Android) to compare average daily focus durations and habit completion counts.
- Cohort Analysis & Merging: Joining user profile DataFrames with daily log DataFrames (`pd.merge`) to analyze retention rates across different registration cohorts.