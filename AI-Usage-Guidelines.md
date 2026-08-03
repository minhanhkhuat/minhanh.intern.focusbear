# Use of AI tools

## Reflection

1. I use AI when I need to figure out syntax roadblocks, structure a long boilerplate SQL script, or look up how to write a difficult RegEx. It saves me tons of time that I would otherwise spend digging through forums. However, I never let AI think through the actual analytics strategy or design the data logic for me. Interpreting what data metrics mean, structuring clean experiments, and ensuring database relationships are structurally sound requires human logic that AI simply can't replicate.
2. To keep my own technical analytical skills sharp, I follow a personal rule: I always try to write code or debug a script manually first. If I get completely stuck or hit a wall, I will consult an AI tool. Once it generates an answer, I don't just copy-paste it blindly, I force myself to study why the code works before typing it into my local workstation. This ensures I'm actually learning the concepts rather than using AI as a mental crutch.
3. Data security is incredibly important to me as an analyst. I never, under any circumstances, upload real data files or copy-paste actual database tables into public models. If I need help fixing a broken SQL script or transforming data with Python, I entirely anonymize the text beforehand. I scrub out any references to Focus Bear, replace actual table structures with generic column placeholders and use mock data to describe the problem safely.

## Tasks

Task Improved: Optimizing an Analytical SQL Query

1. Context: I needed to rewrite a complex SQL query that combined multiple subqueries to extract data trends efficiently. The original query was slowing down performance due to poor formatting.
2. AI Evaluation: I provided the AI with an entirely anonymized skeleton of the query (with mock table and column names). The AI correctly suggested using Common Table Expressions to clean up the query structure and make it highly legible.
3. Critical Review and Edits: The generated script was visually cleaner, but it incorrectly assumed a FULL OUTER JOIN structure that would have resulted in data duplication. I had to manually edit the script to change the joins to LEFT JOIN to preserve correct data matching. This proved why checking the structural logic of the output is vital.
