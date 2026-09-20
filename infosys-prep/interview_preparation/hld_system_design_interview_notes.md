# HLD System Design Interview Notes — Infosys DSE / SP

This file is the dedicated **High-Level Design (HLD)** preparation reference.

It is intentionally separate from **LLD (Low-Level Design)**. LLD will be handled later with classes, interfaces, design patterns, SOLID, object collaboration, and code-level design.

## What This File Is For

HLD is about deciding **how a system should be structured at the component level** so it can satisfy requirements and scale.

The core questions are:

- What components do we need?
- How do components communicate?
- Where does data live?
- How do we scale?
- What happens when a component fails?
- What consistency and availability guarantees do we need?
- Where do caching, queues, replication, partitioning, and load balancing help?
- What trade-off are we accepting with each decision?

A good HLD answer is not a collection of technologies. It is a chain of justified decisions.

## Infosys Interview Relevance

Recent candidate reports show that system-design depth varies by interviewer and resume. Some reports describe basic scaling/load-balancing discussions, while others report explicit HLD questions such as designing a ticket-booking system with atomic seat selection, scaling a RAG pipeline, or broader architecture discussions. System design should therefore be prepared as a **discussion skill**, not as a guaranteed fixed question list. citeturn840250reddit57turn840250reddit59turn840250reddit50

The practical target for Infosys DSE / SP preparation is:

1. Explain common distributed-system components clearly.
2. Design a familiar system end to end.
3. Defend each major architectural decision.
4. Compare similar choices and explain when the alternative is better.
5. Adapt the same reasoning process to an unfamiliar problem.

---

<a id="table-of-contents"></a>

## Table of Contents

