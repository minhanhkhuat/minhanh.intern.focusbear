
# Understanding Clean Code Principles

## Clean code principles
1. Simplicity 
- Definition: Code should be as straightforward as possible, avoiding unnecessary cleverness, overly complex logic trees, or deeply nested structures when a simpler path exists.
- Impact: Simple code reduces the surface area for bugs and makes the execution logic immediately obvious to anyone reading it.

2. Readability
- Definition: Code should be written for humans to read, not just for machines to execute. This involves using clear, intention-revealing variable names, proper spacing, and logical code flow.
- Impact: Developers spend far more time reading existing code than writing new code. High readability drastically reduces cognitive load during development.

3. Maintainability
- Definition: Designing code in a modular, clean way so that future developers (including your future self) can modify, update, or scale the functionality with minimal risk of breaking existing features.
- Impact: Maintainable code prevents codebases from turning into rigid legacy systems where everyone is terrified to change a single line.

4. Consistency
- Definition: Adhering strictly to established formatting rules, naming conventions, and style guides across the entire project (e.g., casing, indentation, folder structures).
- Impact: Eliminates friction. When a project is consistent, any file you open feels familiar and looks like it was written by a single person.

5. Efficiency
- Definition: Writing performant, resource-optimized code without falling into the trap of premature over-engineering.
- Impact: Code should execute efficiently under realistic load scales, but clarity should not be sacrificed for micro-optimizations that offer no real-world performance benefit.


## Example

1. Below is an example of poorly written SQL code often found in unmaintained codebases:

```sql
SELECT u.id, u.name, o.id as order_id, o.total_amt, o.dt FROM users u LEFT JOIN orders o ON u.id = o.user_id WHERE o.total_amt > 500 AND u.status = 'active' AND o.dt >= '2026-01-01' ORDER BY o.total_amt DESC;

2. Rewrite:
SELECT 
    users.id AS user_id,
    users.name AS user_name,
    orders.id AS order_id,
    orders.total_amount,
    orders.created_at
FROM users
LEFT JOIN orders 
    ON users.id = orders.user_id
WHERE 
    users.status = 'active'
    AND orders.total_amount > 500
    AND orders.created_at >= '2026-01-01'
ORDER BY 
    orders.total_amount DESC;