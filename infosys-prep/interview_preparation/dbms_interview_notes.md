# DBMS Interview Notes — Infosys DSE / SP

> A dedicated DBMS interview reference for Infosys DSE / Specialist Programmer preparation.
>
> SQL query writing is intentionally kept in the separate SQL interview notes. This file focuses on how the database system stores, protects, indexes, executes, recovers, and scales data: relational design, keys, constraints, normalization, transactions, ACID, concurrency, isolation, locks, deadlocks, indexes, execution plans, recovery, scaling, and system-design trade-offs.

<a id="table-of-contents"></a>

## Table of Contents

- [How to Use These Notes](#how-to-use-these-notes)
- [DBMS Interview Depth Model](#dbms-interview-depth-model)
- [DBMS Mental Model](#dbms-mental-model)
- [General DBMS Interview Scenarios](#general-dbms-interview-scenarios)
- [Database and DBMS Basics](#database-and-dbms-basics)
- [Relational Model](#relational-model)
- [Keys](#keys)
- [Constraints and Referential Integrity](#constraints-and-referential-integrity)
- [Functional Dependencies](#functional-dependencies)
- [Normalization](#normalization)
- [First Normal Form](#first-normal-form)
- [Second Normal Form](#second-normal-form)
- [Third Normal Form](#third-normal-form)
- [BCNF](#bcnf)
- [Denormalization](#denormalization)
- [Transactions](#transactions)
- [ACID](#acid)
- [Atomicity](#atomicity)
- [Consistency](#consistency)
- [Isolation](#isolation)
- [Durability](#durability)
- [Concurrency Problems](#concurrency-problems)
- [Dirty Read](#dirty-read)
- [Non-Repeatable Read](#non-repeatable-read)
- [Phantom Read](#phantom-read)
- [Lost Update](#lost-update)
- [Isolation Levels](#isolation-levels)
- [Locks](#locks)
- [Deadlocks](#deadlocks)
- [MVCC](#mvcc)
- [Serializability](#serializability)
- [Indexes](#indexes)
- [Why Indexes Help](#why-indexes-help)
- [Composite Indexes](#composite-indexes)
- [Selectivity and Cardinality](#selectivity-and-cardinality)
- [Clustered and Non-Clustered Index Concepts](#clustered-and-non-clustered-index-concepts)
- [Covering Indexes](#covering-indexes)
- [When Indexes Hurt](#when-indexes-hurt)
- [Query Execution Plans](#query-execution-plans)
- [Slow Query Troubleshooting](#slow-query-troubleshooting)
- [Storage and Data Access Concepts](#storage-and-data-access-concepts)
- [Views and Materialized Views](#views-and-materialized-views)
- [Stored Procedures and Triggers](#stored-procedures-and-triggers)
- [Partitioning](#partitioning)
- [Sharding](#sharding)
- [Replication and Read Replicas](#replication-and-read-replicas)
- [Caching and Connection Pooling](#caching-and-connection-pooling)
- [Database Scaling Strategy](#database-scaling-strategy)
- [Consistency and Availability Trade-Offs](#consistency-and-availability-trade-offs)
- [Database Security](#database-security)
- [Backup and Recovery](#backup-and-recovery)
- [Project-Independent Design Scenarios](#project-independent-design-scenarios)
- [Project Connections](#project-connections)
- [Likely Infosys SP Follow-Up Questions](#likely-infosys-sp-follow-up-questions)
- [Hidden DBMS Keywords and Concepts](#hidden-dbms-keywords-and-concepts)
- [Common DBMS Traps](#common-dbms-traps)
- [30-Second Revision Sheet](#30-second-revision-sheet)
- [Final DBMS Interview Checklist](#final-dbms-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

For every DBMS concept, train at four levels:

\`\`\`text
What is it?
↓
Why do we need it?
↓
How does it work?
↓
What engineering problem does it solve?
↓
What trade-off does it introduce?
↓
How would an interviewer change the scenario?
\`\`\`

For interview answers, use:

\`\`\`text
Definition
→ intuition
→ simple example
→ technical example
→ mechanism
→ trade-off
→ follow-up
\`\`\`

This keeps the preparation practical instead of turning it into textbook memorization.

[Back to Table of Contents](#table-of-contents)

---

<a id="dbms-interview-depth-model"></a>

## DBMS Interview Depth Model

### Depth 1 — Definition

> What is an index?

### Depth 2 — Mechanism

> How does it help the database locate rows?

### Depth 3 — Trade-off

> Why not index every column?

### Depth 4 — Scenario

> The table grew from 100,000 rows to 100 million and the query became slow. What do you inspect?

### Depth 5 — System design

> Reads increased 20x but writes stayed stable. How would you change the database architecture?

This progression prepares you for an interviewer moving from theory to engineering without changing the topic.

[Back to Table of Contents](#table-of-contents)

---

<a id="dbms-mental-model"></a>

## DBMS Mental Model

Think of a database system as several layers:

\`\`\`text
Application
↓
SQL / API request
↓
Query parser + optimizer
↓
Execution plan
↓
Indexes / data pages
↓
Buffer / memory
↓
Storage
\`\`\`

Around execution, the DBMS also provides:

\`\`\`text
Transactions
Locks / MVCC
Recovery
Constraints
Security
Replication
\`\`\`

The important interview idea is that a database is not just a collection of tables.

It must provide:

\`\`\`text
Correctness
+
Concurrency
+
Durability
+
Performance
+
Recovery
+
Scalability
+
Security
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="general-dbms-interview-scenarios"></a>

## General DBMS Interview Scenarios

These are intentionally generic. An interviewer does not need to know your project to ask them.

### Two users update the same account

Relevant concepts:

\`\`\`text
transaction
concurrency
locking / MVCC
isolation
lost update
\`\`\`

### A query that took 20 ms now takes 4 seconds

Relevant concepts:

\`\`\`text
indexes
selectivity
execution plan
statistics
data growth
sort / join cost
\`\`\`

### The application crashes after writing half an order

Relevant concepts:

\`\`\`text
transaction
atomicity
rollback
recovery
\`\`\`

### The server loses power after COMMIT

Relevant concepts:

\`\`\`text
durability
logging
recovery
\`\`\`

### Two transactions wait for each other

Relevant concepts:

\`\`\`text
locks
deadlock
detection
victim transaction
retry
\`\`\`

### Read traffic becomes 20x higher

Relevant concepts:

\`\`\`text
read replicas
caching
connection pooling
query/index optimization
\`\`\`

### One table becomes enormous

Relevant concepts:

\`\`\`text
indexes
partitioning
retention
archival
access pattern
\`\`\`

### One customer becomes a hotspot

Relevant concepts:

\`\`\`text
hot rows
contention
partitioning
sharding
caching
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="database-and-dbms-basics"></a>

## Database and DBMS Basics

### Understanding

A database is an organized collection of data.

A DBMS is the software system that manages that data and provides capabilities such as:

\`\`\`text
data definition
data access
transactions
concurrency control
integrity enforcement
recovery
security
\`\`\`

### Simple example

Think of a library.

\`\`\`text
books = data
catalog = organization
library system = management layer
\`\`\`

### Technical example

A relational DBMS such as PostgreSQL or MySQL manages:

\`\`\`text
tables
indexes
transactions
queries
storage
recovery
constraints
\`\`\`

### Interview follow-up

> Why not just store everything in files?

A DBMS provides structured querying, concurrency control, recovery, integrity constraints, transactions, indexing, and other guarantees that raw files would otherwise force the application to implement.

[Back to Table of Contents](#table-of-contents)

---

<a id="relational-model"></a>

## Relational Model

### Understanding

The relational model represents data through relations, commonly exposed as tables.

Think:

\`\`\`text
row
→ one record

column
→ one attribute

table
→ collection of related records
\`\`\`

Relationships between entities are represented through keys.

### Technical example

\`\`\`text
departments(id, name)
employees(id, name, department_id)
\`\`\`

\`employees.department_id\` can reference \`departments.id\`.

### Interview follow-up

> Why is the relational model useful?

It provides a structured way to represent entities and relationships with well-defined integrity rules.

[Back to Table of Contents](#table-of-contents)

---

<a id="keys"></a>

## Keys

### Understanding

Keys identify rows or establish relationships.

### Main types

\`\`\`text
Super key
→ any attribute set that uniquely identifies a row

Candidate key
→ minimal super key

Primary key
→ chosen candidate key

Alternate key
→ candidate key not chosen as primary

Foreign key
→ references a key in another table

Composite key
→ key made from multiple columns

Natural key
→ business/domain value used as identity

Surrogate key
→ generated identifier used as identity
\`\`\`

### Simple example

A student might have:

\`\`\`text
roll_number
email
\`\`\`

Both may uniquely identify a student.

One can be chosen as the primary key while the other is enforced as another uniqueness rule.

### Technical example

\`\`\`text
students(id, email, name)
\`\`\`

Possible design:

\`\`\`text
id
→ primary key

email
→ UNIQUE
\`\`\`

### Interview follow-ups

> Primary key vs UNIQUE?

A primary key is the chosen identity for rows and has primary-key semantics. A UNIQUE constraint enforces uniqueness according to the DBMS's rules, which can differ in NULL handling and syntax.

> Natural vs surrogate key?

Natural keys carry business meaning; surrogate keys are generated identifiers. Discuss stability, width, mutability, and external exposure before choosing.

[Back to Table of Contents](#table-of-contents)

---

<a id="constraints-and-referential-integrity"></a>

## Constraints and Referential Integrity

### Main constraints

\`\`\`text
PRIMARY KEY
FOREIGN KEY
UNIQUE
NOT NULL
CHECK
DEFAULT
\`\`\`

### Understanding

Constraints move data correctness into the database boundary.

### Technical example

\`\`\`sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    salary DECIMAL(12,2) CHECK (salary >= 0),
    department_id INTEGER
);
\`\`\`

### Foreign key

\`\`\`sql
CREATE TABLE employees (
    id INTEGER PRIMARY KEY,
    department_id INTEGER,
    FOREIGN KEY (department_id)
        REFERENCES departments(id)
);
\`\`\`

### Interview question

> Why enforce constraints in the database if the application already validates input?

Because multiple writers, scripts, bugs, races, migrations, and concurrent requests can bypass application-level checks. The database is the final integrity boundary.

### Referential actions

Know the purpose of:

\`\`\`text
CASCADE
RESTRICT / NO ACTION
SET NULL
SET DEFAULT
\`\`\`

Exact behavior depends on the DBMS and constraint definition.

[Back to Table of Contents](#table-of-contents)

---

<a id="functional-dependencies"></a>

## Functional Dependencies

### Understanding

A functional dependency:

\`\`\`text
A → B
\`\`\`

means that knowing A determines B within the relation.

### Example

\`\`\`text
student_id → student_name
\`\`\`

if one student ID identifies one student.

### Why interviewers ask

Functional dependencies help reason about:

- candidate keys,
- redundancy,
- partial dependencies,
- transitive dependencies,
- normalization.

### Follow-up

> Why do functional dependencies matter?

They describe how attributes depend on determinants and provide the reasoning needed for normalization.

[Back to Table of Contents](#table-of-contents)

---

<a id="normalization"></a>

## Normalization

### Understanding

Normalization organizes relational data to reduce unnecessary redundancy and update anomalies.

Think:

\`\`\`text
duplicate facts
→ repeated storage
→ inconsistent updates
→ anomalies
\`\`\`

### Poor design

\`\`\`text
student_course(student_id, student_name, course_id, course_name, grade)
\`\`\`

If one student takes five courses, the student name is repeated five times.

### Better decomposition

\`\`\`text
students(student_id, student_name)
courses(course_id, course_name)
enrollments(student_id, course_id, grade)
\`\`\`

### Anomalies

\`\`\`text
Insert anomaly
Update anomaly
Delete anomaly
\`\`\`

### Interview line

> “Normalization separates independent facts so one fact has a natural place to be stored and updated.”

[Back to Table of Contents](#table-of-contents)

---

<a id="first-normal-form"></a>

## First Normal Form

### Understanding

1NF requires atomic values under the chosen row model and avoids repeating-group style storage.

Bad design:

\`\`\`text
student(id, name, phone1, phone2, phone3)
\`\`\`

or:

\`\`\`text
student(id, name, phones = "111,222,333")
\`\`\`

Better:

\`\`\`text
students(id, name)
student_phones(student_id, phone)
\`\`\`

### Interview line

> “1NF removes repeating-group style storage and keeps attributes atomic for the chosen row grain.”

[Back to Table of Contents](#table-of-contents)

---

<a id="second-normal-form"></a>

## Second Normal Form

### Understanding

2NF addresses partial dependency on part of a composite candidate key.

### Example

\`\`\`text
enrollment(student_id, course_id, student_name, course_name, grade)
\`\`\`

Suppose the key is:

\`\`\`text
(student_id, course_id)
\`\`\`

Then:

\`\`\`text
student_id → student_name
course_id → course_name
\`\`\`

Those attributes depend on only part of the composite key.

### Decompose

\`\`\`text
students(student_id, student_name)
courses(course_id, course_name)
enrollments(student_id, course_id, grade)
\`\`\`

### Interview trigger

When you hear:

> “Composite key”

immediately think:

> “Could there be a partial dependency?”

[Back to Table of Contents](#table-of-contents)

---

<a id="third-normal-form"></a>

## Third Normal Form

### Understanding

3NF addresses transitive dependency problems among non-key attributes.

### Example

\`\`\`text
employees(employee_id, department_id, department_name)
\`\`\`

If:

\`\`\`text
employee_id → department_id
department_id → department_name
\`\`\`

then:

\`\`\`text
employee_id → department_name
\`\`\`

The department name belongs with the department entity.

### Better design

\`\`\`text
employees(employee_id, department_id)
departments(department_id, department_name)
\`\`\`

### Interview line

> “3NF prevents a non-key attribute from depending transitively on the key through another non-key attribute.”

[Back to Table of Contents](#table-of-contents)

---

<a id="bcnf"></a>

## BCNF

### Understanding

BCNF is stronger than 3NF.

A relation is in BCNF when every determinant is a candidate key.

### Interview depth

Know the distinction:

\`\`\`text
3NF
→ removes transitive dependency problems

BCNF
→ every determinant must be a candidate key
\`\`\`

Do not spend disproportionate preparation time on rare decomposition proofs unless the interviewer goes there.

[Back to Table of Contents](#table-of-contents)

---

<a id="denormalization"></a>

## Denormalization

### Understanding

Denormalization intentionally introduces some redundancy to improve read performance or simplify common access patterns.

### Example

Normalized:

\`\`\`text
orders
customers
\`\`\`

A reporting workload may repeatedly need customer information with order rows. A reporting table can store selected customer attributes alongside order facts.

### Trade-off

\`\`\`text
Normalization
→ less redundancy
→ cleaner update boundaries
→ more joins in some reads

Denormalization
→ fewer joins in some workloads
→ duplicated data
→ harder update consistency
\`\`\`

### Interview follow-up

> Should we denormalize first?

No. Understand and measure the workload before introducing the extra complexity.

[Back to Table of Contents](#table-of-contents)

---

<a id="transactions"></a>

## Transactions

### Understanding

A transaction is a logical unit of work whose operations are committed or rolled back according to the transaction's guarantees.

### Personal example

Money transfer:

\`\`\`text
debit A
+
credit B
\`\`\`

Both operations belong to one logical unit.

### Technical example

\`\`\`sql
BEGIN;

UPDATE accounts
SET balance = balance - 100
WHERE id = 1;

UPDATE accounts
SET balance = balance + 100
WHERE id = 2;

COMMIT;
\`\`\`

If the operation cannot complete correctly:

\`\`\`sql
ROLLBACK;
\`\`\`

### Interview focus

Be ready to discuss:

- transaction boundaries,
- commit,
- rollback,
- partial failure,
- concurrency.

[Back to Table of Contents](#table-of-contents)

---

<a id="acid"></a>

## ACID

### Atomicity

All required changes happen, or the transaction is rolled back.

### Consistency

A committed transaction preserves defined database invariants and constraints.

### Isolation

Concurrent transactions do not interact in ways prohibited by the selected isolation behavior.

### Durability

Committed changes survive failures according to the DBMS's durability guarantees.

### Mental model

\`\`\`text
A → all or nothing
C → valid state
I → controlled concurrency interaction
D → survives failure after commit
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="atomicity"></a>

## Atomicity

### Understanding

Atomicity prevents a transaction from leaving only part of its intended work committed.

### Example

Bank transfer:

\`\`\`text
subtract from A
add to B
\`\`\`

If the second operation fails, keeping only the subtraction would be wrong.

### Interview follow-up

> What supports atomicity?

Conceptually:

\`\`\`text
transaction boundaries
rollback
logging / recovery mechanisms
\`\`\`

Exact implementation is DBMS-specific.

[Back to Table of Contents](#table-of-contents)

---

<a id="consistency"></a>

## Consistency

### Understanding

Consistency means that transactions preserve the database rules and invariants defined by the schema and application.

Examples:

\`\`\`text
primary-key uniqueness
foreign-key validity
CHECK constraints
business invariants enforced by the transaction
\`\`\`

### Important distinction

ACID consistency does not simply mean:

> “Every user immediately sees the latest value.”

That is a separate discussion involving isolation and distributed consistency.

[Back to Table of Contents](#table-of-contents)

---

<a id="isolation"></a>

## Isolation

### Understanding

Isolation controls how concurrent transactions observe and affect each other.

Imagine two users changing related data at the same time.

Without controlled concurrency:

\`\`\`text
one transaction
→ reads state

another transaction
→ changes it

first transaction
→ makes a decision based on a different state
\`\`\`

Isolation defines which anomalies are allowed or prevented.

### Leads to

\`\`\`text
dirty read
non-repeatable read
phantom read
lost update
isolation levels
locks
MVCC
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="durability"></a>

## Durability

### Understanding

After a successful commit, the DBMS should preserve the committed state across failures according to its durability guarantees.

### Technical idea

Many database systems use durable logging and recovery mechanisms.

A useful interview phrase:

> “The exact mechanism is DBMS-specific, but the database records enough durable information to recover committed changes after failure.”

### Follow-up

> Why can durability affect write performance?

Durable writes can require logging and synchronization work, depending on the DBMS, storage, and configuration.

[Back to Table of Contents](#table-of-contents)

---

<a id="concurrency-problems"></a>

## Concurrency Problems

Know the problem before learning the solution.

\`\`\`text
Dirty read
Non-repeatable read
Phantom read
Lost update
\`\`\`

The interviewer may describe an anomaly without naming it.

Your job is to identify it.

[Back to Table of Contents](#table-of-contents)

---

<a id="dirty-read"></a>

## Dirty Read

### Scenario

Transaction T1 updates a row but has not committed.

Transaction T2 reads that uncommitted value.

T1 then rolls back.

T2 has read a value that never became committed state.

### Mental model

\`\`\`text
T1: write → not committed
T2: read uncommitted value
T1: rollback
\`\`\`

### Interview phrase

> “T2 observed a value that could disappear because T1 had not committed.”

[Back to Table of Contents](#table-of-contents)

---

<a id="non-repeatable-read"></a>

## Non-Repeatable Read

### Scenario

T1 reads the same row twice.

Between the reads, T2 updates and commits that row.

T1 gets different values.

\`\`\`text
T1 read → 100
T2 update → 150
T1 read → 150
\`\`\`

### Mental trigger

\`\`\`text
same row
+
different committed value
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="phantom-read"></a>

## Phantom Read

### Scenario

T1 queries a set of rows using a predicate.

T2 inserts or deletes a matching row and commits.

T1 repeats the predicate query and sees a different set.

\`\`\`text
first query → 5 matching rows
T2 inserts matching row
second query → 6 rows
\`\`\`

### Mental trigger

\`\`\`text
same predicate
+
different matching row set
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="lost-update"></a>

## Lost Update

### Scenario

Two transactions read the same value, compute different updates, and one overwrites the other's work.

\`\`\`text
balance = 100

T1 reads 100
T2 reads 100

T1 writes 110
T2 writes 90

T1's change is lost
\`\`\`

### Interview direction

Discuss:

\`\`\`text
locking
optimistic concurrency
atomic updates
appropriate isolation
version columns
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="isolation-levels"></a>

## Isolation Levels

The SQL-standard names commonly discussed are:

\`\`\`text
READ UNCOMMITTED
READ COMMITTED
REPEATABLE READ
SERIALIZABLE
\`\`\`

Some systems expose additional snapshot-related modes.

### Mental progression

\`\`\`text
weaker isolation
↔
more concurrency / more possible anomalies

stronger isolation
↔
more coordination / potentially more overhead
\`\`\`

### Common interview mapping

| Level | Key idea |
|---|---|
| READ UNCOMMITTED | May permit dirty reads |
| READ COMMITTED | Prevents dirty reads; other anomalies may remain |
| REPEATABLE READ | Stronger repeat-read guarantees; exact behavior is DBMS-specific |
| SERIALIZABLE | Strongest standard isolation level; behavior is equivalent to some serial ordering |

### Critical interview point

Distinguish SQL-standard concepts from DBMS-specific implementations. Do not claim every DBMS behaves identically.

[Back to Table of Contents](#table-of-contents)

---

<a id="locks"></a>

## Locks

### Understanding

Locks coordinate concurrent access to shared data.

Common conceptual categories:

\`\`\`text
Shared lock
→ compatible read access in many lock models

Exclusive lock
→ protects conflicting writes
\`\`\`

Exact lock modes vary by DBMS.

### Example

If one transaction holds an exclusive lock while changing a row, another transaction attempting a conflicting operation may need to wait.

### Interview follow-up

> Do locks solve concurrency completely?

No.

Locks can introduce:

\`\`\`text
waiting
contention
deadlocks
\`\`\`

Modern systems may combine locking with MVCC.

[Back to Table of Contents](#table-of-contents)

---

<a id="deadlocks"></a>

## Deadlocks

### Understanding

A deadlock occurs when transactions wait on each other in a cycle.

### Classic example

\`\`\`text
T1 locks row A
T2 locks row B

T1 waits for B
T2 waits for A
\`\`\`

Neither can proceed.

### Prevention strategy

Acquire resources in a consistent order.

For example:

\`\`\`text
always lock lower account ID first
then higher account ID
\`\`\`

### Detection

Many DBMSs detect deadlocks and abort one transaction so the others can continue.

### Application behavior

Applications should be prepared to retry a retryable deadlock or serialization failure, subject to idempotency and transaction design.

[Back to Table of Contents](#table-of-contents)

---

<a id="mvcc"></a>

## MVCC

### Understanding

MVCC stands for **Multi-Version Concurrency Control**.

Instead of forcing readers and writers to always block each other on one physical version, the database can keep multiple row versions or visibility metadata.

### Mental model

\`\`\`text
row version A
row version B
row version C
↓
transaction visibility rules
↓
what each transaction can see
\`\`\`

### Why it matters

MVCC can improve concurrency for read/write workloads by allowing readers to see an appropriate visible version without every read taking a conflicting write lock.

### Interview follow-up

> Is MVCC the same as “no locks”?

No. Systems using MVCC can still use locks for writes, coordination, DDL, and other operations.

[Back to Table of Contents](#table-of-contents)

---

<a id="serializability"></a>

## Serializability

### Understanding

Serializability asks whether the effect of concurrent transactions is equivalent to some valid serial execution order.

Imagine:

\`\`\`text
T1 then T2
\`\`\`

A serializable concurrent execution should behave as if some serial ordering had occurred.

### Why interviewers ask

This connects:

\`\`\`text
transactions
→ concurrency
→ isolation
→ correctness
\`\`\`

### Follow-up

> Why not always use SERIALIZABLE?

Because stronger coordination can reduce concurrency and increase overhead or transaction aborts.

Use the strength required by the workload.

[Back to Table of Contents](#table-of-contents)

---

<a id="indexes"></a>

## Indexes

### Understanding

An index is an auxiliary data structure that can provide a more efficient access path for supported queries.

Think of a book index:

\`\`\`text
without index
→ inspect many pages

with useful index
→ jump toward relevant pages
\`\`\`

### Technical example

\`\`\`text
employees(id, name, department_id, salary)
\`\`\`

Query:

\`\`\`sql
SELECT *
FROM employees
WHERE department_id = 10;
\`\`\`

An index on \`department_id\` may provide a better access path.

### Important

An index is not automatically used.

The optimizer considers:

\`\`\`text
selectivity
table size
statistics
predicate
available indexes
estimated cost
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="why-indexes-help"></a>

## Why Indexes Help

Suppose a table has 50 million rows.

Without a useful access path, the database may need to inspect a large part of the table.

A selective index can narrow the candidate set significantly.

### Interview follow-up

> Why not create indexes on every column?

Because indexes:

- consume storage,
- increase INSERT/UPDATE/DELETE maintenance,
- may not help low-selectivity predicates,
- add operational complexity.

### Interview phrase

> “I design indexes from actual workload patterns and verify whether the optimizer uses them.”

[Back to Table of Contents](#table-of-contents)

---

<a id="composite-indexes"></a>

## Composite Indexes

### Understanding

A composite index contains multiple columns.

Example:

\`\`\`text
(customer_id, order_date)
\`\`\`

It can support workloads that filter or order by those columns in compatible ways.

### Why order matters

Think of a dictionary sorted by:

\`\`\`text
last_name
then first_name
\`\`\`

Searching by last name is a natural access pattern; searching only by first name is not equivalent.

### Example workload

\`\`\`sql
SELECT *
FROM orders
WHERE customer_id = 10
ORDER BY order_date DESC;
\`\`\`

An index on:

\`\`\`text
(customer_id, order_date)
\`\`\`

may align with the workload, depending on DBMS behavior and the broader query pattern.

### Follow-up

> Why is column order important?

Composite indexes have a defined ordering structure. Leading columns strongly influence which predicates can efficiently use the index.

[Back to Table of Contents](#table-of-contents)

---

<a id="selectivity-and-cardinality"></a>

## Selectivity and Cardinality

### Selectivity

Informally:

> How strongly does a predicate narrow the candidate rows?

For example:

\`\`\`text
WHERE user_id = 918273
\`\`\`

is often more selective than:

\`\`\`text
WHERE country = 'India'
\`\`\`

on a large global user table.

### Cardinality

Can refer to the number of rows in a result or relationship multiplicity.

Example:

\`\`\`text
one department → many employees
one employee → one department
\`\`\`

### Why it matters

Selectivity influences index usefulness.

Cardinality influences JOIN cost, row multiplication, and plan choice.

[Back to Table of Contents](#table-of-contents)

---

<a id="clustered-and-non-clustered-index-concepts"></a>

## Clustered and Non-Clustered Index Concepts

### Concept

A clustered index organizes table storage around an index ordering in systems that support clustered storage semantics.

A non-clustered index is a separate index structure that points to the underlying records or storage locations.

### Caveat

The exact model differs by DBMS.

Do not answer as if every database has one universal clustered-index implementation.

### Interview point

Know the conceptual trade-off:

\`\`\`text
data locality
vs
additional index structures
vs
write cost
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="covering-indexes"></a>

## Covering Indexes

### Understanding

An index is covering for a query when the index contains the information needed to satisfy that query, allowing the DBMS to avoid some extra table access in supported execution strategies.

### Example

\`\`\`sql
SELECT name
FROM employees
WHERE department_id = 10;
\`\`\`

An index containing the filtering column and the required output column may cover the query, depending on the DBMS.

### Trade-off

Larger indexes consume memory/storage and increase write maintenance.

[Back to Table of Contents](#table-of-contents)

---

<a id="when-indexes-hurt"></a>

## When Indexes Hurt

### INSERT

New index entries may need to be maintained.

### UPDATE

Changing indexed columns may require index maintenance.

### DELETE

Index entries must be removed.

### Mental model

\`\`\`text
More indexes
→ potentially better reads
→ more storage
→ more write maintenance
\`\`\`

### Interview line

> “Indexes trade write and storage cost for potentially faster reads.”

[Back to Table of Contents](#table-of-contents)

---

<a id="query-execution-plans"></a>

## Query Execution Plans

### Understanding

An execution plan describes how the DBMS intends to execute a query.

A plan can contain operations such as:

\`\`\`text
table scan
index scan / seek
join
sort
aggregate
filter
\`\`\`

### Why it matters

Two SQL statements can return the same result but produce different plans and different performance.

### Interview scenario

> “The query is slow. What do you inspect?”

Answer:

\`\`\`text
execution plan
+
estimated vs actual rows
+
chosen indexes
+
join strategy
+
sort / aggregate cost
\`\`\`

### Important distinction

Do not infer performance only from SQL text.

SQL is declarative; the optimizer chooses an execution strategy.

[Back to Table of Contents](#table-of-contents)

---

<a id="slow-query-troubleshooting"></a>

## Slow Query Troubleshooting

Use this workflow:

\`\`\`text
1. Identify the exact query and workload
↓
2. Measure current latency
↓
3. Inspect execution plan
↓
4. Compare estimated vs actual row counts
↓
5. Inspect joins and predicates
↓
6. Check indexes and selectivity
↓
7. Check sorting / aggregation
↓
8. Change one thing
↓
9. Measure again
\`\`\`

### Do not start with

> “Add an index.”

### Better answer

> “First I would inspect the execution plan and workload to determine whether the bottleneck is scanning, joining, sorting, aggregation, poor selectivity, data growth, or something outside the database.”

### If an index exists and the query is still slow

Possible reasons include:

\`\`\`text
wrong index
low selectivity
large result set
expensive sort
expensive join
stale statistics
predicate shape
I/O bottleneck
optimizer chooses another path
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="storage-and-data-access-concepts"></a>

## Storage and Data Access Concepts

### Pages / blocks

Databases commonly read and write storage in pages or blocks rather than individual logical rows.

### Buffer pool / cache

Frequently accessed pages can be kept in memory to reduce storage I/O.

### Why interviewers ask

The same query can have different observed latency depending on whether required pages are already in memory.

### Interview-level depth

Know:

\`\`\`text
page
buffer/cache
I/O
locality
sequential vs random access
\`\`\`

Exact internals are DBMS-specific.

[Back to Table of Contents](#table-of-contents)

---

<a id="views-and-materialized-views"></a>

## Views and Materialized Views

### View

A view is a stored query definition exposed like a relation.

Think:

\`\`\`text
complex query
→ reusable logical interface
\`\`\`

### Materialized view

A materialized view stores the query result physically and must be refreshed according to the DBMS's rules.

### Trade-off

\`\`\`text
View
→ logical abstraction
→ underlying query runs when accessed

Materialized view
→ faster reads for suitable workloads
→ refresh / staleness cost
\`\`\`

### Interview question

> When would you use a materialized view?

For expensive analytical queries whose results can tolerate controlled staleness and where precomputation significantly reduces read cost.

[Back to Table of Contents](#table-of-contents)

---

<a id="stored-procedures-and-triggers"></a>

## Stored Procedures and Triggers

### Stored procedure

Server-side programmable database logic.

### Trigger

Automatically executes database logic in response to specified database events.

### Use carefully

Triggers can enforce useful database-side behavior, but hidden side effects can make application behavior harder to understand and test.

### Interview question

> Should all business logic live inside the database?

No. The right split depends on transaction boundaries, portability, operational requirements, and system architecture.

[Back to Table of Contents](#table-of-contents)

---

<a id="partitioning"></a>

## Partitioning

### Understanding

Partitioning splits one logical table into multiple physical partitions while exposing it as one logical table to the application.

### Common forms

\`\`\`text
range
list
hash
\`\`\`

### Example

A huge events table could be partitioned by event date:

\`\`\`text
events_2026_01
events_2026_02
events_2026_03
...
\`\`\`

A query constrained by date may then access fewer partitions when partition pruning applies.

### Partitioning is not sharding

Partitioning typically remains inside one database system.

Sharding distributes data across multiple database instances/nodes.

[Back to Table of Contents](#table-of-contents)

---

<a id="sharding"></a>

## Sharding

### Understanding

Sharding horizontally distributes data across multiple database nodes.

Example:

\`\`\`text
Shard 1 → customer IDs 1–10M
Shard 2 → customer IDs 10M–20M
Shard 3 → customer IDs 20M–30M
\`\`\`

### Why shard?

When one database node cannot handle the workload or data footprint adequately.

### Trade-offs

\`\`\`text
more capacity
+
more operational complexity
+
cross-shard queries
+
rebalancing
+
distributed transactions
+
hot-shard risk
\`\`\`

### Interview point

Do not jump to sharding for moderate workloads.

Consider first:

\`\`\`text
query optimization
indexes
vertical scaling
read replicas
partitioning
caching
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="replication-and-read-replicas"></a>

## Replication and Read Replicas

### Understanding

Replication copies database state from one server to another according to the DBMS replication model.

A common architecture is:

\`\`\`text
Primary
→ writes

Read replicas
→ reads
\`\`\`

### Useful when

Read traffic is much higher than write traffic.

### Important trade-off

Replicas can lag behind the primary.

Therefore a read immediately after a write may not always see the just-written value if the application routes it to a lagging replica.

### Follow-up

> Can read replicas solve write bottlenecks?

Not by themselves. They primarily scale reads.

[Back to Table of Contents](#table-of-contents)

---

<a id="caching-and-connection-pooling"></a>

## Caching and Connection Pooling

### Caching

A cache stores frequently requested data closer to the application.

Common cache-aside flow:

\`\`\`text
Application
↓
Cache hit?
→ yes → return
→ no → DB → populate cache
\`\`\`

### Connection pooling

\`\`\`text
application
↓
connection pool
↓
reuse existing database connections
\`\`\`

### Why pooling matters

Database connections consume resources.

An oversized pool can overload the database even when the application itself appears healthy.

### Interview follow-up

> What happens if cache is down?

A common resilient design is to fall back to the database when feasible while protecting it from a sudden thundering herd.

[Back to Table of Contents](#table-of-contents)

---

<a id="database-scaling-strategy"></a>

## Database Scaling Strategy

When asked:

> “Traffic increased 100x. How do you scale the database?”

Use this order:

\`\`\`text
Measure bottleneck
↓
Optimize queries
↓
Add / improve indexes
↓
Scale vertically if appropriate
↓
Add caching
↓
Add read replicas for read-heavy workloads
↓
Partition large tables when justified
↓
Sharding when a single node is insufficient
\`\`\`

### Read-heavy workload

Think:

\`\`\`text
query/index optimization
+
cache
+
read replicas
\`\`\`

### Write-heavy workload

Think more carefully about:

\`\`\`text
transaction cost
hot rows
write amplification
batching
partitioning
data model
asynchronous processing
sharding
\`\`\`

### Interview phrase

> “I would scale according to the measured bottleneck rather than adding distributed complexity prematurely.”

[Back to Table of Contents](#table-of-contents)

---

<a id="consistency-and-availability-trade-offs"></a>

## Consistency and Availability Trade-Offs

### Understanding

Distributed architectures involve trade-offs among:

\`\`\`text
latency
consistency
availability
partition tolerance
\`\`\`

### Interview framing

Ask:

\`\`\`text
What consistency does the application require?
Can stale reads be tolerated?
Can writes be retried?
Can operations be asynchronous?
\`\`\`

### Example

A product catalog may tolerate brief stale reads.

A bank balance usually requires much stronger correctness guarantees.

The business invariant should drive the technical design.

[Back to Table of Contents](#table-of-contents)

---

<a id="database-security"></a>

## Database Security

### Core principles

\`\`\`text
least privilege
authentication
authorization
parameterized queries
secret management
encryption in transit
encryption at rest where appropriate
auditing
\`\`\`

### SQL injection connection

Use parameterized queries / prepared statements so untrusted input does not become SQL structure.

### Least privilege

An application account should receive only the permissions it needs.

Do not give every process full database-admin access.

[Back to Table of Contents](#table-of-contents)

---

<a id="backup-and-recovery"></a>

## Backup and Recovery

### Understanding

Backups provide a recovery path when data is lost, corrupted, or accidentally modified.

### Important distinction

\`\`\`text
Backup
→ recovery source

Replication
→ copy of current state for availability/scaling
\`\`\`

Replication is not a substitute for backups. Corruption or deletion can also be replicated.

### Interview concepts

\`\`\`text
full backup
incremental backup
point-in-time recovery
recovery testing
retention policy
\`\`\`

Exact mechanisms vary by DBMS.

[Back to Table of Contents](#table-of-contents)

---

<a id="project-independent-design-scenarios"></a>

## Project-Independent Design Scenarios

These are more important than project-specific database questions because they test transferable DBMS reasoning.

### Student registration

Schema:

\`\`\`text
students(id, name)
courses(id, name, capacity)
enrollments(student_id, course_id, created_at)
\`\`\`

Question:

> Two students try to take the last available seat at the same time. What can go wrong?

Think:

\`\`\`text
concurrency
race condition
transaction
locking / serialization
capacity invariant
\`\`\`

The important invariant is:

\`\`\`text
enrolled_count <= capacity
\`\`\`

### Bank transfer

Schema:

\`\`\`text
accounts(id, balance)
\`\`\`

Question:

> The application crashes after debit but before credit.

Direction:

\`\`\`text
single transaction
+
atomicity
+
rollback/recovery
\`\`\`

### Inventory

Schema:

\`\`\`text
products(id, stock)
orders(id, product_id, quantity)
\`\`\`

Question:

> Two customers purchase the last item simultaneously.

Discuss:

\`\`\`text
lost update
atomic stock decrement
locking / concurrency control
transaction
\`\`\`

### Large activity table

Schema:

\`\`\`text
events(id, user_id, event_time, event_type)
\`\`\`

Question:

> The events table has 500 million rows.

Discuss:

\`\`\`text
query patterns
indexes
partitioning
retention
archival
read replicas
\`\`\`

### Heavy reporting

Question:

> Operational queries and analytics compete for the same database.

Discuss:

\`\`\`text
read replicas
materialized views
ETL / analytical store
caching
workload isolation
\`\`\`

### High-traffic login system

Question:

> Authentication traffic suddenly increases 50x.

Discuss:

\`\`\`text
indexes on lookup fields
connection pooling
caching where appropriate
read replicas
rate limiting
hotspot identification
\`\`\`

### Duplicate payment request

Question:

> A client retries the same payment request twice.

Relevant database/design concepts:

\`\`\`text
idempotency key
unique constraint
transaction
\`\`\`

The database can help ensure the same logical request is not persisted twice.

[Back to Table of Contents](#table-of-contents)

---

<a id="project-connections"></a>

## Project Connections

These are secondary to the general DBMS preparation.

### URL Shortener

Use the project to explain:

\`\`\`text
unique short_code
indexes
atomic click updates
transactions
Redis vs PostgreSQL responsibilities
read-heavy scaling
\`\`\`

### SceneFlow

Use it to explain:

\`\`\`text
relational foreign keys
job state transitions
transactions
worker concurrency
indexes
PostgreSQL vs Redis vs Qdrant responsibilities
large-project pagination
\`\`\`

### Interview principle

First explain the generic DBMS concept.

Then connect it:

> “The same reasoning appears in my project when…”

This demonstrates transferable understanding rather than memorized project-specific answers.

[Back to Table of Contents](#table-of-contents)

---

<a id="likely-infosys-sp-follow-up-questions"></a>

## Likely Infosys SP Follow-Up Questions

These are high-value question shapes, not guaranteed questions.

### Keys and design

- Primary key vs candidate key?
- Primary key vs UNIQUE?
- Composite key?
- Natural vs surrogate key?
- Why foreign key?
- Why enforce constraints in DB instead of only application code?

### Normalization

- Why normalize?
- What is 1NF?
- What is 2NF?
- What is 3NF?
- What is a partial dependency?
- What is a transitive dependency?
- When would you denormalize?
- What are insert/update/delete anomalies?

### Transactions

- What is a transaction?
- Explain ACID.
- Give a real example of atomicity.
- What happens if the application crashes midway?
- What makes a transaction consistent?
- Why does durability matter?

### Concurrency

- What is a dirty read?
- Non-repeatable read?
- Phantom read?
- Lost update?
- What are isolation levels?
- What is serializability?
- What is MVCC?
- Why do locks cause contention?

### Deadlocks

- What is a deadlock?
- Give a concrete example.
- How can you prevent one?
- How does a DBMS detect one?
- Why can retrying a transaction be necessary?

### Indexes

- What is an index?
- Why does it improve reads?
- Why not index every column?
- What is a composite index?
- Why does index column order matter?
- What is selectivity?
- What is a covering index?
- What happens to writes after adding many indexes?
- Why might the optimizer ignore an index?

### Optimization

- How do you debug a slow query?
- What is an execution plan?
- What is a table scan?
- Why can an index still fail to help?
- How can statistics affect planning?
- What happens when data grows 100x?

### Scaling

- Vertical vs horizontal scaling?
- Read replica?
- Can replicas solve write scaling?
- Partitioning vs sharding?
- When would you shard?
- What is connection pooling?
- Why cache database results?
- What happens when cache fails?

### System-design bridge

- How would you scale a database for 100x traffic?
- What if reads dominate?
- What if writes dominate?
- What if one customer becomes a hotspot?
- How would you prevent duplicate writes?
- How would you handle a database outage?
- How would you recover after accidental deletion?

### Strong follow-up pattern

For every answer, be ready for:

\`\`\`text
Why?
How?
Trade-off?
What if traffic grows?
What if two requests arrive together?
What if the database fails?
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="hidden-dbms-keywords-and-concepts"></a>

## Hidden DBMS Keywords and Concepts

| Concept | What to know |
|---|---|
| Candidate key | Minimal unique identifier |
| Surrogate key | Generated identifier |
| Functional dependency | Attribute-determination relationship |
| Partial dependency | Dependency on part of a composite key |
| Transitive dependency | Non-key dependency through another non-key attribute |
| Referential integrity | Foreign-key relationship validity |
| ACID | Transaction guarantees |
| Isolation level | Concurrency visibility/control level |
| Dirty read | Read uncommitted data |
| Non-repeatable read | Same row reads differently within a transaction |
| Phantom read | Predicate returns a different row set |
| Lost update | One concurrent update overwrites another |
| Shared lock | Read-oriented lock concept |
| Exclusive lock | Write-oriented lock concept |
| Deadlock | Cyclic waiting |
| MVCC | Multi-version concurrency control |
| Serializability | Equivalent to some serial transaction ordering |
| Index selectivity | How strongly a predicate narrows candidates |
| Composite index | Multi-column index |
| Covering index | Index can satisfy required query data |
| Execution plan | Chosen execution strategy |
| Partitioning | Split one logical table into partitions |
| Sharding | Distribute data across nodes |
| Replica lag | Delay between source and replica state |
| Connection pool | Reusable database connections |
| Materialized view | Persisted query result |
| Point-in-time recovery | Recover to a time/state using backups + logs where supported |
| Idempotency | Repeating the same logical request does not create unintended duplicate effects |

### SP-level trigger words

\`\`\`text
100x data
→ indexes / partitioning / query plan

100x reads
→ cache / read replicas / pooling

100x writes
→ transaction cost / hot rows / partitioning / sharding

two concurrent requests
→ transaction / isolation / locking / MVCC

crash midway
→ atomicity / rollback / recovery

database committed then power loss
→ durability / logging / recovery

same request repeated
→ idempotency / unique constraint

duplicate data
→ normalization / constraints

query suddenly slow
→ execution plan / statistics / indexes / workload
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="common-dbms-traps"></a>

## Common DBMS Traps

### Trap 1 — ACID consistency means “latest value”

No. ACID consistency concerns preservation of database invariants. Visibility of concurrent changes is a separate isolation/consistency-model discussion.

### Trap 2 — Index means faster everything

No. Indexes can accelerate suitable reads while adding storage and write-maintenance cost.

### Trap 3 — Read replicas solve database scaling

They mainly help read scaling.

### Trap 4 — Partitioning equals sharding

They are related but different architectural techniques.

### Trap 5 — More normalization is always better

No. Workload-specific denormalization can be justified.

### Trap 6 — Serializable means no concurrency

Serializable still allows concurrent transaction processing; it constrains the result to be equivalent to a serial execution.

### Trap 7 — MVCC means no locks

MVCC does not eliminate every form of locking or coordination.

### Trap 8 — Replication replaces backup

Replication can copy corrupted or deleted data. Backups provide a different recovery capability.

### Trap 9 — Add indexes before measuring

First understand the workload and plan.

### Trap 10 — Deadlock means the database is broken

A deadlock is a concurrency conflict that can be detected and resolved by aborting one transaction, depending on the DBMS.

### Trap 11 — Connection pooling means unlimited connections

The pool reuses and limits connections. An oversized pool can still overload the database.

### Trap 12 — One architecture fits every workload

Correct design depends on read/write ratio, data size, latency, consistency requirements, failure requirements, and operational constraints.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-revision-sheet"></a>

## 30-Second Revision Sheet

\`\`\`text
DBMS
→ manages persistent data + integrity + concurrency + recovery

Primary key
→ chosen unique row identity

Foreign key
→ relationship / referential integrity

Normalization
→ reduce redundancy and anomalies

1NF
→ atomic/repeating-group cleanup

2NF
→ remove partial dependency

3NF
→ remove transitive dependency

BCNF
→ every determinant is a candidate key

Denormalization
→ intentional redundancy for workload reasons

Transaction
→ logical unit of work

ACID
→ atomicity, consistency, isolation, durability

Dirty read
→ read uncommitted change

Non-repeatable read
→ same row reads differently

Phantom read
→ matching row set changes

Lost update
→ concurrent write overwrites another change

Isolation level
→ controls concurrency behavior

Lock
→ coordinate conflicting access

Deadlock
→ transactions wait cyclically

MVCC
→ multiple row versions / visibility rules

Index
→ supported faster access path

Composite index
→ multi-column access path; order matters

Selectivity
→ how strongly a predicate narrows candidates

Execution plan
→ how the DBMS intends to execute the query

Partitioning
→ split one logical table into partitions

Replication
→ copy database state

Read replica
→ scale reads

Sharding
→ distribute data across nodes

Connection pool
→ reuse DB connections

Cache
→ reduce repeated database reads

Backup
→ recovery source

Idempotency
→ repeated logical request does not duplicate effects
\`\`\`

[Back to Table of Contents](#table-of-contents)

---

<a id="final-dbms-interview-checklist"></a>

## Final DBMS Interview Checklist

### Database fundamentals

- [ ] DBMS purpose
- [ ] relational model
- [ ] keys
- [ ] constraints
- [ ] referential integrity
- [ ] functional dependencies

### Normalization

- [ ] 1NF
- [ ] 2NF
- [ ] 3NF
- [ ] BCNF
- [ ] insert anomaly
- [ ] update anomaly
- [ ] delete anomaly
- [ ] denormalization trade-off

### Transactions

- [ ] transaction
- [ ] ACID
- [ ] atomicity
- [ ] consistency
- [ ] isolation
- [ ] durability
- [ ] commit
- [ ] rollback

### Concurrency

- [ ] dirty read
- [ ] non-repeatable read
- [ ] phantom read
- [ ] lost update
- [ ] isolation levels
- [ ] locks
- [ ] MVCC
- [ ] serializability
- [ ] deadlocks

### Indexing

- [ ] why indexes help
- [ ] index cost
- [ ] composite indexes
- [ ] column order
- [ ] selectivity
- [ ] cardinality
- [ ] clustered/non-clustered concept
- [ ] covering indexes
- [ ] optimizer choosing/not choosing an index

### Performance

- [ ] execution plans
- [ ] table scans
- [ ] join cost
- [ ] sort cost
- [ ] statistics
- [ ] slow-query troubleshooting
- [ ] measure before changing
- [ ] re-measure after changing

### Scaling

- [ ] vertical scaling
- [ ] caching
- [ ] connection pooling
- [ ] replication
- [ ] read replicas
- [ ] partitioning
- [ ] sharding
- [ ] hot partitions / hot keys
- [ ] workload isolation

### Reliability and security

- [ ] backups
- [ ] point-in-time recovery
- [ ] recovery testing
- [ ] least privilege
- [ ] parameterized queries
- [ ] encryption
- [ ] auditing
- [ ] idempotency

### System-design reasoning

- [ ] read-heavy workload
- [ ] write-heavy workload
- [ ] large table
- [ ] high-cardinality lookup
- [ ] concurrent update
- [ ] duplicate request
- [ ] database outage
- [ ] cache failure
- [ ] 100x data
- [ ] 100x traffic

### Interview execution

- [ ] Give a definition
- [ ] Explain the intuition
- [ ] Give a concrete example
- [ ] Explain the mechanism
- [ ] Mention the trade-off
- [ ] Handle a concurrency variation
- [ ] Handle a scale variation
- [ ] Connect the concept to a project only after explaining it generically

[Back to Table of Contents](#table-of-contents)