### 1. HLD Foundations
- [How to Use These Notes](#how-to-use-these-notes)
- [What HLD Actually Means](#what-hld-actually-means)
- [HLD vs LLD](#hld-vs-lld)
- [The HLD Interview Mindset](#the-hld-interview-mindset)
- [The Core Design Loop](#the-core-design-loop)
- [Functional vs Non-Functional Requirements](#functional-vs-non-functional-requirements)
- [Scale Estimation and Back-of-the-Envelope Calculations](#scale-estimation-and-back-of-the-envelope-calculations)
- [Latency, Throughput, Availability, Reliability and Durability](#latency-throughput-availability-reliability-and-durability)
- [CAP Theorem](#cap-theorem)
- [Consistency Models](#consistency-models)

### 2. Core Architecture
- [Client, API Gateway and Backend Services](#client-api-gateway-and-backend-services)
- [Monolith vs Modular Monolith vs Microservices](#monolith-vs-modular-monolith-vs-microservices)
- [Synchronous vs Asynchronous Communication](#synchronous-vs-asynchronous-communication)
- [Stateless vs Stateful Services](#stateless-vs-stateful-services)
- [Horizontal vs Vertical Scaling](#horizontal-vs-vertical-scaling)
- [Load Balancer](#load-balancer)
- [Load Balancing Algorithms](#load-balancing-algorithms)
- [Layer 4 vs Layer 7 Load Balancing](#layer-4-vs-layer-7-load-balancing)
- [Reverse Proxy](#reverse-proxy)
- [API Gateway](#api-gateway)
- [Service Discovery](#service-discovery)
- [Health Checks and Failover](#health-checks-and-failover)

### 3. Data and Storage
- [Database Selection Framework](#database-selection-framework)
- [SQL vs NoSQL](#sql-vs-nosql)
- [Relational Databases](#relational-databases)
- [Document Databases](#document-databases)
- [Key-Value Stores](#key-value-stores)
- [Wide-Column Stores](#wide-column-stores)
- [Graph Databases](#graph-databases)
- [Object Storage](#object-storage)
- [Indexes](#indexes)
- [Read Replicas](#read-replicas)
- [Database Replication](#database-replication)
- [Sharding and Partitioning](#sharding-and-partitioning)
- [Consistent Hashing](#consistent-hashing)
- [Transactions and Distributed Transactions](#transactions-and-distributed-transactions)

### 4. Caching
- [What Caching Solves](#what-caching-solves)
- [Redis](#redis)
- [Cache-Aside Pattern](#cache-aside-pattern)
- [Read-Through and Write-Through Caching](#read-through-and-write-through-caching)
- [Write-Back and Write-Around Caching](#write-back-and-write-around-caching)
- [Cache Eviction Policies](#cache-eviction-policies)
- [Cache Invalidation](#cache-invalidation)
- [Cache Stampede and Hot Keys](#cache-stampede-and-hot-keys)
- [CDN](#cdn)

### 5. Messaging and Event-Driven Systems
- [Why Use a Queue](#why-use-a-queue)
- [Message Broker](#message-broker)
- [RabbitMQ](#rabbitmq)
- [Kafka](#kafka)
- [Kafka vs RabbitMQ](#kafka-vs-rabbitmq)
- [Pub-Sub](#pub-sub)
- [Consumer Groups](#consumer-groups)
- [Delivery Semantics](#delivery-semantics)
- [Retries, Dead-Letter Queues and Poison Messages](#retries-dead-letter-queues-and-poison-messages)
- [Ordering and Partitioning](#ordering-and-partitioning)
- [Backpressure](#backpressure)
- [Eventual Consistency with Events](#eventual-consistency-with-events)
- [Outbox Pattern](#outbox-pattern)

### 6. Reliability and Distributed-System Patterns
- [Timeouts](#timeouts)
- [Retries and Exponential Backoff](#retries-and-exponential-backoff)
- [Circuit Breaker](#circuit-breaker)
- [Bulkhead Isolation](#bulkhead-isolation)
- [Rate Limiting](#rate-limiting)
- [Idempotency](#idempotency)
- [Distributed Locks](#distributed-locks)
- [Leader Election](#leader-election)
- [Heartbeat and Failure Detection](#heartbeat-and-failure-detection)
- [Single Point of Failure](#single-point-of-failure)
- [Graceful Degradation](#graceful-degradation)

### 7. Traffic and Data Scaling
- [Read-Heavy vs Write-Heavy Systems](#read-heavy-vs-write-heavy-systems)
- [Hotspots and Hot Partitions](#hotspots-and-hot-partitions)
- [Pagination](#pagination)
- [Batching](#batching)
- [Asynchronous Processing](#asynchronous-processing)
- [Fan-Out on Read vs Fan-Out on Write](#fan-out-on-read-vs-fan-out-on-write)
- [CQRS](#cqrs)
- [Materialized Views](#materialized-views)
- [Data Denormalization](#data-denormalization)

### 8. Networking Pieces Used in HLD
- [DNS in System Design](#dns-in-system-design)
- [TLS Termination](#tls-termination)
- [Connection Pooling](#connection-pooling)
- [WebSockets](#websockets)
- [Long Polling](#long-polling)
- [Polling](#polling)
- [CDN and Edge Delivery](#cdn-and-edge-delivery)

### 9. Security and Identity
- [Authentication Architecture](#authentication-architecture)
- [Authorization](#authorization)
- [Session-Based vs Token-Based Authentication](#session-based-vs-token-based-authentication)
- [OAuth 2.0 and OpenID Connect](#oauth-20-and-openid-connect)
- [API Keys and Service Credentials](#api-keys-and-service-credentials)
- [Secrets Management](#secrets-management)
- [Encryption at Rest and in Transit](#encryption-at-rest-and-in-transit)

### 10. Observability
- [Logging](#logging)
- [Metrics](#metrics)
- [Tracing](#tracing)
- [SLO, SLA and SLI](#slo-sla-and-sli)
- [Alerting](#alerting)

### 11. Component Trade-Off Matrix
- [Load Balancer Choices](#load-balancer-choices)
- [Database Choices](#database-choices)
- [Cache Choices](#cache-choices)
- [Messaging Choices](#messaging-choices)
- [Communication Choices](#communication-choices)
- [Storage Choices](#storage-choices)
- [Scaling Choices](#scaling-choices)
- [Consistency Choices](#consistency-choices)

### 12. Reusable HLD Templates
- [URL Shortener](#url-shortener)
- [Rate Limiter Service](#rate-limiter-service)
- [Authentication System](#authentication-system)
- [Ticket Booking System](#ticket-booking-system)
- [Spotify-Like Music Streaming](#spotify-like-music-streaming)
- [Instagram-Like Feed](#instagram-like-feed)
- [Uber-Like Ride Matching](#uber-like-ride-matching)
- [Notification System](#notification-system)
- [File Storage and Sharing System](#file-storage-and-sharing-system)
- [Search and Autocomplete](#search-and-autocomplete)
- [Chat System](#chat-system)
- [Video Streaming Platform](#video-streaming-platform)
- [RAG / AI Application](#rag-ai-application)

### 13. Unfamiliar-System Design Method
- [How to Attack an Unknown Design Problem](#how-to-attack-an-unknown-design-problem)
- [Requirement Questions to Ask](#requirement-questions-to-ask)
- [Capacity Estimation Template](#capacity-estimation-template)
- [API and Data Model Sketch](#api-and-data-model-sketch)
- [First Architecture Diagram](#first-architecture-diagram)
- [Bottleneck Discovery](#bottleneck-discovery)
- [Failure Scenario Analysis](#failure-scenario-analysis)
- [Trade-Off Explanation Framework](#trade-off-explanation-framework)

### 14. Practice and Interview Execution
- [How to Explain a Design on a Whiteboard](#how-to-explain-a-design-on-a-whiteboard)
- [What the Interviewer Is Actually Evaluating](#what-the-interviewer-is-actually-evaluating)
- [Common HLD Follow-Up Questions](#common-hld-follow-up-questions)
- [Common HLD Mistakes](#common-hld-mistakes)
- [30-Second HLD Revision](#30-second-hld-revision)
- [Final HLD Interview Checklist](#final-hld-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

For every HLD topic, use the same learning pattern:

**What is it? → What problem does it solve? → How does it work? → When should I use it? → What are the alternatives? → What trade-off am I accepting? → What failure mode does it introduce? → What follow-up can the interviewer ask?**

Do not memorize “Redis = cache”, “Kafka = queue”, or “load balancer = distributes traffic”.

The interview-ready version is:

> “I would choose X because the system needs A. X gives me B, but I accept C. If the workload changes toward D, I would reconsider Y.”

[Back to Table of Contents](#table-of-contents)

---

<a id="what-hld-actually-means"></a>

## What HLD Actually Means

High-Level Design describes a system in terms of **major components and the interactions between them**.

```text
Clients
   ↓
Edge / Load Balancer
   ↓
API / Application Services
   ↓
Cache / Database / Queue / Object Storage
   ↓
Workers / External Services
```

HLD is not about writing classes. It is about deciding:

- where requests go
- where state lives
- how traffic scales
- how data scales
- how components fail
- how asynchronous work is handled
- how consistency is maintained
- how the system remains observable and secure

### Example

For a URL shortener:

```text
Browser
   ↓
Load Balancer
   ↓
API Service
   ├── Redis
   └── Database
```

The HLD discussion then becomes:

- Why Redis?
- Why a relational database?
- Can the API servers be stateless?
- What happens when Redis is down?
- What happens when one database replica is slow?
- How do we generate unique short codes?
- How do we scale read traffic?
- Do we need asynchronous analytics?

[Back to Table of Contents](#table-of-contents)

---

<a id="hld-vs-lld"></a>

## HLD vs LLD

| HLD | LLD |
|---|---|
| Components | Classes / objects |
| Services | Interfaces / methods |
| Databases | Data structures and object relationships |
| Network flow | In-process control flow |
| Scaling | Encapsulation |
| Replication | Design patterns |
| Partitioning | SOLID |
| Reliability | Detailed implementation |

For this file, stay primarily at the **component / system** level.

[Back to Table of Contents](#table-of-contents)

---

<a id="the-hld-interview-mindset"></a>

## The HLD Interview Mindset

A strong design conversation usually follows:

```text
Requirements
↓
Constraints
↓
Estimates
↓
Core entities / APIs
↓
Simple architecture
↓
Scale bottlenecks
↓
Add scaling mechanisms
↓
Failure handling
↓
Trade-offs
```

Never begin with:

> “Let's use Kafka, Redis, Kubernetes and microservices.”

Begin with the problem.

### Golden rule

> **Requirements choose architecture. Architecture chooses technology.**

[Back to Table of Contents](#table-of-contents)

---

<a id="the-core-design-loop"></a>

## The Core Design Loop

Use this loop for almost every system:

```text
1. Clarify requirements
2. Estimate scale
3. Identify the core request path
4. Draw the simplest working architecture
5. Find the bottleneck
6. Scale the bottleneck
7. Identify failure modes
8. Add reliability mechanisms
9. Re-check consistency
10. Explain trade-offs
```

This prevents “architecture dumping”.

[Back to Table of Contents](#table-of-contents)

---

<a id="functional-vs-non-functional-requirements"></a>

## Functional vs Non-Functional Requirements

### Functional

What the system must do.

Examples:

- Create a shortened URL
- Redirect a short URL
- Book a seat
- Send a notification
- Play a song
- Match a rider with a driver

### Non-functional

How the system should behave.

Examples:

- 99.9% availability
- p95 latency under 200 ms
- millions of users
- data durability
- regional availability
- security
- consistency requirements

A system can be functionally correct and still fail its non-functional requirements.

[Back to Table of Contents](#table-of-contents)

---

<a id="scale-estimation-and-back-of-the-envelope-calculations"></a>

## Scale Estimation and Back-of-the-Envelope Calculations

Interview designs become much stronger when you estimate:

```text
Users
Requests/sec
Peak requests/sec
Read/write ratio
Storage/day
Storage/year
Bandwidth
Cache size
```

### Example

Suppose:

```text
10 million daily active users
10 requests/user/day
```

Then:

```text
100 million requests/day
≈ 100,000,000 / 86,400
≈ 1,157 requests/sec average
```

If peak traffic is 5× average:

```text
≈ 5,785 requests/sec peak
```

The exact number is less important than showing your reasoning.

[Back to Table of Contents](#table-of-contents)

---

<a id="latency-throughput-availability-reliability-and-durability"></a>

## Latency, Throughput, Availability, Reliability and Durability

These terms describe different properties.

| Term | Meaning |
|---|---|
| Latency | Time for one operation |
| Throughput | Work completed per unit time |
| Availability | Probability the service is accessible |
| Reliability | Ability to operate correctly over time |
| Durability | Probability data survives failure |

### Important distinction

A service can have high throughput but poor latency.

A database can have strong durability but lower write throughput.

[Back to Table of Contents](#table-of-contents)

---

<a id="cap-theorem"></a>

## CAP Theorem

CAP is about distributed data systems during a **network partition**.

The three properties are:

- Consistency
- Availability
- Partition tolerance

In a partition, a distributed system cannot simultaneously guarantee both perfect consistency and availability in the CAP sense.

### Interview-safe explanation

> “Because network partitions can occur, a distributed system must choose how it behaves during the partition: continue serving with potentially stale or conflicting views, or reject/delay some operations to preserve stronger consistency.”

Do not oversimplify CAP into “you can choose any two of three under normal operation.”

[Back to Table of Contents](#table-of-contents)

---

<a id="consistency-models"></a>

## Consistency Models

Important models:

| Model | Mental model |
|---|---|
| Strong / linearizable | Reads behave as if operations occurred in one real-time order |
| Eventual | Replicas converge if updates stop |
| Read-your-writes | A user sees their own successful writes |
| Monotonic reads | Reads do not move backward to older state |

### Trade-off

Stronger consistency can increase coordination cost and latency, and can reduce availability during failures.

Eventual consistency can improve availability and scale, but applications must tolerate stale reads.

[Back to Table of Contents](#table-of-contents)

---

<a id="client-api-gateway-and-backend-services"></a>

## Client, API Gateway and Backend Services

A common flow:

```text
Client
  ↓
DNS
  ↓
CDN / Edge
  ↓
Load Balancer
  ↓
API Gateway
  ↓
Application Services
  ↓
Data / Cache / Queue
```

Not every system needs every component.

### API Gateway

Typical responsibilities:

- routing
- authentication checks
- rate limiting
- request transformation
- observability
- aggregation

### Trade-off

Centralizing too much in the gateway can create coupling and a bottleneck.

[Back to Table of Contents](#table-of-contents)

---

<a id="monolith-vs-modular-monolith-vs-microservices"></a>

## Monolith vs Modular Monolith vs Microservices

### Monolith

One deployable application.

**Pros**

- simple deployment
- easy local development
- fewer network calls
- simpler transactions

**Cons**

- large deployment unit
- weaker independent scaling
- failure blast radius can be larger

### Modular monolith

One deployment, but strong internal module boundaries.

Useful when:

- domain boundaries are clear
- scale is moderate
- operational simplicity matters

### Microservices

Multiple independently deployable services.

**Pros**

- independent scaling
- independent deployment
- fault isolation possibilities
- team autonomy

**Cons**

- network failures
- distributed transactions
- observability complexity
- deployment complexity
- service discovery

### Decision rule

Do not choose microservices merely because “large systems use microservices”.

[Back to Table of Contents](#table-of-contents)

---

<a id="synchronous-vs-asynchronous-communication"></a>

## Synchronous vs Asynchronous Communication

### Synchronous

```text
Service A → Service B → response
```

Good when A needs B's result immediately.

### Asynchronous

```text
Service A → Queue → Service B
```

Good when:

- work can happen later
- spikes need buffering
- retries are required
- producers and consumers should be decoupled

### Trade-off

Async improves decoupling and resilience, but introduces:

- eventual consistency
- duplicate processing concerns
- ordering questions
- harder debugging

[Back to Table of Contents](#table-of-contents)

---

<a id="stateless-vs-stateful-services"></a>

## Stateless vs Stateful Services

### Stateless service

Any instance can handle any request.

State lives externally:

```text
App instances
   ↓
Redis / DB / object storage
```

This simplifies horizontal scaling.

### Stateful service

The instance keeps important state locally.

Scaling becomes harder because requests may depend on a particular instance or replicated state.

### Interview default

Prefer stateless application servers when practical.

[Back to Table of Contents](#table-of-contents)

---

<a id="horizontal-vs-vertical-scaling"></a>

## Horizontal vs Vertical Scaling

### Vertical

Make one machine larger.

```text
8 CPU → 32 CPU
```

Simple, but hardware has limits.

### Horizontal

Add more machines.

```text
1 server
↓
10 servers
```

Improves scalability and fault isolation, but requires:

- load balancing
- shared state handling
- service discovery
- distributed observability

[Back to Table of Contents](#table-of-contents)

---

<a id="load-balancer"></a>

## Load Balancer

A load balancer distributes incoming requests or connections across backend instances.

```text
             ┌── App 1
Client → LB ─┼── App 2
             └── App 3
```

### Why use one?

- distribute load
- avoid a single backend receiving everything
- detect unhealthy instances
- enable horizontal scaling
- support failover
- sometimes perform TLS termination

### Important distinction

A load balancer is not only a “traffic splitter”.

It can also make decisions based on:

- connection state
- backend health
- client metadata
- HTTP path
- headers
- cookies
- weighted routing

[Back to Table of Contents](#table-of-contents)

---

<a id="load-balancing-algorithms"></a>

## Load Balancing Algorithms

### Round Robin

```text
A → Server 1
B → Server 2
C → Server 3
D → Server 1
```

**Pros:** simple.

**Cons:** assumes backends are approximately equal and work is similarly distributed.

### Weighted Round Robin

Servers receive traffic proportional to assigned weights.

Useful when machines have different capacities.

### Least Connections

Send traffic to the backend with the fewest active connections.

Useful when request duration varies.

### Weighted Least Connections

Combines capacity weighting with connection counts.

### IP Hash

Hash client IP to choose a backend.

Useful for simple affinity, but can create imbalance and can remap clients when the backend set changes.

### Consistent Hashing

Useful when stable mapping matters and backend membership changes.

Commonly discussed in caches and distributed routing rather than as the default HTTP load-balancing algorithm.

### Random / Power of Two Choices

Choose one or two candidates and select based on current load.

Can distribute load well with low coordination.

### Latency / Least-Response-Time Routing

Choose a backend using observed response-time signals.

Useful when backend performance differs.

### Interview comparison

| Algorithm | Best fit | Main weakness |
|---|---|---|
| Round Robin | Similar servers, predictable requests | Ignores actual load |
| Weighted RR | Different capacity | Static weights may become stale |
| Least Connections | Variable request duration | Connection count ≠ actual work |
| IP Hash | Simple affinity | Imbalance / churn |
| Consistent Hashing | Stable key→node mapping | More complex |
| Dynamic load-aware | Heterogeneous environments | More state/measurement overhead |

[Back to Table of Contents](#table-of-contents)

---

<a id="layer-4-vs-layer-7-load-balancing"></a>

## Layer 4 vs Layer 7 Load Balancing

### Layer 4

Works with transport-level information.

Examples:

```text
IP
Port
TCP/UDP connection
```

Lower overhead and protocol-agnostic.

### Layer 7

Understands application protocols such as HTTP.

It can route using:

```text
Path
Host
Headers
Cookies
Methods
```

### Trade-off

L7 provides richer routing decisions but requires more protocol awareness and processing.

[Back to Table of Contents](#table-of-contents)

---

<a id="reverse-proxy"></a>

## Reverse Proxy

A reverse proxy sits in front of backend services.

```text
Client → Reverse Proxy → Backend
```

Common uses:

- TLS termination
- routing
- caching
- compression
- authentication integration
- hiding internal topology

A load balancer can also act as a reverse proxy.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-gateway"></a>

## API Gateway

An API gateway is an application-aware entry point into backend services.

It may provide:

- authentication
- authorization checks
- routing
- rate limits
- request aggregation
- protocol translation
- observability

### API Gateway vs Reverse Proxy

A reverse proxy is the broader intermediary concept.

An API gateway usually carries more application-level policy.

[Back to Table of Contents](#table-of-contents)

---

<a id="service-discovery"></a>

## Service Discovery

In dynamic systems, service instances may change IPs frequently.

Service discovery answers:

> “Where can I currently reach service X?”

Common approaches:

- client-side discovery
- server-side discovery
- service registry
- DNS-based discovery
- orchestrator-native discovery

### Trade-off

More dynamic discovery improves elasticity, but introduces another dependency that must be reliable.

[Back to Table of Contents](#table-of-contents)

---

<a id="health-checks-and-failover"></a>

## Health Checks and Failover

A load balancer or orchestrator can remove unhealthy instances.

### Health-check types

- liveness
- readiness
- dependency-aware health

### Trap

A process being alive does not mean it can serve useful traffic.

[Back to Table of Contents](#table-of-contents)

---

<a id="database-selection-framework"></a>

## Database Selection Framework

Do not ask:

> “Which database is best?”

Ask:

```text
What data model?
What query patterns?
Read/write ratio?
Transactions?
Consistency?
Scale?
Partitioning needs?
Latency target?
Relationship complexity?
Operational constraints?
```

Then choose the smallest database model that fits.

[Back to Table of Contents](#table-of-contents)

---

<a id="sql-vs-nosql"></a>

## SQL vs NoSQL

### SQL

Strong fit for:

- structured relational data
- joins
- transactions
- integrity constraints
- complex queries

### NoSQL

Broad category. Useful when a workload benefits from:

- flexible schemas
- key-value access
- massive horizontal scale
- document-oriented access
- specialized partitioning models

The phrase “NoSQL is faster” is not a valid general argument.

[Back to Table of Contents](#table-of-contents)

---

<a id="relational-databases"></a>

## Relational Databases

Examples:

- PostgreSQL
- MySQL

Strong features:

- ACID transactions
- joins
- constraints
- indexes
- mature query engines

Good examples:

- banking transactions
- ticket booking
- order management
- user/account data

[Back to Table of Contents](#table-of-contents)

---

<a id="document-databases"></a>

## Document Databases

Examples:

- MongoDB
- Couchbase

Data is stored around document-shaped objects.

Useful when:

- application data maps naturally to documents
- schema flexibility matters
- access patterns avoid complex joins

Trade-off:

Denormalization can make cross-document consistency harder.

[Back to Table of Contents](#table-of-contents)

---

<a id="key-value-stores"></a>

## Key-Value Stores

Examples:

- Redis
- Dynamo-style systems

Pattern:

```text
key → value
```

Excellent when the main access pattern is direct key lookup.

Common uses:

- cache
- sessions
- counters
- rate limiting
- ephemeral state

[Back to Table of Contents](#table-of-contents)

---

<a id="wide-column-stores"></a>

## Wide-Column Stores

Examples:

- Cassandra
- ScyllaDB

Useful for very large distributed datasets with known access patterns and high write throughput.

Trade-off:

Query flexibility is typically more constrained than a relational database.

[Back to Table of Contents](#table-of-contents)

---

<a id="graph-databases"></a>

## Graph Databases

Examples:

- Neo4j

Useful when relationships are central:

```text
User → follows → User
User → purchased → Product
```

A graph model can make relationship traversal natural.

[Back to Table of Contents](#table-of-contents)

---

<a id="object-storage"></a>

## Object Storage

Examples:

- Amazon S3
- Google Cloud Storage
- Azure Blob Storage

Best for large immutable-ish objects:

- images
- videos
- backups
- documents
- model artifacts

Do not store multi-gigabyte media directly in an OLTP database unless there is a strong reason.

[Back to Table of Contents](#table-of-contents)

---

<a id="indexes"></a>

## Indexes

An index avoids scanning every row to find matching data.

```text
Without index:
query → scan many rows

With index:
query → index lookup → relevant rows
```

Trade-off:

- faster reads
- extra storage
- slower writes
- index maintenance cost

[Back to Table of Contents](#table-of-contents)

---

<a id="read-replicas"></a>

## Read Replicas

A primary handles writes. Replicas serve some reads.

```text
                ┌→ Replica 1
App → Router ───┼→ Replica 2
                └→ Primary
```

Useful for read-heavy systems.

### Major issue

Replication lag can cause stale reads.

[Back to Table of Contents](#table-of-contents)

---

<a id="database-replication"></a>

## Database Replication

Replication means maintaining multiple copies of data.

### Common patterns

- primary-replica
- multi-primary
- leaderless / quorum-based

Trade-offs involve:

- consistency
- write conflicts
- failover
- operational complexity
- read scaling

[Back to Table of Contents](#table-of-contents)

---

<a id="sharding-and-partitioning"></a>

## Sharding and Partitioning

Partition data across multiple nodes.

Example:

```text
user_id % 4
```

maps users to four shards.

### Benefits

- more storage capacity
- more write/read capacity
- parallelism

### Problems

- hot partitions
- cross-shard queries
- resharding
- distributed transactions

The partition key is one of the most important design decisions in a sharded system.

[Back to Table of Contents](#table-of-contents)

---

<a id="consistent-hashing"></a>

## Consistent Hashing

Instead of:

```text
key % N
```

consistent hashing reduces the amount of key movement when nodes are added or removed.

Used in:

- distributed caches
- partitioned routing
- some distributed storage systems

### Interview idea

The benefit is not magical hashing speed. It is **reducing remapping during topology changes**.

[Back to Table of Contents](#table-of-contents)

---

<a id="transactions-and-distributed-transactions"></a>

## Transactions and Distributed Transactions

Local database transactions are straightforward.

Across independent services, the problem becomes much harder.

### Prefer

- local transactions
- asynchronous events
- idempotent consumers
- compensating actions

before reaching for a distributed transaction protocol.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-caching-solves"></a>

## What Caching Solves

Caching stores frequently accessed data closer to the caller.

```text
Request
  ↓
Cache hit → response

Cache miss
  ↓
Database
  ↓
populate cache
```

Benefits:

- lower latency
- lower database load
- higher effective throughput

Costs:

- stale data
- invalidation complexity
- cache stampede
- extra operational state

[Back to Table of Contents](#table-of-contents)

---

<a id="redis"></a>

## Redis

Redis is an in-memory data structure server frequently used for:

- caching
- sessions
- counters
- rate limiting
- distributed coordination
- queues/streams in selected designs

Important properties:

- very low latency for memory-resident operations
- rich data structures
- optional persistence/replication features
- core commands are processed sequentially per Redis execution context, while modern Redis also uses threads for selected background/networking work

### Do not define Redis as “just a cache”

That is one of the common weak answers.

### Redis trade-off

Use Redis when memory-speed access or simple shared state provides enough value to justify:

- extra infrastructure
- memory cost
- eviction/staleness concerns
- operational complexity

[Back to Table of Contents](#table-of-contents)

---

<a id="cache-aside-pattern"></a>

## Cache-Aside Pattern

Application controls the cache.

```text
Read:
App → Cache
      ↓ miss
      DB
      ↓
      Cache

Write:
App → DB
```

Pros:

- simple
- cache contains only requested data

Cons:

- application handles cache logic
- stale-entry management remains your responsibility

[Back to Table of Contents](#table-of-contents)

---

<a id="read-through-and-write-through-caching"></a>

## Read-Through and Write-Through Caching

### Read-through

Application asks cache for data; cache loads it on a miss.

### Write-through

Write goes through cache and is propagated to backing storage.

These can reduce application-side cache plumbing but add infrastructure behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="write-back-and-write-around-caching"></a>

## Write-Back and Write-Around Caching

### Write-back

Application writes cache first; backing store is updated later.

Fast, but more data-loss risk if the cache is lost before persistence.

### Write-around

Writes bypass cache and go directly to the backing store.

Useful when newly written data is unlikely to be read immediately.

[Back to Table of Contents](#table-of-contents)

---

<a id="cache-eviction-policies"></a>

## Cache Eviction Policies

Common policies:

- LRU — least recently used
- LFU — least frequently used
- FIFO — first in, first out
- TTL-based expiration

The correct choice depends on access patterns.

[Back to Table of Contents](#table-of-contents)

---

<a id="cache-invalidation"></a>

## Cache Invalidation

Classic problem:

> “How do I know when cached data is no longer correct?”

Strategies:

- TTL
- explicit invalidation
- versioned keys
- write-through updates
- event-driven invalidation

### Interview line

> “Caching is easy; keeping cached state sufficiently correct is the harder part.”

[Back to Table of Contents](#table-of-contents)

---

<a id="cache-stampede-and-hot-keys"></a>

## Cache Stampede and Hot Keys

### Cache stampede

Many requests miss simultaneously and hit the database.

Mitigations:

- request coalescing
- jittered TTLs
- warming
- locking
- stale-while-revalidate patterns

### Hot key

One cache key receives disproportionate traffic.

Mitigations:

- replication
- local caching
- key sharding where appropriate
- workload redesign

[Back to Table of Contents](#table-of-contents)

---

<a id="cdn"></a>

## CDN

A CDN caches content at edge locations closer to users.

Best for:

- images
- videos
- CSS/JS
- public or cacheable API responses

Benefits:

- lower geographic latency
- reduced origin load
- better bandwidth efficiency

[Back to Table of Contents](#table-of-contents)

---

<a id="why-use-a-queue"></a>

## Why Use a Queue

A queue decouples producer and consumer.

```text
Producer → Queue → Consumer
```

Why?

- absorb traffic spikes
- retry failed work
- process asynchronously
- decouple teams/services
- smooth throughput

### Simple example

Image upload:

```text
API
 ↓
Object Storage
 ↓
Queue
 ↓
Image Processing Worker
```

The user need not wait for CPU-intensive processing.

[Back to Table of Contents](#table-of-contents)

---

<a id="message-broker"></a>

## Message Broker

A message broker accepts, stores, routes, and delivers messages between producers and consumers.

The two common interview families:

- queue-oriented brokers
- log/stream-oriented platforms

The key question is not “Which product is better?” but “What delivery and consumption model does the system need?”

[Back to Table of Contents](#table-of-contents)

---

<a id="rabbitmq"></a>

## RabbitMQ

RabbitMQ is a message broker built around concepts such as:

```text
Producer
→ Exchange
→ Queue
→ Consumer
```

Common strengths:

- flexible routing
- acknowledgements
- retries and dead-lettering
- work queues
- request/workflow messaging

A routing key and exchange type can determine which queues receive a message.

### Good use cases

- background jobs
- task queues
- workflow steps
- command-style messaging

### Trade-off

RabbitMQ is often a better conceptual fit when you need broker-managed routing and work distribution rather than a durable replayable event log.

[Back to Table of Contents](#table-of-contents)

---

<a id="kafka"></a>

## Kafka

Kafka is a distributed event-streaming platform.

Core model:

```text
Topic
 ├── Partition 0
 ├── Partition 1
 └── Partition 2
```

Producers append records.

Consumers track their positions.

### Important property

Messages can remain available for retention so consumers can read historical events again.

### Good use cases

- event streaming
- analytics pipelines
- high-throughput pipelines
- event-driven architectures
- replayable event history

[Back to Table of Contents](#table-of-contents)

---

<a id="kafka-vs-rabbitmq"></a>

## Kafka vs RabbitMQ

| Dimension | Kafka | RabbitMQ |
|---|---|---|
| Core model | Distributed log / stream | Message broker |
| Replay | Strong fit | Not the primary mental model |
| Ordering | Within partition | Queue-level semantics |
| Main scaling unit | Partition | Queue / broker topology |
| Common use | Event streams | Work distribution / messaging |
| Consumer position | Offset | Delivery/ack semantics |

### Decision rule

Choose based on **consumption semantics**, not popularity.

[Back to Table of Contents](#table-of-contents)

---

<a id="pub-sub"></a>

## Pub-Sub

Publisher sends an event without directly targeting a specific consumer.

```text
             → Consumer A
Publisher → Topic
             → Consumer B
             → Consumer C
```

Useful for:

- notifications
- audit events
- analytics
- cache invalidation
- domain events

[Back to Table of Contents](#table-of-contents)

---

<a id="consumer-groups"></a>

## Consumer Groups

A consumer group lets multiple consumers share partitions/work.

```text
Partition 0 → Consumer A
Partition 1 → Consumer B
Partition 2 → Consumer C
```

This is a scaling mechanism, not “three consumers all reading the same partition simultaneously”.

[Back to Table of Contents](#table-of-contents)

---

<a id="delivery-semantics"></a>

## Delivery Semantics

### At-most-once

Message may be lost, but is not intentionally redelivered.

### At-least-once

Message is retried until acknowledged, so duplicates are possible.

### Exactly-once

A stronger semantic that requires careful end-to-end design; it is not equivalent to “the broker will never deliver duplicates under any application failure.”

### Interview-safe principle

At-least-once + idempotent processing is often a practical architecture.

[Back to Table of Contents](#table-of-contents)

---

<a id="retries-dead-letter-queues-and-poison-messages"></a>

## Retries, Dead-Letter Queues and Poison Messages

A poison message repeatedly fails processing.

Typical flow:

```text
Queue
 ↓
Consumer
 ↓ failure
Retry
 ↓ repeated failure
Dead-Letter Queue
```

This prevents one bad message from blocking healthy work forever.

[Back to Table of Contents](#table-of-contents)

---

<a id="ordering-and-partitioning"></a>

## Ordering and Partitioning

Global ordering is expensive.

A common compromise is:

> Guarantee ordering only within a partition or key.

Example:

```text
order_id = 123 → same partition
```

Then events for that order remain ordered while unrelated orders scale independently.

[Back to Table of Contents](#table-of-contents)

---

<a id="backpressure"></a>

## Backpressure

Backpressure means slowing producers when downstream capacity is insufficient.

```text
Producer rate > Consumer capacity
            ↓
         backlog
```

Possible responses:

- bounded queue
- rate limiting
- dropping low-priority work
- scaling consumers
- batch processing

[Back to Table of Contents](#table-of-contents)

---

<a id="eventual-consistency-with-events"></a>

## Eventual Consistency with Events

Suppose:

```text
Order Service
 ↓ event
Inventory Service
 ↓
Search / Analytics / Notifications
```

Different systems may update at different times.

That can be acceptable when the product does not require an immediately globally consistent view.

[Back to Table of Contents](#table-of-contents)

---

<a id="outbox-pattern"></a>

## Outbox Pattern

Problem:

```text
DB transaction succeeds
but event publish fails
```

Solution:

Write business data and an outbox event in the same local transaction.

Then a publisher reads the outbox and delivers the event.

This reduces the “database committed but event disappeared” gap.

[Back to Table of Contents](#table-of-contents)

---

<a id="timeouts"></a>

## Timeouts

Every distributed call should have a bounded timeout.

Without timeouts:

```text
Service A waits forever
↓
threads/connections accumulate
↓
capacity drops
↓
failure spreads
```

Timeouts are a reliability boundary.

[Back to Table of Contents](#table-of-contents)

---

<a id="retries-and-exponential-backoff"></a>

## Retries and Exponential Backoff

Retry only when the failure may be transient.

Use:

```text
short delay
→ longer delay
→ longer delay
→ cap
```

Add jitter to avoid synchronized retries.

### Trap

Retries can turn a partial outage into a retry storm.

[Back to Table of Contents](#table-of-contents)

---

<a id="circuit-breaker"></a>

## Circuit Breaker

A circuit breaker stops repeatedly calling an unhealthy dependency.

Typical states:

```text
Closed
  ↓ failures
Open
  ↓ wait
Half-Open
  ↓ test
Closed / Open
```

Benefits:

- reduce cascading failure
- fail fast
- recover dependency gradually

[Back to Table of Contents](#table-of-contents)

---

<a id="bulkhead-isolation"></a>

## Bulkhead Isolation

Partition resources so one workload cannot consume everything.

Example:

```text
Payments pool
Search pool
Notification pool
```

If notifications become slow, payment capacity can remain protected.

[Back to Table of Contents](#table-of-contents)

---

<a id="rate-limiting"></a>

## Rate Limiting

Rate limiting protects a service from excessive request volume.

Common algorithms:

- fixed window
- sliding window
- token bucket
- leaky bucket

### Token bucket mental model

Tokens accumulate up to a capacity.

Each request consumes a token.

This allows controlled bursts while limiting long-term rate.

[Back to Table of Contents](#table-of-contents)

---

<a id="idempotency"></a>

## Idempotency

An operation is idempotent when repeating it produces the same intended final effect.

Important for:

- payment APIs
- booking
- order creation
- retries

### Idempotency key

Client sends a unique request key.

Server records the result.

Repeated request with the same key returns the existing result instead of duplicating the operation.

[Back to Table of Contents](#table-of-contents)

---

<a id="distributed-locks"></a>

## Distributed Locks

A distributed lock coordinates access across multiple instances.

Use carefully.

Questions:

- What if the lock holder crashes?
- How long is the lease?
- Can a stale holder continue?
- What happens during network partition?

A lock is not automatically a correctness guarantee.

[Back to Table of Contents](#table-of-contents)

---

<a id="leader-election"></a>

## Leader Election

Multiple nodes agree on one active coordinator.

Useful for:

- schedulers
- partition ownership
- singleton background work

Trade-off:

Coordination complexity increases.

[Back to Table of Contents](#table-of-contents)

---

<a id="heartbeat-and-failure-detection"></a>

## Heartbeat and Failure Detection

Nodes periodically signal that they are alive.

```text
Node A ← heartbeat → Node B
```

Missing heartbeats can trigger suspicion or failover.

But:

> “No heartbeat” means “we could not observe the node,” not necessarily “the node is definitely dead.”

[Back to Table of Contents](#table-of-contents)

---

<a id="single-point-of-failure"></a>

## Single Point of Failure

A component is a single point of failure when its failure can make the system unavailable.

Examples:

- one database instance
- one gateway
- one message broker node
- one region

HLD should identify these explicitly.

[Back to Table of Contents](#table-of-contents)

---

<a id="graceful-degradation"></a>

## Graceful Degradation

When optional components fail, the core service continues.

Example:

```text
Product page
├── price → required
├── stock → required
└── recommendations → optional
```

If recommendations fail, the product page can still load.

[Back to Table of Contents](#table-of-contents)

---

<a id="read-heavy-vs-write-heavy-systems"></a>

## Read-Heavy vs Write-Heavy Systems

### Read-heavy

Typical tools:

- caching
- read replicas
- CDN
- denormalized views

### Write-heavy

Typical tools:

- batching
- partitioning
- append-friendly storage
- asynchronous processing
- careful indexing

Always design around the dominant bottleneck.

[Back to Table of Contents](#table-of-contents)

---

<a id="hotspots-and-hot-partitions"></a>

## Hotspots and Hot Partitions

A theoretically scalable partitioning scheme can still fail if one key receives disproportionate traffic.

Examples:

- celebrity user feed
- flash-sale product
- one popular URL
- one partition key

Mitigations:

- key redesign
- sharding hot keys
- caching
- replication
- request coalescing

[Back to Table of Contents](#table-of-contents)

---

<a id="pagination"></a>

## Pagination

### Offset pagination

```text
?page=100
```

Simple, but deep offsets can become expensive and unstable under concurrent writes.

### Cursor pagination

```text
after_id=...
```

Usually better for large changing datasets.

[Back to Table of Contents](#table-of-contents)

---

<a id="batching"></a>

## Batching

Batch multiple operations into fewer calls.

Benefits:

- lower network overhead
- better throughput

Cost:

- larger per-request latency
- more complicated failure handling

[Back to Table of Contents](#table-of-contents)

---

<a id="asynchronous-processing"></a>

## Asynchronous Processing

Move slow non-critical work out of the request path.

```text
User request
   ↓
Fast response
   ↓
Queue
   ↓
Worker
```

Examples:

- email
- report generation
- image processing
- analytics
- embeddings

[Back to Table of Contents](#table-of-contents)

---

<a id="fan-out-on-read-vs-fan-out-on-write"></a>

## Fan-Out on Read vs Fan-Out on Write

Important for feeds.

### Fan-out on read

When a user opens a feed, gather content from followed accounts.

Pros:

- cheap writes
- fresh assembly

Cons:

- expensive reads for users following many accounts

### Fan-out on write

When content is created, distribute it into followers' feed storage.

Pros:

- fast reads

Cons:

- expensive writes
- celebrity users create huge fan-out

Hybrid strategies are common.

[Back to Table of Contents](#table-of-contents)

---

<a id="cqrs"></a>

## CQRS

Command Query Responsibility Segregation separates write and read models.

```text
Commands → write model
Queries  → read model
```

Useful when read and write workloads have very different needs.

Costs:

- duplicated models
- synchronization complexity
- eventual consistency

[Back to Table of Contents](#table-of-contents)

---

<a id="materialized-views"></a>

## Materialized Views

Precompute commonly requested data.

Example:

```text
raw events
   ↓
aggregation
   ↓
materialized leaderboard
```

Trade-off:

Faster reads, more complexity and update work.

[Back to Table of Contents](#table-of-contents)

---

<a id="data-denormalization"></a>

## Data Denormalization

Store duplicated data to avoid expensive joins or repeated computation.

Benefits:

- faster reads
- simpler read path

Costs:

- duplicate updates
- consistency complexity
- larger storage

[Back to Table of Contents](#table-of-contents)

---

<a id="dns-in-system-design"></a>

## DNS in System Design

DNS maps names to addresses or other records.

In HLD, DNS can participate in:

- service endpoints
- region routing
- failover
- traffic steering
- load distribution

[Back to Table of Contents](#table-of-contents)

---

<a id="tls-termination"></a>

## TLS Termination

TLS can terminate at:

```text
Client
 ↓
Load Balancer / Reverse Proxy
 ↓
Backend
```

This can simplify certificate management and reduce work on application servers.

Trade-off:

Traffic between proxy and backend is not automatically encrypted merely because external HTTPS exists. Internal TLS may still be required.

[Back to Table of Contents](#table-of-contents)

---

<a id="connection-pooling"></a>

## Connection Pooling

Reuse existing database or HTTP connections.

Benefits:

- avoid repeated setup
- lower latency
- better resource utilization

But pools must be bounded.

Too many connections can overload:

- application
- database
- OS file descriptors
- network

[Back to Table of Contents](#table-of-contents)

---

<a id="websockets"></a>

## WebSockets

Persistent full-duplex communication.

Useful for:

- chat
- live dashboards
- multiplayer state updates
- ride tracking

Costs:

- connection state
- scaling complexity
- load-balancing affinity or shared state
- connection management

[Back to Table of Contents](#table-of-contents)

---

<a id="long-polling"></a>

## Long Polling

Client sends request; server holds it until data is available or timeout occurs.

Simpler than WebSockets, but less efficient for frequent bidirectional updates.

[Back to Table of Contents](#table-of-contents)

---

<a id="polling"></a>

## Polling

Client repeatedly asks:

```text
Any new data?
Any new data?
Any new data?
```

Simple but can create waste and latency.

[Back to Table of Contents](#table-of-contents)

---

<a id="cdn-and-edge-delivery"></a>

## CDN and Edge Delivery

Move cacheable content closer to users.

Useful for:

- static assets
- media
- downloadable files
- cacheable API responses

Not everything belongs on the CDN.

Personalized, rapidly changing, or security-sensitive responses may need origin processing.

[Back to Table of Contents](#table-of-contents)

---

<a id="authentication-architecture"></a>

## Authentication Architecture

Authentication answers:

> “Who are you?”

Typical flow:

```text
Client
 ↓
Auth Service
 ↓
Identity / Credential Store
 ↓
Access Token / Session
```

The core design questions are:

- token/session storage
- token expiry
- refresh
- revocation
- password security
- MFA
- device/session management

[Back to Table of Contents](#table-of-contents)

---

<a id="authorization"></a>

## Authorization

Authorization answers:

> “What are you allowed to do?”

Examples:

- role-based access
- resource ownership
- policy-based access

Authentication without authorization is not enough.

[Back to Table of Contents](#table-of-contents)

---

<a id="session-based-vs-token-based-authentication"></a>

## Session-Based vs Token-Based Authentication

### Session

Server stores session state.

Pros:

- easy revocation
- simple server-side control

Cons:

- distributed session storage required when many instances exist

### Tokens

Client presents a token.

Pros:

- useful for distributed APIs
- fewer server-side session lookups in some designs

Cons:

- revocation is harder
- token leakage is dangerous
- long-lived tokens increase risk

[Back to Table of Contents](#table-of-contents)

---

<a id="oauth-20-and-openid-connect"></a>

## OAuth 2.0 and OpenID Connect

OAuth 2.0 is primarily an authorization framework.

OpenID Connect adds an identity layer on top of OAuth 2.0.

Do not describe OAuth as simply “the login protocol”.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-keys-and-service-credentials"></a>

## API Keys and Service Credentials

Useful for:

- machine-to-machine access
- simple service authentication
- partner integrations

They require:

- secure storage
- rotation
- revocation
- scoping

[Back to Table of Contents](#table-of-contents)

---

<a id="secrets-management"></a>

## Secrets Management

Never hard-code:

- database passwords
- private keys
- service credentials

Use a secret-management system and rotate credentials.

[Back to Table of Contents](#table-of-contents)

---

<a id="encryption-at-rest-and-in-transit"></a>

## Encryption at Rest and in Transit

### In transit

TLS.

### At rest

Disk/database/object-level encryption.

These solve different threat models.

[Back to Table of Contents](#table-of-contents)

---

<a id="logging"></a>

## Logging

Logs explain individual events.

Include enough context to correlate requests:

- request ID
- user/session identifier where appropriate
- service
- timestamp
- result

Do not log secrets.

[Back to Table of Contents](#table-of-contents)

---

<a id="metrics"></a>

## Metrics

Useful metrics:

- request rate
- error rate
- p50/p95/p99 latency
- queue depth
- cache hit ratio
- CPU/memory
- database latency

[Back to Table of Contents](#table-of-contents)

---

<a id="tracing"></a>

## Tracing

Distributed tracing follows a request across services.

```text
Gateway
 ↓
Service A
 ↓
Service B
 ↓
Database
```

Useful for identifying where latency is actually introduced.

[Back to Table of Contents](#table-of-contents)

---

<a id="slo-sla-and-sli"></a>

## SLO, SLA and SLI

| Term | Meaning |
|---|---|
| SLI | Measured indicator |
| SLO | Target value |
| SLA | Agreement with consequences |

Example:

```text
SLI = successful request percentage
SLO = 99.9%
SLA = contractual commitment
```

[Back to Table of Contents](#table-of-contents)

---

<a id="alerting"></a>

## Alerting

Alerts should indicate actionable conditions.

Examples:

- sustained error-rate increase
- latency above target
- queue backlog growing
- database replication lag
- cache failure

Avoid alerting on every small transient fluctuation.

[Back to Table of Contents](#table-of-contents)

---

<a id="load-balancer-choices"></a>

## Load Balancer Choices

### Round Robin vs Least Connections

Choose **Round Robin** when backend capacity and request costs are relatively uniform.

Choose **Least Connections** when active connection duration varies enough that connection count gives useful load information.

### L4 vs L7

Choose **L4** when:

- low overhead matters
- protocol-aware routing is unnecessary
- transport-level forwarding is sufficient

Choose **L7** when:

- routing depends on HTTP metadata
- application-aware policies are useful

### Sticky Sessions vs Stateless

Sticky sessions can preserve local state.

Stateless servers plus shared state are usually easier to scale horizontally.

[Back to Table of Contents](#table-of-contents)

---

<a id="database-choices"></a>

## Database Choices

### SQL vs Document

Choose SQL when:

- relations are important
- transactions matter
- query flexibility matters

Choose document storage when:

- document-shaped aggregates dominate
- schema flexibility matters
- access patterns are mostly document-centric

### SQL vs Key-Value

Choose SQL for rich query and relational integrity.

Choose key-value for extremely simple, high-speed key-based access.

### Read Replica vs Sharding

Read replicas primarily scale reads.

Sharding partitions data to scale storage and/or reads/writes across nodes.

They solve different bottlenecks and can coexist.

[Back to Table of Contents](#table-of-contents)

---

<a id="cache-choices"></a>

## Cache Choices

### Redis vs Local In-Process Cache

Redis:

- shared across instances
- more consistent across workers
- network hop required

Local cache:

- fastest access
- isolated per instance
- stale/inconsistent across instances

### Redis vs Database

Redis is often for low-latency transient/shared access.

The database remains the system of record when durability and relational integrity matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="messaging-choices"></a>

## Messaging Choices

### RabbitMQ vs Kafka

Ask:

```text
Do I need task/work routing?
→ RabbitMQ may fit naturally.

Do I need durable event streams, partitions and replay?
→ Kafka may fit naturally.
```

Do not frame this as “Kafka is newer, so Kafka is better.”

[Back to Table of Contents](#table-of-contents)

---

<a id="communication-choices"></a>

## Communication Choices

### REST / HTTP

Good for conventional request/response APIs.

### gRPC

Useful for efficient service-to-service RPC, especially typed internal APIs.

### Async messaging

Better when decoupling, buffering, and delayed processing matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="storage-choices"></a>

## Storage Choices

### Database vs Object Storage

Database:

- structured query
- transactional metadata

Object storage:

- large blobs
- cheap scalable storage

A common architecture stores metadata in a database and the actual file in object storage.

[Back to Table of Contents](#table-of-contents)

---

<a id="scaling-choices"></a>

## Scaling Choices

### Vertical → Horizontal

Start vertically for simplicity.

Move horizontally when a single machine becomes a capacity or availability limit.

### Cache → Replica → Shard

A common progression for a read-heavy application is:

```text
Optimize queries
→ Cache hot reads
→ Add read replicas
→ Partition/shard when one database node is insufficient
```

The exact order depends on the workload.

[Back to Table of Contents](#table-of-contents)

---

<a id="consistency-choices"></a>

## Consistency Choices

Ask:

```text
Must every read immediately reflect the latest write?
```

If yes, stronger consistency may be necessary.

If slight staleness is acceptable:

```text
caching
replication
async events
materialized views
```

can improve scale and latency.

[Back to Table of Contents](#table-of-contents)

---

<a id="url-shortener"></a>

## URL Shortener

### Requirements

- create short URL
- redirect short URL
- optional analytics

### Core flow

```text
Create:
Client → API → DB → short code

Redirect:
Client → LB → API → Redis → DB fallback → 3xx redirect
```

### Decisions

**Code generation**

Options:

- random Base62
- sequence-based ID + Base62
- hash-based generation

Trade-off:

- random needs collision handling
- sequence-based is easy to reason about but may expose ordering
- deterministic hashes can have collision/truncation issues

**Cache**

Short-code → long URL is a strong cache candidate.

**Analytics**

Keep redirect path fast. Send analytics asynchronously.

### Scaling

```text
LB
 ↓
Stateless API × N
 ↓
Redis
 ↓
Read replicas / sharded DB
 ↓
Queue → analytics workers
```

[Back to Table of Contents](#table-of-contents)

---

<a id="rate-limiter-service"></a>

## Rate Limiter Service

### Requirements

Limit requests per:

- user
- IP
- API key
- endpoint

### Algorithms

- fixed window
- sliding window
- token bucket
- leaky bucket

### Distributed design

```text
Client
 ↓
Gateway
 ↓
Rate Limiter
 ↓
Redis / distributed state
 ↓
Backend
```

### Token bucket

State:

```text
tokens
last_refill_time
capacity
refill_rate
```

Decision:

```text
refill tokens
if tokens >= 1:
    consume
    allow
else:
    reject / delay
```

### Trade-off

A centralized limiter gives consistent global decisions but creates a network hop and dependency.

Local limiters are fast but can exceed the intended global limit across many instances.

[Back to Table of Contents](#table-of-contents)

---

<a id="authentication-system"></a>

## Authentication System

### Requirements

- registration
- login
- password reset
- session/token management
- logout/revocation
- optional MFA

### High-level flow

```text
Client
 ↓
Auth API
 ↓
User DB
 ↓
Session / Token Store
```

Add:

```text
Rate Limiter
Password hashing
Audit logs
Notification service
```

### Critical design decisions

- session vs token
- short-lived access token vs long-lived token
- refresh-token storage
- revocation model
- device/session management
- password reset token expiry

[Back to Table of Contents](#table-of-contents)

---

<a id="ticket-booking-system"></a>

## Ticket Booking System

A strong HLD practice problem because it forces concurrency reasoning.

```text
Client
 ↓
LB
 ↓
Booking Service
 ├── Seat Inventory
 ├── Payment
 └── Booking DB
```

### Core challenge

Two users must not successfully book the same seat.

Possible mechanisms:

- database row locking
- optimistic concurrency with version checks
- temporary seat holds
- unique constraints
- transactional booking

### Example decision

A seat can transition:

```text
AVAILABLE
→ HELD
→ BOOKED
```

A hold expires.

### Trade-off

Long lock durations reduce conflicts but hurt throughput.

Short holds improve user experience and throughput but require expiry handling.

[Back to Table of Contents](#table-of-contents)

---

<a id="spotify-like-music-streaming"></a>

## Spotify-Like Music Streaming

### Major components

```text
Client
 ↓
API / Auth
 ↓
Catalog Service
 ↓
Recommendation / Search
 ↓
CDN / Object Storage → audio segments
```

### Design ideas

- metadata in database
- audio files in object storage
- CDN for delivery
- asynchronous pipelines for transcoding
- event stream for playback analytics

### Trade-offs

Origin storage is centralized but creates bandwidth pressure.

CDN reduces origin load and geographic latency but adds cache-control complexity.

[Back to Table of Contents](#table-of-contents)

---

<a id="instagram-like-feed"></a>

## Instagram-Like Feed

### Core services

```text
Post Service
Feed Service
Media Service
User Graph
Notification Service
```

### Main scaling problem

Feed generation.

Use:

- fan-out on read
- fan-out on write
- hybrid approach

Celebrity accounts are the classic hot-key problem.

[Back to Table of Contents](#table-of-contents)

---

<a id="uber-like-ride-matching"></a>

## Uber-Like Ride Matching

Major components:

```text
Rider
Driver
Location Service
Matching Service
Trip Service
Pricing
Notification
```

The difficult requirement is low-latency geospatial matching.

Useful concepts:

- geospatial indexes
- partitioning by region/cell
- event streams
- real-time updates
- eventual consistency where acceptable

[Back to Table of Contents](#table-of-contents)

---

<a id="notification-system"></a>

## Notification System

Channels:

```text
Email
SMS
Push
In-app
```

Architecture:

```text
Producer
 ↓
Notification Queue
 ↓
Workers
 ├── Email Provider
 ├── SMS Provider
 └── Push Provider
```

Use separate retry and rate-limit policies per provider.

[Back to Table of Contents](#table-of-contents)

---

<a id="file-storage-and-sharing-system"></a>

## File Storage and Sharing System

Use:

```text
Metadata → DB
File bytes → Object Storage
Delivery → CDN / signed URLs
```

Do not route giant file bodies unnecessarily through application servers.

[Back to Table of Contents](#table-of-contents)

---

<a id="search-and-autocomplete"></a>

## Search and Autocomplete

Typical components:

```text
API
 ↓
Search Index
 ↓
Ranking
```

Autocomplete often needs:

- prefix index
- trie-like structures or search-engine indexes
- popularity signals
- caching

[Back to Table of Contents](#table-of-contents)

---

<a id="chat-system"></a>

## Chat System

Typical flow:

```text
Client
 ↓
Gateway
 ↓
WebSocket Service
 ↓
Message Service
 ↓
Message Store
 ↓
Notification Service
```

Questions:

- message ordering
- delivery semantics
- offline users
- reconnects
- unread counts
- fan-out

[Back to Table of Contents](#table-of-contents)

---

<a id="video-streaming-platform"></a>

## Video Streaming Platform

Typical architecture:

```text
Upload
 ↓
Object Storage
 ↓
Transcoding Queue
 ↓
Workers
 ↓
Multiple Encodings
 ↓
CDN
 ↓
Viewer
```

The application server should not perform every video transformation synchronously in the request path.

[Back to Table of Contents](#table-of-contents)

---

<a id="rag-ai-application"></a>

## RAG / AI Application

A useful personalized example:

```text
User
 ↓
API Gateway
 ↓
RAG Service
 ├── Cache
 ├── Retriever
 ├── Vector DB
 ├── Metadata DB
 └── LLM Provider
```

Asynchronous ingestion:

```text
Upload
 ↓
Object Storage
 ↓
Queue
 ↓
Parsing / Chunking
 ↓
Embedding
 ↓
Vector Store
```

Relevant trade-offs:

- synchronous vs asynchronous ingestion
- vector DB vs relational/vector extension
- cache query results vs fresh retrieval
- external LLM vs self-hosted model
- model latency vs quality
- duplicate ingestion handling

[Back to Table of Contents](#table-of-contents)

---

<a id="how-to-attack-an-unknown-design-problem"></a>

## How to Attack an Unknown Design Problem

This is the most important section for an unfamiliar interview question.

When the interviewer gives you a system you have never designed:

```text
1. Clarify
2. Estimate
3. Define APIs
4. Define data
5. Draw simple architecture
6. Find bottlenecks
7. Scale bottlenecks
8. Add reliability
9. Discuss trade-offs
```

Do not panic because the exact product is unfamiliar.

The underlying building blocks repeat.

[Back to Table of Contents](#table-of-contents)

---

<a id="requirement-questions-to-ask"></a>

## Requirement Questions to Ask

Ask:

### Users

- Who uses the system?
- How many users?

### Core operations

- Read-heavy or write-heavy?
- Real-time or asynchronous?

### Data

- What data must be durable?
- How much data?

### Performance

- Latency target?
- Peak traffic?

### Reliability

- What happens during dependency failure?

### Consistency

- Is stale data acceptable?

These questions turn a vague problem into constraints.

[Back to Table of Contents](#table-of-contents)

---

<a id="capacity-estimation-template"></a>

## Capacity Estimation Template

Write:

```text
DAU =
requests/user/day =
average RPS =
peak multiplier =
peak RPS =
average payload =
bandwidth =
daily storage =
annual storage =
```

Then ask:

> Which component becomes the bottleneck first?

[Back to Table of Contents](#table-of-contents)

---

<a id="api-and-data-model-sketch"></a>

## API and Data Model Sketch

Before drawing 20 boxes, identify:

```text
POST /...
GET /...
PUT /...
DELETE /...
```

Then identify core entities.

Example booking:

```text
User
Show
Seat
Hold
Booking
Payment
```

This reveals data relationships and concurrency constraints.

[Back to Table of Contents](#table-of-contents)

---

<a id="first-architecture-diagram"></a>

## First Architecture Diagram

Start small:

```text
Client
 ↓
Load Balancer
 ↓
Stateless API
 ↓
Database
```

Then evolve:

```text
Client
 ↓
CDN / LB
 ↓
API
 ├── Cache
 ├── Primary DB
 ├── Read Replicas
 └── Queue → Workers
```

Only add components after identifying the problem they solve.

[Back to Table of Contents](#table-of-contents)

---

<a id="bottleneck-discovery"></a>

## Bottleneck Discovery

Common bottlenecks:

```text
CPU
Memory
Database
Network
Lock contention
Hot partition
Queue backlog
External dependency
Connection pool
```

Do not say “we need Kafka” until you know which bottleneck asynchronous processing is solving.

[Back to Table of Contents](#table-of-contents)

---

<a id="failure-scenario-analysis"></a>

## Failure Scenario Analysis

For each major component ask:

```text
What if it becomes slow?
What if it returns errors?
What if it disappears?
What if it returns stale data?
What if traffic doubles?
What if traffic spikes 20×?
```

Then decide:

- retry?
- timeout?
- circuit breaker?
- fallback?
- queue?
- replica?
- failover?
- degradation?

[Back to Table of Contents](#table-of-contents)

---

<a id="trade-off-explanation-framework"></a>

## Trade-Off Explanation Framework

Use this sentence structure:

> “I choose **X** because the workload requires **A**. The benefit is **B**. The cost is **C**. If the workload changes toward **D**, I would switch toward **Y**.”

### Example

> “I would use Redis for hot URL lookups because reads dominate and latency matters. The trade-off is cache invalidation and an additional dependency. If the dataset no longer fits comfortably in memory, I would rely more heavily on database replicas and cache only the hottest entries.”

This is the reasoning style the interviewer is looking for.

[Back to Table of Contents](#table-of-contents)

---

<a id="how-to-explain-a-design-on-a-whiteboard"></a>

## How to Explain a Design on a Whiteboard

Use this drawing order:

```text
1. Client
2. Entry point
3. Core service
4. Primary datastore
5. Cache
6. Queue / workers
7. Secondary systems
8. Reliability mechanisms
```

Then narrate the request path from left to right.

Do not draw every possible component.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-the-interviewer-is-actually-evaluating"></a>

## What the Interviewer Is Actually Evaluating

A strong HLD response demonstrates:

- requirement clarification
- decomposition
- sensible component selection
- scale awareness
- bottleneck recognition
- failure reasoning
- consistency understanding
- trade-off reasoning
- ability to communicate clearly

The exact technology name is less important than the reason it exists.

[Back to Table of Contents](#table-of-contents)

---

<a id="common-hld-follow-up-questions"></a>

## Common HLD Follow-Up Questions

Expect questions such as:

- Why Redis?
- Why not just use the database cache?
- Why Kafka instead of RabbitMQ?
- Why SQL instead of MongoDB?
- Why not keep this synchronous?
- What happens if the queue is down?
- What happens if Redis is down?
- What happens if the database becomes read-hot?
- How do you handle duplicate messages?
- How do you prevent double booking?
- How do you scale a single hot key?
- What if one region fails?
- Where does TLS terminate?
- How does the load balancer choose a server?
- Why L4 instead of L7?
- How do you detect unhealthy servers?
- How do you preserve ordering?
- What consistency do you need?
- How do you handle retries safely?
- Where is the single point of failure?
- What would you change at 10× traffic?

[Back to Table of Contents](#table-of-contents)

---

<a id="common-hld-mistakes"></a>

## Common HLD Mistakes

### 1. Tool-first design

> “Let's use Kafka.”

Instead:

> “The work is asynchronous and bursty, so a durable queue is useful.”

### 2. Overengineering immediately

Start simple and scale only where needed.

### 3. Ignoring failures

Every network call can fail.

### 4. Ignoring data semantics

Ask whether data can be stale, duplicated, reordered, or lost.

### 5. Confusing components

Know exactly what Redis, Kafka, RabbitMQ, CDN, API gateway, load balancer, object storage, and database each solve.

### 6. No trade-off discussion

Every major architectural choice should have a reason and a cost.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-hld-revision"></a>

## 30-Second HLD Revision

```text
Requirements
↓
Scale
↓
API + data model
↓
Simple architecture
↓
Load balancing
↓
Cache
↓
Database
↓
Queue
↓
Workers
↓
Replication / partitioning
↓
Failure handling
↓
Observability
↓
Security
↓
Trade-offs
```

### Component memory

```text
LB      → distribute traffic
Gateway → API entry/policy
Redis   → fast shared state/cache
SQL     → transactions/relations
NoSQL   → workload-specific horizontal scale/flexible models
Kafka   → durable event stream/replay
Rabbit  → brokered work/routing
CDN     → edge delivery/cache
Queue   → decouple/buffer
Worker  → asynchronous processing
Object  → large blobs
Replica → read/failover capacity
Shard   → partition data
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-hld-interview-checklist"></a>

## Final HLD Interview Checklist

### Fundamentals

- [ ] HLD vs LLD
- [ ] Functional vs non-functional requirements
- [ ] capacity estimation
- [ ] latency / throughput
- [ ] availability / durability
- [ ] CAP
- [ ] consistency models

### Core components

- [ ] load balancer
- [ ] load-balancing algorithms
- [ ] reverse proxy
- [ ] API gateway
- [ ] service discovery
- [ ] health checks
- [ ] stateless services
- [ ] queues
- [ ] workers

### Databases

- [ ] SQL vs NoSQL
- [ ] relational
- [ ] document
- [ ] key-value
- [ ] wide-column
- [ ] graph
- [ ] object storage
- [ ] indexes
- [ ] replication
- [ ] read replicas
- [ ] sharding
- [ ] partition keys
- [ ] consistent hashing

### Caching

- [ ] Redis
- [ ] cache-aside
- [ ] read-through
- [ ] write-through
- [ ] write-back
- [ ] eviction
- [ ] invalidation
- [ ] cache stampede
- [ ] hot keys
- [ ] CDN

### Messaging

- [ ] RabbitMQ
- [ ] Kafka
- [ ] pub-sub
- [ ] consumer groups
- [ ] delivery semantics
- [ ] retries
- [ ] DLQ
- [ ] ordering
- [ ] backpressure
- [ ] outbox

### Reliability

- [ ] timeouts
- [ ] retries
- [ ] jitter
- [ ] circuit breaker
- [ ] bulkhead
- [ ] rate limiting
- [ ] idempotency
- [ ] distributed locks
- [ ] leader election
- [ ] graceful degradation

### Design questions

- [ ] URL shortener
- [ ] rate limiter
- [ ] authentication
- [ ] booking
- [ ] feed
- [ ] music streaming
- [ ] ride matching
- [ ] notification
- [ ] file storage
- [ ] search
- [ ] chat
- [ ] video streaming
- [ ] RAG / AI system

### Unfamiliar systems

- [ ] clarify requirements
- [ ] estimate scale
- [ ] identify core APIs
- [ ] identify entities
- [ ] draw simple architecture
- [ ] find bottleneck
- [ ] scale bottleneck
- [ ] analyze failures
- [ ] discuss consistency
- [ ] explain trade-offs

### Interview execution

- [ ] Do not start with technologies.
- [ ] State assumptions.
- [ ] Draw the request path.
- [ ] Explain why each component exists.
- [ ] Compare plausible alternatives.
- [ ] Explain what happens when dependencies fail.
- [ ] Explain how the system changes at 10× scale.
- [ ] Design unfamiliar systems from first principles.

[Back to Table of Contents](#table-of-contents)
