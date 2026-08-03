# Data Privacy & Confidentiality

## Reflection

1. In my day-to-day work, I need to make sure I treat every piece of data with extreme care. When writing queries or processing application metrics, I will actively ensure I am working with aggregated, anonymized sets rather than raw user tables. I will also make it a rule to close active database connections as soon as my analytical task is completed.
2. I will never store credentials, configuration files, or database keys in plain text files on my local machine. When sharing snippets of code or SQL queries for code review, I will completely scrub them of any internal table schema definitions or mock configuration details. Any temporary CSV outputs or mock datasets used for testing logic will be permanently deleted from my local drive as soon as the pull request is merged.
3. The biggest mistake leading to privacy incidents is accidental leakage via third-party tools or pushing exposed access tokens to public GitHub repositories. These can be avoided by making text sanitization a mandatory step before sharing any snippet outside our secure internal network.

## Tasks

1. I will strictly run all analytical queries on anonymized or mock data models, and I will thoroughly review every code snippet, SQL script, and terminal log to strip out credentials or PII before sharing it across team channels or querying external AI tools.
