# Infosys SP/DSE Interview — Layered Preparation Roadmap

> **Purpose:** Prepare for the Infosys SP/DSE technical interview without depending on a fixed interview date.
>
> **Strategy:** Build depth in layers. Do not rush into a day-wise schedule while the interview date is uncertain. Move to the next layer only when the current layer can be recalled and explained independently.

---

## 1. Core Objective

The target is not simply to memorize interview answers.

The target is to be able to:

```text
Question
  ↓
Concept
  ↓
Clear explanation
  ↓
Simple example
  ↓
Project application
  ↓
Trade-off / why
  ↓
Follow-up question
  ↓
Engineering reasoning
```

The preparation must support both **normal CS interview questions** and **project-driven follow-ups**.

Primary projects for deep preparation:

1. **SceneFlow — Semantic Visual Asset Generator**
2. **URL Shortener**

Parallel preparation remains active for:

- DSA / coding interview
- SQL
- DBMS
- Operating Systems
- Computer Networks
- Backend/software engineering fundamentals
- Basic system design
- HR / behavioral questions

---

# 2. Priority Model

## Tier 1 — Deep mastery

### OOP + Python OOP

This is the main interview study area.

### Projects

SceneFlow + URL Shortener should be prepared deeply enough to survive repeated interviewer follow-ups.

### SQL + DBMS

Continue practical SQL and DBMS theory in parallel.

### DSA

Continue coding practice and, importantly, learn to explain the approach and complexity verbally.

## Tier 2 — Strong interview readiness

- Operating Systems
- Computer Networks
- Backend fundamentals
- REST / HTTP
- Caching
- Concurrency
- Authentication / authorization concepts
- Docker / deployment basics

## Tier 3 — Final polish

- HR / behavioral
- Resume walkthrough
- Self-introduction
- Strengths / weaknesses
- Teamwork / conflict / failure examples
- Questions to ask the interviewer

---

# 3. Layered Preparation System

The layers are deliberately independent of calendar dates.

```text
LAYER 0 — Baseline
      ↓
LAYER 1 — OOP Core
      ↓
LAYER 2 — Python OOP + Design Thinking
      ↓
LAYER 3 — Project Mastery
      ↓
LAYER 4 — CS-Core Integration
      ↓
LAYER 5 — DSA + SQL Interview Readiness
      ↓
LAYER 6 — Mock Interview Readiness
      ↓
LAYER 7 — Final Interview Mode
```

You can spend several days or several weeks in a layer. The interview date does not change the structure.

---

# 4. Layer 0 — Baseline and Resume Control

## Goal

Know exactly what appears on your resume and GitHub, and never claim a feature you did not implement.

## Checklist

- Know your resume line by line.
- Know the technologies listed under each project.
- Know your exact contribution.
- Know the main architecture of SceneFlow.
- Know the main architecture of URL Shortener.
- Know important limitations honestly.
- Know which parts are implemented, mocked, planned, or incomplete.

## Readiness test

Without opening the repository, explain each project in 60 seconds.

Then explain each one again in 2–3 minutes using architecture, data flow, design choices and trade-offs.

---

# 5. Layer 1 — OOP Core

## Goal

Build strong textbook-level OOP understanding before using projects to deepen it.

## A. Fundamentals

- Class
- Object
- Constructor
- Instance variable
- Class variable
- Instance method
- Class method
- Static method
- `self`
- `__init__`

## B. Four pillars

### Encapsulation

Know:

- Definition
- Why it exists
- Example
- Benefits
- Limitations / trade-offs
- How Python approaches it

### Abstraction

Know:

- Definition
- Why it exists
- Abstract interface vs implementation details
- Python mechanisms

### Inheritance

Know:

- Is-a relationship
- Single / multiple / multilevel inheritance
- Reuse vs coupling
- `super()`
- MRO

### Polymorphism

Know:

- Same interface, different behavior
- Overriding
- Duck typing
- Dynamic dispatch
- Real-world example

## C. High-frequency distinctions

