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
- System design and engineering reasoning
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
- System design fundamentals

## Tier 3 — Final polish

- HR / behavioral
- Resume walkthrough
- Self-introduction
- Strengths / weaknesses
- Teamwork / conflict / failure examples
- Questions to ask the interviewer

> **SP/DSE calibration:** System design is important, but the immediate target is **project-driven engineering design and reasoning**, not senior-level distributed-systems depth. OOP, projects, coding, SQL/DBMS and core CS remain the higher-priority interview preparation areas.

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
LAYER 4 — System Design & Engineering Reasoning
      ↓
LAYER 5 — CS-Core Integration
      ↓
LAYER 6 — DSA + SQL Interview Readiness
      ↓
LAYER 7 — Mock Interview Readiness
      ↓
LAYER 8 — Final Interview Mode
```

You can spend several days or several weeks in a layer. The interview date does not change the structure.

> **Important:** The layers are not strict silos. SQL, DSA and coding continue in parallel while you deepen OOP and projects. The layer number indicates the dominant interview objective, not a requirement to stop the other tracks.

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
- Error handling boundaries
- Testability

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

## Layer-2 mini design exercises

Practice small designs before full system design:

- Payment method interface
- Notification service
- File storage abstraction
- Image provider interface
- URL service / repository split

The purpose is to make OOP concepts visible in code and architecture.

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

# 8. Layer 4 — System Design & Engineering Reasoning

## Goal

Learn to design a reasonable backend system from requirements and explain the trade-offs clearly.

This is the **SP-level system-design target** for this roadmap: practical architecture, project-based reasoning, scalability basics, failure handling and trade-offs. It is **not** a senior distributed-systems curriculum.

## A. Standard design sequence

For every design problem, follow this order:

```text
1. Clarify requirements
        ↓
2. Identify users / actors
        ↓
3. Functional requirements
        ↓
4. Non-functional requirements
        ↓
5. Estimate scale (roughly)
        ↓
6. Define APIs / interfaces
        ↓
7. Choose data model + storage
        ↓
8. Draw major components + data flow
        ↓
9. Identify bottlenecks
        ↓
10. Add caching / queues / workers only when justified
        ↓
11. Discuss failure cases
        ↓
