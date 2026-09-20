# SQL Interview Notes — Infosys DSE / SP

> A dedicated SQL-only interview reference for Infosys DSE / SP-oriented technical interviews.
>
> DBMS theory, transactions, isolation, normalization, deadlocks, storage engines, and database internals will be kept in a separate DBMS interview file. This file focuses on **writing SQL, choosing the right SQL construct, explaining query intent, reasoning about results, handling edge cases, and discussing SQL performance from a query perspective**.

<a id="table-of-contents"></a>

## Table of Contents

- [How to Use These Notes](#how-to-use-these-notes)
- [SQL Interview Depth Model](#sql-interview-depth-model)
- [SQL Mental Model](#sql-mental-model)
- [Schemas Used in Examples](#schemas-used-in-examples)
- [General Interview Schema Library](#general-interview-schema-library)
- [General Interview Query Bank](#general-interview-query-bank)
- [General Query Variation Drills](#general-query-variation-drills)
- [Query Pattern Matrix](#query-pattern-matrix)
- [SELECT and Projection](#select-and-projection)
- [WHERE and Filtering](#where-and-filtering)
- [ORDER BY LIMIT and DISTINCT](#order-by-limit-and-distinct)
- [NULL and Three-Valued Logic](#null-and-three-valued-logic)
- [CASE and Conditional Logic](#case-and-conditional-logic)
- [Aggregate Functions](#aggregate-functions)
- [GROUP BY](#group-by)
- [HAVING](#having)
- [Conditional Aggregation](#conditional-aggregation)
- [JOINs](#joins)
- [INNER JOIN](#inner-join)
- [LEFT JOIN and Anti-Join](#left-join-and-anti-join)
- [SELF JOIN](#self-join)
- [JOIN Multiplication and Duplicates](#join-multiplication-and-duplicates)
- [Subqueries](#subqueries)
- [Correlated Subqueries](#correlated-subqueries)
- [IN and NOT IN](#in-and-not-in)
- [EXISTS and NOT EXISTS](#exists-and-not-exists)
- [CTEs](#ctes)
- [When to Use JOIN vs Subquery vs CTE](#when-to-use-join-vs-subquery-vs-cte)
- [Window Functions](#window-functions)
- [PARTITION BY](#partition-by)
- [ROW_NUMBER RANK and DENSE_RANK](#row_number-rank-and-dense_rank)
- [LAG and LEAD](#lag-and-lead)
- [Running Totals and Window Aggregates](#running-totals-and-window-aggregates)
- [Window Functions vs GROUP BY](#window-functions-vs-group-by)
- [Top-N and Ranking Problems](#top-n-and-ranking-problems)
- [Nth-Highest Problems](#nth-highest-problems)
- [Latest Row per Group](#latest-row-per-group)
- [Conditional and Analytical Query Patterns](#conditional-and-analytical-query-patterns)
- [Date and Time Query Patterns](#date-and-time-query-patterns)
- [Set Operations](#set-operations)
- [INSERT UPDATE DELETE](#insert-update-delete)
- [Transactions in SQL Usage](#transactions-in-sql-usage)
- [SQL Query Design Thinking](#sql-query-design-thinking)
- [Query Debugging and Common Mistakes](#query-debugging-and-common-mistakes)
- [Indexes from a Query Perspective](#indexes-from-a-query-perspective)
- [Query Performance Reasoning](#query-performance-reasoning)
- [SQL Interview Implementation Drills](#sql-interview-implementation-drills)
- [High-Value Query Problems](#high-value-query-problems)
- [Project-Based SQL — URL Shortener](#project-based-sql--url-shortener)
- [Project-Based SQL — SceneFlow](#project-based-sql--sceneflow)
- [Infosys SP Follow-Up Questions](#infosys-sp-follow-up-questions)
- [Hidden SQL Keywords and Concepts](#hidden-sql-keywords-and-concepts)
- [Common SQL Traps](#common-sql-traps)
- [30-Second Revision Sheet](#30-second-revision-sheet)
- [Final SQL Interview Checklist](#final-sql-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

For every important SQL topic, use:

```text
Understanding
↓
Purpose
↓
Small example
↓
Interview query
↓
Why this construct?
↓
Edge case
↓
Performance discussion
↓
Follow-up
```

For query problems, do not memorize the final SQL.

Train yourself to identify:

```text
What rows do I need?
↓
Which tables contain them?
↓
How are the tables related?
↓
Should I filter before grouping?
↓
Do I need grouping?
↓
Do I need a window function?
↓
Do I need existence/membership logic?
↓
What should happen with duplicates, NULLs, and ties?
```

[Back to Table of Contents](#table-of-contents)

---

<a id="sql-interview-depth-model"></a>

## SQL Interview Depth Model

### Depth 1 — Query writing

Can you produce the SQL?

### Depth 2 — Query explanation

Can you explain every major clause?

### Depth 3 — Query choice

Can you explain why you used:

- a join instead of a subquery,
- a window function instead of GROUP BY,
- EXISTS instead of an unnecessary join,
- a CTE to structure a multi-step query?

### Depth 4 — Performance

Can you discuss:

- possible indexes,
- row counts,
- join cardinality,
- duplicate multiplication,
- filtering early,
- unnecessary sorting,
- large-table behavior?

This is where ordinary SQL preparation becomes SP-oriented SQL preparation.

[Back to Table of Contents](#table-of-contents)

---

<a id="sql-mental-model"></a>

## SQL Mental Model

A useful **logical** query-processing model is:

```text
FROM
↓
JOIN / ON
↓
WHERE
↓
GROUP BY
↓
HAVING
↓
SELECT
↓
DISTINCT
↓
ORDER BY
↓
LIMIT / OFFSET
```

Window functions conceptually operate over the rows produced by the earlier relational operations, before the final result is ordered/limited.

### Why interviewers care

This explains questions like:

- Why does aggregate filtering belong in HAVING?
- Why can a SELECT alias be unavailable in WHERE?
- Why do we often wrap a window-function query in a CTE/derived table before filtering its result?

### Example

Schema: `employees(id, name, department_id, salary, status)`

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
WHERE status = 'ACTIVE'
GROUP BY department_id
HAVING COUNT(*) >= 5
ORDER BY employee_count DESC;
```

The query first identifies active employee rows, groups them, removes groups with fewer than five employees, then returns and orders the result.

[Back to Table of Contents](#table-of-contents)

---

<a id="schemas-used-in-examples"></a>

## Schemas Used in Examples

The examples use compact schemas so the SQL stays readable.

### Common interview schema

```text
employees(id, name, department_id, manager_id, salary, status, hire_date)
departments(id, name)
customers(id, name, created_at)
orders(id, customer_id, order_date, amount, status)
products(id, name, category_id, price)
order_items(order_id, product_id, quantity)
users(id, name, email, created_at)
events(id, user_id, event_type, event_time)
```

### URL Shortener schema

```text
urls(id, short_code, original_url, clicks, created_at, expires_at, is_active)
```

### SceneFlow-style schema

```text
projects(id, user_id, name, created_at)
scripts(id, project_id, title, created_at)
scenes(id, script_id, title, status, created_at)
search_jobs(id, scene_id, status, requested_query, created_at)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="select-and-projection"></a>

## SELECT and Projection

### Understanding

`SELECT` chooses which expressions/columns appear in the result.

The deeper idea is **projection**:

> Start with a row set, then choose the information the caller needs.

### Example

```sql
SELECT id, name, salary
FROM employees;
```

### Why not SELECT *?

For interview reasoning and backend code:

- it returns columns you may not need,
- increases data transfer,
- couples the query to schema changes,
- can make result shape less explicit.

### Useful follow-up

> What does an alias do?

```sql
SELECT salary * 12 AS annual_salary
FROM employees;
```

An alias names an expression in the returned result.

[Back to Table of Contents](#table-of-contents)

---

<a id="where-and-filtering"></a>

## WHERE and Filtering

### Understanding

`WHERE` removes rows before grouping.

### Common operators

```text
=
<>
!=
>
<
>=
<=
AND
OR
NOT
BETWEEN
IN
LIKE
IS NULL
IS NOT NULL
```

### Example

```sql
SELECT id, name
FROM employees
WHERE salary > 70000
  AND status = 'ACTIVE';
```

### Interview point

Filtering as early as the query semantics allow can reduce the number of rows later operations must process, although the optimizer can rewrite execution internally.

### Follow-up

> WHERE vs HAVING?

```text
WHERE
→ filters rows before grouping

HAVING
→ filters groups after aggregation
```

[Back to Table of Contents](#table-of-contents)

---

<a id="order-by-limit-and-distinct"></a>

## ORDER BY, LIMIT and DISTINCT

### ORDER BY

Controls final result ordering.

```sql
SELECT id, name, salary
FROM employees
ORDER BY salary DESC, id ASC;
```

Use a deterministic tie-breaker such as `id` when consistent ordering matters.

### LIMIT

Returns only part of the ordered result.

```sql
SELECT id, name, salary
FROM employees
ORDER BY salary DESC
LIMIT 10;
```

### DISTINCT

Removes duplicate result rows after projection.

```sql
SELECT DISTINCT department_id
FROM employees;
```

### Interview follow-up

> DISTINCT vs GROUP BY?

They can sometimes produce the same result for simple de-duplication, but GROUP BY is primarily for grouping/aggregation.

### Performance point

Large `OFFSET` values can become expensive because the database may still need to locate/skip many earlier rows. For large ordered datasets, know the concept of **keyset/cursor pagination**.

[Back to Table of Contents](#table-of-contents)

---

<a id="null-and-three-valued-logic"></a>

## NULL and Three-Valued Logic

### Understanding

`NULL` means “unknown / missing value”; it is not an ordinary value.

SQL comparisons involving NULL can evaluate to `UNKNOWN`, creating three-valued logic:

```text
TRUE
FALSE
UNKNOWN
```

### Correct

```sql
SELECT *
FROM employees
WHERE manager_id IS NULL;
```

### Incorrect

```sql
WHERE manager_id = NULL
```

### Important aggregate behavior

```text
COUNT(*)       → counts rows
COUNT(column)  → counts non-NULL values
AVG(column)    → normally ignores NULL values
SUM(column)    → normally ignores NULL values
```

### COALESCE

```sql
SELECT name,
       COALESCE(manager_id, 0) AS manager_id
FROM employees;
```

### Interview trap: NOT IN

`NOT IN` can behave unexpectedly when the subquery/set contains NULL.

For existence-style questions, `NOT EXISTS` is often a safer semantic pattern.

[Back to Table of Contents](#table-of-contents)

---

<a id="case-and-conditional-logic"></a>

## CASE and Conditional Logic

### Understanding

`CASE` converts conditions into values.

### Simple form

```sql
SELECT name,
       CASE
           WHEN salary >= 100000 THEN 'HIGH'
           WHEN salary >= 70000 THEN 'MEDIUM'
           ELSE 'LOW'
       END AS salary_band
FROM employees;
```

### Why interviewers care

`CASE` becomes powerful when combined with aggregation.

### Conditional aggregation

```sql
SELECT department_id,
       COUNT(*) AS total_employees,
       SUM(CASE WHEN salary >= 100000 THEN 1 ELSE 0 END) AS high_salary_count
FROM employees
GROUP BY department_id;
```

This answers multiple conditional counts in one grouped query.

### Follow-up

> How would you count active and inactive users in one query?

Use separate conditional expressions inside aggregate functions.

[Back to Table of Contents](#table-of-contents)

---

<a id="aggregate-functions"></a>

## Aggregate Functions

### Core functions

```text
COUNT
SUM
AVG
MIN
MAX
```

### Example

Schema: `employees(id, name, department_id, salary, status)`

```sql
SELECT department_id,
       COUNT(*) AS employee_count,
       AVG(salary) AS average_salary,
       MIN(salary) AS minimum_salary,
       MAX(salary) AS maximum_salary
FROM employees
GROUP BY department_id;
```

### Key distinction

An aggregate reduces multiple input rows into one value per group.

A window function can calculate across related rows **without collapsing them**.

That distinction becomes critical later.

[Back to Table of Contents](#table-of-contents)

---

<a id="group-by"></a>

## GROUP BY

### Understanding

`GROUP BY` forms groups of rows based on one or more expressions.

### Example

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

### Interview follow-up

> Why can’t I select arbitrary non-grouped columns here?

Because one group can contain multiple employees, so a single unaggregated employee name would be ambiguous.

### Multi-column grouping

```sql
SELECT department_id,
       status,
       COUNT(*) AS count
FROM employees
GROUP BY department_id, status;
```

Now the groups are defined by the pair `(department_id, status)`.

[Back to Table of Contents](#table-of-contents)

---

<a id="having"></a>

## HAVING

### Understanding

`HAVING` filters groups produced by aggregation.

### Example

```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 70000;
```

### Mental model

```text
WHERE
→ Which rows participate?

GROUP BY
→ How should rows be grouped?

HAVING
→ Which groups survive?
```

### Follow-up

> Can HAVING exist without GROUP BY?

Yes, depending on the SQL dialect and query form; the entire qualifying result can be treated as one group for aggregate purposes.

[Back to Table of Contents](#table-of-contents)

---

<a id="conditional-aggregation"></a>

## Conditional Aggregation

### Understanding

Conditional aggregation lets one grouped query calculate several conditional metrics.

### Example

Schema: `orders(id, customer_id, order_date, amount, status)`

```sql
SELECT customer_id,
       COUNT(*) AS total_orders,
       SUM(CASE WHEN status = 'PAID' THEN 1 ELSE 0 END) AS paid_orders,
       SUM(CASE WHEN status = 'CANCELLED' THEN 1 ELSE 0 END) AS cancelled_orders
FROM orders
GROUP BY customer_id;
```

### Personal-style example

Think of a student report:

```text
one group = one student
conditional counts = passed subjects / failed subjects
```

### Interview follow-up

> Why not run three separate queries?

One grouped scan can express multiple metrics together, although actual execution should be verified with the database optimizer and workload.

[Back to Table of Contents](#table-of-contents)

---

<a id="joins"></a>

## JOINs

### Understanding

A JOIN combines rows from related tables according to a matching condition.

The key interview question is:

> **What should happen to rows that do not match?**

### Quick mental model

```text
INNER JOIN
→ keep matches

LEFT JOIN
→ keep every left row

RIGHT JOIN
→ keep every right row

FULL OUTER JOIN
→ keep rows from both sides

CROSS JOIN
→ combinations of every left/right row
```

### Technical example

Schema:

```text
employees(id, name, department_id, salary)
departments(id, name)
```

```sql
SELECT e.name,
       d.name AS department
FROM employees e
INNER JOIN departments d
    ON d.id = e.department_id;
```

### What to say

> “I use the JOIN to connect the employee's foreign key to the department's primary key, then project the fields I need.”

[Back to Table of Contents](#table-of-contents)

---

<a id="inner-join"></a>

## INNER JOIN

### Understanding

An INNER JOIN returns rows where the join condition matches.

### Example

Schema:

```text
customers(id, name)
orders(id, customer_id, amount)
```

```sql
SELECT c.id,
       c.name,
       o.amount
FROM customers c
INNER JOIN orders o
    ON o.customer_id = c.id;
```

Customers without orders disappear from the result.

### Interview question

> “I only need customers who have at least one order.”

An INNER JOIN is appropriate when you need matching rows and the relationship itself establishes existence.

[Back to Table of Contents](#table-of-contents)

---

<a id="left-join-and-anti-join"></a>

## LEFT JOIN and Anti-Join

### Understanding

A LEFT JOIN preserves every row from the left table.

### Classic interview query

Schema:

```text
customers(id, name)
orders(id, customer_id, amount)
```

Question:

> Find customers who never placed an order.

Answer:

```sql
SELECT c.id,
       c.name
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.id
WHERE o.id IS NULL;
```

The pattern is often called an **anti-join**: find rows on one side with no matching rows on the other.

### Alternative with NOT EXISTS

```sql
SELECT c.id,
       c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

### Follow-up

> Which one is faster?

Do not memorize “one is always faster.” Explain semantics and say that the optimizer, schema, indexes, and data distribution determine actual performance.

[Back to Table of Contents](#table-of-contents)

---

<a id="self-join"></a>

## SELF JOIN

### Understanding

A table can join to itself when rows in the same table have a relationship.

### Classic interview query

Schema: `employees(id, name, manager_id, salary)`

Question:

> Find employees and their managers.

Answer:

```sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON m.id = e.manager_id;
```

Two aliases represent two logical roles of the same table.

### Technical reason

The same physical table is being viewed from two perspectives:

```text
e = employee role
m = manager role
```

[Back to Table of Contents](#table-of-contents)

---

<a id="join-multiplication-and-duplicates"></a>

## JOIN Multiplication and Duplicates

This is a high-value interview trap.

Suppose:

```text
customers(id)
orders(id, customer_id)
order_items(order_id, product_id)
```

One customer can have many orders, and each order can have many items.

Joining all three can multiply rows.

### Example problem

If one customer has:

```text
2 orders
×
3 items per order
```

the joined result can contain six rows for that customer.

### Interview point

Before using `COUNT`, `SUM`, or `AVG`, ask:

> What is the row grain after the joins?

### Common correction

Sometimes you need:

```sql
COUNT(DISTINCT o.id)
```

instead of:

```sql
COUNT(*)
```

But do not blindly add DISTINCT. First understand why the join multiplied rows.

[Back to Table of Contents](#table-of-contents)

---

<a id="subqueries"></a>

## Subqueries

### Understanding

A subquery is a query nested inside another SQL statement.

It can return:

- one value,
- one row,
- multiple rows,
- or a derived table.

### Scalar example

Question:

> Find employees earning above the company average.

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT id,
       name,
       salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

The inner query returns one value.

### Multi-row example

Question:

> Find employees working in departments located in Hyderabad.

Schema:

```text
employees(id, name, department_id, salary)
departments(id, name, city)
```

```sql
SELECT e.id,
       e.name
FROM employees e
WHERE e.department_id IN (
    SELECT d.id
    FROM departments d
    WHERE d.city = 'Hyderabad'
);
```

### Interview follow-up

> When would you replace this with a JOIN?

When the problem is naturally relational and the JOIN makes the data relationship or filtering clearer.

[Back to Table of Contents](#table-of-contents)

---

<a id="correlated-subqueries"></a>

## Correlated Subqueries

### Understanding

A correlated subquery refers to a value from the current row of the outer query.

### Classic interview query

Question:

> Find employees earning above their own department's average.

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT e.id,
       e.name,
       e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

### What to say

> “The inner query depends on the outer employee row because it uses that employee's department_id.”

### Performance discussion

A correlated query may be evaluated repeatedly in a naive execution strategy. Modern optimizers can transform many queries, so discuss it as a potential shape, then compare with a JOIN/CTE/window alternative.

[Back to Table of Contents](#table-of-contents)

---

<a id="in-and-not-in"></a>

## IN and NOT IN

### Understanding

`IN` tests whether an expression belongs to a set of values.

### Example

```sql
SELECT id,
       name
FROM employees
WHERE department_id IN (1, 3, 5);
```

### With a subquery

```sql
SELECT id,
       name
FROM employees
WHERE department_id IN (
    SELECT id
    FROM departments
    WHERE city = 'Hyderabad'
);
```

### Important NULL trap

`NOT IN` with a set containing NULL can result in UNKNOWN rather than TRUE for rows that you expected to match.

For existence-style exclusion, know `NOT EXISTS` as an alternative.

### Interview question

> IN vs EXISTS?

Answer semantically first:

```text
IN
→ membership in a returned set

EXISTS
→ whether at least one matching row exists
```

Then discuss optimizer/data-shape considerations instead of claiming a universal performance winner.

[Back to Table of Contents](#table-of-contents)

---

<a id="exists-and-not-exists"></a>

## EXISTS and NOT EXISTS

### Understanding

`EXISTS` answers:

> Does at least one matching row exist?

### Example

Question:

> Find customers who have placed at least one order.

Schema:

```text
customers(id, name)
orders(id, customer_id, amount)
```

```sql
SELECT c.id,
       c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

The subquery does not need to return the order columns; existence is the goal.

### NOT EXISTS

```sql
SELECT c.id,
       c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

### Interview follow-up

> Why SELECT 1?

Because the EXISTS operator cares about whether a row exists, not the projected value.

### Important design distinction

```text
Need related data
→ JOIN

Need to test existence
→ EXISTS / NOT EXISTS
```

This is a useful query-design heuristic, not an absolute law.

[Back to Table of Contents](#table-of-contents)

---

<a id="ctes"></a>

## CTEs

### Understanding

A Common Table Expression gives a name to an intermediate query result within one SQL statement.

Syntax:

```sql
WITH department_avg AS (
    SELECT department_id,
           AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT e.id,
       e.name,
       e.salary
FROM employees e
JOIN department_avg d
    ON d.department_id = e.department_id
WHERE e.salary > d.avg_salary;
```

### Why use it?

- Break a complicated query into named steps.
- Improve readability.
- Make multi-stage logic easier to reason about.
- Support recursive queries when needed.

### Interview point

A CTE is primarily a **query-organization construct**. Do not automatically claim that it materializes or improves performance; behavior depends on the DBMS and query plan.

[Back to Table of Contents](#table-of-contents)

---

<a id="when-to-use-join-vs-subquery-vs-cte"></a>

## When to Use JOIN vs Subquery vs CTE

Think by query intent.

### JOIN

Use when you need columns or relational combinations from another table.

```text
“I need data from both tables.”
```

### EXISTS

Use when you only care whether a related row exists.

```text
“I only need to know whether a match exists.”
```

### IN

Use when membership in a set is the direct question.

```text
“Is this value in that set?”
```

### CTE

Use when a multi-step query benefits from named intermediate logic.

```text
“First calculate this result, then use it.”
```

### Subquery

Use when the nested result is naturally part of an expression, filter, or derived table.

### Interview rule

Do not say:

> “CTE is faster.”

or:

> “EXISTS is always faster.”

Explain semantics first, then performance based on the actual workload and plan.

[Back to Table of Contents](#table-of-contents)

---

<a id="window-functions"></a>

## Window Functions

### Understanding

A window function calculates a value across a related set of rows **while keeping each input row visible**.

That is the key difference from GROUP BY.

### General form

```sql
FUNCTION(...) OVER (
    PARTITION BY ...
    ORDER BY ...
)
```

### Major categories

```text
Ranking
→ ROW_NUMBER, RANK, DENSE_RANK

Navigation
→ LAG, LEAD

Window aggregates
→ SUM, AVG, COUNT, MIN, MAX
```

### Why interviewers like them

They solve common problems:

- ranking,
- top-N per group,
- previous/next row,
- running totals,
- comparisons with group averages,
- latest row per group.

[Back to Table of Contents](#table-of-contents)

---

<a id="partition-by"></a>

## PARTITION BY

### Understanding

`PARTITION BY` divides the result into independent groups for the window function.

It does **not** collapse rows like GROUP BY.

### Example

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT id,
       name,
       department_id,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS department_avg
FROM employees;
```

Every employee row remains visible, but each row receives its department's average salary.

### Mental model

```text
GROUP BY
→ make one result row per group

PARTITION BY
→ calculate independently inside each group while retaining rows
```

[Back to Table of Contents](#table-of-contents)

---

<a id="row_number-rank-and-dense_rank"></a>

## ROW_NUMBER, RANK and DENSE_RANK

Suppose salaries are:

```text
100
100
90
80
```

Then:

```text
ROW_NUMBER  → 1, 2, 3, 4
RANK        → 1, 1, 3, 4
DENSE_RANK  → 1, 1, 2, 3
```

### ROW_NUMBER

Gives each row a unique sequence within the window ordering.

### RANK

Equal values share a rank, and gaps appear after ties.

### DENSE_RANK

Equal values share a rank, without gaps.

### Interview rule

Before choosing one, ask:

> How should ties behave?

That is the semantic reason for choosing the ranking function.

[Back to Table of Contents](#table-of-contents)

---

<a id="lag-and-lead"></a>

## LAG and LEAD

### Understanding

`LAG` accesses an earlier row in the window ordering.

`LEAD` accesses a later row.

### Example

Schema: `events(id, user_id, event_type, event_time)`

```sql
SELECT user_id,
       event_time,
       LAG(event_time) OVER (
           PARTITION BY user_id
           ORDER BY event_time
       ) AS previous_event,
       LEAD(event_time) OVER (
           PARTITION BY user_id
           ORDER BY event_time
       ) AS next_event
FROM events;
```

### Typical interview tasks

- Compare current salary to previous salary record.
- Find time since previous event.
- Compare today's metric with yesterday's.
- Find the next event for each user.

[Back to Table of Contents](#table-of-contents)

---

<a id="running-totals-and-window-aggregates"></a>

## Running Totals and Window Aggregates

### Running total

Schema: `orders(id, customer_id, order_date, amount)`

```sql
SELECT order_date,
       amount,
       SUM(amount) OVER (
           ORDER BY order_date, id
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS running_total
FROM orders;
```

### Per-customer running total

```sql
SELECT customer_id,
       order_date,
       amount,
       SUM(amount) OVER (
           PARTITION BY customer_id
           ORDER BY order_date, id
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS customer_running_total
FROM orders;
```

### Interview point

The explicit tie-breaker `id` makes the ordering deterministic when two rows share the same date.

[Back to Table of Contents](#table-of-contents)

---

<a id="window-functions-vs-group-by"></a>

## Window Functions vs GROUP BY

This is a frequent conceptual question.

### GROUP BY

```text
Input rows
↓
collapse into groups
↓
one result row per group
```

### Window function

```text
Input rows
↓
keep rows
↓
calculate across related rows
↓
return value on each row
```

### Example question

> “Show every employee together with the average salary of their department.”

Window function:

```sql
SELECT id,
       name,
       department_id,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS department_avg
FROM employees;
```

A GROUP BY query alone would collapse employee rows and would not directly retain every employee row.

[Back to Table of Contents](#table-of-contents)

---

<a id="top-n-and-ranking-problems"></a>

## Top-N and Ranking Problems

### Top 3 salaries per department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT id,
           name,
           department_id,
           salary,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
)
SELECT id,
       name,
       department_id,
       salary
FROM ranked
WHERE rnk <= 3;
```

### What this demonstrates

```text
PARTITION BY
+
DENSE_RANK
+
CTE
+
outer filter
```

### Follow-up

> What if I need exactly three employees rather than three distinct salary levels?

Use `ROW_NUMBER()` with a deterministic tie-breaker.

[Back to Table of Contents](#table-of-contents)

---

<a id="nth-highest-problems"></a>

## Nth-Highest Problems

### Second-highest distinct salary

Schema: `employees(id, name, salary)`

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### Second-highest using DENSE_RANK

```sql
WITH ranked AS (
    SELECT salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
)
SELECT MAX(salary) AS second_highest_salary
FROM ranked
WHERE rnk = 2;
```

### Interview discussion

The key question is whether duplicates count as separate positions.

```text
Distinct salary level
→ DENSE_RANK

Physical row number
→ ROW_NUMBER
```

[Back to Table of Contents](#table-of-contents)

---

<a id="latest-row-per-group"></a>

## Latest Row per Group

Question:

> Find the latest order for every customer.

Schema: `orders(id, customer_id, order_date, amount)`

```sql
WITH ranked AS (
    SELECT id,
           customer_id,
           order_date,
           amount,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date DESC, id DESC
           ) AS rn
    FROM orders
)
SELECT id,
       customer_id,
       order_date,
       amount
FROM ranked
WHERE rn = 1;
```

### Why ROW_NUMBER?

We need one physical row per customer.

### Follow-up

> What if multiple latest orders should all be returned?

Use a tie-preserving strategy such as `RANK()` or `DENSE_RANK()`, depending on the precise semantics.

[Back to Table of Contents](#table-of-contents)

---

<a id="conditional-and-analytical-query-patterns"></a>

## Conditional and Analytical Query Patterns

### Percentage of department payroll

```sql
SELECT id,
       department_id,
       salary,
       salary * 100.0 /
       SUM(salary) OVER (PARTITION BY department_id) AS pct_of_department_payroll
FROM employees;
```

### Compare employee salary with department average

```sql
SELECT id,
       name,
       salary,
       AVG(salary) OVER (
           PARTITION BY department_id
       ) AS department_avg
FROM employees;
```

### Detect salary increases

Suppose:

```text
salary_history(employee_id, effective_date, salary)
```

```sql
WITH x AS (
    SELECT employee_id,
           effective_date,
           salary,
           LAG(salary) OVER (
               PARTITION BY employee_id
               ORDER BY effective_date
           ) AS previous_salary
    FROM salary_history
)
SELECT employee_id,
       effective_date,
       salary,
       previous_salary
FROM x
WHERE salary > previous_salary;
```

These are useful because they turn “advanced SQL” into reusable patterns.

[Back to Table of Contents](#table-of-contents)

---

<a id="date-and-time-query-patterns"></a>

## Date and Time Query Patterns

Date syntax varies by SQL dialect, so learn the reasoning first.

### Common interview tasks

- records in a date range,
- users created in a month,
- daily counts,
- latest event,
- rolling windows,
- month-over-month changes,
- time between current and previous event.

### Example concept

Schema: `events(id, user_id, event_type, event_time)`

Daily event counts can be expressed with the appropriate date-truncation/extraction function for the target SQL dialect.

### Interview point

Always clarify or recognize the SQL dialect when date syntax materially changes.

[Back to Table of Contents](#table-of-contents)

---

<a id="set-operations"></a>

## Set Operations

### UNION

Combines compatible result sets and removes duplicates.

### UNION ALL

Combines result sets and preserves duplicates.

### INTERSECT

Returns rows appearing in both result sets.

### EXCEPT

Returns rows from the first result that are absent from the second.

### Interview point

The queries being combined must have compatible column counts and compatible data types.

### Follow-up

> UNION vs UNION ALL?

Use `UNION ALL` when duplicate elimination is not required; avoiding the de-duplication work can be cheaper.

[Back to Table of Contents](#table-of-contents)

---

<a id="insert-update-delete"></a>

## INSERT, UPDATE, DELETE

Although most interview drills focus on SELECT, know the basic mutation operations.

### INSERT

```sql
INSERT INTO employees (name, department_id, salary, status)
VALUES ('Sai', 1, 80000, 'ACTIVE');
```

### UPDATE

```sql
UPDATE employees
SET salary = salary * 1.10
WHERE department_id = 1;
```

### DELETE

```sql
DELETE FROM employees
WHERE status = 'INACTIVE';
```

### Interview safety

Never discuss an UPDATE or DELETE without considering its filter and transaction context.

A forgotten WHERE clause can change every row.

[Back to Table of Contents](#table-of-contents)

---

<a id="transactions-in-sql-usage"></a>

## Transactions in SQL Usage

DBMS will cover transactions in depth. Here the SQL-only focus is practical usage.

### Example

Imagine creating an order and its items:

```sql
BEGIN;

INSERT INTO orders (...);
INSERT INTO order_items (...);

COMMIT;
```

If the second operation fails, the application may need:

```text
ROLLBACK
```

### Interview perspective

Know why multiple related mutations may need to succeed or fail together.

Do not turn this section into a full ACID/isolation lecture; keep those details in the DBMS notes.

[Back to Table of Contents](#table-of-contents)

---

<a id="sql-query-design-thinking"></a>

## SQL Query Design Thinking

Before writing SQL, say this mentally:

### Step 1 — Define the answer

> What exactly should one output row represent?

This is the **row grain**.

Examples:

```text
one row per employee
one row per department
one row per customer
one row per customer per month
one row per user containing their latest event
```

### Step 2 — Identify the tables

Which table owns the required information?

### Step 3 — Identify relationships

Which key connects the tables?

### Step 4 — Filter

Which rows should participate?

### Step 5 — Choose the operation

```text
Need one result per group
→ GROUP BY

Need every row + group statistic
→ window function

Need to test related-row existence
→ EXISTS

Need values from another table
→ JOIN

Need a staged intermediate result
→ CTE / derived table
```

### Step 6 — Check duplicates

Ask:

> Did my JOIN change the row grain?

### Step 7 — Check ties

Especially for ranking and latest-row queries.

### Step 8 — Check NULLs

Especially with `NOT IN`, aggregates, and outer joins.

### Step 9 — Check performance

Think about:

- indexes,
- large scans,
- joins,
- sorting,
- repeated computation.

[Back to Table of Contents](#table-of-contents)

---

<a id="query-debugging-and-common-mistakes"></a>

## Query Debugging and Common Mistakes

### Mistake: aggregate in WHERE

Wrong shape:

```sql
WHERE AVG(salary) > 70000
```

Use `HAVING` after grouping.

### Mistake: NULL comparison

Wrong:

```sql
WHERE manager_id = NULL
```

Correct:

```sql
WHERE manager_id IS NULL
```

### Mistake: accidental INNER JOIN behavior

Putting a right-table filter in WHERE can turn a LEFT JOIN into effective inner-join behavior.

Example:

```sql
SELECT c.id, o.amount
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.id
WHERE o.status = 'PAID';
```

Customers without a paid order disappear.

If the requirement is to preserve every customer and only match paid orders, move the condition into ON:

```sql
SELECT c.id, o.amount
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.id
   AND o.status = 'PAID';
```

### Mistake: duplicate multiplication

Always inspect the join cardinality before using aggregates.

### Mistake: ranking ties incorrectly

Choose:

```text
ROW_NUMBER
RANK
DENSE_RANK
```

based on the requirement.

### Mistake: assuming CTE always improves performance

CTE improves query organization; performance depends on the database and plan.

### Mistake: assuming an index automatically makes a query fast

An index is useful only when it matches the workload and the optimizer can use it effectively.

[Back to Table of Contents](#table-of-contents)

---

<a id="indexes-from-a-query-perspective"></a>

## Indexes from a Query Perspective

Indexes will also have a dedicated DBMS treatment later. Here the goal is:

> **Can you look at a query and reason about what access path might help?**

### Suppose

Schema: `urls(id, short_code, original_url, clicks, created_at, expires_at, is_active)`

Query:

```sql
SELECT original_url
FROM urls
WHERE short_code = 'abc123'
  AND is_active = TRUE;
```

A useful index discussion might be:

```text
short_code is highly selective and used for lookup
+
is_active is part of the filter
→ consider the workload and index design
```

Do not say “index every WHERE column.”

### Composite index mental model

For an index such as:

```text
(customer_id, order_date)
```

the column order matters.

Think:

```text
Which predicates are common?
Which column provides useful narrowing?
Do we also sort/range on the second column?
```

### Index interview questions

- Which index would you create for this query?
- Why this column first?
- What happens if the leading column is not filtered?
- Why can too many indexes hurt writes?
- What would you inspect before adding an index?
- Why should you verify with the query plan?

[Back to Table of Contents](#table-of-contents)

---

<a id="query-performance-reasoning"></a>

## Query Performance Reasoning

When asked:

> “This SQL query is slow. What will you do?”

Do not jump immediately to “add an index.”

Use:

```text
1. Understand the workload
↓
2. Identify the slow query
↓
3. Check row counts / selectivity
↓
4. Inspect joins and predicates
↓
5. Look for unnecessary columns
↓
6. Check sorting / grouping cost
↓
7. Check useful indexes
↓
8. Inspect the execution plan
↓
9. Change one thing
↓
10. Measure again
```

### High-value causes

- full/large table scans,
- poor join access,
- missing or unsuitable indexes,
- functions applied to indexed columns in ways that prevent useful access,
- unnecessary DISTINCT,
- sorting large datasets,
- row multiplication,
- repeated correlated work,
- fetching more data than needed.

### Interview phrase

> “I would measure first and use the execution plan to identify the actual bottleneck instead of assuming the query is slow because of one missing index.”

### Explain vs execution

SQL is declarative.

You describe the desired result; the DBMS optimizer decides an execution strategy.

That distinction matters in SP-level discussions.

[Back to Table of Contents](#table-of-contents)

---

<a id="sql-interview-implementation-drills"></a>

## SQL Interview Implementation Drills

Use a progressive coding style.

### Drill 1 — Basic filter

Question:

> Return active employees earning above 70,000.

```sql
SELECT id, name, salary
FROM employees
WHERE status = 'ACTIVE'
  AND salary > 70000;
```

### Drill 2 — Add grouping

Question:

> Return departments with at least five active employees.

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
WHERE status = 'ACTIVE'
GROUP BY department_id
HAVING COUNT(*) >= 5;
```

### Drill 3 — Add relational data

Question:

> Return department names with at least five active employees.

```sql
SELECT d.name,
       COUNT(*) AS employee_count
FROM departments d
JOIN employees e
    ON e.department_id = d.id
WHERE e.status = 'ACTIVE'
GROUP BY d.id, d.name
HAVING COUNT(*) >= 5;
```

### Drill 4 — Add ranking

Question:

> Return the top three distinct salaries in each department.

```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT id, name, department_id, salary
FROM ranked
WHERE rnk <= 3;
```

### What to say while coding

```text
First I identify the required row grain.
Then I choose the tables and relationship.
Then I filter.
Then I group or rank depending on whether I need one row per group or every row with group context.
Finally I check ties and duplicates.
```

[Back to Table of Contents](#table-of-contents)

---

<a id="high-value-query-problems"></a>

## High-Value Query Problems

These are the problems you should be able to write **without notes**.

### Core

#### Find employees above salary threshold

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT id, name, salary
FROM employees
WHERE salary > 70000;
```

### GROUP BY

#### Count employees per department

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

### HAVING

#### Departments with more than 10 employees

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 10;
```

### JOIN

#### Employee with department name

Schema: `employees(id, name, department_id, salary)`
Schema: `departments(id, name)`

```sql
SELECT e.name,
       d.name AS department
FROM employees e
JOIN departments d
    ON d.id = e.department_id;
```

### LEFT JOIN

#### Customers without orders

Schema: `customers(id, name)`
Schema: `orders(id, customer_id, amount)`

```sql
SELECT c.id, c.name
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.id
WHERE o.id IS NULL;
```

### EXISTS

#### Customers with at least one order

Schema: `customers(id, name)`
Schema: `orders(id, customer_id, amount)`

```sql
SELECT c.id, c.name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

### Correlated subquery

#### Employees above department average

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT e.id, e.name, e.salary
FROM employees e
WHERE e.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.department_id = e.department_id
);
```

### Window function

#### Top 3 salaries per department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT id, name, department_id, salary
FROM ranked
WHERE rnk <= 3;
```

### Latest row per customer

Schema: `orders(id, customer_id, order_date, amount)`

```sql
WITH ranked AS (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date DESC, id DESC
           ) AS rn
    FROM orders o
)
SELECT id, customer_id, order_date, amount
FROM ranked
WHERE rn = 1;
```

### Second-highest distinct salary

Schema: `employees(id, name, salary)`

```sql
SELECT MAX(salary) AS second_highest
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

### Second-highest per department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT department_id,
           salary,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
)
SELECT department_id,
       MAX(salary) AS second_highest_salary
FROM ranked
WHERE rnk = 2
GROUP BY department_id;
```

### Running total

Schema: `orders(id, customer_id, order_date, amount)`

```sql
SELECT order_date,
       amount,
       SUM(amount) OVER (
           ORDER BY order_date, id
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS running_total
FROM orders;
```

### Previous event

Schema: `events(id, user_id, event_type, event_time)`

```sql
SELECT user_id,
       event_time,
       LAG(event_time) OVER (
           PARTITION BY user_id
           ORDER BY event_time
       ) AS previous_event
FROM events;
```

### Employees earning more than managers

Schema: `employees(id, name, manager_id, salary)`

```sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
JOIN employees m
    ON m.id = e.manager_id
WHERE e.salary > m.salary;
```

### Duplicate emails

Schema: `users(id, email)`

```sql
SELECT email,
       COUNT(*) AS duplicate_count
FROM users
GROUP BY email
HAVING COUNT(*) > 1;
```

### Customers with at least three orders

Schema: `orders(id, customer_id, order_date, amount)`

```sql
SELECT customer_id,
       COUNT(*) AS order_count
FROM orders
GROUP BY customer_id
HAVING COUNT(*) >= 3;
```

### Highest-paid employee in every department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT id, name, department_id, salary
FROM ranked
WHERE rnk = 1;
```

### Interview follow-up to every query

After producing the query, be ready for:

```text
Why this approach?
What if there are ties?
What if values are NULL?
Can you write it another way?
What happens with duplicate rows?
What index would help?
How would this behave on a very large table?
```

[Back to Table of Contents](#table-of-contents)

---

<a id="project-based-sql--url-shortener"></a>

## Project-Based SQL — URL Shortener

Schema:

```text
urls(id, short_code, original_url, clicks, created_at, expires_at, is_active)
```

### Question: Top 10 most-clicked URLs

```sql
SELECT id,
       short_code,
       original_url,
       clicks
FROM urls
ORDER BY clicks DESC, id ASC
LIMIT 10;
```

Use an explicit tie-breaker for deterministic ordering.

### Question: Active non-expired URLs

```sql
SELECT id,
       short_code,
       original_url
FROM urls
WHERE is_active = TRUE
  AND (expires_at IS NULL OR expires_at > CURRENT_TIMESTAMP);
```

### Question: Count URLs created per day

Date functions vary by dialect; the core pattern is:

```text
group by the calendar date extracted/truncated from created_at
```

### Question: Find duplicate original URLs

```sql
SELECT original_url,
       COUNT(*) AS occurrences
FROM urls
GROUP BY original_url
HAVING COUNT(*) > 1;
```

### Question: Latest URL created for each original URL

```sql
WITH ranked AS (
    SELECT u.*,
           ROW_NUMBER() OVER (
               PARTITION BY original_url
               ORDER BY created_at DESC, id DESC
           ) AS rn
    FROM urls u
)
SELECT id,
       short_code,
       original_url,
       created_at
FROM ranked
WHERE rn = 1;
```

### Query-design follow-ups

- Why is `short_code` lookup different from analytics queries?
- What index supports redirect lookup?
- What happens if a user has millions of URLs?
- Should click counts be updated synchronously forever?
- Which reads are cacheable?
- What query pattern becomes the bottleneck first?

These connect SQL to system design without moving DBMS theory into this file.

[Back to Table of Contents](#table-of-contents)

---

<a id="project-based-sql--sceneflow"></a>

## Project-Based SQL — SceneFlow

Schemas:

```text
projects(id, user_id, name, created_at)
scripts(id, project_id, title, created_at)
scenes(id, script_id, title, status, created_at)
search_jobs(id, scene_id, status, requested_query, created_at)
```

### Question: Scene count per project

```sql
SELECT p.id,
       p.name,
       COUNT(scenes.id) AS scene_count
FROM projects p
JOIN scripts s
    ON s.project_id = p.id
JOIN scenes
    ON scenes.script_id = s.id
GROUP BY p.id, p.name;
```

### Question: Projects with more than 10 scenes

```sql
SELECT p.id,
       p.name,
       COUNT(scenes.id) AS scene_count
FROM projects p
JOIN scripts s
    ON s.project_id = p.id
JOIN scenes
    ON scenes.script_id = s.id
GROUP BY p.id, p.name
HAVING COUNT(scenes.id) > 10;
```

### Question: Latest script for each project

```sql
WITH ranked AS (
    SELECT s.*,
           ROW_NUMBER() OVER (
               PARTITION BY project_id
               ORDER BY created_at DESC, id DESC
           ) AS rn
    FROM scripts s
)
SELECT id,
       project_id,
       title,
       created_at
FROM ranked
WHERE rn = 1;
```

### Question: Count search jobs by status

```sql
SELECT status,
       COUNT(*) AS job_count
FROM search_jobs
GROUP BY status;
```

### Question: Latest search job per scene

```sql
WITH ranked AS (
    SELECT sj.*,
           ROW_NUMBER() OVER (
               PARTITION BY scene_id
               ORDER BY created_at DESC, id DESC
           ) AS rn
    FROM search_jobs sj
)
SELECT id,
       scene_id,
       status,
       requested_query,
       created_at
FROM ranked
WHERE rn = 1;
```

### Question: User → project → script → scene report

```sql
SELECT p.user_id,
       p.name AS project_name,
       s.title AS script_title,
       sc.title AS scene_title,
       sc.status
FROM projects p
JOIN scripts s
    ON s.project_id = p.id
JOIN scenes sc
    ON sc.script_id = s.id;
```

### Interview follow-ups

- Which foreign keys matter for joins?
- What query would become slow with millions of scenes?
- How would pagination work?
- Which indexes would you consider?
- How would you avoid duplicate scene results after additional joins?
- How would you count only completed search jobs?
- How would you find a scene whose latest job failed?

[Back to Table of Contents](#table-of-contents)


---

<a id="general-interview-schema-library"></a>

## General Interview Schema Library

Project schemas are useful for project defense, but interviewers can ask SQL using completely generic schemas. These are the schemas to become comfortable with first.

### Employee and Department

```text
employees(id, name, department_id, manager_id, salary, job_title, hire_date, status)
departments(id, name, location)
```

Common question families:

```text
salary ranking
department counts
department averages
employees above department average
manager relationships
highest / second-highest / nth-highest salary
recent hires
employees without departments
departments without employees
```

### Student, Course and Enrollment

```text
students(id, name, department_id, age, admission_year)
courses(id, name, department_id, credits)
enrollments(student_id, course_id, semester, grade)
```

Common question families:

```text
students enrolled in courses
students with no enrollment
course enrollment counts
top students by average grade
students taking multiple courses
courses with no students
department-wise student counts
semester-wise results
```

### Teacher and Class

```text
teachers(id, name, department_id, salary)
classes(id, name, teacher_id, room, schedule)
students(id, name, department_id)
class_enrollments(student_id, class_id)
```

Common question families:

```text
teacher workload
students per class
teachers with no classes
classes with no students
department-wise teaching load
```

### Customer and Order

```text
customers(id, name, city, created_at)
orders(id, customer_id, order_date, amount, status)
order_items(order_id, product_id, quantity, unit_price)
products(id, name, category_id, price)
```

Common question families:

```text
top customers
customers without orders
monthly revenue
repeat customers
highest-value order
latest order per customer
products never ordered
category revenue
```

### Project and Employee Assignment

```text
projects(id, name, department_id, budget, start_date)
employees(id, name, department_id, salary)
project_assignments(employee_id, project_id, assigned_at, hours)
```

Common question families:

```text
employees per project
projects with no employees
employees on multiple projects
project cost
highest-hours employee per project
department project counts
```

### User and Event / Activity

```text
users(id, name, created_at)
events(id, user_id, event_type, event_time)
```

Common question families:

```text
daily active users
first event per user
latest event per user
previous event
users with no events
repeated events
activity by day
retention-style queries
```

[Back to Table of Contents](#table-of-contents)

---

<a id="general-interview-query-bank"></a>

## General Interview Query Bank

This is the **primary practice bank**. The goal is to become comfortable with generic schemas that an interviewer can introduce without relying on your project context.

### Employees and Departments

#### Find employees earning more than 70,000

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT id, name, salary
FROM employees
WHERE salary > 70000;
```

Uses a simple row filter with `WHERE`.

#### Count employees in each department

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id;
```

Uses grouping because the required answer is one row per department.

#### Find departments with more than 5 employees

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id
HAVING COUNT(*) > 5;
```

`WHERE` filters employees; `HAVING` filters the department groups.

#### Find the highest salary

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT MAX(salary) AS highest_salary
FROM employees;
```

#### Find the second-highest distinct salary

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

The subquery finds the maximum; the outer query finds the maximum below it.

#### Find employees who earn more than the company average

Schema: `employees(id, name, department_id, salary)`

```sql
SELECT id, name, salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

Uses a scalar subquery returning one value.

#### Find employees who earn more than their department average

Schema: `employees(id, name, department_id, salary)`

```sql
WITH department_avg AS (
    SELECT department_id,
           AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT e.id,
       e.name,
       e.department_id,
       e.salary
FROM employees e
JOIN department_avg d
    ON d.department_id = e.department_id
WHERE e.salary > d.avg_salary;
```

The CTE calculates one average per department, then the main query compares each employee against that value.

#### Find the highest-paid employee in each department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT id, name, department_id, salary
FROM ranked
WHERE rnk = 1;
```

`DENSE_RANK` preserves ties, so multiple employees can be returned.

#### Find the second-highest salary in each department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT id, name, department_id, salary
FROM ranked
WHERE rnk = 2;
```

The partition resets ranking for every department.

#### Find employees and their managers

Schema: `employees(id, name, department_id, manager_id, salary)`

```sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
LEFT JOIN employees m
    ON m.id = e.manager_id;
```

This is a self join because employees and managers are rows in the same table.

#### Find employees earning more than their managers

Schema: `employees(id, name, manager_id, salary)`

```sql
SELECT e.name AS employee,
       m.name AS manager
FROM employees e
JOIN employees m
    ON m.id = e.manager_id
WHERE e.salary > m.salary;
```

The comparison happens after the employee-manager relationship is formed.

#### Find departments with no employees

Schema: `departments(id, name)`
Schema: `employees(id, name, department_id)`

```sql
SELECT d.id,
       d.name
FROM departments d
LEFT JOIN employees e
    ON e.department_id = d.id
WHERE e.id IS NULL;
```

This is the standard anti-join pattern.

#### Count employees by department and status

Schema: `employees(id, name, department_id, status)`

```sql
SELECT department_id,
       status,
       COUNT(*) AS employee_count
FROM employees
GROUP BY department_id, status;
```

The grouping key is the pair `(department_id, status)`.

#### Find the top 3 salaries in each department

Schema: `employees(id, name, department_id, salary)`

```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT id, name, department_id, salary
FROM ranked
WHERE rnk <= 3;
```

Use `ROW_NUMBER` instead when the requirement is exactly three employee rows and ties must not expand the result.

### Students, Courses and Enrollment

#### Find students enrolled in at least one course

Schema: `students(id, name)`
Schema: `enrollments(student_id, course_id, semester, grade)`

```sql
SELECT s.id,
       s.name
FROM students s
WHERE EXISTS (
    SELECT 1
    FROM enrollments e
    WHERE e.student_id = s.id
);
```

The question is existence-oriented, so `EXISTS` expresses the intent directly.

#### Find students not enrolled in any course

Schema: `students(id, name)`
Schema: `enrollments(student_id, course_id, semester, grade)`

```sql
SELECT s.id,
       s.name
FROM students s
WHERE NOT EXISTS (
    SELECT 1
    FROM enrollments e
    WHERE e.student_id = s.id
);
```

`NOT EXISTS` safely expresses the absence of a related row.

#### Count students in each course

Schema: `courses(id, name)`
Schema: `enrollments(student_id, course_id, semester, grade)`

```sql
SELECT c.id,
       c.name,
       COUNT(e.student_id) AS student_count
FROM courses c
LEFT JOIN enrollments e
    ON e.course_id = c.id
GROUP BY c.id, c.name;
```

The LEFT JOIN keeps courses with zero students.

#### Find courses with no students

Schema: `courses(id, name)`
Schema: `enrollments(student_id, course_id)`

```sql
SELECT c.id,
       c.name
FROM courses c
LEFT JOIN enrollments e
    ON e.course_id = c.id
WHERE e.course_id IS NULL;
```

#### Find students taking more than 3 courses

Schema: `enrollments(student_id, course_id)`

```sql
SELECT student_id,
       COUNT(DISTINCT course_id) AS course_count
FROM enrollments
GROUP BY student_id
HAVING COUNT(DISTINCT course_id) > 3;
```

Use DISTINCT when the schema or business rule allows duplicate enrollment records.

#### Find the student with the highest average grade

Schema: `enrollments(student_id, course_id, grade)`

```sql
SELECT student_id,
       AVG(grade) AS avg_grade
FROM enrollments
GROUP BY student_id
ORDER BY avg_grade DESC
LIMIT 1;
```

For ties or multiple top students, use a ranking query rather than `LIMIT 1`.

### Customer and Order

#### Find customers who never placed an order

Schema: `customers(id, name)`
Schema: `orders(id, customer_id, amount)`

```sql
SELECT c.id,
       c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.id
);
```

#### Find each customer's total spending

Schema: `customers(id, name)`
Schema: `orders(id, customer_id, amount)`

```sql
SELECT c.id,
       c.name,
       COALESCE(SUM(o.amount), 0) AS total_spending
FROM customers c
LEFT JOIN orders o
    ON o.customer_id = c.id
GROUP BY c.id, c.name;
```

The LEFT JOIN keeps customers who have never ordered.

#### Find customers whose total spending exceeds 100,000

Schema: `orders(id, customer_id, amount)`

```sql
SELECT customer_id,
       SUM(amount) AS total_spending
FROM orders
GROUP BY customer_id
HAVING SUM(amount) > 100000;
```

#### Find the latest order for each customer

Schema: `orders(id, customer_id, order_date, amount)`

```sql
WITH ranked AS (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date DESC, id DESC
           ) AS rn
    FROM orders o
)
SELECT id, customer_id, order_date, amount
FROM ranked
WHERE rn = 1;
```

#### Find customers who placed orders in both January and February

Schema: `orders(id, customer_id, order_date)`

```sql
SELECT customer_id
FROM orders
WHERE order_date >= DATE '2026-01-01'
  AND order_date < DATE '2026-03-01'
GROUP BY customer_id
HAVING COUNT(DISTINCT CASE
           WHEN order_date < DATE '2026-02-01' THEN 'JAN'
           ELSE 'FEB'
       END) = 2;
```

This demonstrates conditional aggregation over a customer group. Exact date literals can vary by SQL dialect.

### Products and Orders

#### Find products that were never ordered

Schema: `products(id, name)`
Schema: `order_items(order_id, product_id)`

```sql
SELECT p.id,
       p.name
FROM products p
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items oi
    WHERE oi.product_id = p.id
);
```

#### Find the top 3 products by quantity sold

Schema: `products(id, name)`
Schema: `order_items(order_id, product_id, quantity)`

```sql
SELECT p.id,
       p.name,
       SUM(oi.quantity) AS total_quantity
FROM products p
JOIN order_items oi
    ON oi.product_id = p.id
GROUP BY p.id, p.name
ORDER BY total_quantity DESC, p.id ASC
LIMIT 3;
```

#### Find the highest-revenue category

Schema: `products(id, category_id, price)`
Schema: `order_items(order_id, product_id, quantity)`

```sql
SELECT p.category_id,
       SUM(p.price * oi.quantity) AS revenue
FROM products p
JOIN order_items oi
    ON oi.product_id = p.id
GROUP BY p.category_id
ORDER BY revenue DESC
LIMIT 1;
```

The important interview point is understanding revenue grain: one order item contributes `price × quantity`.

### Projects and Employee Assignment

#### Find employees assigned to more than one project

Schema: `project_assignments(employee_id, project_id)`

```sql
SELECT employee_id,
       COUNT(DISTINCT project_id) AS project_count
FROM project_assignments
GROUP BY employee_id
HAVING COUNT(DISTINCT project_id) > 1;
```

#### Find projects with no assigned employees

Schema: `projects(id, name)`
Schema: `project_assignments(employee_id, project_id)`

```sql
SELECT p.id,
       p.name
FROM projects p
LEFT JOIN project_assignments pa
    ON pa.project_id = p.id
WHERE pa.project_id IS NULL;
```

#### Find the employee with the highest hours on each project

Schema: `project_assignments(employee_id, project_id, hours)`

```sql
WITH ranked AS (
    SELECT pa.*,
           ROW_NUMBER() OVER (
               PARTITION BY project_id
               ORDER BY hours DESC, employee_id ASC
           ) AS rn
    FROM project_assignments pa
)
SELECT employee_id,
       project_id,
       hours
FROM ranked
WHERE rn = 1;
```

This is a classic top-1-per-group problem.

### User and Events

#### Find the first event for each user

Schema: `events(id, user_id, event_type, event_time)`

```sql
WITH ranked AS (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY user_id
               ORDER BY event_time ASC, id ASC
           ) AS rn
    FROM events e
)
SELECT id, user_id, event_type, event_time
FROM ranked
WHERE rn = 1;
```

#### Find users whose latest event is LOGIN

Schema: `users(id, name)`
Schema: `events(id, user_id, event_type, event_time)`

```sql
WITH ranked AS (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY user_id
               ORDER BY event_time DESC, id DESC
           ) AS rn
    FROM events e
)
SELECT u.id,
       u.name
FROM users u
JOIN ranked e
    ON e.user_id = u.id
   AND e.rn = 1
WHERE e.event_type = 'LOGIN';
```

#### Find the time between consecutive events

Schema: `events(id, user_id, event_type, event_time)`

```sql
SELECT user_id,
       event_time,
       LAG(event_time) OVER (
           PARTITION BY user_id
           ORDER BY event_time, id
       ) AS previous_event_time
FROM events;
```

The interviewer may then ask you to calculate the actual duration using the date/time arithmetic supported by the chosen SQL dialect.

#### Count daily active users

Schema: `events(id, user_id, event_time)`

```sql
SELECT CAST(event_time AS DATE) AS event_date,
       COUNT(DISTINCT user_id) AS active_users
FROM events
GROUP BY CAST(event_time AS DATE)
ORDER BY event_date;
```

The exact date-casting syntax can vary by SQL dialect.

[Back to Table of Contents](#table-of-contents)

---

<a id="general-query-variation-drills"></a>

## General Query Variation Drills

After solving a query, expect the interviewer to modify one requirement.

### Example: Top 3 salaries

Start:

```text
top 3 employees overall
```

Variation 1:

```text
top 3 distinct salary values overall
```

Variation 2:

```text
top 3 employees in every department
```

Variation 3:

```text
top 3 distinct salaries in every department
```

Variation 4:

```text
return all employees tied at third place
```

Variation 5:

```text
exclude inactive employees
```

Variation 6:

```text
return the result for one department only
```

This is why the real skill is recognizing the pattern rather than memorizing one query.

### Other high-value variations

Be ready to modify a basic query into:

```text
WHERE
→ GROUP BY
→ HAVING
→ JOIN
→ LEFT JOIN
→ EXISTS
→ window function
→ CTE
→ tie-aware ranking
→ NULL-safe logic
```

[Back to Table of Contents](#table-of-contents)

---

<a id="query-pattern-matrix"></a>

## Query Pattern Matrix

Use this as a pattern-recognition table during revision.

| Requirement | Natural SQL pattern |
|---|---|
| Filter individual rows | WHERE |
| Return unique values | DISTINCT |
| One result per group | GROUP BY |
| Filter groups | HAVING |
| Need columns from another table | JOIN |
| Preserve unmatched left rows | LEFT JOIN |
| Find rows with no match | LEFT JOIN + IS NULL / NOT EXISTS |
| Test whether related rows exist | EXISTS |
| Test set membership | IN |
| Compare with a single calculated value | Scalar subquery |
| Stage a multi-step query | CTE |
| Keep rows while calculating group statistics | Window function |
| Rank every row | ROW_NUMBER / RANK / DENSE_RANK |
| One latest row per group | ROW_NUMBER |
| All tied latest/top rows | RANK / DENSE_RANK |
| Previous row | LAG |
| Next row | LEAD |
| Running total | SUM() OVER |
| Conditional metrics | CASE + aggregate |
| Combine result sets | UNION / UNION ALL |
| Large ordered pagination | Keyset/cursor pattern |
| Understand access strategy | EXPLAIN / execution plan |

[Back to Table of Contents](#table-of-contents)


---

<a id="infosys-sp-follow-up-questions"></a>

## Infosys SP Follow-Up Questions

The exact interview is not predictable, but these are the **high-value question shapes** you should be ready to handle.

### Query-purpose questions

- Why did you choose GROUP BY here?
- Why HAVING instead of WHERE?
- Why LEFT JOIN instead of INNER JOIN?
- Why EXISTS instead of JOIN?
- Why a CTE?
- Why a window function?
- Why ROW_NUMBER instead of RANK?
- Why DENSE_RANK instead of ROW_NUMBER?
- Why use DISTINCT?
- Why did you add a tie-breaker to ORDER BY?

### Query-correction questions

An interviewer may give an incorrect query and ask you to fix it.

Be ready for:

- wrong NULL comparison,
- aggregate in WHERE,
- incorrect LEFT JOIN filter,
- duplicate multiplication,
- incorrect ranking,
- accidental loss of rows,
- missing grouping column.

### Query-construction questions

Be able to build a query progressively:

```text
Start with one table
↓
Add filter
↓
Add second table
↓
Add grouping
↓
Add HAVING
↓
Add ranking
↓
Add final filter
```

### Performance questions

- Which index would help this query?
- Why is this query scanning many rows?
- What happens when the table grows 100x?
- How would you investigate a slow query?
- What would you look at in an execution plan?
- Can the query return duplicate rows?
- Could a window function replace the correlated subquery?
- Could the result be paginated more efficiently?

### Design-purpose questions

These are especially valuable:

> “You need one result per department. Which SQL feature naturally matches that?”

Answer direction:

```text
GROUP BY
```

> “You need every employee row plus the department average.”

Answer direction:

```text
window function
```

> “You only need to know whether an order exists.”

Answer direction:

```text
EXISTS
```

> “You need to stage a multi-step calculation so the main query is readable.”

Answer direction:

```text
CTE
```

The goal is to choose SQL constructs from **intent**, not from memorized patterns.

[Back to Table of Contents](#table-of-contents)

---

<a id="hidden-sql-keywords-and-concepts"></a>

## Hidden SQL Keywords and Concepts

These are easy to overlook but useful when an interviewer goes one layer deeper.

| Keyword / concept | What to know |
|---|---|
| WHERE | Row filtering |
| HAVING | Group filtering |
| DISTINCT | Duplicate elimination in result rows |
| COALESCE | First non-NULL expression |
| NULLIF | NULL when two expressions are equal |
| EXISTS | Existence test |
| ANY | Compare against at least one value |
| ALL | Compare against every value |
| BETWEEN | Inclusive range predicate in common SQL semantics |
| LIKE | Pattern matching |
| CASE | Conditional expression |
| WITH | CTE |
| OVER | Defines a window for a window function |
| PARTITION BY | Window grouping without collapsing rows |
| ROWS | Physical row-based window frame |
| RANGE | Value-based window framing semantics |
| ROW_NUMBER | Unique sequence in window order |
| RANK | Ties share rank; gaps |
| DENSE_RANK | Ties share rank; no gaps |
| LAG | Previous row |
| LEAD | Next row |
| UNION | Combine results and remove duplicates |
| UNION ALL | Combine results without duplicate elimination |
| EXISTS SELECT 1 | Common existence-check shape |
| DISTINCT ON | PostgreSQL-specific feature worth recognizing, not mandatory to use everywhere |
| FETCH / LIMIT | Result limiting syntax depends on dialect |
| OFFSET | Skips rows; can become expensive at large offsets |
| keyset pagination | Range-based pagination using an ordered key |
| row grain | Meaning of one output row |
| cardinality | Number of rows / relationship multiplicity |
| execution plan | DBMS strategy for executing a query |

### SP-level mental trigger

When you see a SQL question, silently ask:

```text
What is the row grain?
What is the relationship?
What is the filter?
What is the grouping?
Are ties possible?
Can NULL appear?
Will the JOIN multiply rows?
Can a window function simplify this?
What index might support the access pattern?
```

[Back to Table of Contents](#table-of-contents)

---

<a id="common-sql-traps"></a>

## Common SQL Traps

### Trap 1 — WHERE vs HAVING

```text
WHERE → rows
HAVING → groups
```

### Trap 2 — COUNT(*) vs COUNT(column)

```text
COUNT(*) → rows
COUNT(column) → non-NULL column values
```

### Trap 3 — LEFT JOIN + WHERE on the right table

This can remove NULL-extended rows and effectively behave like an inner join.

### Trap 4 — NOT IN + NULL

A NULL inside the subquery/set can change the truth result.

### Trap 5 — ROW_NUMBER vs RANK

Ask whether ties should produce one row per tie or multiple rows sharing the same rank.

### Trap 6 — DISTINCT as a band-aid

DISTINCT can hide a join-design error.

First understand why duplicates appeared.

### Trap 7 — Window function filtering

A window-function alias usually cannot simply be used in the same query block's WHERE clause. Use a CTE/derived table or dialect-specific supported syntax.

### Trap 8 — CTE equals materialization

Not necessarily. The optimizer may inline or materialize depending on the DBMS and query.

### Trap 9 — Index every filtered column

No. Index design depends on workload, selectivity, write cost, and access patterns.

### Trap 10 — Equivalent SQL always has identical performance

Not necessarily. The optimizer, statistics, indexes, data distribution, and DBMS version matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-revision-sheet"></a>

## 30-Second Revision Sheet

```text
SELECT
→ choose result expressions

WHERE
→ filter rows

GROUP BY
→ form groups

HAVING
→ filter groups

JOIN
→ combine related rows

LEFT JOIN
→ preserve left rows

EXISTS
→ test whether a related row exists

IN
→ test membership

CTE
→ name an intermediate query

CASE
→ conditional value

COUNT / SUM / AVG / MIN / MAX
→ aggregation

Window function
→ calculate across related rows without collapsing them

PARTITION BY
→ define independent windows

ROW_NUMBER
→ unique sequence

RANK
→ ties + gaps

DENSE_RANK
→ ties + no gaps

LAG
→ previous row

LEAD
→ next row

NULL
→ unknown / missing; use IS NULL

DISTINCT
→ remove duplicate result rows

ORDER BY
→ final ordering

LIMIT
→ return only part of the result

UNION
→ combine + de-duplicate

UNION ALL
→ combine without de-duplication

row grain
→ what one output row represents

cardinality
→ relationship / row multiplicity

index
→ possible faster access path, not a guarantee

execution plan
→ how the DBMS intends to execute the query
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-sql-interview-checklist"></a>

## Final SQL Interview Checklist

### Core SQL

- [ ] SELECT
- [ ] WHERE
- [ ] ORDER BY
- [ ] LIMIT / OFFSET
- [ ] DISTINCT
- [ ] NULL
- [ ] CASE
- [ ] Aggregates
- [ ] GROUP BY
- [ ] HAVING

### JOINs

- [ ] INNER JOIN
- [ ] LEFT JOIN
- [ ] SELF JOIN
- [ ] Anti-join
- [ ] JOIN multiplication
- [ ] Join cardinality

### Subqueries and query organization

- [ ] Scalar subquery
- [ ] Multi-row subquery
- [ ] Correlated subquery
- [ ] IN
- [ ] NOT IN
- [ ] EXISTS
- [ ] NOT EXISTS
- [ ] CTE

### Window functions

- [ ] OVER
- [ ] PARTITION BY
- [ ] ORDER BY in window
- [ ] ROW_NUMBER
- [ ] RANK
- [ ] DENSE_RANK
- [ ] LAG
- [ ] LEAD
- [ ] Running total
- [ ] Latest row per group
- [ ] Top-N per group

### Query design

- [ ] Identify row grain
- [ ] Choose tables
- [ ] Understand relationships
- [ ] Filter correctly
- [ ] Choose grouping/windowing
- [ ] Handle NULL
- [ ] Handle duplicates
- [ ] Handle ties

### Performance

- [ ] Read vs write query shape
- [ ] Index reasoning
- [ ] Composite index reasoning
- [ ] Selectivity
- [ ] Join cardinality
- [ ] Large sort/grouping
- [ ] Execution plan concept
- [ ] Keyset pagination
- [ ] Avoid SELECT *
- [ ] Measure before optimizing

### General SQL Query Practice

- [ ] Employee / department schema
- [ ] Student / course / enrollment schema
- [ ] Teacher / class schema
- [ ] Customer / order schema
- [ ] Product / order-item schema
- [ ] Project / employee-assignment schema
- [ ] User / event schema
- [ ] Joins + aggregation
- [ ] Subqueries + EXISTS
- [ ] Window functions
- [ ] Top-N / latest-row problems
- [ ] NULL / duplicate / tie handling
- [ ] Query variations

### Project SQL

- [ ] URL Shortener queries
- [ ] SceneFlow queries
- [ ] Project-specific joins
- [ ] Project-specific ranking
- [ ] Project-specific indexing discussion

### Interview execution

- [ ] Explain the query while writing
- [ ] State why you chose the construct
- [ ] Mention edge cases
- [ ] Discuss ties / NULLs / duplicates
- [ ] Give an alternative query when useful
- [ ] Explain performance implications
- [ ] Handle one follow-up modification without restarting from zero

[Back to Table of Contents](#table-of-contents)
