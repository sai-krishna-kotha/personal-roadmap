# Infosys SP — Interview Preparation Roadmap

> **Purpose:** A standalone interview-preparation roadmap separated from the main Infosys assessment roadmap. It is focused on the technical interview after Round 2, with extra emphasis on the **Specialist Programmer (SP)** role.
>
> The roadmap is extracted and reorganized from the interview/core-subject material already present in `infosys-prep/structure_roadmap.md`. The main roadmap remains the assessment + overall preparation plan; this file is the dedicated interview checklist.

<a id="table-of-contents"></a>

## 📑 Table of Contents

### 🎯 Interview Strategy
- [1. Interview Target](#1-interview-target)
- [2. What the Interview Is Testing](#2-what-the-interview-is-testing)
- [3. Priority Order](#3-priority-order)
- [4. Interview Answer Method](#4-interview-answer-method)

### 💻 DSA + Coding
- [5. DSA Interview Syllabus](#5-dsa-interview-syllabus)
- [6. Coding Problem Patterns](#6-coding-problem-patterns)
- [7. Coding Interview Explanation Structure](#7-coding-interview-explanation-structure)
- [8. New Problem Strategy](#8-new-problem-strategy)
- [9. Complexity](#9-complexity)

### 🧱 Core CS Subjects
- [10. OOP](#10-oop)
- [11. DBMS](#11-dbms)
- [12. SQL](#12-sql)
- [13. Operating Systems](#13-operating-systems)
- [14. Computer Networks](#14-computer-networks)

### 🛠️ SP Engineering + Projects
- [15. Project Deep Dive](#15-project-deep-dive)
- [16. Backend and Software Engineering](#16-backend-and-software-engineering)
- [17. Basic System Design](#17-basic-system-design)
- [18. Resume Defense](#18-resume-defense)

### 🗣️ Behavioral + Final Preparation
- [19. Self Introduction](#19-self-introduction)
- [20. HR and Behavioral Questions](#20-hr-and-behavioral-questions)
- [21. Technical Mock Interview](#21-technical-mock-interview)
- [22. Final Revision Checklist](#22-final-revision-checklist)
- [23. Final Interview Mental Model](#23-final-interview-mental-model)

---

<a id="1-interview-target"></a>
# 1. Interview Target

The main target is the **Infosys Specialist Programmer (SP)** technical interview.

Prepare to demonstrate four things:

```text
Can I code?
      +
Do I understand core CS?
      +
Do I understand my own projects?
      +
Can I reason about software-engineering decisions?
```

The existing preparation roadmap identifies the interview areas as:

- Coding questions
- DSA explanation
- SQL + DBMS
- OOP
- Operating Systems
- Computer Networks
- Projects and resume deep-dive
- Backend / software-development fundamentals
- Basic system-design and engineering reasoning
- HR / behavioral questions

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="2-what-the-interview-is-testing"></a>
# 2. What the Interview Is Testing

Think of the interview as five simultaneous checks:

```text
1. Coding ability
2. Computer-science fundamentals
3. Project ownership
4. Engineering reasoning
5. Communication
```

For SP-oriented preparation, do not prepare only definitions. Be ready for follow-up questions such as:

```text
What happens internally?
Why did you choose this approach?
Why this technology?
What is the trade-off?
What happens at larger scale?
What can fail?
How did you debug it?
```

A strong answer should normally move from:

```text
Definition
    ↓
Why it exists
    ↓
Example
    ↓
Trade-off / limitation
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="3-priority-order"></a>
# 3. Priority Order

Use this order when preparation time is limited.

## Priority 1 — Must be strong

1. **SQL + DBMS**
2. **Projects / resume**
3. **OOP**
4. **DSA coding + explanation**

## Priority 2 — Must know clearly

5. **Operating Systems**
6. **Computer Networks**
7. **Backend / software-engineering fundamentals**

## Priority 3 — SP-oriented depth

8. **Basic system design**
9. **Scalability and performance reasoning**
10. **Security / API / database engineering basics**

## Priority 4 — Behavioral

11. **Self introduction**
12. **Why Infosys?**
13. **Why SP?**
14. **Career goals and behavioral questions**

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="4-interview-answer-method"></a>
# 4. Interview Answer Method

Do not answer every technical question with a memorized one-line definition.

Use this structure:

```text
Definition
↓
Purpose
↓
Example
↓
Trade-off / limitation
```

### Example: What is a database index?

```text
Definition:
An index is an auxiliary data structure used to speed up data retrieval.

Purpose:
It can avoid scanning the entire table for many queries.

Trade-off:
It needs additional storage and can make writes slower because the index must be maintained.
```

Then stop and let the interviewer decide whether to go deeper.

For comparison questions, use:

```text
A vs B
→ definition of both
→ key difference
→ practical example
→ trade-off
```

For “why” questions, use:

```text
Problem
→ decision
→ reason
→ alternative
→ trade-off
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="5-dsa-interview-syllabus"></a>
# 5. DSA Interview Syllabus

The goal is not only to solve the problem. You must be able to **explain the reasoning**.

## Arrays and Strings

Know:

- Traversal
- Frequency counting
- Hashing
- Prefix Sum
- Two Pointers
- Sliding Window
- Sorting
- Maximum / minimum subarray ideas

## Stack / Queue / Heap

Know:

- Stack operations
- Queue / deque
- Monotonic Stack
- Next Greater / Smaller
- Heap / Priority Queue
- Top K patterns

## Binary Search

Know:

- Basic binary search
- First / last occurrence
- Search in rotated array
- Lower / upper bound concepts
- Binary Search on Answer
- Feasibility function

## Linked List

Know the basics:

- Traversal
- Reverse linked list
- Fast / slow pointers
- Cycle detection
- Merge lists
- Middle node

## Trees / BST

Know:

- Preorder
- Inorder
- Postorder
- Level order
- Maximum depth
- Diameter
- Path Sum
- Lowest Common Ancestor
- BST search / insert
- Validate BST
- Kth smallest
- Tree DP basics

## Graphs

Know:

- Adjacency list
- DFS
- BFS
- Connected components
- Cycle detection
- Topological sort
- Shortest path
- DSU / Union-Find
- Grid DFS / BFS

## Greedy

Know:

- Sorting-based greedy
- Interval greedy
- Greedy + heap
- Activity selection
- Jump Game
- Gas Station
- Non-overlapping intervals

## Dynamic Programming

This is especially important for an SP-oriented coding discussion.

Know:

- Recursion → memoization → tabulation → space optimization
- 1D DP
- 2D / grid DP
- Pick / not-pick
- 0/1 Knapsack
- Unbounded Knapsack
- Subset Sum
- Target Sum
- State DP
- Counting DP
- LIS
- LCS
- Edit Distance
- Tree DP
- Interval / Partition DP basics

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="6-coding-problem-patterns"></a>
# 6. Coding Problem Patterns

When you see a new problem, identify the underlying pattern instead of trying to remember an exact question.

| Problem signal | First pattern to consider |
|---|---|
| Fast lookup / frequency | Hashing |
| Range / subarray sum | Prefix Sum |
| Sorted array + pair | Two Pointers |
| Contiguous range + condition | Sliding Window |
| Sorted search space | Binary Search |
| Matching / nested structure | Stack |
| Next greater / smaller | Monotonic Stack |
| Top K / repeated minimum or maximum | Heap |
| Intervals | Sorting + Greedy / Heap |
| Equal-cost shortest path | BFS |
| Weighted non-negative shortest path | Dijkstra |
| Connected regions | DFS / BFS / DSU |
| Choose / skip | Pick / Not Pick DP |
| Count number of ways | Counting DP |
| State changes over positions | State DP |
| Subproblem over a range | Interval / Partition DP |

For DP, always derive:

```text
State
↓
Choices / transition
↓
Base case
↓
Memoization / tabulation
↓
Complexity
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="7-coding-interview-explanation-structure"></a>
# 7. Coding Interview Explanation Structure

When the interviewer gives a coding problem, follow this sequence:

```text
1. Restate the problem
2. State assumptions
3. Clarify important constraints if necessary
4. Give brute force
5. Explain why brute force is too slow
6. Derive the optimized idea
7. State the data structure / state
8. Explain the algorithm
9. State time complexity
10. State space complexity
11. Code
12. Dry-run with an example
13. Discuss edge cases
```

### Example explanation skeleton

```text
The problem asks us to ...

A brute-force approach would ...
Its complexity is ..., which is too expensive for ...

The key observation is ...
So I will maintain ...

For each ..., I will ...

The time complexity is ...
The space complexity is ...
```

Do not start typing code before you have communicated the core idea.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="8-new-problem-strategy"></a>
# 8. New Problem Strategy

When the problem is unfamiliar:

### Step 1 — Constraints

```text
N ≤ 20
→ backtracking / bitmask / exponential DP may be possible

N ≤ 10^3
→ O(N²) may be possible

N ≤ 10^5
→ usually target O(N) or O(N log N)

N very large
→ look for math / greedy / binary search / optimization
```

### Step 2 — Brute force

Find the obvious solution first.

### Step 3 — Bottleneck

Ask:

```text
What repeated work makes brute force slow?
```

### Step 4 — Pattern

Look for:

```text
Hashing
Prefix Sum
Binary Search
Heap
Greedy
Graph
DP
Math
```

### Step 5 — State / data structure

Ask:

```text
What information do I need to remember?
```

### Step 6 — Transition

For DP or graph problems, explicitly derive how one state leads to another.

### Step 7 — Complexity

Check whether the solution fits the constraints.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="9-complexity"></a>
# 9. Complexity

Be comfortable discussing:

```text
O(1)
O(log N)
O(N)
O(N log N)
O(N²)
O(N³)
O(2^N)
O(N!)
```

Know both:

- **Time complexity**
- **Space complexity**

For every coding solution, be ready to explain why the complexity is acceptable for the input constraints.

Common interview follow-up:

> Can you optimize this further?

Answer by identifying the current bottleneck first rather than blindly changing the algorithm.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="10-oop"></a>
# 10. OOP

## Core concepts

Know thoroughly:

- Class
- Object
- Constructor
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction
- Method Overloading
- Method Overriding
- Composition
- Association
- `is-a` vs `has-a`

## Deeper concepts

Understand conceptually:

- Static vs dynamic binding
- Dynamic dispatch
- Interface vs abstract class
- Composition vs inheritance
- Why abstraction is useful
- Why encapsulation matters
- Loose coupling
- High cohesion
- SOLID principles
- Dependency inversion

## Questions to practice

1. What is OOP?
2. Explain the four pillars with examples.
3. What is polymorphism?
4. Overloading vs overriding?
5. Abstraction vs encapsulation?
6. Interface vs abstract class?
7. Composition vs inheritance?
8. What is dynamic dispatch?
9. Why use private fields?
10. Give a real-world example of polymorphism.
11. Explain one SOLID principle with a practical example.
12. Why is composition often preferred over inheritance?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="11-dbms"></a>
# 11. DBMS

## Database fundamentals

Know:

- Database vs DBMS
- Relational database
- Tables and relationships
- ER concept
- Constraints

## Keys

Know:

- Primary key
- Candidate key
- Super key
- Foreign key
- Composite key

## Normalization

Understand:

- 1NF
- 2NF
- 3NF
- Why normalization reduces redundancy
- When denormalization can be useful

## Transactions

Know:

- Transaction
- ACID
- Isolation
- Atomicity
- Consistency
- Durability

## Isolation problems

Understand:

- Dirty read
- Non-repeatable read
- Phantom read
- Serializability concept

## Indexing

Know:

- Why indexes speed up reads
- Index storage cost
- Write/update overhead
- B-tree / B+ tree concept
- Why indexes are not automatically beneficial for every column

## Joins

Understand:

- INNER JOIN
- LEFT JOIN
- RIGHT JOIN concept
- Self join
- Join conditions

## Query optimization basics

Understand conceptually:

- Why indexes matter
- Why unnecessary scans are expensive
- Why selecting only required columns can help
- Why query structure affects execution cost

### DBMS questions

1. What is normalization?
2. Explain 1NF, 2NF and 3NF.
3. What is ACID?
4. What is a transaction?
5. What is an index?
6. Why can an index slow down writes?
7. What is a deadlock in database transactions?
8. What is the difference between clustered/non-clustered indexing conceptually?
9. What is a foreign key?
10. Explain different types of joins.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="12-sql"></a>
# 12. SQL

SQL should be treated as a **coding skill**, not only theory.

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
AGGREGATE FUNCTIONS
CTE concept
WINDOW FUNCTIONS
```

Know conceptually:

```text
ROW_NUMBER()
RANK()
DENSE_RANK()
```

## Core practice set

1. Second highest salary
2. Nth highest salary
3. Employees earning more than their managers
4. Department with highest average salary
5. Duplicate rows
6. Customers with no orders
7. Top 3 salaries in each department
8. Count employees per department
9. Join + filter
10. Join + aggregation
11. Employees earning above department average
12. Multiple-table JOIN + GROUP BY + HAVING

## SQL explanation checklist

For every query, know:

```text
What tables are involved?
↓
How are they joined?
↓
Which rows are filtered?
↓
How are rows grouped?
↓
Where is HAVING needed?
↓
Would a subquery / CTE / window function simplify it?
```

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="13-operating-systems"></a>
# 13. Operating Systems

## Processes and threads

Know:

- Process
- Thread
- Process vs thread
- Context switching
- Why threads can be cheaper than processes

## CPU scheduling

Know conceptually:

- FCFS
- SJF
- Priority Scheduling
- Round Robin

## Synchronization

Know:

- Race condition
- Critical section
- Mutex
- Semaphore

Be able to explain:

```text
Why can two threads corrupt shared data?
How does a mutex help?
How is a semaphore different?
```

## Deadlocks

Know the four necessary conditions:

1. Mutual exclusion
2. Hold and wait
3. No preemption
4. Circular wait

Also know:

- Prevention
- Avoidance
- Detection

## Memory

Know:

- Stack
- Heap
- Paging
- Virtual memory
- Page fault
- Fragmentation

### OS questions

1. Process vs thread?
2. Why are threads cheaper?
3. What is context switching?
4. What is a race condition?
5. Mutex vs semaphore?
6. What is deadlock?
7. What are the four conditions for deadlock?
8. What is virtual memory?
9. What is a page fault?
10. Stack vs heap?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="14-computer-networks"></a>
# 14. Computer Networks

## Core concepts

Know:

- OSI model
- TCP/IP model
- TCP vs UDP
- HTTP vs HTTPS
- DNS
- IP address
- MAC address
- ARP concept
- TCP three-way handshake
- Connection termination
- Cookies
- Sessions
- REST API
- HTTP methods
- HTTP status codes

## The most important flow

Be able to explain:

> **What happens when you type a URL in the browser?**

Use this structure:

```text
URL
↓
DNS resolution
↓
Network connection
↓
TCP connection
↓
TLS handshake if HTTPS
↓
HTTP request
↓
Server processing
↓
HTTP response
↓
Browser processing / rendering
```

You should be able to explain each major step at a basic interview level.

### CN questions

1. TCP vs UDP?
2. What is DNS?
3. Explain the TCP three-way handshake.
4. HTTP vs HTTPS?
5. What are HTTP methods?
6. What are common HTTP status codes?
7. Cookies vs sessions?
8. What is REST?
9. What is an IP address?
10. What happens when you type a URL in a browser?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="15-project-deep-dive"></a>
# 15. Project Deep Dive

For SP interviews, your projects must be defensible technically.

Choose your **two strongest projects** and prepare them deeply.

For each project, be able to explain:

## 1. Problem

```text
What problem does it solve?
Who has the problem?
Why is the problem worth solving?
```

## 2. Your exact contribution

Be precise about:

- What you personally implemented
- Which modules you owned
- What decisions you made
- What you did not implement

Never claim a component you cannot explain internally.

## 3. Architecture

Explain the request / data flow:

```text
Client
↓
Frontend
↓
API
↓
Business Logic
↓
Database
```

Adapt the diagram to the actual project.

## 4. Technology choice

For every major technology:

```text
Why this technology?
Why not an alternative?
What trade-off did you accept?
```

## 5. Database

Know:

- Tables
- Relationships
- Keys
- Important indexes
- Important queries
- Transactions where relevant

## 6. Backend

Know:

- API routing
- Request validation
- Authentication
- Authorization
- Middleware
- Business logic
- Database interaction
- Error handling
- Concurrency basics

## 7. Debugging

Prepare at least one real debugging story:

```text
Bug
↓
How you reproduced it
↓
How you investigated it
↓
Root cause
↓
Fix
↓
How you verified the fix
```

## 8. Production questions

Prepare answers for:

1. How would you handle 10x traffic?
2. Where would caching help?
3. What if the database becomes slow?
4. What if one component fails?
5. How do you secure the API?
6. How would you monitor the application?
7. How would you test it?
8. How would you deploy it?
9. What is the biggest weakness of the current architecture?
10. What would you redesign?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="16-backend-and-software-engineering"></a>
# 16. Backend and Software Engineering

For an SP-oriented interview, understand the fundamentals behind a backend application.

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

## Database interaction

Know conceptually:

- Connection management
- Connection pooling
- Transactions
- Indexing
- Query performance

## Reliability

Understand:

- Logging
- Monitoring
- Error handling
- Retries concept
- Background jobs
- Rate limiting

## Security basics

Know why applications need protection against:

- Broken authentication / authorization
- Injection attacks
- Invalid input
- Exposed secrets
- Insecure endpoints

Be able to explain security decisions made in your own project rather than memorizing a generic checklist.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="17-basic-system-design"></a>
# 17. Basic System Design

Do not try to become a system-design specialist solely for the interview. The target is **engineering reasoning**.

Know these concepts:

- Monolith vs microservices
- REST API
- Stateless backend
- Authentication
- Authorization
- Caching
- Database indexing
- Connection pooling
- Load balancing
- Horizontal scaling
- Vertical scaling
- Background jobs
- Message queues concept
- Logging
- Monitoring
- Rate limiting
- API validation
- Error handling

## Use this reasoning sequence

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
Bottlenecks
↓
Caching / indexing / queues where useful
↓
Failure handling
↓
Security
↓
Scaling
```

### Common questions

- How would you scale your project?
- What happens when traffic increases 10x?
- Where would you add caching?
- What happens if the database becomes the bottleneck?
- How would you handle a failing service?
- How would you rate-limit an API?
- Why might a queue be useful?
- When would you choose a monolith?
- When would you consider splitting services?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="18-resume-defense"></a>
# 18. Resume Defense

Everything written on the resume is potentially an interview question.

For every skill, project, internship, certification, achievement, or technology, be ready for:

```text
What is it?
↓
Where did you use it?
↓
Why did you use it?
↓
What did you implement?
↓
What problem did it solve?
↓
What limitation did you face?
```

Do not list technologies you cannot explain at an interview level.

### Project / internship questions

Prepare:

- What exactly did you do?
- What was your role?
- What was the hardest problem?
- What did you learn?
- What would you improve?
- How did you work with others?
- How did you debug problems?
- What result did your work produce?

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="19-self-introduction"></a>
# 19. Self Introduction

Prepare a **60–90 second** introduction.

Structure:

```text
Name / current background
↓
Core technical strengths
↓
Strong project / experience
↓
What kind of software work interests you
↓
Why you are interested in this opportunity
```

Do not turn the introduction into a chronological biography.

The objective is to give the interviewer useful technical hooks for the rest of the interview.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="20-hr-and-behavioral-questions"></a>
# 20. HR and Behavioral Questions

Prepare concise, genuine answers for:

1. Tell me about yourself.
2. Why Infosys?
3. Why Specialist Programmer?
4. Why software engineering?
5. What are your career goals?
6. What are your strengths?
7. What is your weakness?
8. Tell me about a failure.
9. Tell me about a difficult technical problem you solved.
10. Tell me about a team conflict.
11. Tell me about a time you showed leadership.
12. How do you handle deadline pressure?
13. Why should we hire you?
14. Are you comfortable learning a new technology?
15. Where do you see yourself in the next few years?

For experience-based answers, use:

```text
Situation
→ Task
→ Action
→ Result
→ Learning
```

Keep the answer truthful and based on your actual experience.

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="21-technical-mock-interview"></a>
# 21. Technical Mock Interview

Before the actual interview, run at least one complete mock.

## Round A — Coding

Take 1–2 unfamiliar Medium-level DSA problems.

For each:

```text
Understand
→ derive
→ explain
→ code
→ dry run
→ complexity
```

## Round B — SQL

Solve approximately five queries in one sitting.

Include:

- JOIN
- GROUP BY
- HAVING
- Subquery / CTE
- Window function

## Round C — Core CS

Answer without notes:

- 5 OOP questions
- 5 DBMS questions
- 5 OS questions
- 5 CN questions

## Round D — Project

Pick one project and defend it for 15–20 minutes.

Expect repeated:

```text
Why?
Why this?
What happens internally?
What if it fails?
How would you scale it?
How did you test it?
```

## Round E — Behavioral

Practice:

- Self introduction
- Why Infosys?
- Why SP?
- Strength / weakness
- Failure
- Team conflict
- Leadership
- Career goals

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="22-final-revision-checklist"></a>
# 22. Final Revision Checklist

## DSA

- [ ] Arrays / Strings
- [ ] Hashing
- [ ] Prefix Sum
- [ ] Two Pointers
- [ ] Sliding Window
- [ ] Binary Search
- [ ] Stack
- [ ] Monotonic Stack
- [ ] Heap
- [ ] Greedy
- [ ] Linked List basics
- [ ] Trees / BST
- [ ] Graph DFS / BFS
- [ ] Topological Sort
- [ ] DSU
- [ ] Dijkstra basics
- [ ] 1D DP
- [ ] 2D / Grid DP
- [ ] Pick / Not Pick
- [ ] State DP
- [ ] Counting DP
- [ ] LIS / LCS
- [ ] Tree DP
- [ ] Interval / Partition DP basics

## OOP

- [ ] Four pillars
- [ ] Overloading / overriding
- [ ] Interface / abstract class
- [ ] Composition / inheritance
- [ ] Dynamic dispatch
- [ ] SOLID basics

## DBMS + SQL

- [ ] Keys
- [ ] Normalization
- [ ] ACID
- [ ] Isolation problems
- [ ] Indexing
- [ ] Joins
- [ ] GROUP BY / HAVING
- [ ] Subqueries
- [ ] CTE concept
- [ ] Window functions
- [ ] Second / Nth highest salary
- [ ] Top K per group

## OS

- [ ] Process / thread
- [ ] Context switching
- [ ] Scheduling
- [ ] Race condition
- [ ] Mutex / semaphore
- [ ] Deadlock
- [ ] Virtual memory
- [ ] Paging / page fault
- [ ] Stack / heap

## CN

- [ ] OSI / TCP-IP
- [ ] TCP / UDP
- [ ] DNS
- [ ] TCP handshake
- [ ] HTTP / HTTPS
- [ ] Methods / status codes
- [ ] Cookies / sessions
- [ ] REST
- [ ] Browser URL flow

## SP Engineering

- [ ] REST APIs
- [ ] Authentication / authorization
- [ ] Validation / error handling
- [ ] Indexing / connection pooling
- [ ] Caching
- [ ] Load balancing
- [ ] Scaling
- [ ] Background jobs / queues
- [ ] Logging / monitoring
- [ ] Rate limiting
- [ ] Basic security

## Projects / Resume

- [ ] Two strongest projects deeply prepared
- [ ] Exact contribution known
- [ ] Architecture explained
- [ ] Database explained
- [ ] API flow explained
- [ ] Technology choices justified
- [ ] One real debugging story
- [ ] Testing explained
- [ ] Deployment explained
- [ ] 10x scaling question prepared
- [ ] Weakness / redesign prepared
- [ ] Every resume skill defensible

## Behavioral

- [ ] 60–90 second introduction
- [ ] Why Infosys?
- [ ] Why SP?
- [ ] Career goals
- [ ] Strength
- [ ] Weakness
- [ ] Failure
- [ ] Team conflict
- [ ] Leadership
- [ ] Deadline pressure

[⬆️ Back to Table of Contents](#table-of-contents)

---

<a id="23-final-interview-mental-model"></a>
# 23. Final Interview Mental Model

Do not try to sound like you memorized an interview guide.

The target is:

```text
Understand
↓
Explain clearly
↓
Reason about trade-offs
↓
Implement when asked
↓
Defend your decisions
```

For coding:

```text
Problem
↓
Constraints
↓
Brute force
↓
Bottleneck
↓
Pattern
↓
State / data structure
↓
Transition
↓
Complexity
↓
Code
↓
Test
```

For core CS:

```text
Definition
↓
Purpose
↓
Example
↓
Trade-off
```

For projects:

```text
Problem
↓
Architecture
↓
Your contribution
↓
Technology choices
↓
Implementation details
↓
Failure / debugging
↓
Performance
↓
Security
↓
Scaling
↓
Redesign
```

For behavioral questions:

```text
Situation
↓
Action
↓
Result
↓
Learning
```

The final goal is simple:

> **Be able to explain what you know, code what you understand, and defend the engineering decisions you actually made.**

[⬆️ Back to Table of Contents](#table-of-contents)