12. Explain trade-offs and alternatives
```

Do not jump directly to Redis, Kafka, sharding or microservices.

## B. Core concepts to understand

### Architecture

- Client / API / service / repository responsibilities
- Monolith vs modular monolith vs microservices
- Stateless services
- Horizontal vs vertical scaling
- Load balancing
- Reverse proxy

### Storage

- SQL vs NoSQL at a high level
- Source of truth
- Indexes
- Read-heavy vs write-heavy workloads
- Transactions
- Basic replication concepts

### Performance

- Latency vs throughput
- Caching
- Cache-aside
- Cache invalidation basics
- Hot keys
- Pagination
- Connection pooling

### Asynchronous systems

- Why queues exist
- Producer / consumer model
- Background workers
- Retries
- Backoff
- Idempotency
- Duplicate delivery

### Reliability

- Timeouts
- Retries
- Graceful degradation
- Circuit-breaker concept
- Health checks
- Failure isolation
- Observability basics: logs, metrics, traces

### API design

- Resource-oriented REST basics
- Status codes
- Idempotent operations
- Pagination
- Validation
- Authentication / authorization boundaries

## C. Project-first design exercises

Master these in this order:

### 1. URL Shortener

Already partially covered in Layer 3. Now redesign it from requirements upward.

Be able to explain:

```text
requirements
→ API
→ Base62 generation
→ DB schema
→ cache
→ redirect path
→ rate limit
→ click analytics
→ hot key handling
→ scaling
→ failure recovery
```

### 2. SceneFlow processing system

Design the system for:

```text
script upload
→ scene extraction
→ semantic processing
→ external asset search
→ ranking
→ result persistence
```

Explain:

- Why synchronous processing would be problematic.
- Why workers / queues help.
- How to retry external API failures.
- How to avoid duplicate jobs.
- How to handle partial failure.
- How to scale workers independently from the API.

### 3. Rate limiter

Know at least:

- Fixed window
- Sliding window concept
- Token bucket concept
- Redis-based implementation at a high level
- Trade-offs between algorithms

### 4. Notification service

Be able to design:

```text
API
→ queue
→ worker
→ provider
→ retry / failure handling
```

### 5. File / image processing system

Understand when to use:

- object storage
- metadata DB
- asynchronous workers
- status tracking
- retries

### 6. Search / semantic retrieval system

Tie the design back to Qdrant / embeddings / metadata storage in SceneFlow.

## D. Scaling checklist

When asked “How would you scale it?”, reason through:

```text
1. Is the API stateless?
2. Can we add API replicas?
3. Where is the hottest path?
4. Can caching remove repeated reads?
5. Can heavy work move to workers?
6. What is the DB bottleneck?
7. Which indexes help?
8. Is one key / tenant / item unusually hot?
9. What can fail independently?
10. What trade-off are we making?
```

## E. Failure-mode checklist

For any design, ask:

- What if the DB is unavailable?
- What if Redis is unavailable?
- What if an external API times out?
- What if the same request arrives twice?
- What if a worker crashes halfway through a job?
- What if traffic spikes suddenly?
- What if one resource becomes a hot key?
- What data can be stale?
- What must never be lost?

## F. Trade-off vocabulary

Use explicit engineering language:

- consistency vs availability
- latency vs throughput
- simplicity vs scalability
- synchronous vs asynchronous
- strong consistency vs eventual consistency
- cost vs performance
- reliability vs complexity

Do not force a trade-off into an answer when it does not actually matter.

## G. OOP ↔ system design connection

This layer must reinforce Layer 2 rather than become a separate memorization subject.

Examples:

- Controller/router → service → repository separation
- Provider abstraction
- Dependency injection
- Interfaces / protocols
- Composition over inheritance
- Encapsulation of infrastructure details
- Testable business logic

## H. System design interview exercises

Practice verbally before writing code.

Start with:

1. URL Shortener
2. Rate limiter
3. Notification service
4. Background job / task processing system
5. File upload + processing system
6. Image / semantic search service

For each exercise, aim to produce:

```text
2-minute requirements discussion
+
5–8 minute architecture discussion
+
3–5 minute bottleneck / failure / trade-off discussion
```

## Layer-4 readiness gate

You are ready when you can take an unfamiliar but reasonable backend design problem and, without memorized diagrams:

- ask useful requirement questions,
- identify the main components,
- choose a reasonable data store,
- define a basic API/data flow,
- identify at least two bottlenecks,
- explain caching / queue decisions,
- discuss two failure cases,
- state at least one trade-off,
- connect the design to OOP / CS fundamentals.

## What NOT to prioritize yet

Do not spend major preparation time on:

- deep consensus algorithms
- Raft / Paxos internals
- advanced distributed databases
- multi-region active-active architecture
- complex service-mesh internals
- deep Kafka implementation internals
- advanced sharding strategies
- senior-level capacity planning

These can be added later only if the interview evidence or interviewer feedback calls for them.

---

# 9. Layer 5 — CS-Core Integration

The goal here is not to study each subject independently. Tie each concept back to your projects and system-design reasoning.

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
- How does a database bottleneck affect the system design?

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
- What happens when a worker crashes?

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
- Why latency matters in a redirect service

---

# 10. Layer 6 — DSA + SQL Interview Readiness

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

# 11. Layer 7 — Mock Interview Readiness

Do not start full mocks too early.

Start when Layers 1–6 are reasonably stable.

## Mock structure

### Round A — OOP

5–10 questions.

At least two follow-up chains.

### Round B — Project

One deep SceneFlow discussion.

One deep URL Shortener discussion.

### Round C — System Design

One project redesign or standard backend design.

Must include requirements, architecture, bottlenecks and trade-offs.

### Round D — CS Core

Mix DBMS, SQL, OS and CN.

### Round E — Coding

One problem solved while explaining the reasoning aloud.

### Round F — Behavioral

Self-introduction + project ownership + failure + teamwork + learning.

## Mock scoring

Score each area from 1–5:

- Concept accuracy
- Communication clarity
- Project depth
- Design reasoning
- Coding ability
- SQL accuracy
- CS-core recall
- Handling follow-ups

Any repeated score of **2 or below** becomes the next study target.

---

# 12. Layer 8 — Final Interview Mode

Activate this layer once the interview is scheduled or appears likely within a short window.

Reduce learning of new material.

Increase:

- Active recall
- Mock interviews
- Project explanation
- System-design verbal practice
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
- How you would scale it

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
- Failure handling

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

### System Design

- Requirements first
- API + data model
- Components and data flow
- Cache / queue decisions
- Bottlenecks
- Failure cases
- Trade-offs

---

# 13. Daily Study Template — Date Independent

Use this template regardless of the interview date.

## Block A — Main depth topic

60–120 minutes

Current primary focus:

- OOP / Python OOP
- System design
- Project mastery

## Block B — SQL / DBMS

30–60 minutes

- Write queries
- Review one DBMS topic
- Connect it to a project

## Block C — DSA

60–120 minutes

- Problem solving
- Timed practice
- Explain solution aloud

## Block D — CS Core / project follow-up

30–60 minutes

Rotate:

- OS
- CN
- Backend
- Project questions
- System-design exercise

## Block E — Active recall

15–30 minutes

Without notes:

- Explain one OOP topic
- Explain one project component
- Explain one CS concept
- Recall one SQL pattern
- Explain one DSA solution

---

# 14. Rules for Efficient Preparation

## Rule 1 — Do not memorize isolated answers

Understand the concept and connect it to a project.

## Rule 2 — Projects are the bridge

A project question can become:

```text
Project
→ OOP
→ DBMS
→ OS
→ CN
→ Backend
→ System design
→ DSA
```

## Rule 3 — Use layered revision

Review older layers through active recall while studying the current layer.

## Rule 4 — Prefer depth over breadth

It is better to explain five technologies deeply than twenty technologies superficially.

## Rule 5 — Always discuss trade-offs

Especially for architecture, databases, caches, queues and concurrency.

## Rule 6 — Never bluff

For unknown questions, explain what you know, state assumptions, and reason from fundamentals.

## Rule 7 — Coding communication matters

Do not silently solve DSA. Practice explaining your thinking.

## Rule 8 — System design should stay proportional

System design supports the interview; it should not consume the time needed for OOP, projects, DSA and SQL/DBMS.

---

# 15. Master Readiness Checklist

Before considering yourself interview-ready, verify:

### OOP

- [ ] Four pillars explained clearly
- [ ] Python OOP strong
- [ ] Major comparisons strong
- [ ] SOLID understood
- [ ] Can connect OOP to projects

### Projects

- [ ] SceneFlow explained in 60 seconds
- [ ] SceneFlow explained in 5–10 minutes
- [ ] URL Shortener explained in 60 seconds
- [ ] URL Shortener explained in 5–10 minutes
- [ ] Can answer repeated follow-ups
- [ ] Can explain limitations honestly

### System Design

- [ ] Can clarify requirements
- [ ] Can identify functional / non-functional requirements
- [ ] Can draw component architecture
- [ ] Can define basic APIs
- [ ] Can choose storage and explain why
- [ ] Understand caching
- [ ] Understand queues / workers
- [ ] Understand idempotency / retries
- [ ] Can identify bottlenecks
- [ ] Can discuss failure cases
- [ ] Can explain trade-offs
- [ ] Can redesign URL Shortener from scratch
- [ ] Can design one unfamiliar backend system verbally

### SQL / DBMS

- [ ] JOINs
- [ ] GROUP BY / HAVING
- [ ] Aggregation
- [ ] Window functions
- [ ] Subqueries
- [ ] CTEs
- [ ] Keys / normalization
- [ ] Indexes
- [ ] ACID / transactions
- [ ] Concurrency basics

### OS / CN

- [ ] Process / thread
- [ ] Synchronization
- [ ] Deadlock
- [ ] Memory basics
- [ ] HTTP / HTTPS
- [ ] DNS
- [ ] TCP
- [ ] REST
- [ ] CORS

### DSA

- [ ] Can identify common patterns
- [ ] Can solve under time pressure
- [ ] Can explain complexity
- [ ] Can handle follow-up variations

### Interview communication

- [ ] Strong self-introduction
- [ ] Resume walkthrough
- [ ] Project ownership story
- [ ] Failure story
- [ ] Teamwork story
- [ ] Can say “I don't know” professionally and reason forward

---

# 16. Final Mental Model

The complete preparation loop is:

```text
OOP
 ↓
Design thinking
 ↓
Projects
 ↓
System design
 ↓
CS-core connections
 ↓
DSA + SQL
 ↓
Mocks
 ↓
Active recall
 ↓
Interview
```

The goal is not to know everything.

The goal is to make the following chain natural:

```text
“What?”
   ↓
“Why?”
   ↓
“How?”
   ↓
“What can go wrong?”
   ↓
“How would you improve it?”
```

That is the reasoning pattern the roadmap is designed to build.