Be able to compare:

- Overloading vs overriding
- Abstraction vs encapsulation
- Interface vs abstract class
- Composition vs inheritance
- Association vs aggregation vs composition
- Static vs dynamic binding
- Class method vs static method vs instance method
- `is` vs `==`

## D. Python-specific OOP

Prepare:

- Method overriding
- Multiple inheritance
- MRO
- `super()`
- `@property`
- `@classmethod`
- `@staticmethod`
- Abstract Base Classes
- Duck typing
- Magic / dunder methods
- `__new__` vs `__init__`
- Object identity and equality
- Mutable vs immutable objects
- Shallow vs deep copy

## Core OOP question bank

1. What is OOP?
2. Why use OOP?
3. What are the four pillars?
4. Explain encapsulation with an example.
5. Explain abstraction with an example.
6. Explain inheritance and its types.
7. Explain polymorphism with an example.
8. Overloading vs overriding.
9. Abstraction vs encapsulation.
10. Interface vs abstract class.
11. Composition vs inheritance.
12. What is dynamic dispatch?
13. What is MRO in Python?
14. What does `super()` do?
15. Does Python support method overloading?
16. What is duck typing?
17. Why use private/protected-style fields?
18. What is a class method?
19. Static method vs class method.
20. Give a real-world polymorphism example.

## Layer-1 readiness gate

You are ready when you can answer the core questions **without reading notes**, in your own words, in under 60–90 seconds each.

---

# 6. Layer 2 — Python OOP + Design Thinking

## Goal

Move from definitions to design reasoning.

## Topics

- High cohesion
- Low coupling
- Separation of concerns
- Composition over inheritance
- Dependency injection
- SOLID basics
- Single Responsibility Principle
- Open/Closed Principle
- Liskov Substitution Principle
- Interface Segregation Principle
- Dependency Inversion Principle
- Repository/service separation
- Data models vs schemas
- Business logic isolation

## Question pattern

For every design concept, answer:

```text
What is it?
Why do we need it?
What problem does it solve?
What is a simple example?
Where could it appear in my project?
What happens if we ignore it?
What is the trade-off?
```

---

# 7. Layer 3 — Project Mastery

# A. SceneFlow

## What the project is

SceneFlow is a semantic visual asset generator that transforms scripts into structured visual storyboards and retrieves relevant visual assets using NLP / embeddings and multiple external providers.

## Architecture to memorize

```text
React + TypeScript
        ↓
      FastAPI
        ↓
PostgreSQL / Redis / Qdrant
        ↓
      Celery
        ↓
External APIs + Gemini
```

## Technologies

- React
- TypeScript
- Tailwind CSS
- FastAPI
- Pydantic
- SQLAlchemy
- Alembic
- PostgreSQL
- Redis
- Qdrant
- Celery
- Gemini
- Sentence Transformers
- Docker

## Explain the request flow

Be able to walk through:

```text
User submits script
      ↓
API receives request
      ↓
Script / scenes are persisted
      ↓
Scene segmentation / semantic analysis
      ↓
Search jobs are created
      ↓
Celery handles long-running work
      ↓
External providers are queried
      ↓
Embeddings / semantic retrieval
      ↓
Ranking / reranking
      ↓
Results persisted
      ↓
Frontend displays selected assets
```

## SceneFlow OOP questions

- Where is abstraction useful in SceneFlow?
- Why separate API routes from business logic?
- Why separate services from repositories?
- Where could polymorphism be useful for multiple image providers?
- How would you design a common provider interface?
- Why is composition preferable in some parts of the system?
- Where is encapsulation useful?
- How would you test provider implementations independently?

## SceneFlow backend questions

- Why FastAPI?
- Why Celery?
- Why Redis?
- Why PostgreSQL?
- Why Qdrant?
- Why use both PostgreSQL and Qdrant?
- Why use asynchronous/background processing?
- What if a Celery task runs twice?
- How do you prevent duplicate processing?
- What happens if an external image API fails?
- What happens if Gemini fails?
- How would you retry safely?
- How would you make the pipeline idempotent?

