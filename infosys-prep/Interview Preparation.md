# Infosys SP — Interview Preparation Roadmap

> **Purpose:** A dedicated, execution-focused roadmap for the Infosys technical interview after Round 2, with **Specialist Programmer (SP)** as the primary target.
>
> This file is intentionally different from `structure_roadmap.md`. The main roadmap covers the broader assessment journey; this file is the **interview execution plan**.

<a id="table-of-contents"></a>

## 📑 Table of Contents

### 🧭 Strategy
- [1. Interview Mission](#1-interview-mission)
- [2. Why the Plan Is Layered](#2-why-the-plan-is-layered)
- [3. Priority Pyramid](#3-priority-pyramid)
- [4. Preparation Rule](#4-preparation-rule)
- [5. Interview Answer Framework](#5-interview-answer-framework)

### 🔥 Layer 1 — Interview Safety Net
- [6. Layer 1 Overview](#6-layer-1-overview)
- [7. Self Introduction + HR](#7-self-introduction--hr)
- [8. Resume Defense](#8-resume-defense)
- [9. Project Ownership](#9-project-ownership)
- [10. Core OOP](#10-core-oop)

### 🎯 Layer 2 — Highest-Yield Technical Preparation
- [11. SQL](#11-sql)
- [12. DBMS](#12-dbms)
- [13. DSA Coding](#13-dsa-coding)
- [14. DSA Follow-Up Skills](#14-dsa-follow-up-skills)

### 🛠️ Layer 3 — SP Engineering Depth
- [15. Backend + APIs](#15-backend--apis)
- [16. Database Optimization + Scaling](#16-database-optimization--scaling)
- [17. API Security + Reliability](#17-api-security--reliability)
- [18. Basic System Design](#18-basic-system-design)

### 📚 Layer 4 — Core CS Coverage
- [19. Operating Systems](#19-operating-systems)
- [20. Computer Networks](#20-computer-networks)

### 🧪 Layer 5 — Interview Execution
- [21. Project Technical Drill](#21-project-technical-drill)
- [22. SQL Drill](#22-sql-drill)
- [23. DSA Drill](#23-dsa-drill)
- [24. Core CS Rapid Revision](#24-core-cs-rapid-revision)
- [25. Technical Mock Interview](#25-technical-mock-interview)
- [26. Final 24-Hour Checklist](#26-final-24-hour-checklist)
- [27. Final Interview Mental Model](#27-final-interview-mental-model)

---

<a id="1-interview-mission"></a>
# 1. Interview Mission

The target is not to know every computer-science topic deeply.

The target is to prove five things:

```text
I can code.
      +
I understand core CS.
      +
I understand my own projects.
      +
I can reason about real software systems.
      +
I can communicate my thinking clearly.
```

For this preparation stage, **depth should follow probability and usefulness**.

The current priority signal from recent candidate feedback is especially strong around:

```text
SQL
DBMS / indexing / optimization
API security and scaling
Project architecture + technology choices
One Easy/Medium DSA problem
```

Treat this as a preparation signal, not a guaranteed Infosys interview question list.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="2-why-the-plan-is-layered"></a>
# 2. Why the Plan Is Layered

The previous version had the right topics, but a flat syllabus can make preparation inefficient.

Use five layers instead:

```text
Layer 1
Interview Safety Net
↓
Layer 2
High-Yield Technical
↓
Layer 3
SP Engineering Depth
↓
Layer 4
Core CS Coverage
↓
Layer 5
Execution + Mocking
```

The rule is:

> **Do not move deeper until the previous layer is interview-safe.**

Example:

```text
Do not spend 2 hours on obscure OS details
while still being unable to explain your own project architecture.
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="3-priority-pyramid"></a>
# 3. Priority Pyramid

## 🔴 Priority A — Highest return

These should receive the largest share of preparation time.

1. **Projects + Resume Defense**
2. **SQL + DBMS**
3. **DSA Coding + Explanation**
4. **OOP**

## 🟠 Priority B — SP-oriented engineering

5. **Backend / REST APIs**
6. **API security**
7. **Database optimization**
8. **Database scaling**
9. **API scaling**
10. **Basic system design**

## 🟡 Priority C — Core CS

11. **Operating Systems**
12. **Computer Networks**

## 🟢 Priority D — Behavioral

13. **Self introduction**
14. **Why Infosys?**
15. **Why SP?**
16. **Strength / weakness / failure / teamwork / goals**

### Time allocation guide

For a short preparation window:

```text
Projects + Resume       25%
SQL + DBMS              25%
DSA + OOP               20%
Backend / API / Scale   15%
OS + CN                 10%
HR / Behavioral          5%
```

This is a planning heuristic, not an official Infosys weighting.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="4-preparation-rule"></a>
# 4. Preparation Rule

For every topic, prepare at **three depths**.

### Depth 1 — 30-second answer

Can I define it clearly?

### Depth 2 — 2-minute explanation

Can I explain how it works with an example?

### Depth 3 — Follow-up defense

Can I answer:

```text
Why?
Why this approach?
What is the trade-off?
What can fail?
How would you optimize it?
How would you scale it?
```

Do not memorize essays.

Use:

```text
Definition
→ purpose
→ example
→ trade-off
```

For project questions use:

```text
Problem
→ architecture
→ your contribution
→ decision
→ trade-off
→ result
→ limitation
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="5-interview-answer-framework"></a>
# 5. Interview Answer Framework

## Technical definition

```text
Definition
↓
Why it exists
↓
Example
↓
Trade-off
```

## Comparison

```text
A definition
↓
B definition
↓
Key difference
↓
Use case
↓
Trade-off
```

## Coding problem

```text
Understand
↓
Constraints
↓
Brute force
↓
Bottleneck
↓
Pattern
↓
Data structure / state
↓
Transition
↓
Complexity
↓
Code
↓
Dry run
↓
Edge cases
```

## Project question

```text
Problem
↓
Architecture
↓
Request / data flow
↓
Your exact work
↓
Why each technology
↓
Alternative considered
↓
Trade-off
↓
Failure / debugging
↓
Scaling
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="6-layer-1-overview"></a>
# 6. Layer 1 — Interview Safety Net

Before advanced preparation, make these automatic:

```text
1. 60–90 second self introduction
2. Resume line-by-line defense
3. Two strongest projects
4. Core OOP
5. Why Infosys?
6. Why SP?
7. One failure + one debugging story
8. One teamwork story
```

Success condition:

> **The interviewer should never find a basic question on your resume that you cannot answer.**

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="7-self-introduction--hr"></a>
# 7. Self Introduction + HR

Prepare a **60–90 second** technical introduction.

Structure:

```text
Name / B.Tech background
↓
Core technical strengths
↓
Strong project / internship
↓
What type of engineering work interests you
↓
Why this opportunity
```

Prepare concise answers for:

1. Tell me about yourself.
2. Why Infosys?
3. Why Specialist Programmer?
4. Why software engineering?
5. What are your strengths?
6. What is your weakness?
7. Tell me about a failure.
8. Tell me about a difficult technical problem.
9. Tell me about teamwork / conflict.
10. Where do you see yourself in a few years?
11. Why should we hire you?
12. Are you comfortable learning new technologies?

For experience-based answers:

```text
Situation
→ Task
→ Action
→ Result
→ Learning
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="8-resume-defense"></a>
# 8. Resume Defense

Treat every resume line as a potential question.

For every skill / project / internship / certification:

```text
What is it?
↓
Where did I use it?
↓
Why did I use it?
↓
What exactly did I implement?
↓
What problem did it solve?
↓
What went wrong?
↓
What would I improve?
```

### Resume danger rule

Do not merely recognize a technology.

You should be able to explain **how you used it**.

For a project bullet mentioning a framework, database, API, model, or deployment tool, prepare at least one concrete implementation detail.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="9-project-ownership"></a>
# 9. Project Ownership

Choose **two strongest projects** as primary interview projects.

For each, prepare a one-page mental model:

## A. Problem

```text
What problem?
Who faces it?
Why is it useful?
```

## B. Architecture

```text
Client
↓
Frontend
↓
API
↓
Business logic
↓
Database / external service
```

Use the real architecture, not this generic diagram blindly.

## C. Data flow

Be able to trace one complete request:

```text
User action
→ HTTP request
→ backend route
→ validation
→ business logic
→ database / model
→ response
→ frontend update
```

## D. Technology decisions

For every important choice:

```text
Why this?
Why not alternative X?
What trade-off did I accept?
```

## E. Failure and debugging

Prepare one real story:

```text
Bug
→ reproduction
→ investigation
→ root cause
→ fix
→ verification
```

## F. Production thinking

Be ready for:

- What if traffic becomes 10x?
- What if the DB becomes slow?
- Where can caching help?
- What happens if a service fails?
- How would you secure the API?
- How would you test it?
- How would you monitor it?
- What is the weakest part of the current design?
- What would you redesign?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="10-core-oop"></a>
# 10. Core OOP

Know these well enough to explain with a real example:

- Class and object
- Constructor
- Encapsulation
- Abstraction
- Inheritance
- Polymorphism
- Method overloading
- Method overriding
- Composition
- Association
- `is-a` vs `has-a`
- Interface vs abstract class
- Composition vs inheritance
- Dynamic dispatch
- Loose coupling / high cohesion
- Basic SOLID principles

### High-value questions

1. Explain the four pillars with examples.
2. Overloading vs overriding?
3. Abstraction vs encapsulation?
4. Interface vs abstract class?
5. Why prefer composition in some designs?
6. What is dynamic dispatch?
7. Explain one SOLID principle practically.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="11-sql"></a>
# 11. Layer 2 — SQL

**SQL is now a top-tier preparation area.** Treat it like coding.

## Must know

```text
SELECT
WHERE
ORDER BY
GROUP BY
HAVING
JOIN
LEFT JOIN
INNER JOIN
SUBQUERY
CTE
AGGREGATES
WINDOW FUNCTIONS
```

## Window functions

Understand:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
```

Know what `PARTITION BY` does and when a window function is preferable to a grouped query.

## Practice set

1. Second highest salary
2. Nth highest salary
3. Top 3 salaries in each department
4. Employees earning more than their managers
5. Employees above department average
6. Duplicate rows
7. Customers with no orders
8. Department with highest average salary
9. JOIN + filter
10. JOIN + GROUP BY + HAVING
11. CTE-based query
12. Window-function ranking query

## SQL explanation checklist

```text
Which tables?
↓
How are they joined?
↓
Which rows are filtered?
↓
How are rows grouped?
↓
Do I need HAVING?
↓
Would a subquery / CTE / window function be clearer?
```

## Interview standard

You should be able to write a query on a whiteboard/editor **without depending on memorized templates**.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="12-dbms"></a>
# 12. Layer 2 — DBMS

Focus on the parts that naturally connect to backend engineering.

## Fundamentals

- Database vs DBMS
- Relational model
- Tables and relationships
- Constraints
- Primary / candidate / foreign / composite keys

## Normalization

Know:

- 1NF
- 2NF
- 3NF
- Redundancy
- When denormalization can make sense

## Transactions

Know:

- Transaction
- ACID
- Atomicity
- Consistency
- Isolation
- Durability
- Serializability concept

## Isolation problems

Understand:

- Dirty read
- Non-repeatable read
- Phantom read

## Indexing — very high priority

Know:

- What an index is
- Why it can speed reads
- Why it consumes storage
- Why writes can become slower
- B-tree / B+ tree concept
- Why indexing every column is a bad idea
- How selectivity affects usefulness
- Why the query planner matters conceptually

## Query optimization

Be ready to discuss:

```text
Full table scan
vs
Index-assisted access

Too many rows
vs
Early filtering

SELECT *
vs
Required columns

Poor join strategy
vs
Better join conditions / indexes
```

## Database scaling

Know the concepts:

```text
Vertical scaling
Horizontal scaling
Read replicas
Partitioning / sharding concept
Caching
Connection pooling
```

Do not memorize implementation details you cannot defend.

### High-value questions

1. Why does an index speed up reads?
2. Why can an index slow writes?
3. When should you not create an index?
4. How would you optimize a slow query?
5. What happens when the database becomes the bottleneck?
6. Vertical vs horizontal scaling?
7. What is a read replica?
8. Why is connection pooling useful?
9. What is a deadlock?
10. Normalization vs denormalization?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="13-dsa-coding"></a>
# 13. Layer 2 — DSA Coding

The interview target is **pattern recognition + explanation**, not another full competitive-programming syllabus.

## Tier A — Must be automatic

- Hashing
- Prefix Sum
- Two Pointers
- Sliding Window
- Binary Search
- Stack
- Monotonic Stack
- Heap / Priority Queue
- BFS / DFS
- Grid DFS / BFS

## Tier B — Strong interview coverage

- Linked List basics
- Trees / BST
- Greedy
- 1D DP
- Pick / Not Pick DP
- 2D / Grid DP
- State DP
- Counting DP
- Shortest path basics

## Tier C — Know the idea, not endless practice

- Topological Sort
- DSU
- Dijkstra
- LIS / LCS
- Tree DP
- Interval / Partition DP

## Problem recognition

| Signal | First pattern |
|---|---|
| Frequency / fast lookup | Hashing |
| Subarray / range sum | Prefix Sum |
| Sorted pair relationship | Two Pointers |
| Contiguous range + condition | Sliding Window |
| Sorted search space | Binary Search |
| Next greater / smaller | Monotonic Stack |
| Repeated min/max / Top K | Heap |
| Equal-cost shortest path | BFS |
| Weighted non-negative path | Dijkstra |
| Connected region | DFS / BFS / DSU |
| Choose / skip | DP |
| Count ways | Counting DP |
| State changes | State DP |

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="14-dsa-follow-up-skills"></a>
# 14. DSA Follow-Up Skills

Do not only practice solving.

For every problem, be able to answer:

```text
Why this pattern?
Why this data structure?
Why is this correct?
What is the time complexity?
What is the space complexity?
What edge cases matter?
Can it be optimized?
```

### For DP

Always derive:

```text
State
↓
Choices / transition
↓
Base case
↓
Memoization
↓
Tabulation
↓
Space optimization if useful
```

### Important lesson from Round 2

Your Round 2 experience showed why **state derivation matters more than memorizing movement patterns**.

For a grid/state problem, think:

```text
What does dp[r][c] mean?
↓
From this state, where can I go?
↓
What value determines the next state?
↓
What is the best answer for this state?
```

Do not assume every grid DP moves only right/down.

### Coding interview sequence

```text
Restate
→ constraints
→ brute force
→ bottleneck
→ optimized idea
→ code
→ dry run
→ complexity
→ edge cases
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="15-backend--apis"></a>
# 15. Layer 3 — Backend + APIs

This layer converts project knowledge into SP-level engineering reasoning.

## API fundamentals

Know:

- REST
- HTTP methods
- HTTP status codes
- Request / response
- Validation
- Error handling
- Authentication
- Authorization
- Statelessness

## Backend flow

Be able to explain:

```text
Request
↓
Routing
↓
Validation
↓
Authentication / authorization
↓
Business logic
↓
Database interaction
↓
Response
```

## Scaling an API

Think in layers:

```text
Measure bottleneck
↓
Optimize application code
↓
Database indexes / query optimization
↓
Caching where appropriate
↓
Connection pooling
↓
Horizontal application scaling
↓
Load balancing
↓
Background jobs / queues when appropriate
```

Never answer “scale it” with only “add more servers.” Explain the bottleneck first.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="16-database-optimization--scaling"></a>
# 16. Database Optimization + Scaling

Use this interview framework when asked:

> “The database is slow. What will you do?”

```text
1. Identify the slow query / workload
2. Inspect execution behavior conceptually
3. Check filtering and joins
4. Check useful indexes
5. Reduce unnecessary data transfer
6. Consider caching
7. Consider connection pooling
8. Measure again
9. Only then discuss larger-scale architecture
```

For a database under high traffic, discuss:

```text
Read-heavy workload
→ read replicas / caching

Large dataset
→ partitioning / sharding concept

Too many connections
→ connection pooling

Repeated expensive reads
→ caching

Write-heavy contention
→ workload / schema / transaction analysis
```

The important interview skill is **diagnosis before solution**.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="17-api-security--reliability"></a>
# 17. API Security + Reliability

Prepare the basic security model.

## Authentication

```text
Who are you?
```

## Authorization

```text
What are you allowed to do?
```

## Input security

Understand:

- Validation
- Injection prevention
- Safe handling of user input
- Output encoding concept where relevant

## Secrets

Know why:

- Passwords / API keys / tokens should not be hard-coded
- Secrets should be stored securely

## Reliability

Know conceptually:

- Logging
- Monitoring
- Retries
- Timeouts
- Rate limiting
- Background jobs
- Graceful error handling

## High-value questions

1. How would you secure an API?
2. Authentication vs authorization?
3. What is rate limiting?
4. Why are timeouts necessary?
5. When are retries dangerous?
6. How would you handle an API that becomes unavailable?
7. How would you protect against SQL injection?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="18-basic-system-design"></a>
# 18. Layer 3 — Basic System Design

The target is not advanced system-design theory.

The target is to answer:

> **How would you design and improve a practical backend system?**

Use:

```text
Requirements
↓
API / interface
↓
Data model
↓
Main components
↓
Request flow
↓
Bottleneck
↓
Optimization
↓
Failure handling
↓
Security
↓
Scaling
```

Know:

- Monolith vs microservices
- Stateless services
- Load balancing
- Caching
- Database indexing
- Read replicas
- Connection pooling
- Background jobs
- Message queues concept
- Rate limiting
- Logging / monitoring
- Horizontal vs vertical scaling

### Common design prompts

- Scale one of your projects to 10x traffic.
- Design a simple scoring API.
- Design a URL-shortening backend at a basic level.
- Handle a traffic spike.
- Design an API that should remain available when one component fails.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="19-operating-systems"></a>
# 19. Layer 4 — Operating Systems

Prepare the **high-yield interview layer**, not the entire textbook.

## Must know

### Process / thread

- Process
- Thread
- Process vs thread
- Context switching

### Synchronization

- Race condition
- Critical section
- Mutex
- Semaphore

### Deadlock

Know the four conditions:

1. Mutual exclusion
2. Hold and wait
3. No preemption
4. Circular wait

Also know prevention / avoidance / detection conceptually.

### Memory

- Stack vs heap
- Virtual memory
- Paging
- Page fault
- Fragmentation concept

### High-value questions

1. Process vs thread?
2. Why can threads be cheaper?
3. What is context switching?
4. What is a race condition?
5. Mutex vs semaphore?
6. What is deadlock?
7. Four necessary deadlock conditions?
8. What is virtual memory?
9. What is a page fault?
10. Stack vs heap?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="20-computer-networks"></a>
# 20. Layer 4 — Computer Networks

Prepare the concepts that connect directly to web/backend development.

## Must know

- OSI model
- TCP/IP model
- TCP vs UDP
- HTTP vs HTTPS
- DNS
- IP address
- MAC address concept
- TCP three-way handshake
- HTTP methods
- HTTP status codes
- Cookies / sessions
- REST

## Most important flow

Be able to explain:

```text
URL
↓
DNS resolution
↓
Network connection
↓
TCP connection
↓
TLS handshake for HTTPS
↓
HTTP request
↓
Server processing
↓
HTTP response
↓
Browser rendering / client processing
```

### High-value questions

1. TCP vs UDP?
2. What is DNS?
3. Explain the TCP three-way handshake.
4. HTTP vs HTTPS?
5. What are HTTP methods?
6. Common HTTP status codes?
7. Cookies vs sessions?
8. What is REST?
9. What happens when you type a URL?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="21-project-technical-drill"></a>
# 21. Layer 5 — Project Technical Drill

For each of your two primary projects, do this drill **out loud**.

### Round 1 — 60 seconds

Explain the project to a non-expert.

### Round 2 — 3 minutes

Explain the architecture and request flow.

### Round 3 — 5 minutes

Defend technology choices.

### Round 4 — 5 minutes

Explain one difficult implementation problem.

### Round 5 — 5 minutes

Answer:

```text
What if traffic becomes 10x?
What if DB becomes slow?
What if API fails?
How do you secure it?
How do you test it?
What would you redesign?
```

### Project ownership rule

The safest project answer is always based on what **you actually implemented**.

Never bluff an internal detail.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="22-sql-drill"></a>
# 22. Layer 5 — SQL Drill

Do one timed SQL sitting.

### Set

```text
2 JOIN queries
2 GROUP BY / HAVING queries
2 subquery / CTE queries
2 window-function queries
2 mixed queries
```

### Target

```text
Read schema
↓
Understand relationships
↓
Build query
↓
Run mentally
↓
Check edge cases
↓
Explain why it works
```

After every query ask:

> Could I solve this with another valid SQL approach, and why would I choose one over the other?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="23-dsa-drill"></a>
# 23. Layer 5 — DSA Drill

The interview drill is deliberately smaller than the Round 2 preparation.

Do:

```text
1 Easy
+
2 Medium
```

Across different patterns.

At least one should be a problem you have **not memorized**.

For each:

```text
Explain pattern
→ derive
→ code
→ dry run
→ complexity
```

### Preferred pattern spread

```text
1 array / hashing / sliding-window style
1 binary search / stack / heap style
1 tree / graph / DP style
```

The goal is to demonstrate adaptability, not volume.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="24-core-cs-rapid-revision"></a>
# 24. Core CS Rapid Revision

Use this order:

```text
OOP
↓
DBMS
↓
SQL
↓
OS
↓
CN
```

For each subject, prepare:

```text
10 high-value questions
+
5 comparison questions
+
2 practical examples
```

Do not spend final-day time on obscure theory.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="25-technical-mock-interview"></a>
# 25. Technical Mock Interview

Run one full mock before the real interview.

## Part A — Introduction

2 minutes.

## Part B — Project

15 minutes.

Expect:

```text
Why?
Why this technology?
How does it work?
What did you implement?
What failed?
How did you debug it?
How would you scale it?
```

## Part C — SQL / DBMS

15 minutes.

Include:

- JOIN
- GROUP BY / HAVING
- Window function
- Indexing
- Query optimization
- Scaling

## Part D — DSA

1 Easy/Medium coding problem.

Explain before coding.

## Part E — Core CS

Rapid questions from:

```text
OOP
OS
CN
DBMS
```

## Part F — HR

Why Infosys?
Why SP?
Strength / weakness?
Failure?
Career goal?

### Mock scoring

Score each from 1–5:

```text
Technical correctness
Explanation clarity
Coding ability
Project ownership
Engineering reasoning
Confidence / composure
```

Any score below 4 becomes the next revision target.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="26-final-24-hour-checklist"></a>
# 26. Final 24-Hour Checklist

## Projects

- [ ] Two projects fully explainable
- [ ] Architecture memorized conceptually
- [ ] Request/data flow clear
- [ ] Every major technology choice defensible
- [ ] One debugging story ready
- [ ] Scaling answer ready
- [ ] Security answer ready

## SQL / DBMS

- [ ] Joins
- [ ] GROUP BY / HAVING
- [ ] Subquery / CTE
- [ ] Window functions
- [ ] Indexing
- [ ] Query optimization
- [ ] ACID
- [ ] Isolation problems
- [ ] Database scaling

## DSA

- [ ] Explain a solution before coding
- [ ] Hashing / prefix sum
- [ ] Binary search
- [ ] Stack / monotonic stack
- [ ] Heap
- [ ] BFS / DFS
- [ ] DP state derivation

## OOP

- [ ] Four pillars
- [ ] Overloading / overriding
- [ ] Interface / abstract class
- [ ] Composition / inheritance
- [ ] Dynamic dispatch

## Backend / SP

- [ ] REST
- [ ] Authentication / authorization
- [ ] API security
- [ ] Rate limiting
- [ ] Caching
- [ ] Connection pooling
- [ ] API scaling
- [ ] Database scaling

## OS / CN

- [ ] Process / thread
- [ ] Race condition
- [ ] Mutex / semaphore
- [ ] Deadlock
- [ ] Virtual memory
- [ ] TCP / UDP
- [ ] DNS
- [ ] HTTPS
- [ ] URL flow

## HR

- [ ] 60–90 second introduction
- [ ] Why Infosys?
- [ ] Why SP?
- [ ] Strength
- [ ] Weakness
- [ ] Failure
- [ ] Teamwork
- [ ] Career goals

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="27-final-interview-mental-model"></a>
# 27. Final Interview Mental Model

Do not try to sound like you memorized a guide.

The interviewer should see:

```text
Knowledge
+
Reasoning
+
Ownership
+
Adaptability
+
Communication
```

### For technical theory

```text
Define
→ explain
→ example
→ trade-off
```

### For coding

```text
Understand
→ derive
→ explain
→ code
→ test
→ analyze
```

### For projects

```text
Problem
→ architecture
→ your work
→ why
→ trade-off
→ debugging
→ security
→ scaling
```

### The final target

> **Be strong enough in the highest-probability areas that an interviewer can keep going deeper without finding a weak foundation.**

And remember the most important project rule:

> **Anything on your resume can become a follow-up question. Prepare what you actually built, not what you merely recognize.**

[⬆️ Back to Table of Contents](#table-of-contents)
