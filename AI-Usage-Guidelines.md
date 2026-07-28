# Use of AI tools
## Research and learn
1. AI Tools Typically Used by Data Analysts
  - Coding and Query Assistants: GitHub Copilot, ChatGPT or Claude for writing, debugging and optimizing SQL queries, Python scripts (pandas, numpy), and R code.
  - Automated Data Cleaning and Visualization: Tools embedded in BI platforms to spot outliers or generate instant charts.
  - Documentation and Translation: Large Language Models used to draft clean documentation, explain legacy data pipelines, or translate business requirements into technical specs.
2. Benefits and Risks of AI in Data Analytics
  - Benefits:
    - Massive time savings when writing repetitive boilerplate code or complex regex patterns.
    - Faster debugging: AI can read an error stack trace and instantly suggest solutions.
    - Brainstorming fresh approaches to statistical modeling or data structure strategies.
  - Risks:
    - AI might confidently invent synthetic data functions, Python libraries, or fake SQL syntax that doesn't exist.
    - AI might write code that runs perfectly but uses the wrong business logic, leading to inaccurate reports.
    - Accidentally feeding sensitive business metrics or proprietary data schemas into public models.
3. What Information Should Never Be Entered Into AI Tools
  - Personally Identifiable Information: Customer names, emails, addresses, user IDs, or employee records.
  - Proprietary Business Data: Raw financial metrics, internal strategy decks, or active business datasets.
  - Sensitive Code Infrastructure: Hardcoded API keys, server credentials, production database connection strings, or highly proprietary algorithms.

4. How to Fact-Check and Validate AI-Generated Content
  - Dry-Run Code: Never push AI generated SQL or Python directly to production. Test it locally or in a staging environment using dummy data.
  - Verify Row Counts and Aggregations: When using an AI generated query, manually verify the output using a known benchmark dataset to ensure rows aren't being dropped or duplicated.
  - Cross-Reference Documentation: Check the official documentation of libraries or SQL engines if the AI suggests an unfamiliar function or syntax.

## Reflection