## SceneFlow AI questions

- What is an embedding?
- What is semantic search?
- Keyword search vs semantic search.
- Why vector database?
- What is cosine similarity?
- Why reranking?
- Why combine multiple providers?
- What are the limitations of embedding search?

## SceneFlow honesty checkpoint

Do not claim features as production-complete if they were not fully implemented or verified.

Especially distinguish implemented behavior from planned production hardening such as real authentication, observability and reliability improvements.

---

# B. URL Shortener

## What the project is

A production-oriented URL shortener built with FastAPI, PostgreSQL, Redis and React.

## Features to know

- 7-character Base62 short codes
- Custom aliases
- Optional expiration
- Redirect handling
- Redis cache-aside caching
- PostgreSQL source of truth
- Atomic click tracking
- Redis rate limiting
- Analytics endpoint
- Docker Compose
- Alembic
- Backend tests
- Railway deployment

## Architecture to memorize

```text
React SPA
   ↓
FastAPI Router
   ↓
URLService
   ↓
URLRepository
   ↓
PostgreSQL

Redis → cache + rate limiting
```

## Critical redirect flow

```text
GET /{short_code}
        ↓
Check Redis
   ↙         ↘
Hit          Miss
 ↓             ↓
URL data   PostgreSQL
   ↘         ↙
   Redirect
      ↓
Atomic click increment
```

## URL Shortener OOP questions

- Why separate Router, Service and Repository?
- What is the benefit of the service layer?
- What is the benefit of the repository layer?
- How does this reduce coupling?
- How would you replace PostgreSQL without changing business logic?
- How would you replace Redis?
- How could abstraction help here?
- Where is dependency injection useful?

## DBMS questions

- Why PostgreSQL as source of truth?
- What constraints protect the short code?
- How does uniqueness prevent collisions?
- Why use an atomic SQL update for clicks?
- What race condition are you avoiding?
- What indexes would you create?
- What transaction boundaries matter?

## Redis / systems questions

- Why Redis for redirects?
- What is cache-aside?
- What happens on a cache miss?
- What happens if Redis goes down?
- What is rate limiting?
- Why fixed-window rate limiting?
- What are its limitations?
- How would you improve it for high traffic?

## Networking questions

- What happens when a user opens a short URL?
- DNS role
- TCP / TLS role
- HTTP request / response
- 307 redirect
- HTTPS
- Reverse proxy / Nginx

## System design follow-ups

- How would you handle millions of redirects?
- How would you scale the API?
- How would you scale Redis?
- How would you avoid a hot key?
- What happens if a single URL receives extremely high traffic?
- Should click counting remain synchronous?
- When would you introduce asynchronous event processing?

---

# 8. Layer 4 — CS-Core Integration

The goal here is not to study each subject independently. Tie each concept back to your projects.

## DBMS / SQL

### Core theory

- Database vs DBMS
- Relational database
- Keys
- Normalization
- Denormalization
- Transactions
- ACID
- Constraints
- Indexes
- Joins
- GROUP BY / HAVING
- Window functions
- Subqueries
- CTE basics
- Transactions / concurrency

### Project-linked questions

- SceneFlow database design
- URL Shortener database design
- Why PostgreSQL?
- What indexes are useful?
- What happens under concurrent writes?
- Why is PostgreSQL the source of truth?

### SQL practice

Continue joins first, then return to deeper subquery patterns.

Priority order:

```text
JOINs
 ↓
GROUP BY / HAVING
 ↓
Aggregations
 ↓
Window functions
 ↓
Subqueries
 ↓
CTEs
 ↓
Anti-joins / self joins
```

## Operating Systems

Focus on:

- Process vs thread
- Context switch
- CPU scheduling
- Synchronization
- Race condition
- Mutex vs semaphore
- Deadlock
- Virtual memory
- Paging
- Page fault
- Stack vs heap

Project-linked questions:

