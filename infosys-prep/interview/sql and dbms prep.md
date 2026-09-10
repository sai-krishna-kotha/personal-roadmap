# Infosys DSE / SP — SQL & DBMS Interview Preparation Roadmap

> **Target:** Infosys DSE / Specialist Programmer (SP) technical interview, with SP L1 as the primary target and DSE as the safety target.
>
> **How to use this file:** Treat it as an execution roadmap, not a theory checklist. Learn each concept, solve the linked-style SQL problems, apply it to your own projects, and then answer the interview follow-ups aloud without notes.
>
> **Priority signal:** Recent personal/public candidate reports associated with this preparation have specifically pointed toward **SQL, window functions, indexing, database optimization, API security/scaling, database scaling, project flow/technology choices, and one Easy/Medium DSA problem**. These are signals rather than an official Infosys syllabus.

<a id="table-of-contents"></a>

## 📑 Table of Contents

### 🎯 Strategy
- [1. Interview Target](#1-interview-target)
- [2. What This Roadmap Is Optimized For](#2-what-this-roadmap-is-optimized-for)
- [3. The 3-Depth Preparation Rule](#3-the-3-depth-preparation-rule)
- [4. Priority Order](#4-priority-order)

### 🧱 SQL Foundation
- [5. SQL Execution Mental Model](#5-sql-execution-mental-model)
- [6. Core SELECT and Filtering](#6-core-select-and-filtering)
- [7. Aggregation, GROUP BY and HAVING](#7-aggregation-group-by-and-having)
- [8. JOINs and Relationship Queries](#8-joins-and-relationship-queries)
- [9. Subqueries, EXISTS, IN and CTEs](#9-subqueries-exists-in-and-ctes)
- [10. CASE, NULL and Conditional Logic](#10-case-null-and-conditional-logic)

### 🔥 Advanced SQL — High Priority
- [11. Window Functions](#11-window-functions)
- [12. Top-N, Ranking and Nth-Value Problems](#12-top-n-ranking-and-nth-value-problems)
- [13. Time-Series and Analytical SQL](#13-time-series-and-analytical-sql)
- [14. SQL Interview Problem Set](#14-sql-interview-problem-set)

### 🗄️ DBMS Core
- [15. Relational Design and Keys](#15-relational-design-and-keys)
- [16. Constraints and Referential Integrity](#16-constraints-and-referential-integrity)
- [17. Normalization and Denormalization](#17-normalization-and-denormalization)
- [18. Transactions and ACID](#18-transactions-and-acid)
- [19. Concurrency and Isolation](#19-concurrency-and-isolation)
- [20. Deadlocks](#20-deadlocks)

### ⚡ Indexing and Optimization — Very High Priority
- [21. Indexes](#21-indexes)
- [22. Composite Indexes and Selectivity](#22-composite-indexes-and-selectivity)
- [23. Query Execution Plans](#23-query-execution-plans)
- [24. Slow Query Troubleshooting Playbook](#24-slow-query-troubleshooting-playbook)

### 📈 Scaling and Backend Scenarios
- [25. Database Scaling](#25-database-scaling)
- [26. Read Replicas, Partitioning and Sharding](#26-read-replicas-partitioning-and-sharding)
- [27. Connection Pooling and Caching](#27-connection-pooling-and-caching)
- [28. API + Database Security](#28-api--database-security)

### 🔗 Project-Specific Preparation
- [29. URL Shortener — Database Deep Dive](#29-url-shortener--database-deep-dive)
- [30. URL Shortener — SQL Questions](#30-url-shortener--sql-questions)
- [31. URL Shortener — Optimization and Scaling Scenarios](#31-url-shortener--optimization-and-scaling-scenarios)
- [32. SceneFlow — Database Deep Dive](#32-sceneflow--database-deep-dive)
- [33. SceneFlow — SQL Questions](#33-sceneflow--sql-questions)
- [34. SceneFlow — Optimization and Scaling Scenarios](#34-sceneflow--optimization-and-scaling-scenarios)
- [35. Cross-Project Comparison Questions](#35-cross-project-comparison-questions)

### 🧪 Interview Drills
- [36. Recent Infosys Interview Signals](#36-recent-infosys-interview-signals)
- [37. SQL Whiteboard Drill](#37-sql-whiteboard-drill)
- [38. DBMS Rapid-Fire Drill](#38-dbms-rapid-fire-drill)
- [39. Scenario Drill](#39-scenario-drill)
- [40. 3-Day Crash Plan](#40-3-day-crash-plan)
- [41. 7-Day Strong Plan](#41-7-day-strong-plan)
- [42. Final 24-Hour Revision](#42-final-24-hour-revision)
- [43. Master Checklist](#43-master-checklist)

### 📚 Evidence / Notes
- [44. Evidence and Reliability Notes](#44-evidence-and-reliability-notes)
- [45. Sources Inside the Personal Roadmap](#45-sources-inside-the-personal-roadmap)

---

<a id="1-interview-target"></a>
# 1. Interview Target

### Primary target
**Infosys Specialist Programmer (SP L1)**

### Safety target
**Infosys DSE**

### Stretch target
**SP L2-level follow-up depth** where practical.

This roadmap is intentionally not a generic SQL course. It is designed around a likely technical interview conversation:

```text
SQL query
↓
Why this query?
↓
How does the DB execute it?
↓
What index helps?
↓
What if data becomes 100x larger?
↓
What if traffic becomes 100x larger?
↓
How would you secure the API?
↓
How did you handle this in your project?
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="2-what-this-roadmap-is-optimized-for"></a>
# 2. What This Roadmap Is Optimized For

Your existing Infosys interview roadmap places **SQL + DBMS in the highest-yield technical tier**, alongside projects, DSA and OOP. It also explicitly calls out indexing, optimization, database scaling, API security and basic system-design reasoning. fileciteturn5file0

Your existing DSA interview question bank records recent candidate reports mentioning SQL questions such as **department counts and second-highest salary**, and treats those reports as signals rather than guarantees. fileciteturn10file0

This file therefore emphasizes:

1. **Writing SQL from scratch**
2. **Window functions**
3. **Indexing**
4. **Query optimization**
5. **Transactions and concurrency**
6. **Database scaling**
7. **Project-specific schemas and queries**
8. **Explaining trade-offs aloud**

The target is not to memorize 100 SQL interview answers. The target is to become difficult to surprise.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="3-the-3-depth-preparation-rule"></a>
# 3. The 3-Depth Preparation Rule

For every important concept, train at three levels.

### Depth 1 — 30 seconds

Answer:

> What is it?

### Depth 2 — 2 minutes

Answer:

> How does it work, and give me an example.

### Depth 3 — follow-up defense

Answer:

```text
Why use it?
What are the trade-offs?
When would it fail or become expensive?
How would you optimize it?
How does it appear in your project?
```

For SQL, an additional rule applies:

> **Write the query, then explain the logical processing order.**

For DBMS:

> **Define the concept, connect it to a real failure mode, then explain the engineering trade-off.**

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="4-priority-order"></a>
# 4. Priority Order

## 🔴 Priority A — Must be interview-ready

```text
SQL joins + aggregation
Window functions
Second / nth highest
Top-N per group
Subqueries + CTEs
Indexes
Composite indexes
Query optimization
Execution plans
Transactions + ACID
Isolation levels
Normalization
Database scaling
Project database design
```

## 🟠 Priority B — Strong SP depth

```text
EXISTS vs IN
Correlated subqueries
NULL semantics
Deadlocks
Connection pooling
Read replicas
Partitioning vs sharding
Caching vs database reads
API/database security
Consistency trade-offs
```

## 🟡 Priority C — Know the concept

```text
Views
Stored procedures
Triggers
Materialized views
B-tree/B+ tree internals
MVCC concept
Distributed transaction basics
```

Do not spend your limited interview preparation time on obscure DB internals while still struggling with window functions or indexes.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="5-sql-execution-mental-model"></a>
# 5. SQL Execution Mental Model

You should understand the logical order in which a query is conceptually processed:

```text
FROM / JOIN
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

Window functions conceptually operate after the grouped result has been formed but before final ordering/limiting is applied.

### Why this matters

It explains common interview questions such as:

- Why can't a `WHERE` clause use an aggregate alias directly?
- Why do we use `HAVING` after `GROUP BY`?
- Why can a window-function result be filtered with an outer query/CTE?

### Practice example

```sql
SELECT department_id,
       COUNT(*) AS employee_count
FROM employees
WHERE status = 'active'
GROUP BY department_id
HAVING COUNT(*) >= 5
ORDER BY employee_count DESC;
```

Be able to explain each clause in order rather than saying only "this query counts employees."

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="6-core-select-and-filtering"></a>
# 6. Core SELECT and Filtering

Master:

- `SELECT`
- column aliases
- `WHERE`
- comparison operators
- `AND`, `OR`, `NOT`
- `BETWEEN`
- `IN`
- `LIKE`
- `IS NULL`
- `ORDER BY`
- `LIMIT`
- `DISTINCT`

### Interview drills

1. Find employees with salary above a threshold.
2. Find users created in the last 30 days.
3. Find URLs that are active and not expired.
4. Find scenes whose status is `PENDING`.
5. Return the top 10 most-clicked URLs.

### Do not miss

`NULL` is not equal to anything, including another `NULL`.

Use:

```sql
WHERE expires_at IS NULL
```

not:

```sql
WHERE expires_at = NULL
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="7-aggregation-group-by-and-having"></a>
# 7. Aggregation, GROUP BY and HAVING

Know:

```text
COUNT(*)
COUNT(column)
SUM()
AVG()
MIN()
MAX()
GROUP BY
HAVING
```

### Core distinction

`WHERE` filters **rows before grouping**.

`HAVING` filters **groups after aggregation**.

### Practice

```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 70000;
```

### Interview follow-ups

- `COUNT(*)` vs `COUNT(column)`?
- What happens when the column contains `NULL`?
- Why can't aggregate filtering normally be written in `WHERE`?
- Can `HAVING` be used without `GROUP BY`?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="8-joins-and-relationship-queries"></a>
# 8. JOINs and Relationship Queries

This is a core interview area because both of your projects naturally contain relationships.

## Must know

```text
INNER JOIN
LEFT JOIN
RIGHT JOIN concept
FULL OUTER JOIN concept
SELF JOIN
CROSS JOIN concept
```

### Mental model

```text
INNER JOIN
→ only matching rows

LEFT JOIN
→ keep every left row + matching right rows
```

### Classic question

> Find customers who have never placed an order.

A robust pattern is:

```sql
SELECT c.id
FROM customers c
LEFT JOIN orders o ON o.customer_id = c.id
WHERE o.id IS NULL;
```

Know the alternative with `NOT EXISTS` and be prepared to compare them conceptually.

### Project connection

For SceneFlow, reason about joins such as:

```text
users
  ↓
projects
  ↓
scripts
  ↓
scenes
  ↓
search_jobs
  ↓
assets
```

The current project models explicitly include foreign-key relationships between these entities. fileciteturn13file0 fileciteturn14file0 fileciteturn15file0 fileciteturn19file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="9-subqueries-exists-in-and-ctes"></a>
# 9. Subqueries, EXISTS, IN and CTEs

### Learn the purpose of each

```text
Subquery
→ nested query used as an expression/source

CTE
→ named intermediate query for clarity/reuse within one statement

EXISTS
→ test whether at least one matching row exists

IN
→ test membership in a set/list
```

### Typical interview comparison

> `EXISTS` vs `IN`?

Do not answer with a simplistic rule such as "EXISTS is always faster." Performance depends on the database, data distribution and optimizer. Explain the semantic difference first, then mention that the optimizer may transform equivalent forms.

### Correlated subquery

Be able to explain why a correlated subquery refers to a row from the outer query and why it can be expensive if executed naively.

### CTE drill

Write a CTE that computes average department salary, then selects employees above their department average.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="10-case-null-and-conditional-logic"></a>
# 10. CASE, NULL and Conditional Logic

Know:

```sql
CASE
  WHEN condition THEN value
  ELSE value
END
```

### Useful interview pattern

```sql
SELECT short_code,
       CASE
           WHEN is_active = false THEN 'inactive'
           WHEN expires_at IS NOT NULL AND expires_at <= NOW() THEN 'expired'
           ELSE 'active'
       END AS lifecycle_state
FROM urls;
```

### NULL topics

Understand:

- three-valued logic (`TRUE`, `FALSE`, `UNKNOWN`)
- `IS NULL` / `IS NOT NULL`
- aggregate interaction with `NULL`
- `COALESCE`

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="11-window-functions"></a>
# 11. Window Functions

**Highest-priority SQL topic for this interview.**

A window function computes a value across a related set of rows **without collapsing those rows like `GROUP BY` does**.

## Must know

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
SUM() OVER(...)
AVG() OVER(...)
COUNT() OVER(...)
PARTITION BY
ORDER BY inside OVER
```

## The three ranking functions

Suppose salaries are:

```text
100
100
90
80
```

Then:

```text
ROW_NUMBER → 1,2,3,4
RANK       → 1,1,3,4
DENSE_RANK → 1,1,2,3
```

### Must write from memory

```sql
SELECT employee_id,
       department_id,
       salary,
       DENSE_RANK() OVER (
           PARTITION BY department_id
           ORDER BY salary DESC
       ) AS salary_rank
FROM employees;
```

### Interview questions

1. What does `PARTITION BY` mean?
2. How is a window function different from `GROUP BY`?
3. `RANK()` vs `DENSE_RANK()`?
4. `ROW_NUMBER()` vs `RANK()`?
5. How do you get the second-highest salary?
6. How do you get top 3 salaries per department?
7. How do you calculate a running total?
8. How do you compare the current row to the previous row?
9. How do you detect the first event for each user?
10. When would a window function be clearer than a self join?

### Running total

```sql
SELECT created_at,
       clicks,
       SUM(clicks) OVER (
           ORDER BY created_at
       ) AS running_clicks
FROM daily_clicks;
```

### Previous/next row

```sql
SELECT event_time,
       clicks,
       LAG(clicks) OVER (ORDER BY event_time) AS previous_clicks,
       LEAD(clicks) OVER (ORDER BY event_time) AS next_clicks
FROM daily_clicks;
```

### Practice rule

Do not only copy examples. Change:

- the partition column
- the ordering column
- ascending vs descending
- ranking function
- ties
- additional filter conditions

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="12-top-n-ranking-and-nth-value-problems"></a>
# 12. Top-N, Ranking and Nth-Value Problems

These are classic interview formats.

## Must solve without notes

### A. Second-highest salary

Know at least two approaches:

```text
MAX-based approach
Window-function approach
```

### B. Nth-highest salary

Understand how ties affect the answer.

### C. Top 3 salaries in each department

Use a partitioned ranking function.

### D. Highest-paid employee in each department

Know a window-function solution and understand why a plain `MAX(salary)` query alone cannot return every non-aggregated employee column directly.

### E. Employees above department average

Know:

```text
JOIN against aggregated subquery/CTE
or
window AVG() approach
```

### F. Latest record per user

Use:

```text
ROW_NUMBER() OVER (PARTITION BY user_id ORDER BY created_at DESC)
```

then keep rank 1.

### Interview trap

Ask yourself:

> Are ties allowed?

That determines whether `ROW_NUMBER`, `RANK`, or `DENSE_RANK` is the right semantic choice.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="13-time-series-and-analytical-sql"></a>
# 13. Time-Series and Analytical SQL

Be able to solve:

1. Daily event counts.
2. Seven-day rolling average.
3. Running total.
4. Month-over-month comparison.
5. First and latest event per user.
6. Detect repeated events.
7. Calculate percentage contribution of each group.
8. Find periods with zero activity.

### Useful window patterns

```text
SUM() OVER
AVG() OVER
LAG()
LEAD()
PARTITION BY
ROWS BETWEEN ...
```

The exact date functions differ by SQL dialect, so understand the idea rather than memorizing vendor-specific syntax without context.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="14-sql-interview-problem-set"></a>
# 14. SQL Interview Problem Set

Complete these in increasing difficulty.

## 🔴 Tier 1 — Core

- Employees above salary threshold
- Active users
- Duplicate emails
- Count employees by department
- Departments with more than N employees
- Customers without orders
- Highest salary
- Second-highest salary
- Average salary by department
- Records with `NULL`

## 🟠 Tier 2 — Joins + subqueries

- Employees above department average
- Employees earning more than manager
- Latest order per customer
- Customers with at least 3 orders
- Departments with no employees
- Products never purchased
- Users with activity in the last 30 days

## 🔥 Tier 3 — Window functions

- Top 3 salaries per department
- Second-highest distinct salary per department
- Latest row per user
- Running total
- Previous event using `LAG`
- Next event using `LEAD`
- Rank customers by monthly spend
- Detect consecutive/repeated events

## 🟣 Tier 4 — SP-style reasoning

- Rewrite a correlated subquery as a window-function/CTE solution.
- Compare two equivalent queries and discuss readability/performance considerations.
- Design indexes for a given query workload.
- Explain how the plan might change after indexing.
- Explain how the same query should change when the table reaches tens/hundreds of millions of rows.

### Practice standard

For every problem:

```text
Read
↓
Identify tables
↓
Identify relationship
↓
Define required rows
↓
Choose join/filter
↓
Choose grouping/windowing
↓
Write query
↓
Dry run on small data
↓
Check edge cases
↓
Explain complexity/performance
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="15-relational-design-and-keys"></a>
# 15. Relational Design and Keys

Know precisely:

- super key
- candidate key
- primary key
- alternate key
- foreign key
- composite key
- surrogate key
- natural key

### Interview question

> Why would you use a surrogate ID instead of a business field as the primary key?

Good reasoning should mention stability, uniqueness, foreign-key references and separation between identity and mutable business data.

### Project connection

Your URL shortener uses an integer primary key plus a unique short code. The short code is the externally meaningful identifier for redirects while the internal ID is used for database identity/relationships. fileciteturn16file0

SceneFlow uses UUID primary keys and foreign keys across users, projects, scripts, scenes and jobs. fileciteturn13file0 fileciteturn14file0 fileciteturn15file0 fileciteturn19file0

Be prepared to explain why those choices differ.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="16-constraints-and-referential-integrity"></a>
# 16. Constraints and Referential Integrity

Know:

```text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
```

Understand why constraints belong in the database even when application validation exists.

### Important project example

Your URL shortener uses a unique constraint/index on `short_code`, meaning the database participates in protecting uniqueness rather than relying only on application logic. fileciteturn16file0

That leads to a strong interview answer:

> "Application code can try to generate a unique value, but the database must still enforce the invariant because concurrent requests can race."

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="17-normalization-and-denormalization"></a>
# 17. Normalization and Denormalization

Know the purpose before memorizing normal forms.

### 1NF
Atomic values; no repeating groups.

### 2NF
In 1NF and every non-key attribute depends on the whole candidate key, not just part of a composite key.

### 3NF
In 2NF and non-key attributes do not depend transitively on another non-key attribute.

### BCNF
Every determinant is a candidate key.

### Interview questions

- Why normalize?
- What redundancy does normalization remove?
- Can normalization hurt performance?
- When is denormalization useful?
- How would you decide whether to denormalize?

### Practical answer

Normalization is primarily about **correctness, consistency and reducing unnecessary redundancy**. Denormalization can intentionally add redundancy to improve read performance or simplify hot read paths, but it adds write/update complexity and consistency responsibility.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="18-transactions-and-acid"></a>
# 18. Transactions and ACID

## Atomicity
All operations in the transaction succeed or the transaction is rolled back.

## Consistency
The transaction preserves defined database constraints/invariants.

## Isolation
Concurrent transactions should not interfere in unacceptable ways.

## Durability
Committed data should survive expected failures according to the database's durability guarantees.

### Must explain with an example

Suppose an operation moves ₹500 from A to B:

```text
Debit A
+
Credit B
```

You do not want a failure between the two operations to leave only one side committed.

### Project connection

Your URL shortener increments clicks with an atomic SQL update rather than reading the count into Python, incrementing it, and writing it back. The project README explicitly identifies this as protection against concurrent read-modify-write races. fileciteturn6file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="19-concurrency-and-isolation"></a>
# 19. Concurrency and Isolation

Know these anomalies:

```text
Dirty read
Non-repeatable read
Phantom read
Lost update
```

Know the names and general intent of common isolation levels:

```text
Read Uncommitted
Read Committed
Repeatable Read
Serializable
```

Exact behavior can vary by DB engine, so avoid pretending that every database implements these labels identically.

### Interview question

> Two requests read clicks = 10, both calculate 11, both write 11. What went wrong?

Answer:

> A read-modify-write race caused a lost update. Use an atomic database-side increment such as `SET clicks = clicks + 1`, or another concurrency-safe design.

That exact pattern maps directly to your URL shortener. fileciteturn17file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="20-deadlocks"></a>
# 20. Deadlocks

A deadlock occurs when transactions wait on each other's locks in a cycle.

Classic shape:

```text
T1 locks A → waits for B
T2 locks B → waits for A
```

### Prevention / handling ideas

- consistent lock ordering
- keep transactions short
- avoid unnecessary locking
- retry failed transactions when appropriate
- monitor and investigate deadlocks

Interview follow-up:

> "Should we just increase the database timeout?"

No. A timeout may hide symptoms; first understand the locking cycle and transaction design.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="21-indexes"></a>
# 21. Indexes

**Very high priority.**

### Core answer

An index is an auxiliary data structure maintained by the database to help locate rows efficiently for certain access patterns instead of scanning every row.

### Why it helps

For a selective lookup such as:

```sql
SELECT *
FROM urls
WHERE short_code = 'abc1234';
```

an index on `short_code` can allow efficient lookup.

### Why indexes are not free

Indexes:

- consume storage
- add write/update maintenance
- can increase insert/update/delete cost
- may be useless for low-selectivity predicates or unsuitable query shapes
- can be ignored by the optimizer if another plan is cheaper

### The interviewer may ask

> Why not index every column?

Answer using the trade-off above, not "because indexes take memory" alone.

Your URL shortener explicitly indexes/uniquely constrains `short_code` because redirect lookups are a core access path. fileciteturn16file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="22-composite-indexes-and-selectivity"></a>
# 22. Composite Indexes and Selectivity

Understand that index design follows the **query workload**, not just individual columns.

Suppose the common query is:

```sql
SELECT *
FROM events
WHERE user_id = ?
  AND created_at >= ?
ORDER BY created_at DESC;
```

A composite index such as:

```text
(user_id, created_at)
```

may be appropriate because the query filters by `user_id` and then works within the user's time range/order.

### Learn

- leftmost-prefix intuition for composite indexes
- equality vs range predicates
- ordering considerations
- selectivity
- covering-index concept
- index-only scan concept

Do not memorize a universal "always put X first" rule. Explain the actual predicates and workload.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="23-query-execution-plans"></a>
# 23. Query Execution Plans

Know the purpose of `EXPLAIN` and `EXPLAIN ANALYZE` in systems that support them.

### What you are looking for

```text
Seq/table scan
Index scan / index lookup
Join strategy
Estimated rows
Actual rows
Sort
Aggregate
Filter
Cost estimates
```

### Interview question

> "You added an index, but the query is still slow. What next?"

Answer:

```text
Verify the index matches the predicate/order.
↓
Inspect the execution plan.
↓
Check whether the optimizer actually uses it.
↓
Compare estimated vs actual rows where available.
↓
Look for expensive joins/sorts/scans.
↓
Measure again after the change.
```

Do not claim that indexing automatically makes a query faster.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="24-slow-query-troubleshooting-playbook"></a>
# 24. Slow Query Troubleshooting Playbook

This should become a memorized interview framework because recent candidate feedback specifically called out **database optimization**. fileciteturn9file0

When asked:

> **"A query takes 10 seconds. How do you optimize it?"**

Use this order:

### Step 1 — Measure

- Reproduce the query.
- Capture latency.
- Identify whether the database is actually the bottleneck.

### Step 2 — Inspect the plan

```text
EXPLAIN / EXPLAIN ANALYZE
```

### Step 3 — Check access paths

- Missing indexes?
- Wrong index?
- Poor composite-index order?
- Very low selectivity?

### Step 4 — Reduce work

- Select only needed columns.
- Filter early where semantically valid.
- Avoid unnecessary joins.
- Avoid repeated subqueries.
- Avoid accidental Cartesian products.

### Step 5 — Revisit query shape

Consider:

```text
JOIN vs subquery
CTE vs repeated logic
window function vs self join
keyset pagination vs large OFFSET
```

### Step 6 — Check data volume / statistics

A good query on 1,000 rows may behave very differently at 100 million rows.

### Step 7 — Consider caching

Only for stable/reusable reads where caching semantics are correct.

### Step 8 — Re-measure

Optimization without measurement is guesswork.

### Step 9 — Consider architecture

If the database is fundamentally overwhelmed:

```text
connection pooling
read replicas
partitioning
archival
asynchronous processing
sharding (if truly necessary)
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="25-database-scaling"></a>
# 25. Database Scaling

The interviewer may ask:

> **"How will you scale the database?"**

Do not immediately say "sharding."

Use a progression:

```text
1. Fix inefficient queries
2. Add appropriate indexes
3. Tune connection pooling
4. Add caching where useful
5. Scale vertically if appropriate
6. Add read replicas for read-heavy workloads
7. Partition large tables when useful
8. Archive cold data
9. Shard only when scale/workload justifies the complexity
```

### Vertical scaling

Increase CPU/RAM/IO resources on the database host.

### Horizontal scaling

Distribute workload across multiple database instances.

### Key interview principle

> **Scale the bottleneck, not the architecture diagram.**

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="26-read-replicas-partitioning-and-sharding"></a>
# 26. Read Replicas, Partitioning and Sharding

## Read replicas

Useful when:

```text
reads >> writes
```

Typical model:

```text
Application
   |
   +---- writes ---> Primary
   |
   +---- reads ----> Replica(s)
```

Trade-off: replication lag can mean a read replica is temporarily behind the primary.

## Partitioning

Split one logical table into partitions, often by range/list/hash.

Examples:

```text
click_events_2026_01
click_events_2026_02
click_events_2026_03
```

Useful for very large tables and data-locality/maintenance patterns.

## Sharding

Distribute rows across separate database nodes according to a shard key.

Trade-offs:

- more operational complexity
- cross-shard queries
- data rebalancing
- shard-key design
- more difficult distributed transactions

### Interview question

> "Read replicas or sharding?"

Answer based on the bottleneck:

```text
Read-heavy workload
→ read replicas may be a simpler first move

Data/throughput beyond one DB node
→ partitioning/sharding may be considered
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="27-connection-pooling-and-caching"></a>
# 27. Connection Pooling and Caching

## Connection pooling

Opening a fresh database connection for every request is expensive.

A pool keeps reusable connections and limits concurrent DB connections.

Interview question:

> Why can an oversized connection pool also be bad?

Because too many concurrent database connections can cause contention, memory pressure and overload.

## Caching

Caching is appropriate when a read is:

- frequent
- relatively stable
- expensive to recompute/fetch
- safe to serve from cached state within the freshness requirements

Your URL shortener uses Redis as a cache-aside layer for redirect lookups while PostgreSQL remains the source of truth. fileciteturn6file0

SceneFlow uses Redis for its worker/infrastructure layer together with Celery while PostgreSQL persists the relational application entities. fileciteturn8file0

### Cache-aside pattern

```text
Read
↓
Cache?
├─ Hit → return
└─ Miss → DB → populate cache → return
```

Be prepared for:

- cache invalidation
- TTL
- stale data
- cache stampede concept
- fallback behavior if Redis fails

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="28-api--database-security"></a>
# 28. API + Database Security

This section connects directly to the candidate feedback mentioning **API security**. fileciteturn9file0

Know:

### SQL injection

Use parameterized queries / ORM parameter binding.

### Authentication

Prove who the caller is.

### Authorization

Prove what the caller is allowed to do.

### Least privilege

The application DB user should have only the permissions required.

### Secrets

Never hard-code passwords/API keys in source code.

### Transport security

Use HTTPS/TLS in deployed environments.

### Input validation

Validate external inputs before business/database use.

### Rate limiting

Protect expensive or abuse-prone endpoints.

### Logging

Do not leak credentials/tokens through logs.

### Project connection

Your URL shortener already uses request validation and Redis-based rate limiting; it also documents a known limitation: analytics is currently public. Be ready to acknowledge that limitation rather than pretending the project is production-perfect. fileciteturn6file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="29-url-shortener--database-deep-dive"></a>
# 29. URL Shortener — Database Deep Dive

This project should be one of your strongest SQL/DBMS interview anchors.

The project uses **FastAPI + PostgreSQL + Redis + React**, with PostgreSQL as the source of truth. It supports short-code generation, custom aliases, expiration, click analytics, Redis cache-aside redirects and rate limiting. fileciteturn6file0

## Current relational model

The `urls` table includes:

```text
id             INTEGER PRIMARY KEY
short_code     VARCHAR(...) UNIQUE / indexed
 target_url    VARCHAR(2048)
created_at     TIMESTAMP WITH TIME ZONE
expires_at     TIMESTAMP WITH TIME ZONE NULL
clicks         INTEGER
is_active      BOOLEAN
```

The actual model currently exposes `id`, `short_code`, `target_url`, `created_at`, `expires_at`, `clicks`, and `is_active`. fileciteturn16file0

## Core access paths

### Redirect

```text
GET /{short_code}
↓
Redis lookup
↓
PostgreSQL on cache miss
↓
redirect
↓
atomic click increment
```

This is documented in the project architecture and design decisions. fileciteturn6file0

### Why `short_code` should be indexed

The hot database lookup is by `short_code`. The model explicitly uses `unique=True` and `index=True`. fileciteturn16file0

### Why atomic click increment

Current repository code uses:

```sql
UPDATE urls
SET clicks = clicks + 1
WHERE short_code = :short_code;
```

This is a direct database-side increment and avoids the classic read-modify-write race. fileciteturn17file0

## Questions you must answer aloud

1. Why PostgreSQL and not MongoDB?
2. Why Redis if PostgreSQL already stores the URL?
3. Why is PostgreSQL the source of truth?
4. What happens on a Redis cache miss?
5. What happens if Redis goes down?
6. Why index `short_code`?
7. Why enforce uniqueness in the DB?
8. Why can click counting become a bottleneck?
9. Why is `clicks = clicks + 1` safer than read-modify-write?
10. What if one URL receives 100,000 redirects per second?
11. Would you use a read replica for redirects?
12. Would a read replica solve click-counter writes?
13. How would you redesign analytics for very high write volume?
14. How would you expire or archive old URLs?
15. What happens if two requests try to create the same custom alias?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="30-url-shortener--sql-questions"></a>
# 30. URL Shortener — SQL Questions

Use these as **project-authentic SQL drills**.

### Q1. Top 10 most-clicked active URLs

Skills:

```text
WHERE
ORDER BY
LIMIT
```

### Q2. Number of URLs created per day

Skills:

```text
GROUP BY date/time bucket
COUNT
```

### Q3. Average clicks per active URL

Skills:

```text
AVG
WHERE
```

### Q4. URLs that have expired but remain active

Reason about:

```text
is_active
expires_at
CURRENT_TIMESTAMP
NULL handling
```

### Q5. Duplicate-target analysis

Find target URLs that have more than one short code.

Skills:

```text
GROUP BY
HAVING COUNT(*) > 1
```

### Q6. Top 3 URLs by clicks for each lifecycle bucket

Use a window function after defining the lifecycle group.

### Q7. Most recently created URL per day

Use:

```text
ROW_NUMBER()
PARTITION BY date
ORDER BY created_at DESC
```

### Q8. Find inactive URLs with no clicks

Combine filters cleanly.

### Q9. Explain the index for the redirect lookup

Given:

```sql
SELECT target_url, expires_at, is_active, clicks
FROM urls
WHERE short_code = ?;
```

Explain what index helps and why.

### Q10. Design analytics query for a future click-events table

Imagine:

```text
click_events(
    id,
    url_id,
    clicked_at,
    referrer,
    user_agent
)
```

Then solve:

- daily clicks per URL
- top URLs per day
- 7-day rolling clicks
- latest click per URL

This prepares you for scaling the current project beyond a single integer counter.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="31-url-shortener--optimization-and-scaling-scenarios"></a>
# 31. URL Shortener — Optimization and Scaling Scenarios

## Scenario A — Redirects become slow

Answer:

```text
Check Redis hit ratio
↓
Check DB fallback latency
↓
Inspect PostgreSQL plan for short_code lookup
↓
Verify index
↓
Check connection pool
↓
Measure DB saturation
```

## Scenario B — Redis is unavailable

Your current project deliberately falls back to PostgreSQL for redirects, so the core redirect path remains usable. fileciteturn6file0

Interview follow-up:

> Is fallback always a good choice?

Answer:

It improves availability, but a large Redis outage can suddenly push all traffic toward PostgreSQL and create a thundering-herd/load-spike problem. Discuss rate limiting, circuit breaking/fallback controls and capacity planning rather than claiming fallback is free.

## Scenario C — One short URL gets huge traffic

The project README identifies synchronous PostgreSQL click increments as a potential bottleneck at very high traffic. fileciteturn6file0

A better large-scale design could be:

```text
Redirect
↓
Redis lookup
↓
Redirect immediately
↓
Emit click event asynchronously
↓
Queue / worker
↓
Aggregate analytics
↓
PostgreSQL / analytics store
```

This separates the hot redirect path from high-volume analytics writes.

## Scenario D — Custom alias collision

Two requests ask for `/openai` simultaneously.

Correct reasoning:

```text
Application checks
        ↓
Both see "available"
        ↓
Both try INSERT
        ↓
Database UNIQUE constraint decides winner
```

Then handle the uniqueness error cleanly.

That is why application checks should not replace database constraints.

## Scenario E — 100x data growth

Discuss:

```text
indexes
query plans
archival
partitioning where needed
analytics separation
cache strategy
connection pooling
read replicas where useful
```

## Scenario F — Database is write-bound

Do not jump directly to more replicas because replicas primarily help reads.

For write-heavy click analytics, discuss asynchronous event ingestion/aggregation or a workload-specific analytics design.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="32-sceneflow--database-deep-dive"></a>
# 32. SceneFlow — Database Deep Dive

SceneFlow is the **Semantic Visual Asset Generator** project.

Its architecture uses:

```text
React + TypeScript
        ↓
FastAPI
        ↓
PostgreSQL / Redis / Qdrant
        ↓
Celery + external APIs + Gemini
```

PostgreSQL stores **Projects, Scripts, Scenes and Search Jobs**, while Qdrant handles persistent vector embeddings and Redis/Celery support background work. fileciteturn8file0

## Current relational chain

```text
User
 ↓
Project
 ↓
Script
 ↓
Scene
 ↓
SearchJob
 ↓
Asset
```

The current SQLAlchemy models show:

- `Project.user_id` → `users.id`, indexed
- `Script.project_id` → `projects.id`, indexed
- `Scene.script_id` → `scripts.id`, indexed
- `SearchJob.scene_id` → `scenes.id`, indexed
- `SearchJob.status` → indexed

The models also use cascading deletes down the relationship chain. fileciteturn13file0 fileciteturn14file0 fileciteturn15file0 fileciteturn19file0

## Why this is interview gold

The interviewer can ask you to reason about:

```text
JOINs
foreign keys
indexes
cascade deletes
status filtering
pagination
job queues
transaction boundaries
large projects
concurrent workers
```

## Key current fields

### Projects

```text
id
user_id
name
description
created_at
updated_at
```

### Scripts

```text
id
project_id
title
full_text
orientation_preference
created_at
updated_at
```

### Scenes

```text
id
script_id
title
sentence_text
order
status
analysis(JSON)
analyzed_at
created_at
updated_at
```

### Search jobs

```text
id
scene_id
requested_query
ranking_version
status
error_message
created_at
updated_at
```

These fields are reflected in the current model code. fileciteturn13file0 fileciteturn14file0 fileciteturn15file0 fileciteturn19file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="33-sceneflow--sql-questions"></a>
# 33. SceneFlow — SQL Questions

### Q1. Count scenes per project

```text
users/projects/scripts/scenes
JOIN + GROUP BY
```

### Q2. Projects with more than 10 scenes

Use:

```text
GROUP BY
HAVING
```

### Q3. Latest script for each project

Use `ROW_NUMBER()` / `RANK()` depending on desired tie semantics.

### Q4. Top 3 scenes per script by search-job count

Requires joins + aggregation + window ranking.

### Q5. Count search jobs by status

Use:

```text
GROUP BY status
```

### Q6. Find pending jobs older than a threshold

Use:

```text
WHERE status = 'PENDING'
AND created_at < ...
```

### Q7. Find scenes that have failed jobs but no completed job

Use aggregation / existence logic.

### Q8. Latest job per scene

Use:

```text
ROW_NUMBER() OVER (
    PARTITION BY scene_id
    ORDER BY created_at DESC
)
```

### Q9. User → project → script → scene report

Write a multi-join query that returns:

```text
user_id
project_name
script_title
scene_title
scene_status
```

### Q10. Search-job success rate

Calculate completed / total jobs per project or day.

### Q11. JSON analysis

Know conceptually that JSON columns are useful when fields are semi-structured, but you should not blindly put all relational data into JSON. Be prepared to discuss indexing and queryability trade-offs.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="34-sceneflow--optimization-and-scaling-scenarios"></a>
# 34. SceneFlow — Optimization and Scaling Scenarios

## Scenario A — "Users open a project with 100,000 scenes"

Discuss:

```text
pagination
keyset pagination where appropriate
indexes on foreign keys
status filtering
avoid SELECT *
query only required columns
```

## Scenario B — "Pending job dashboard is slow"

The model already indexes `SearchJob.status`. fileciteturn19file0

But that may not be sufficient.

Ask:

```text
What exactly is the query?
How many rows match?
What order is required?
Does the plan use the index?
Would a composite index be better?
```

For example, if the common workload becomes:

```text
WHERE status = 'PENDING'
ORDER BY created_at
```

you can discuss whether a composite index on the actual access pattern would help, then verify using the query plan.

## Scenario C — Many Celery workers update jobs concurrently

Discuss:

- transaction boundaries
- idempotency
- row locking where necessary
- status transitions
- retries
- duplicate work
- consistent state transitions

## Scenario D — PostgreSQL is storing too much transient job data

Think about:

```text
What belongs in relational DB?
What belongs in Redis?
What belongs in object storage?
What belongs in Qdrant?
```

Do not claim every data type belongs in PostgreSQL.

SceneFlow already separates responsibilities across PostgreSQL, Redis and Qdrant. fileciteturn8file0

## Scenario E — Vector search becomes the bottleneck

Do not solve a Qdrant problem by adding random PostgreSQL indexes.

Explain workload separation:

```text
Relational metadata
→ PostgreSQL

Vector similarity
→ Qdrant

Short-lived/cache/worker coordination
→ Redis
```

This is a strong SP-level architecture discussion because it shows you understand why different storage systems exist.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="35-cross-project-comparison-questions"></a>
# 35. Cross-Project Comparison Questions

Prepare these because interviewers often switch from one project to another to test whether your understanding is genuine.

### Q1. Both projects use PostgreSQL. Why?

Expected direction:

- relational entities
- constraints
- joins
- transactional behavior
- structured application metadata

### Q2. Why does SceneFlow also use Qdrant while the URL shortener uses Redis?

Expected direction:

```text
Redis
→ caching / rate limiting / transient coordination

Qdrant
→ vector similarity search
```

### Q3. Why not store SceneFlow embeddings directly in PostgreSQL?

Discuss specialized vector search capability vs keeping structured relational metadata in PostgreSQL.

### Q4. Why is Redis the source of truth in neither project?

Because cache/transient state and durable relational truth have different requirements.

### Q5. Which project has the more write-heavy bottleneck?

Reason about click updates in the URL shortener versus background search-job/workflow writes in SceneFlow.

### Q6. Which schema is more hierarchical?

SceneFlow's user → project → script → scene → job relationship chain is naturally hierarchical.

### Q7. Where would you add an index first?

Answer based on actual query workload, not a generic list.

### Q8. Which project needs asynchronous processing more urgently at scale?

The URL shortener's click analytics is a clear candidate because the current project itself notes synchronous click tracking as a potential bottleneck at very high traffic. fileciteturn6file0

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="36-recent-infosys-interview-signals"></a>
# 36. Recent Infosys Interview Signals

Your personal roadmap contains recent 2026 candidate/interview signals rather than official company documentation.

The existing interview roadmap records a particularly strong signal around:

```text
SQL
DBMS / indexing / optimization
API security and scaling
Project architecture + technology choices
One Easy/Medium DSA problem
```

It explicitly warns that these are **preparation signals, not guaranteed question lists**. fileciteturn5file0

The existing DSA interview bank records recent public reports that include SQL topics such as **department counts and second-highest salary** alongside project/resume questions and live coding. fileciteturn10file0

The current peer report motivating this roadmap also specifically highlighted:

```text
SQL
Window functions
Indexing
Database optimization
API security and scaling
Database scaling
Project flow + technology choices
One Easy/Medium DSA question
```

### What this means for your preparation

Do not prepare SQL as a semester subject.

Prepare it as:

```text
Query writing
+
Database reasoning
+
Performance reasoning
+
Project application
+
Scaling reasoning
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="37-sql-whiteboard-drill"></a>
# 37. SQL Whiteboard Drill

Do this without autocomplete.

## Round 1 — 10 minutes

Write from memory:

1. Second-highest distinct salary.
2. Top 3 salaries per department.
3. Customers with no orders.
4. Employees above department average.
5. Latest row per user.

## Round 2 — 15 minutes

Write:

6. Running total.
7. Previous event using `LAG`.
8. Monthly top customer using a window function.
9. Duplicate-target analysis for URLs.
10. Pending SceneFlow jobs older than a threshold.

## Round 3 — 15 minutes

For each query, answer:

```text
What indexes would you consider?
Would the query scale?
Could a window function simplify it?
Could a CTE improve readability?
What happens with NULLs?
What happens with ties?
```

### Pass condition

You can write all 10 with only minor syntax errors, then explain each query aloud.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="38-dbms-rapid-fire-drill"></a>
# 38. DBMS Rapid-Fire Drill

Answer each in 30–60 seconds.

1. What is a DBMS?
2. Primary key vs unique key?
3. Foreign key?
4. Candidate key?
5. Composite key?
6. Why normalization?
7. 1NF / 2NF / 3NF?
8. When denormalize?
9. What is an index?
10. Why does an index help?
11. Why can an index slow writes?
12. Why not index every column?
13. Clustered vs non-clustered concept?
14. Composite index?
15. Selectivity?
16. What is a transaction?
17. Explain ACID.
18. Dirty read?
19. Non-repeatable read?
20. Phantom read?
21. Lost update?
22. Isolation levels?
23. Deadlock?
24. Query execution plan?
25. How do you optimize a slow query?
26. Read replica?
27. Partitioning?
28. Sharding?
29. Connection pool?
30. Cache-aside?

### Pass condition

If you need more than 5–10 seconds to begin most answers, revise the topic and repeat.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="39-scenario-drill"></a>
# 39. Scenario Drill

These are the questions most likely to expose whether you understand the concepts beyond definitions.

### Scenario 1

> A database query became slow after data grew from 10,000 to 10 million rows. What do you do?

### Scenario 2

> You added an index and the query is still slow. Why?

### Scenario 3

> Your DB CPU is 95%. What do you inspect first?

### Scenario 4

> Read traffic increased 20x, writes stayed roughly constant. How do you scale?

### Scenario 5

> Writes increased 20x. Will read replicas fix it?

### Scenario 6

> Two users try to create the same URL alias simultaneously. How do you guarantee uniqueness?

### Scenario 7

> Your cache is down. Should the application fail?

### Scenario 8

> Your analytics counter gets millions of writes per minute. Would you keep updating one row synchronously?

### Scenario 9

> A user has 100,000 scenes. Why is `OFFSET 90000 LIMIT 100` potentially undesirable?

### Scenario 10

> Celery workers process the same job twice. How do you prevent or tolerate duplicate processing?

### Scenario 11

> Why does SceneFlow need Qdrant if PostgreSQL already exists?

### Scenario 12

> What would you redesign in your URL shortener for 100x traffic?

For every scenario use:

```text
Identify bottleneck
↓
Measure
↓
Local optimization
↓
Architectural change
↓
Trade-off
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="40-3-day-crash-plan"></a>
# 40. 3-Day Crash Plan

Use this when the interview could arrive very soon.

## Day 1 — SQL Core + Window Functions

### Session A — 90 min

```text
SELECT / WHERE
GROUP BY / HAVING
JOINs
NULL
CASE
```

Solve 8 basic/intermediate queries.

### Session B — 90 min

```text
ROW_NUMBER
RANK
DENSE_RANK
PARTITION BY
LAG / LEAD
running totals
```

Solve 8 window-function queries.

### Session C — 60 min

URL shortener SQL:

- top clicks
- daily counts
- duplicate targets
- expired URLs
- latest URL per day
- lifecycle analytics

### Session D — 30 min

Speak answers aloud:

```text
WHERE vs HAVING
RANK vs DENSE_RANK
GROUP BY vs window function
EXISTS vs IN
```

## Day 2 — DBMS + Indexing

### Session A — 90 min

```text
Keys
Constraints
Normalization
Transactions
ACID
```

### Session B — 90 min

```text
Isolation
Deadlocks
Indexes
Composite indexes
Selectivity
```

### Session C — 60 min

Practice:

> Optimize this slow query.

Use the troubleshooting playbook from [24](#24-slow-query-troubleshooting-playbook).

### Session D — 45 min

URL shortener DB deep dive:

```text
short_code index
unique constraint
atomic click update
Redis cache
high-traffic analytics
```

## Day 3 — Scaling + SceneFlow + Mock

### Session A — 90 min

```text
Vertical scaling
Read replicas
Partitioning
Sharding
Connection pooling
Caching
```

### Session B — 90 min

SceneFlow database deep dive:

```text
User → Project → Script → Scene → SearchJob → Asset
```

Write 8 project SQL queries.

### Session C — 60 min

API/database security:

```text
SQL injection
authentication
authorization
least privilege
HTTPS
rate limiting
secret management
```

### Session D — 60 min

Mock interview:

```text
5 SQL questions
5 DBMS questions
3 optimization questions
2 scaling questions
5 project questions
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="41-7-day-strong-plan"></a>
# 41. 7-Day Strong Plan

## Day 1 — SQL fundamentals

Core syntax + filtering + aggregation + `HAVING`.

**Output:** 15 queries.

## Day 2 — JOINs + subqueries

`INNER`, `LEFT`, self joins, `EXISTS`, `IN`, CTEs.

**Output:** 15 queries.

## Day 3 — Window functions

Ranking + partitioning + `LAG/LEAD` + running totals.

**Output:** 15 queries.

## Day 4 — DBMS fundamentals

Keys + constraints + normalization + ACID + isolation + deadlocks.

**Output:** 30 rapid-fire answers.

## Day 5 — Indexing + optimization

Indexes + composite indexes + execution plans + slow-query framework.

**Output:** 10 optimization scenarios.

## Day 6 — Scaling + projects

URL shortener + SceneFlow + Redis + Qdrant + Celery + DB scaling + API security.

**Output:** 20 project questions.

## Day 7 — Full mock

```text
20 min SQL
20 min DBMS
15 min optimization/scaling
20 min project deep dive
10 min DSA
10 min HR
```

Then review every weak answer.

### 7-day success condition

You should be able to:

```text
write SQL
+
explain SQL
+
explain index choice
+
explain transaction behavior
+
optimize a slow query
+
scale a DB-backed API
+
defend both projects
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="42-final-24-hour-revision"></a>
# 42. Final 24-Hour Revision

Do not learn new obscure topics.

Revise only:

### SQL

```text
JOINs
GROUP BY / HAVING
Second-highest
Top-N per group
ROW_NUMBER / RANK / DENSE_RANK
LAG / LEAD
CTE
EXISTS vs IN
```

### DBMS

```text
Keys
3NF
ACID
Isolation
Deadlocks
Indexes
Composite indexes
Execution plan
```

### Scenarios

```text
Slow query
DB bottleneck
Read-heavy scaling
Write-heavy scaling
Cache failure
Unique alias race
High-volume analytics
```

### Projects

Know cold:

```text
schema
request flow
database flow
indexes
transaction boundaries
failure modes
scaling bottleneck
```

### Final oral drill

Explain each in under 90 seconds:

1. Why PostgreSQL in URL Shortener?
2. Why Redis?
3. Why index short_code?
4. Why atomic click increment?
5. How would you scale click analytics?
6. Why PostgreSQL + Qdrant in SceneFlow?
7. Why index foreign keys/status fields?
8. How would you optimize a slow project query?
9. How would you scale the DB?
10. How would you secure the APIs?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="43-master-checklist"></a>
# 43. Master Checklist

## SQL

- [ ] SELECT / WHERE / ORDER BY
- [ ] GROUP BY / HAVING
- [ ] INNER JOIN
- [ ] LEFT JOIN
- [ ] SELF JOIN
- [ ] Subqueries
- [ ] CTEs
- [ ] EXISTS / IN
- [ ] CASE
- [ ] NULL
- [ ] Second-highest salary
- [ ] Nth-highest salary
- [ ] Top-N per group
- [ ] Duplicate detection
- [ ] Latest row per group
- [ ] `ROW_NUMBER()`
- [ ] `RANK()`
- [ ] `DENSE_RANK()`
- [ ] `LAG()`
- [ ] `LEAD()`
- [ ] Running total
- [ ] Rolling aggregate

## DBMS

- [ ] Primary / candidate / foreign keys
- [ ] Constraints
- [ ] 1NF / 2NF / 3NF
- [ ] Denormalization
- [ ] ACID
- [ ] Isolation levels
- [ ] Dirty / non-repeatable / phantom reads
- [ ] Lost update
- [ ] Deadlocks
- [ ] Indexes
- [ ] Composite indexes
- [ ] Selectivity
- [ ] Query plans
- [ ] Connection pooling
- [ ] Caching
- [ ] Read replicas
- [ ] Partitioning
- [ ] Sharding

## Project defense

- [ ] URL Shortener schema
- [ ] `short_code` uniqueness/index
- [ ] atomic click increment
- [ ] Redis cache-aside
- [ ] rate limiting
- [ ] analytics bottleneck
- [ ] high-traffic redesign
- [ ] SceneFlow schema
- [ ] foreign keys
- [ ] indexed relationships
- [ ] job status indexing
- [ ] cascade behavior
- [ ] PostgreSQL vs Qdrant roles
- [ ] Celery/Redis/database interaction
- [ ] large-project pagination
- [ ] worker concurrency

## Scenario defense

- [ ] Slow query
- [ ] DB CPU high
- [ ] Read traffic high
- [ ] Write traffic high
- [ ] Cache failure
- [ ] Alias race condition
- [ ] Duplicate job execution
- [ ] High-volume analytics
- [ ] Data growth 100x
- [ ] Traffic growth 100x

## Interview standard

- [ ] I can explain each major topic in 30 seconds.
- [ ] I can explain each major topic for 2 minutes with an example.
- [ ] I can handle at least 2 follow-ups without notes.
- [ ] I can write SQL without autocomplete.
- [ ] I can defend every major database choice in both projects.
- [ ] I can explain an index using a real query.
- [ ] I can explain how I would optimize a slow query.
- [ ] I can explain how I would scale both projects.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="44-evidence-and-reliability-notes"></a>
# 44. Evidence and Reliability Notes

This roadmap intentionally separates **interview signals** from guaranteed requirements.

The personal `infosys-prep` roadmap contains recent 2026 candidate-report material and explicitly frames it as preparation guidance rather than an official Infosys question list. fileciteturn5file0

The existing DSA/Interview question bank likewise labels public interview reports as signals and includes reported SQL examples such as department counts and second-highest salary. fileciteturn10file0

The current project sections are based on the actual repositories inspected for this roadmap, including their current READMEs and model/repository code. fileciteturn6file0 fileciteturn8file0 fileciteturn16file0 fileciteturn17file0 fileciteturn13file0 fileciteturn14file0 fileciteturn15file0 fileciteturn19file0

Do not describe any candidate-reported question as guaranteed to appear in your interview.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="45-sources-inside-the-personal-roadmap"></a>
# 45. Sources Inside the Personal Roadmap

For internal preparation context, these existing roadmap files are useful companions:

- `infosys-prep/Interview Preparation.md` — overall Infosys interview priorities and answer framework. fileciteturn5file0
- `infosys-prep/Interview DSA Questions.md` — candidate-reported interview patterns, including SQL examples and DSA follow-ups. fileciteturn10file0
- `infosys-prep/pyqs.md` — Round 2 public-question evidence and reliability framing. fileciteturn11file0
- `infosys-prep/structure_roadmap.md` — broad assessment-to-interview structure. fileciteturn18file0

Project references used to make this roadmap project-specific:

- `sai-krishna-kotha/URL-shortener/README.md` and URL repository/model files. fileciteturn6file0 fileciteturn16file0 fileciteturn17file0
- `sai-krishna-kotha/scene-flow-visuals-generator/Readme.md` and current SQLAlchemy model files. fileciteturn8file0 fileciteturn13file0 fileciteturn14file0 fileciteturn15file0 fileciteturn19file0

[⬆️ Back to Table of Contents](#table-of-contents)