- Why background workers?
- What does concurrency mean for your API?
- What happens when many requests arrive together?
- Why are worker processes useful?

## Computer Networks

Focus on:

- OSI / TCP-IP basics
- HTTP / HTTPS
- TCP vs UDP
- DNS
- TCP handshake
- TLS basics
- REST
- Status codes
- Headers
- Cookies / tokens
- CORS
- Reverse proxy

Project-linked questions:

- What happens when a URL Shortener redirect is requested?
- Frontend → FastAPI communication
- CORS in SceneFlow
- API deployment

---

# 9. Layer 5 — DSA + SQL Interview Readiness

## DSA objective

The coding track remains separate from OOP study, but interview readiness requires explanation.

For every solved problem be able to state:

```text
Brute force
↓
Why it fails
↓
Pattern
↓
Optimized idea
↓
Data structure
↓
Complexity
↓
Edge cases
```

## DSA priority

1. DP / state DP
2. Greedy
3. Arrays / hashing
4. Binary search
5. Heap
6. Trees
7. Graphs
8. Sliding window / two pointers
9. Interval / partition DP
10. Number theory / optimization

## SQL readiness

For each query:

```text
Understand tables
↓
Understand desired rows
↓
Choose JOIN / GROUP / window / subquery
↓
Write query
↓
Check duplicates
↓
Explain complexity / indexing intuition when relevant
```

---

# 10. Layer 6 — Mock Interview Readiness

Do not start full mocks too early.

Start when Layers 1–5 are reasonably stable.

## Mock structure

### Round A — OOP

5–10 questions.

At least two follow-up chains.

### Round B — Project

One deep SceneFlow discussion.

One deep URL Shortener discussion.

### Round C — CS Core

Mix DBMS, SQL, OS and CN.

### Round D — Coding

One problem solved while explaining the reasoning aloud.

### Round E — Behavioral

Self-introduction + project ownership + failure + teamwork + learning.

---

# 11. Layer 7 — Final Interview Mode

Activate this layer once the interview is scheduled or appears likely within a short window.

Reduce learning of new material.

Increase:

- Active recall
- Mock interviews
- Project explanation
- SQL query writing
- DSA explanation
- Rapid OOP revision
- OS/CN rapid recall
- Resume walkthrough

## Final 24–48 hour goals

You should be able to explain without notes:

### OOP

- Four pillars
- Major comparisons
- Python-specific OOP
- Composition vs inheritance
- SOLID basics

### SceneFlow

- Problem
- Architecture
- Full data flow
- Why each major technology
- Hardest problem
- Concurrency / Celery
- Vector search
- Failure cases
- Limitations

### URL Shortener

- Problem
- Architecture
- Base62
- Cache-aside
- Redis
- Rate limiting
- Atomic click count
- Database design
- Scaling

### SQL / DBMS

- Joins
- Aggregation
- Window functions
- Keys
- Normalization
- ACID
- Indexes
- Transactions

### OS / CN

- Process vs thread
- Race condition
- Deadlock
- Mutex / semaphore
- HTTP / HTTPS
- DNS
- TCP
- REST / status codes

---

# 12. Daily Study Template — Date Independent

Use this template regardless of whether the interview is 7 days or 30 days away.

## Block 1 — OOP

**60–90 min**

Learn one concept deeply.

Structure:

```text
Definition
Example
Difference
Python implementation
Project application
Follow-up
```

## Block 2 — Project

**45–60 min**

Alternate SceneFlow and URL Shortener.

One day = architecture.

Next = code/design.

Next = CS-core questions.

Next = mock explanation.

## Block 3 — SQL / DBMS

**60–90 min**

Continue current SQL progression and DBMS recall.

## Block 4 — DSA

**2–4 hours**

Continue your existing coding roadmap.

At least some problems should be solved completely without AI.

## Block 5 — OS / CN / Backend

**30–60 min**

One focused concept group.

## Block 6 — Oral recall

**15–30 min**

Close all notes and explain what you studied aloud.

---

# 13. Weekly Review Gate

At the end of each study cycle, ask:

### OOP

Can I explain the concept without memorization?

### Project

Can I defend why I chose the technology?

### DBMS

Can I solve a query from a blank editor?

### DSA

Can I explain the approach without code?

### OS/CN

Can I explain the mechanism rather than only the definition?

### Communication

Can I explain all of this in simple, structured English?

If the answer is "no", stay in the layer.

---

# 14. How We Should Use AI During This Preparation

AI should be used primarily as an **interviewer, reviewer and explainer**, not as the first source of a coding solution.

For DSA:

```text
Attempt yourself
 ↓
Only then ask for a hint if necessary
 ↓
Re-derive
 ↓
Implement independently
```

For interview topics:

```text
Try answer yourself
 ↓
Receive feedback
 ↓
Fix gaps
 ↓
Answer again without notes
```

For projects:

```text
Explain from memory
 ↓
Compare with repository
 ↓
Find inaccuracies
 ↓
Correct explanation
 ↓
Practice follow-ups
```

---

# 15. Interview Answer Standard

A strong answer usually follows:

```text
1. Direct definition / answer
2. Why it matters
3. Small example
4. Project connection when relevant
5. Trade-off / limitation if relevant
```

Avoid:

- Long memorized paragraphs
- Unnecessary jargon
- Claiming implementation you did not do
- Giving a tool name without explaining why it was chosen
- Saying "because it is faster" without explaining what changed

---

# 16. Progress Tracker

Update this section manually.

## OOP

- [ ] OOP fundamentals
- [ ] Four pillars
- [ ] OOP comparisons
- [ ] Python OOP
- [ ] MRO / `super()`
- [ ] Duck typing
- [ ] Abstract classes
- [ ] Composition / aggregation
- [ ] SOLID basics
- [ ] OOP mock

## SceneFlow

- [ ] 30-second explanation
- [ ] 2-minute explanation
- [ ] Full architecture
- [ ] Request flow
- [ ] Database design
- [ ] Celery / Redis
- [ ] Qdrant / embeddings
- [ ] Gemini / segmentation
- [ ] Failure handling
- [ ] Idempotency
- [ ] Production limitations
- [ ] Deep mock

## URL Shortener

- [ ] 30-second explanation
- [ ] 2-minute explanation
- [ ] Architecture
- [ ] Base62
- [ ] PostgreSQL design
- [ ] Redis cache-aside
- [ ] Rate limiting
- [ ] Atomic click updates
- [ ] Concurrency
- [ ] HTTP redirect flow
- [ ] Scaling discussion
- [ ] Deep mock

## SQL / DBMS

- [ ] Joins
- [ ] Aggregation
- [ ] HAVING
- [ ] Window functions
- [ ] Subqueries
- [ ] CTEs
- [ ] Keys
- [ ] Normalization
- [ ] ACID
- [ ] Indexes
- [ ] Transactions

## OS / CN

- [ ] Process / thread
- [ ] Scheduling
- [ ] Synchronization
- [ ] Deadlocks
- [ ] Virtual memory
- [ ] HTTP / HTTPS
- [ ] DNS
- [ ] TCP
- [ ] REST
- [ ] CORS

## DSA

- [ ] Arrays / hashing
- [ ] Binary search
- [ ] Sliding window
- [ ] Stack / heap
- [ ] Greedy
- [ ] DP
- [ ] Trees
- [ ] Graphs
- [ ] Hard / mixed problems
- [ ] Interview explanation practice

---

# 17. Final Principle

Do not measure preparation by the number of questions read.

Measure it by what you can **produce without notes**.

```text
Read
 ↓
Understand
 ↓
Recall
 ↓
Explain
 ↓
Apply to project
 ↓
Defend with follow-ups
 ↓
Perform under pressure
```

The interview date may move.

This roadmap does not need to move.

We simply move through the layers more deeply until the interview is scheduled, then switch from **learning mode → performance mode**.
