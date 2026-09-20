# Software Engineering Interview Notes

> **Purpose:** A structured Software Engineering layer for the Infosys SP/DSE technical interview.
>
> This file complements the OOP, OS, CN, SQL/DBMS, Python, FastAPI, LLD and HLD notes. It focuses on the engineering concepts that connect software fundamentals with real-world development, APIs, delivery and production.

<a id="table-of-contents"></a>

##  Table of Contents

###  Part 1 — Software Engineering Foundations
- [Software Engineering](#software-engineering)
- [SDLC](#sdlc)
- [SDLC Models](#sdlc-models)
- [Agile and Scrum](#agile-and-scrum)
- [Requirements Engineering](#requirements-engineering)
- [Functional vs Non-Functional Requirements](#functional-vs-non-functional-requirements)
- [User Stories and Acceptance Criteria](#user-stories-and-acceptance-criteria)

###  Part 2 — APIs and API Engineering
- [What Is an API?](#what-is-an-api)
- [Different Types of APIs](#different-types-of-apis)
- [REST API](#rest-api)
- [SOAP API](#soap-api)
- [GraphQL API](#graphql-api)
- [gRPC / RPC APIs](#grpc--rpc-apis)
- [WebSocket API](#websocket-api)
- [Webhooks](#webhooks)
- [Server-Sent Events](#server-sent-events)
- [Library / SDK APIs](#library--sdk-apis)
- [API Type Comparison](#api-type-comparison)
- [REST Interview Essentials](#rest-interview-essentials)
- [API Request and Response](#api-request-and-response)
- [HTTP Methods](#http-methods)
- [HTTP Status Codes](#http-status-codes)
- [API Parameters](#api-parameters)
- [API Design Principles](#api-design-principles)
- [Pagination, Filtering and Sorting](#pagination-filtering-and-sorting)
- [API Versioning](#api-versioning)
- [API Error Handling](#api-error-handling)
- [Idempotency](#idempotency)
- [API Authentication and Authorization](#api-authentication-and-authorization)
- [API Security](#api-security)
- [API Gateway](#api-gateway)
- [Reverse Proxy vs Load Balancer vs API Gateway](#reverse-proxy-vs-load-balancer-vs-api-gateway)
- [API Reliability](#api-reliability)
- [API Documentation and OpenAPI](#api-documentation-and-openapi)
- [API Testing](#api-testing)

###  Part 3 — Testing and Quality
- [STLC](#stlc)
- [Testing Levels](#testing-levels)
- [Testing Types](#testing-types)
- [Unit vs Integration vs E2E](#unit-vs-integration-vs-e2e)
- [Contract Testing](#contract-testing)
- [Test Case Thinking](#test-case-thinking)

###  Part 4 — Git, Collaboration and CI/CD
- [Git and Version Control](#git-and-version-control)
- [Merge vs Rebase](#merge-vs-rebase)
- [Pull Requests and Code Review](#pull-requests-and-code-review)
- [Branching Strategies](#branching-strategies)
- [CI/CD](#cicd)
- [Build → Test → Deploy Pipeline](#build--test--deploy-pipeline)
- [Environments and Configuration](#environments-and-configuration)
- [Release Strategies](#release-strategies)

###  Part 5 — Architecture and Design
- [Monolith vs Modular Monolith vs Microservices](#monolith-vs-modular-monolith-vs-microservices)
- [Layered Architecture](#layered-architecture)
- [Event-Driven Architecture](#event-driven-architecture)
- [Message Queues and Pub/Sub](#message-queues-and-pubsub)
- [Clean Architecture and Separation of Concerns](#clean-architecture-and-separation-of-concerns)
- [Coupling and Cohesion](#coupling-and-cohesion)
- [SOLID, DRY, KISS and YAGNI](#solid-dry-kiss-and-yagni)

###  Part 6 — Production Engineering
- [Logging](#logging)
- [Monitoring and Metrics](#monitoring-and-metrics)
- [Observability and Tracing](#observability-and-tracing)
- [Health Checks](#health-checks)
- [Timeouts, Retries and Circuit Breakers](#timeouts-retries-and-circuit-breakers)
- [Graceful Shutdown](#graceful-shutdown)
- [Performance and Profiling](#performance-and-profiling)
- [Caching](#caching)
- [Database Connection Pooling](#database-connection-pooling)
- [Docker and Container Basics](#docker-and-container-basics)

###  Part 7 — Security
- [Authentication vs Authorization](#authentication-vs-authorization)
- [Sessions vs JWT](#sessions-vs-jwt)
- [OAuth 2.0](#oauth-20)
- [RBAC and Access Control](#rbac-and-access-control)
- [CORS, CSRF and XSS](#cors-csrf-and-xss)
- [Secrets and Least Privilege](#secrets-and-least-privilege)

###  Part 8 — Documentation and Engineering Practices
- [UML Diagrams You Should Recognize](#uml-diagrams-you-should-recognize)
- [API Documentation](#api-documentation)
- [Architecture Decision Records](#architecture-decision-records)
- [Maintenance, Refactoring and Technical Debt](#maintenance-refactoring-and-technical-debt)
- [Backward Compatibility and Deprecation](#backward-compatibility-and-deprecation)

###  Part 9 — Infosys Interview Execution
- [Generic Software Engineering Q&A](#generic-software-engineering-qa)
- [API Interview Q&A](#api-interview-qa)
- [Infosys-Focused Questions](#infosys-focused-questions)
- [Project-Based Questions](#project-based-questions)
- [Scenario Questions](#scenario-questions)
- [Interview Traps](#interview-traps)
- [Final Interview Checklist](#final-interview-checklist)

---

# Software Engineering Foundations

<a id="software-engineering"></a>
## Software Engineering

Software engineering is the disciplined process of understanding a problem, designing software, implementing it, testing it, deploying it, operating it and maintaining it.

### Mental model

```
Requirement
    ↓
Design
    ↓
Code
    ↓
Test
    ↓
Review
    ↓
Build
    ↓
Deploy
    ↓
Monitor
    ↓
Maintain
```

### Interview answer

> Software engineering is not only coding. It covers the complete lifecycle of building and maintaining reliable software.

### Simple example

A student portal needs requirements, database/API design, implementation, testing, deployment and maintenance.

[Back to Table of Contents](#table-of-contents)

---

<a id="sdlc"></a>
## SDLC

**SDLC = Software Development Life Cycle.**

### Typical flow

```
Requirements
    ↓
Analysis
    ↓
Design
    ↓
Implementation
    ↓
Testing
    ↓
Deployment
    ↓
Maintenance
```

The exact order varies by methodology; modern teams often iterate through these activities.

### SceneFlow example

```
Requirement
    ↓
Architecture / API / DB design
    ↓
FastAPI + React + workers
    ↓
Testing
    ↓
Deployment
    ↓
Monitoring + maintenance
```

### High-value questions

**What is SDLC?**

> SDLC is the lifecycle used to take software from requirements through design, implementation, testing, deployment and maintenance.

**Why is SDLC needed?**

> It gives the team a structured way to manage requirements, development, quality and maintenance.

**Does testing happen only at the end?**

> No. Modern development uses testing and feedback throughout the lifecycle.

[Back to Table of Contents](#table-of-contents)

---

<a id="sdlc-models"></a>
## SDLC Models

Know the purpose and trade-offs of these models.

| Model | Core idea | Typical context |
|---|---|---|
| Waterfall | Sequential phases | Stable requirements |
| V-Model | Development paired with testing | Strong verification focus |
| Iterative | Repeated refinement | Evolving requirements |
| Incremental | Deliver functionality in pieces | Early usable releases |
| Spiral | Iteration + risk analysis | Higher-risk projects |
| Agile | Short feedback-driven cycles | Frequently changing requirements |

### Waterfall

```
Requirements
    ↓
Design
    ↓
Development
    ↓
Testing
    ↓
Deployment
```

### V-Model

Development activities are paired with corresponding verification/testing activities.

### Iterative

Build → learn → refine → repeat.

### Incremental

Deliver the product as multiple usable pieces.

### Spiral

Iterate while explicitly analyzing risk.

### Interview question

**Waterfall vs Agile?**

> Waterfall emphasizes sequential planning and phase progression. Agile emphasizes shorter feedback cycles, incremental delivery and adaptation.

[Back to Table of Contents](#table-of-contents)

---

<a id="agile-and-scrum"></a>
## Agile and Scrum

**Agile** is a broad approach emphasizing feedback, collaboration, incremental delivery and adaptation.

**Scrum** is a specific framework commonly used to organize Agile development.

### Scrum accountabilities

- Product Owner
- Scrum Master
- Developers

### Scrum artifacts

- Product Backlog
- Sprint Backlog
- Increment

### Scrum events

- Sprint
- Sprint Planning
- Daily Scrum
- Sprint Review
- Sprint Retrospective

### Simple example

```
Sprint 1 → Authentication
Sprint 2 → Profiles
Sprint 3 → Reporting
Sprint 4 → Improvements
```

### Interview trap

Agile is broader than Scrum. Scrum is not synonymous with Agile.

[Back to Table of Contents](#table-of-contents)

---

<a id="requirements-engineering"></a>
## Requirements Engineering

Requirements engineering is the process of discovering, analyzing, documenting, validating and managing what a system must do.

### Flow

```
Elicit
  ↓
Analyze
  ↓
Specify
  ↓
Validate
  ↓
Manage changes
```

### Questions to ask

- Who is the user?
- What problem are we solving?
- What inputs are valid?
- What happens on failure?
- What scale is expected?
- What security constraints exist?

### Interview point

A technically correct implementation can still fail if the requirement is misunderstood.

[Back to Table of Contents](#table-of-contents)

---

<a id="functional-vs-non-functional-requirements"></a>
## Functional vs Non-Functional Requirements

### Functional requirement

Describes **what the system does**.

Examples:
- User can sign in.
- User can create a scene.
- User can shorten a URL.

### Non-functional requirement

Describes **how well or under what constraints** the system works.

Examples:
- latency
- availability
- security
- scalability
- maintainability

### URL Shortener example

**Functional:** Create a short URL and redirect from it.

**Non-functional:** Redirects should have low latency and the service should tolerate traffic spikes.

### Interview answer

> Functional requirements describe behavior; non-functional requirements describe quality attributes and constraints.

[Back to Table of Contents](#table-of-contents)

---

<a id="user-stories-and-acceptance-criteria"></a>
## User Stories and Acceptance Criteria

### User story

> As a user, I want to create a shortened URL so that I can share a compact link.

### Acceptance criteria

```
Given a valid URL
When the user submits it
Then a unique short code is returned
```

Good acceptance criteria should be observable and testable.

### Interview question

**Requirement vs acceptance criterion?**

> A requirement expresses what is needed; acceptance criteria define the concrete conditions that demonstrate the requirement is satisfied.

[Back to Table of Contents](#table-of-contents)

---

# APIs and API Engineering

<a id="what-is-an-api"></a>
## What Is an API?

**API = Application Programming Interface.**

An API is a defined interface/contract through which software components interact.

### Mental model

```
Caller
  ↓
Contract
  ↓
Provider
  ↓
Result
```

The contract may define:
- operations
- inputs
- outputs
- errors
- authentication
- authorization
- semantics

### Important

An API does **not** require REST or HTTP.

Examples:

```
React → FastAPI
FastAPI → Gemini
FastAPI → PostgreSQL driver
Python code → library function
```

### Interview answer

> An API is a defined contract through which software components communicate. REST is only one way to design a network API.

[Back to Table of Contents](#table-of-contents)

---

<a id="different-types-of-apis"></a>
## Different Types of APIs

This is one of the most important additions because **API does not mean REST only**.

| API type | Main idea | Practical use |
|---|---|---|
| REST | Resource-oriented HTTP API | General web/backend APIs |
| SOAP | Formal XML messaging protocol | Enterprise integrations |
| GraphQL | Client requests fields through a schema | Flexible frontend APIs |
| gRPC / RPC | Remote procedure calls with typed contracts | Internal services |
| WebSocket | Persistent bidirectional channel | Chat/live systems |
| Webhook | HTTP callback triggered by an event | Payment/provider events |
| SSE | Server → client event stream | Notifications/progress |
| Library / SDK API | In-process interface | Reusable code |

### Interview taxonomy

Do not treat all of these as exactly the same category.

```
Common API interaction styles
    ├── REST
    ├── GraphQL
    └── RPC

Communication mechanisms
    ├── HTTP
    └── WebSocket

Interface/protocol technologies
    ├── SOAP
    └── gRPC

Event callback pattern
    └── Webhook
```

The taxonomy can vary by context. In an interview, explain the communication model and use case.

[Back to Table of Contents](#table-of-contents)

---

<a id="rest-api"></a>
## REST API

**REST = Representational State Transfer.**

REST is an architectural style commonly implemented using HTTP.

### Core ideas

- resources
- standard HTTP semantics
- stateless requests
- representations such as JSON
- cacheability where applicable
- uniform interface

### Example

```http
GET    /users/42
POST   /users
PATCH  /users/42
DELETE /users/42
```

### FastAPI example

```python
@app.get("/users/{user_id}")
async def get_user(user_id: int):
    return {"id": user_id}
```

### Interview answer

> REST is a resource-oriented architectural style commonly implemented over HTTP. Not every HTTP/JSON API is fully RESTful.

[Back to Table of Contents](#table-of-contents)

---

<a id="soap-api"></a>
## SOAP API

**SOAP** is a protocol for structured messages, commonly represented using XML.

### Know these terms

- Envelope
- Header
- Body
- WSDL
- XML Schema
- Fault
- Enterprise security standards where relevant

### Simple example

```xml
<soap:Envelope>
  <soap:Body>
    <GetCustomer>
      <CustomerId>42</CustomerId>
    </GetCustomer>
  </soap:Body>
</soap:Envelope>
```

### Practical example

A legacy enterprise/banking integration can expose a SOAP operation described by WSDL.

### Interview answer

> SOAP is a formal structured messaging protocol, commonly XML-based. REST is an architectural style commonly built around HTTP semantics.

[Back to Table of Contents](#table-of-contents)

---

<a id="graphql-api"></a>
## GraphQL API

GraphQL provides a schema through which clients request the fields they need.

### Example

```graphql
query {
  user(id: 42) {
    name
    email
    projects {
      name
    }
  }
}
```

### Strengths

- client controls response shape
- strong schema
- related data can be requested together
- can reduce under-fetching

### Trade-offs

- resolver complexity
- N+1 query risk
- more complex caching
- query-cost/abuse controls
- field-level authorization can be nuanced

### Interview answer

> GraphQL is useful when clients need flexible data shapes. The trade-off is more server-side query and caching complexity.

[Back to Table of Contents](#table-of-contents)

---

<a id="grpc--rpc-apis"></a>
## gRPC / RPC APIs

**RPC = Remote Procedure Call.**

The client invokes a remote operation conceptually like a function:

```
getUser(42)
```

**gRPC** is a popular RPC framework commonly using:

- Protocol Buffers
- generated client/server code
- HTTP/2
- strongly typed contracts
- streaming

### Example

```protobuf
service UserService {
  rpc GetUser(GetUserRequest) returns (User);
}
```

### Practical use

Internal service-to-service communication.

### Interview answer

> REST commonly models resources. RPC models operations. gRPC is useful for strongly typed and efficient service-to-service communication.

[Back to Table of Contents](#table-of-contents)

---

<a id="websocket-api"></a>
## WebSocket API

WebSocket provides a persistent bidirectional connection.

### HTTP

```
Client → request
Server → response
```

### WebSocket

```
Client ↔ persistent connection ↔ Server
```

### Use cases

- chat
- live sports
- collaboration
- live dashboards

### ScoreHub connection

WebSockets can push live score updates instead of repeated polling.

### Trap

WebSocket is not simply “faster REST”. It solves a different communication pattern.

[Back to Table of Contents](#table-of-contents)

---

<a id="webhooks"></a>
## Webhooks

A webhook is an HTTP callback sent when an event occurs.

### Example

```
Payment succeeds
      ↓
Payment provider
      ↓
POST /webhooks/payment
      ↓
Your backend
```

### Receiver responsibilities

1. Verify authenticity.
2. Validate the payload.
3. Handle duplicate delivery.
4. Acknowledge quickly.
5. Queue slow work when appropriate.

### Webhook vs polling

**Polling:** consumer repeatedly asks for changes.

**Webhook:** producer pushes an event.

[Back to Table of Contents](#table-of-contents)

---

<a id="server-sent-events"></a>
## Server-Sent Events

SSE provides a server-to-client event stream over HTTP.

```
Client
  ↓ HTTP connection
Server
  ↓
event
event
event
```

### Good use cases

- notifications
- progress updates
- streaming status
- server-generated feeds

### SSE vs WebSocket

| SSE | WebSocket |
|---|---|
| Server → client | Bidirectional |
| HTTP streaming | Persistent WebSocket connection |
| Simpler for one-way updates | Better for two-way interaction |

[Back to Table of Contents](#table-of-contents)

---

<a id="library--sdk-apis"></a>
## Library / SDK APIs

An API does not need to be a network endpoint.

### Library API

```python
from datetime import datetime

now = datetime.now()
```

### SDK API

```python
client.create_payment(...)
```

### Interview line

> API means a defined interface/contract. HTTP is only one way to expose an API.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-type-comparison"></a>
## API Type Comparison

| Technology | Communication model | Typical use | Main consideration |
|---|---|---|---|
| REST | HTTP request/response | Public/web APIs | Broad compatibility |
| SOAP | Structured XML messaging | Enterprise integration | Formal standards |
| GraphQL | Schema-driven queries | Flexible frontend data | Query complexity |
| gRPC | Typed RPC | Internal services | Contract/tooling |
| WebSocket | Persistent bidirectional | Chat/live systems | Connection management |
| Webhook | Event callback | Provider events | Duplicates/retries |
| SSE | Server push over HTTP | Notifications/status | One-way only |
| SDK/Library | In-process call | Reusable functionality | Not network communication |

### Interview rule

Do not say “X is always best”.

Say:

> I would choose based on consumers, data shape, latency, compatibility, coupling and operational requirements.

[Back to Table of Contents](#table-of-contents)

---

<a id="rest-interview-essentials"></a>
## REST Interview Essentials

### HTTP method semantics

| Method | Typical use | Safe? | Idempotent? |
|---|---|---:|---:|
| GET | Retrieve | Yes | Yes |
| POST | Create/action | No | No |
| PUT | Replace/create at known URI | No | Yes |
| PATCH | Partial update | No | Not inherently |
| DELETE | Delete | No | Yes |

### High-value status codes

```
200 OK
201 Created
202 Accepted
204 No Content

400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
409 Conflict
422 Validation-related error
429 Too Many Requests

500 Internal Server Error
502 Bad Gateway
503 Service Unavailable
504 Gateway Timeout
```

### 401 vs 403

**401:** authentication is missing or invalid.

**403:** the request is not permitted.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-request-and-response"></a>
## API Request and Response

### Request

```
Method
URL
Headers
Path/query parameters
Body
```

### Response

```
Status code
Headers
Body
```

### Example

```http
POST /api/v1/short-urls
Authorization: Bearer <token>
Content-Type: application/json

{"url":"https://example.com"}
```

Response:

```http
201 Created

{"short_code":"aB91x","url":"https://example.com"}
```

[Back to Table of Contents](#table-of-contents)

---

<a id="http-methods"></a>
## HTTP Methods

### GET
Retrieve a representation.

### POST
Create a resource or trigger an operation.

### PUT
Replace a representation at a known URI.

### PATCH
Apply a partial modification.

### DELETE
Remove a resource.

### Interview question

**Does PUT require parameters?**

**Answer:** The API contract decides. A typical endpoint can use a path parameter plus a request body:

```http
PUT /users/42

{
  "name": "Sai",
  "email": "sai@example.com"
}
```

[Back to Table of Contents](#table-of-contents)

---

<a id="http-status-codes"></a>
## HTTP Status Codes

Know the meaning, not just the number.

- **200** — successful request
- **201** — resource created
- **202** — accepted for processing
- **204** — successful response with no content
- **400** — invalid request
- **401** — authentication problem
- **403** — access forbidden
- **404** — resource not found
- **409** — conflict
- **422** — validation/content problem in common API usage
- **429** — rate limited
- **500** — server failure
- **502** — bad gateway
- **503** — service unavailable
- **504** — gateway timeout

[Back to Table of Contents](#table-of-contents)

---

<a id="api-parameters"></a>
## API Parameters

### Path parameter

Identifies a resource:

```
/users/42
```

### Query parameter

Filtering/options:

```
/users?role=admin&limit=20
```

### Header

Request metadata:

```
Authorization: Bearer ...
```

### Body

Structured input:

```json
{"name":"Sai"}
```

### Interview trap

“Parameter” does not mean only query parameters.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-design-principles"></a>
## API Design Principles

A production API should have:

```
Clear resource naming
        ↓
Explicit request/response contracts
        ↓
Validation
        ↓
Consistent status codes
        ↓
Predictable errors
        ↓
Authentication / authorization
        ↓
Pagination
        ↓
Idempotency where needed
        ↓
Versioning
        ↓
Documentation
```

### Example

```
GET /users/42
```

is usually clearer as a resource-oriented endpoint than:

```
GET /getUserById?id=42
```

[Back to Table of Contents](#table-of-contents)

---

<a id="pagination-filtering-and-sorting"></a>
## Pagination, Filtering and Sorting

Do not assume collections are small.

### Offset pagination

```
GET /users?offset=100&limit=20
```

Simple, but large offsets can become expensive and changing datasets can shift results.

### Cursor pagination

```
GET /users?cursor=abc&limit=20
```

Useful for large or frequently changing ordered datasets.

Also know:

- filtering
- sorting
- searching
- maximum page size

### Interview point

Pagination is both an API-design concern and a database-performance concern.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-versioning"></a>
## API Versioning

Versioning protects consumers from breaking changes.

### Common approach

```
/api/v1/users
```

### Breaking changes

- removing a field
- changing a field type
- changing semantics
- removing an endpoint

### Good evolution

Prefer additive/backward-compatible changes when practical.

**Interview line:** Versioning is a compatibility strategy, not merely a URL convention.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-error-handling"></a>
## API Error Handling

Use predictable, machine-readable errors.

### Example

```json
{
  "error": {
    "code": "INVALID_SCENE",
    "message": "Scene script is required",
    "request_id": "req_123"
  }
}
```

### Good practices

- stable error code
- useful message
- field-level details where useful
- request/correlation ID
- no stack traces or secrets

### FastAPI connection

Pydantic validation errors and `HTTPException` are part of the API error contract.

[Back to Table of Contents](#table-of-contents)

---

<a id="idempotency"></a>
## Idempotency

An operation is idempotent when repeating it has the same intended final effect as doing it once.

### Example

```http
PUT /users/42
```

For retry-sensitive POST operations:

```http
Idempotency-Key: abc123
```

The server can store the key/result and prevent unintended duplicate effects.

### SceneFlow

Repeated client retries should not create duplicate expensive image-search jobs.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-authentication-and-authorization"></a>
## API Authentication and Authorization

**Authentication:** Who are you?

**Authorization:** What are you allowed to do?

### Request flow

```
Request
  ↓
Authenticate
  ↓
Identify caller
  ↓
Load resource
  ↓
Authorize
  ↓
Response
```

**SceneFlow:** Being logged in does not automatically grant access to every project.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-security"></a>
## API Security

High-value points:

- HTTPS/TLS
- password hashing
- input validation
- parameterized DB access
- server-side authorization
- rate limiting
- secret management
- safe file uploads
- controlled error responses
- audit logging
- least privilege

### Interview answer

> API security is layered. Authentication alone does not secure every endpoint.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-gateway"></a>
## API Gateway

An API gateway is an API-facing entry point in a distributed architecture.

Possible responsibilities:

- routing
- authentication/policy enforcement
- rate limiting
- request transformation
- observability

### Example

```
Client
  ↓
API Gateway
  ├── User Service
  ├── Order Service
  └── Payment Service
```

**Trap:** Do not automatically equate an API gateway with a load balancer.

[Back to Table of Contents](#table-of-contents)

---

<a id="reverse-proxy-vs-load-balancer-vs-api-gateway"></a>
## Reverse Proxy vs Load Balancer vs API Gateway

### Reverse proxy

Receives requests on behalf of backend servers.

### Load balancer

Distributes requests among backend instances/targets.

### API gateway

Adds API-oriented routing and policy capabilities such as auth, quotas and transformations.

They can be separate components or combined in one infrastructure product.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-reliability"></a>
## API Reliability

Production API reliability includes:

- timeouts
- bounded retries
- exponential backoff
- jitter
- circuit breakers
- idempotency
- rate limiting
- backpressure
- health checks
- observability

### Example

```
FastAPI
   ↓
Third-party API
   ↓
Timeout
   ↓
Bounded retry + backoff
   ↓
Fallback / controlled error
```

**Retry trap:** Retrying blindly can duplicate side effects or amplify an outage.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-documentation-and-openapi"></a>
## API Documentation and OpenAPI

**OpenAPI** is a machine-readable description of an HTTP API.

It can describe:

- endpoints
- methods
- parameters
- request schemas
- response schemas
- security schemes

FastAPI generates OpenAPI documentation automatically.

Common endpoints:

```
/docs
/redoc
/openapi.json
```

**Interview answer:** OpenAPI acts as a machine-readable API contract that can drive documentation and tooling.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-testing"></a>
## API Testing

Test more than the happy path.

```
Valid request
Invalid input
Unauthorized
Forbidden
Not found
Conflict
Rate limited
Downstream failure
Timeout
Duplicate request
Edge cases
```

Useful levels:

- unit
- integration
- contract
- E2E

### SceneFlow example

Test scene creation for:
- valid data
- validation failure
- unauthorized user
- duplicate request
- database failure

[Back to Table of Contents](#table-of-contents)

---

# Testing and Quality

<a id="stlc"></a>
## STLC

**STLC = Software Testing Life Cycle.**

### Practical flow

```
Requirement analysis
   ↓
Test planning
   ↓
Test design
   ↓
Environment setup
   ↓
Execution
   ↓
Defect reporting
   ↓
Retesting / regression
   ↓
Closure
```

**SDLC vs STLC**

- SDLC = overall software lifecycle.
- STLC = testing-focused activities.

[Back to Table of Contents](#table-of-contents)

---

<a id="testing-levels"></a>
## Testing Levels

### Unit testing
Tests a small component in isolation.

### Integration testing
Tests interactions between components.

### System testing
Tests the complete application.

### End-to-end testing
Tests a realistic user journey across the whole system.

[Back to Table of Contents](#table-of-contents)

---

<a id="testing-types"></a>
## Testing Types

Know:

- **Smoke testing** — quick validation that a build is usable.
- **Sanity testing** — focused verification after a targeted change.
- **Regression testing** — verify existing behavior after changes.
- **Black-box testing** — based on external behavior.
- **White-box testing** — uses knowledge of internal implementation.
- **Load testing** — expected workload.
- **Stress testing** — beyond expected capacity.
- **Spike testing** — sudden workload change.
- **Soak testing** — long-duration workload.
- **Contract testing** — verify producer/consumer agreement.

[Back to Table of Contents](#table-of-contents)

---

<a id="unit-vs-integration-vs-e2e"></a>
## Unit vs Integration vs E2E

| Type | Scope | Strength | Cost |
|---|---|---|---|
| Unit | Small component | Fast and focused | Low |
| Integration | Component interaction | Finds integration failures | Medium |
| E2E | Full user journey | High system confidence | High |

### Interview answer

> These levels complement each other. Unit tests are fast, integration tests validate boundaries, and E2E tests validate important user flows.

[Back to Table of Contents](#table-of-contents)

---

<a id="contract-testing"></a>
## Contract Testing

Contract testing checks whether communicating systems agree on an API contract.

### Example

A consumer expects:

```json
{"id": 42}
```

The provider changes `id` to a string.

A contract test can detect this breaking change before deployment.

Useful when independently deployed services evolve separately.

[Back to Table of Contents](#table-of-contents)

---

<a id="test-case-thinking"></a>
## Test Case Thinking

For an endpoint or feature, think:

```
Happy path
   ↓
Invalid input
   ↓
Missing input
   ↓
Boundary values
   ↓
Unauthorized
   ↓
Forbidden
   ↓
Not found
   ↓
Conflict
   ↓
Dependency failure
   ↓
Retry / duplicate request
   ↓
Concurrency
```

This is highly useful during project-defense questions.

[Back to Table of Contents](#table-of-contents)

---

# Git, Collaboration and CI/CD

<a id="git-and-version-control"></a>
## Git and Version Control

Know:

```
clone
status
add
commit
pull
push
branch
switch
merge
rebase
stash
cherry-pick
revert
reset
diff
log
```

### Mental model

```
Working tree
    ↓ git add
Staging area
    ↓ git commit
Local repository
    ↓ git push
Remote repository
```

### Important distinction

- `git revert` creates a new commit that undoes an earlier commit.
- `git reset` moves the branch pointer and can rewrite history.

[Back to Table of Contents](#table-of-contents)

---

<a id="merge-vs-rebase"></a>
## Merge vs Rebase

### Merge

Combines histories and may create a merge commit.

### Rebase

Replays commits onto a new base and rewrites commit history.

**Important:** Rebasing already-shared commits can create coordination problems.

### Interview answer

> Neither is universally better. Use the team's agreed workflow and be careful about rewriting shared history.

[Back to Table of Contents](#table-of-contents)

---

<a id="pull-requests-and-code-review"></a>
## Pull Requests and Code Review

### Typical workflow

```
Feature branch
    ↓
Focused commits
    ↓
Push
    ↓
Pull Request
    ↓
CI checks
    ↓
Code review
    ↓
Changes
    ↓
Merge
```

### Review for

- correctness
- security
- tests
- maintainability
- readability
- performance where relevant

A code review is more than syntax checking.

[Back to Table of Contents](#table-of-contents)

---

<a id="branching-strategies"></a>
## Branching Strategies

Know the concepts behind:

- feature branches
- trunk-based development
- Git Flow

### Interview answer

> A branching strategy should reduce integration risk and fit the team's release process. There is no universally best workflow.

[Back to Table of Contents](#table-of-contents)

---

<a id="cicd"></a>
## CI/CD

### Continuous Integration

Frequently integrate changes with automated build/test validation.

### Continuous Delivery

Keep software in a deployable state.

### Continuous Deployment

Automatically deploy qualifying changes to production.

**Trap:** Continuous Delivery and Continuous Deployment are not identical.

[Back to Table of Contents](#table-of-contents)

---

<a id="build--test--deploy-pipeline"></a>
## Build → Test → Deploy Pipeline

Typical pipeline:

```
Commit
  ↓
Lint / static checks
  ↓
Unit tests
  ↓
Integration tests
  ↓
Security checks
  ↓
Build artifact / image
  ↓
Deploy staging
  ↓
Smoke / health checks
  ↓
Production
  ↓
Monitor
```

**Important:** A successful deployment command does not prove the application is healthy.

[Back to Table of Contents](#table-of-contents)

---

<a id="environments-and-configuration"></a>
## Environments and Configuration

Common environments:

```
Development
Testing
Staging
Production
```

Configuration examples:

- database URL
- Redis URL
- API keys
- signing secrets
- feature flags
- logging levels

Keep environment-specific configuration outside application logic and store secrets securely.

[Back to Table of Contents](#table-of-contents)

---

<a id="release-strategies"></a>
## Release Strategies

### Rolling
Replace instances gradually.

### Blue-Green
Keep old and new environments, then switch traffic after verification.

### Canary
Send a small amount of traffic to the new version first.

### Feature Flag
Deploy code while separately controlling user exposure.

**Why:** Reduce blast radius during releases.

[Back to Table of Contents](#table-of-contents)

---

# Architecture and Design

<a id="monolith-vs-modular-monolith-vs-microservices"></a>
## Monolith vs Modular Monolith vs Microservices

### Monolith

One deployable application.

### Modular monolith

One deployable application with strong internal module boundaries.

### Microservices

Multiple independently deployable services, often organized around business capabilities.

### Trade-offs

| Approach | Main strength | Main cost |
|---|---|---|
| Monolith | Simpler deployment/operations | Harder independent scaling |
| Modular monolith | Boundaries without distributed deployment | Still one deployment unit |
| Microservices | Independent deployment/scaling | Distributed-system complexity |

**Trap:** Microservices are not automatically “better” architecture.

[Back to Table of Contents](#table-of-contents)

---

<a id="layered-architecture"></a>
## Layered Architecture

Common backend structure:

```
Router / Controller
        ↓
Service / Business Logic
        ↓
Repository / Data Access
        ↓
Database
```

### Why?

- separation of concerns
- easier testing
- clearer responsibilities
- reduced coupling

**FastAPI connection:** Router → service → repository/ORM → PostgreSQL.

[Back to Table of Contents](#table-of-contents)

---

<a id="event-driven-architecture"></a>
## Event-Driven Architecture

Instead of synchronously invoking every downstream component:

```
OrderCreated
     ↓
   Event
     ↓
┌─────────────┬──────────────┐
Inventory     Email          Analytics
Consumer      Consumer       Consumer
```

Know:

- producer
- event
- broker
- consumer
- ordering
- retries
- delivery semantics
- dead-letter handling

[Back to Table of Contents](#table-of-contents)

---

<a id="message-queues-and-pubsub"></a>
## Message Queues and Pub/Sub

### Queue

Work is distributed among consumers/workers according to the messaging system's semantics.

### Pub/Sub

One published event can be delivered to multiple subscribers.

Example:

```
OrderCreated
    ↓
├── Billing
├── Analytics
└── Notification
```

Important concepts:

- acknowledgement
- retries
- dead-letter queue/topic
- consumer scaling
- ordering
- delivery semantics

### SceneFlow connection

```
FastAPI
   ↓
Queue
   ↓
Celery worker
   ↓
Image processing
```

[Back to Table of Contents](#table-of-contents)

---

<a id="clean-architecture-and-separation-of-concerns"></a>
## Clean Architecture and Separation of Concerns

Core idea: keep business rules from becoming tightly coupled to frameworks and infrastructure.

One practical shape:

```
API Layer
   ↓
Application / Service Layer
   ↓
Domain Logic
   ↓
Infrastructure Adapters
```

You do not need to memorize one exact diagram. Explain responsibilities and dependency direction.

[Back to Table of Contents](#table-of-contents)

---

<a id="coupling-and-cohesion"></a>
## Coupling and Cohesion

### Coupling

How strongly modules depend on one another.

### Cohesion

How closely related responsibilities within a module are.

Good design generally aims for:

```
High cohesion
+
Low unnecessary coupling
```

**Example:** A SceneService should not contain unrelated billing logic.

[Back to Table of Contents](#table-of-contents)

---

<a id="solid-dry-kiss-and-yagni"></a>
## SOLID, DRY, KISS and YAGNI

### SOLID

OO design principles. Covered deeply in the LLD notes.

### DRY

Avoid unnecessary duplication of knowledge or logic.

### KISS

Prefer the simplest design that satisfies the requirements.

### YAGNI

Do not build speculative functionality before it is needed.

**Trap:** These are heuristics, not absolute laws.

[Back to Table of Contents](#table-of-contents)

---

# Production Engineering

<a id="logging"></a>
## Logging

A useful log answers:

```
What happened?
Where?
When?
For which request/job?
```

Example:

```
request_id=req_123
route=/scenes
status=201
duration_ms=28
```

Use structured logging where practical.

**Never log:** passwords, tokens or secrets.

[Back to Table of Contents](#table-of-contents)

---

<a id="monitoring-and-metrics"></a>
## Monitoring and Metrics

Useful metrics:

- request rate
- latency
- error rate
- CPU/memory
- DB connections
- queue depth
- worker duration

Know:

```
p50
p95
p99
```

Average latency can hide poor tail latency.

[Back to Table of Contents](#table-of-contents)

---

<a id="observability-and-tracing"></a>
## Observability and Tracing

Common telemetry:

- **Logs** → events/details
- **Metrics** → numbers/trends
- **Traces** → request path across components

### SceneFlow example

```
Request ID
   ↓
FastAPI
   ↓
Celery job
   ↓
Gemini
   ↓
Image provider
   ↓
Qdrant / PostgreSQL
```

**Interview line:** Monitoring tells you that something is wrong; observability helps investigate why.

[Back to Table of Contents](#table-of-contents)

---

<a id="health-checks"></a>
## Health Checks

### Liveness

> Is the process alive?

### Readiness

> Is the instance ready to receive traffic?

Example:

```http
GET /health/live
GET /health/ready
```

Readiness is especially useful during startup, deployment and dependency failures.

[Back to Table of Contents](#table-of-contents)

---

<a id="timeouts-retries-and-circuit-breakers"></a>
## Timeouts, Retries and Circuit Breakers

### Timeout

Bounds how long we wait.

### Retry

Repeats a failed operation when appropriate.

### Exponential backoff

Increases the delay between retries.

### Jitter

Adds randomness to reduce synchronized retry spikes.

### Circuit breaker

Temporarily stops calling a repeatedly failing dependency.

### Flow

```
Request
   ↓
Timeout
   ↓
Bounded retry + backoff
   ↓
Repeated failures
   ↓
Circuit opens
   ↓
Fallback / controlled error
```

**Trap:** Retries can amplify outages or duplicate side effects.

[Back to Table of Contents](#table-of-contents)

---

<a id="graceful-shutdown"></a>
## Graceful Shutdown

During shutdown:

```
Stop accepting new work
        ↓
Handle in-flight work
        ↓
Close connections/resources
        ↓
Exit
```

This reduces dropped requests and incomplete work during deployments.

[Back to Table of Contents](#table-of-contents)

---

<a id="performance-and-profiling"></a>
## Performance and Profiling

Use:

```
Measure
   ↓
Find bottleneck
   ↓
Optimize
   ↓
Measure again
```

Potential bottlenecks:

- SQL queries
- missing indexes
- external APIs
- CPU-heavy work
- network
- serialization
- lock contention
- excessive DB connections

**Interview trap:** “Make it faster” is not a diagnosis.

[Back to Table of Contents](#table-of-contents)

---

<a id="caching"></a>
## Caching

Common flow:

```
Request
   ↓
Cache?
 ├─ hit  → return
 └─ miss → DB/API → cache → return
```

Know:

- TTL
- invalidation
- cache-aside
- stale data
- cache stampede
- eviction
- local vs distributed cache

### URL Shortener

```
short_code → destination URL
```

is a natural cache entry.

[Back to Table of Contents](#table-of-contents)

---

<a id="database-connection-pooling"></a>
## Database Connection Pooling

Opening a new DB connection for every request can be expensive.

### Pool model

```
Request
  ↓
Connection Pool
  ↓
Reusable connection
  ↓
Query
  ↓
Return to pool
```

Benefits:

- less connection setup overhead
- controlled DB concurrency
- protection from connection storms

[Back to Table of Contents](#table-of-contents)

---

<a id="docker-and-container-basics"></a>
## Docker and Container Basics

Know:

- image
- container
- Dockerfile
- layers
- ports
- volumes
- environment variables
- networks
- health checks

### Mental model

```
Dockerfile
    ↓ build
Image
    ↓ run
Container
```

**Interview answer:** Containers package applications and dependencies into reproducible runtime environments. They are not the same isolation model as virtual machines.

[Back to Table of Contents](#table-of-contents)

---

# Security

<a id="authentication-vs-authorization"></a>
## Authentication vs Authorization

**Authentication:** Who are you?

**Authorization:** What can you do?

### Flow

```
Login
  ↓
Authentication
  ↓
Session/JWT
  ↓
Request
  ↓
Permission check
  ↓
Authorization
```

[Back to Table of Contents](#table-of-contents)

---

<a id="sessions-vs-jwt"></a>
## Sessions vs JWT

### Session-based

```
Client → Session ID
Server → Stores session state
```

### JWT-based

```
Client → Signed token
Server → Verifies token/claims
```

Both have trade-offs around state, revocation, storage, token lifetime and scaling.

**Trap:** A signed JWT is not automatically encrypted.

[Back to Table of Contents](#table-of-contents)

---

<a id="oauth-20"></a>
## OAuth 2.0

OAuth 2.0 is an authorization framework for delegated access.

### Concept

```
User
 ↓
Authorization Server
 ↓
Access Token
 ↓
Client
 ↓
Resource Server
```

**Trap:** OAuth 2.0 is not simply “login”. OpenID Connect adds standardized authentication on top of OAuth 2.0.

[Back to Table of Contents](#table-of-contents)

---

<a id="rbac-and-access-control"></a>
## RBAC and Access Control

**RBAC = Role-Based Access Control.**

| Role | Typical permissions |
|---|---|
| Admin | Create / read / update / delete |
| Editor | Create / read / update |
| Viewer | Read |

Other models use permissions, scopes or attributes.

**Important:** Authorization must be enforced server-side.

[Back to Table of Contents](#table-of-contents)

---

<a id="cors-csrf-and-xss"></a>
## CORS, CSRF and XSS

### CORS

Browser mechanism controlling cross-origin access.

**Trap:** CORS is not authentication.

### CSRF

An attacker causes a browser with existing credentials to perform an unwanted state-changing request.

Especially relevant to cookie-based authentication.

### XSS

Attacker-controlled script executes in a user's browser.

Defense concepts include:
- output encoding
- safe templating
- sanitization where appropriate
- Content Security Policy as an additional layer

[Back to Table of Contents](#table-of-contents)

---

<a id="secrets-and-least-privilege"></a>
## Secrets and Least Privilege

Never hard-code:

- passwords
- API keys
- JWT/signing secrets
- private credentials

Use:

- environment configuration
- secret managers
- restricted credentials

**Least privilege:** Give each user/service only the permissions required for its job.

[Back to Table of Contents](#table-of-contents)

---

# Documentation and Engineering Practices

<a id="uml-diagrams-you-should-recognize"></a>
## UML Diagrams You Should Recognize

| Diagram | Purpose |
|---|---|
| Class | Structure and relationships |
| Sequence | Time-ordered interactions |
| Activity | Workflow |
| Use Case | Actors and system goals |
| State | States and transitions |
| Component | Major software components |
| Deployment | Runtime/infrastructure view |

**Interview tip:** Sequence diagrams are especially useful for explaining API/request flows.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-documentation"></a>
## API Documentation

A useful API document communicates:

```
Endpoint
Method
Authentication
Parameters
Request schema
Response schema
Status codes
Errors
Examples
Limits/constraints
```

OpenAPI can represent much of this in a machine-readable format.

[Back to Table of Contents](#table-of-contents)

---

<a id="architecture-decision-records"></a>
## Architecture Decision Records

An ADR records an important technical decision.

### Structure

```
Context
  ↓
Decision
  ↓
Alternatives
  ↓
Trade-offs
  ↓
Consequences
```

### SceneFlow example

**Context:** image processing is long-running and retryable.

**Decision:** queue + Celery workers.

**Alternative:** lightweight in-process background work.

**Trade-off:** more infrastructure, but independent worker execution, retries and scaling.

[Back to Table of Contents](#table-of-contents)

---

<a id="maintenance-refactoring-and-technical-debt"></a>
## Maintenance, Refactoring and Technical Debt

### Refactoring

Improve internal structure without intentionally changing external behavior.

### Technical debt

Future engineering cost created by shortcuts, deferred work or design compromises.

### Maintenance categories

- corrective
- adaptive
- perfective
- preventive

**Interview question:** Why refactor?

> To reduce complexity and improve maintainability while preserving required behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="backward-compatibility-and-deprecation"></a>
## Backward Compatibility and Deprecation

Backward compatibility means existing consumers continue to work.

### Safer API evolution

- add fields instead of removing them
- preserve existing semantics
- version breaking changes
- document deprecation timelines
- provide migration guidance

**Example:** Keep `/v1/users` working while clients migrate to `/v2/users`.

[Back to Table of Contents](#table-of-contents)

---

# Infosys Interview Execution

<a id="generic-software-engineering-qa"></a>
## Generic Software Engineering Q&A

### Q1. What is SDLC?

**Answer:** SDLC is the lifecycle used to take software from requirements through design, implementation, testing, deployment and maintenance.

### Q2. Agile vs Waterfall?

**Answer:** Waterfall is more sequential and plan-driven; Agile uses shorter feedback cycles and adapts during development.

### Q3. What is a non-functional requirement?

**Answer:** A quality attribute or constraint such as latency, availability, security or scalability.

### Q4. What is CI?

**Answer:** Frequently integrating changes with automated build and test validation.

### Q5. What is technical debt?

**Answer:** Future engineering cost caused by shortcuts, deferred work or design compromises.

### Q6. What is observability?

**Answer:** The ability to investigate system behavior using telemetry such as logs, metrics and traces.

[Back to Table of Contents](#table-of-contents)

---

<a id="api-interview-qa"></a>
## API Interview Q&A

### Q1. Is every API a REST API?

**Answer:** No. REST is one API style. APIs can also be SOAP, GraphQL, gRPC/RPC, WebSocket-based, webhook-based or in-process library APIs.

### Q2. REST vs SOAP?

**Answer:** REST is an architectural style commonly implemented over HTTP; SOAP is a formal structured messaging protocol commonly represented using XML.

### Q3. REST vs GraphQL?

**Answer:** REST commonly exposes resource-oriented endpoints; GraphQL uses a schema-driven query interface where clients request the data shape they need.

### Q4. REST vs gRPC?

**Answer:** REST is common for broad HTTP-facing APIs. gRPC provides strongly typed RPC and is commonly useful for internal service-to-service communication.

### Q5. WebSocket vs REST?

**Answer:** REST is generally request/response. WebSocket maintains a persistent bidirectional connection for ongoing messages.

### Q6. Webhook vs polling?

**Answer:** Polling repeatedly asks for changes; a webhook pushes an event from the producer.

### Q7. What is idempotency?

**Answer:** Repeating a logical operation produces the same intended final effect instead of creating unintended duplicate effects.

### Q8. Why use pagination?

**Answer:** To bound response size, database work, network transfer and client memory.

### Q9. What is an API gateway?

**Answer:** An API-facing entry point that can centralize routing and policies such as authentication and rate limiting.

### Q10. Why use timeouts?

**Answer:** To prevent a slow dependency from holding resources indefinitely.

[Back to Table of Contents](#table-of-contents)

---

<a id="infosys-focused-questions"></a>
## Infosys-Focused Questions

These should be treated as **high-priority practice questions**, not an official Infosys question bank.

### Q1. Explain SDLC.

**Answer:** Requirements → analysis → design → implementation → testing → deployment → maintenance, with iteration depending on the development model.

### Q2. Waterfall vs Agile?

**Answer:** Waterfall is more sequential; Agile delivers in shorter cycles with frequent feedback and adaptation.

### Q3. What is a REST API and how did you use it?

**Answer:** REST is a resource-oriented architectural style commonly implemented over HTTP. In my projects, React communicates with FastAPI endpoints for project, scene and user operations.

### Q4. How did you implement an API?

**Answer:**

```
Route
 ↓
Request validation
 ↓
Authentication / authorization
 ↓
Service logic
 ↓
Database / external service
 ↓
Response
```

### Q5. How would you secure an API?

**Answer:** HTTPS, strong authentication, server-side authorization, input validation, parameterized DB access, rate limiting, secure secrets and controlled error responses.

### Q6. What is GitHub used for?

**Answer:** Repository hosting, collaboration, pull requests, code review, issue tracking and CI/CD integration.

### Q7. Explain a normal Git workflow.

**Answer:**

```
Feature branch
→ focused commits
→ push
→ pull request
→ CI + review
→ merge
```

### Q8. What happens if an API dependency fails?

**Answer:** Use a timeout, retry only appropriate transient failures, apply backoff, provide fallback/controlled errors and monitor the dependency.

### Q9. How would you scale an API?

**Answer:**

```
Measure bottleneck
→ optimize SQL/indexes
→ cache hot reads
→ pool connections
→ queue long-running work
→ multiple stateless instances
→ load balancing
→ monitoring
```

[Back to Table of Contents](#table-of-contents)

---

<a id="project-based-questions"></a>
## Project-Based Questions

### SceneFlow

### Why FastAPI?

> I needed an API-focused Python backend with typed request/response contracts, dependency injection and async-compatible I/O. It also fits naturally with my Python AI/backend ecosystem.

### Why Celery?

> Image search, embedding generation and external API processing can be long-running and retryable. A queue lets workers execute independently of HTTP request processing and scale separately.

### Why Redis?

> Redis supports shared temporary state/cache and participates in the background-processing infrastructure depending on the subsystem.

### Why Qdrant?

> Qdrant performs vector similarity search over embeddings to retrieve semantically relevant assets.

### Why polling?

> The frontend can submit an asynchronous job and periodically retrieve its status/results. WebSockets are an alternative when push updates are preferable.

### URL Shortener

### Request flow

```
Browser
  ↓
DNS
  ↓
TCP/TLS
  ↓
HTTP
  ↓
Reverse Proxy / Load Balancer
  ↓
FastAPI
  ↓
Redis / PostgreSQL
  ↓
Redirect
```

### Scaling points

- cache hot short codes
- unique/index short codes
- stateless API workers
- load balancing
- rate limiting/abuse controls

### ScoreHub

### REST or WebSocket?

> REST for durable resource operations; WebSocket for live score delivery.

### Concurrent score updates?

> Define transaction boundaries, use suitable concurrency controls, keep the database authoritative, and make duplicate event processing safe when necessary.

[Back to Table of Contents](#table-of-contents)

---

<a id="scenario-questions"></a>
## Scenario Questions

### Q1. API becomes slow. What do you do?

```
Measure
→ break latency into components
→ identify bottleneck
→ optimize
→ re-measure
```

### Q2. Database is slow.

```
Find slow query
→ inspect filters/joins
→ check indexes/query plan
→ reduce unnecessary data
→ consider cache/pooling
→ measure
→ scale architecture if required
```

### Q3. Third-party API is down.

```
Timeout
→ bounded retry/backoff if safe
→ circuit breaker/fallback
→ queue asynchronous work when possible
→ controlled failure
→ monitoring
```

### Q4. Deployment succeeds but application is unhealthy.

```
Health check
→ stop promotion / remove from traffic
→ inspect logs + metrics
→ rollback/fix
→ verify
```

### Q5. Client sends the same request twice.

**Answer:** Use idempotency keys and/or database uniqueness/constraints according to the operation.

### Q6. Traffic suddenly becomes 10×.

**Answer:** Protect the system first with rate limiting/backpressure, identify the bottleneck, scale stateless application workers, protect the DB and move long work to queues where appropriate.

[Back to Table of Contents](#table-of-contents)

---

<a id="interview-traps"></a>
## Interview Traps

Avoid statements like:

- “REST is JSON over HTTP.”
- “SOAP is REST with XML.”
- “GraphQL is always faster.”
- “gRPC is only for browsers.”
- “WebSocket replaces REST.”
- “Webhooks are always exactly-once.”
- “CORS secures the API.”
- “JWT is always encrypted.”
- “401 and 403 are the same.”
- “Async automatically makes CPU work faster.”
- “BackgroundTasks is the same as Celery.”
- “Microservices are always better.”
- “CI/CD always means automatic production deployment.”
- “Adding an index always fixes a slow database.”

Instead:

```
Explain the concept
   ↓
State the use case
   ↓
Mention trade-off
   ↓
Mention failure mode
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-interview-checklist"></a>
## Final Interview Checklist

### Software engineering

- [ ] SDLC
- [ ] Waterfall
- [ ] V-Model
- [ ] Iterative
- [ ] Incremental
- [ ] Spiral
- [ ] Agile
- [ ] Scrum
- [ ] Requirements engineering
- [ ] Functional vs non-functional requirements
- [ ] User stories
- [ ] Acceptance criteria

### APIs

- [ ] API definition
- [ ] REST
- [ ] SOAP
- [ ] GraphQL
- [ ] gRPC / RPC
- [ ] WebSocket
- [ ] Webhooks
- [ ] SSE
- [ ] Library/SDK APIs
- [ ] HTTP methods
- [ ] status codes
- [ ] parameters
- [ ] API design
- [ ] pagination
- [ ] versioning
- [ ] error handling
- [ ] idempotency
- [ ] authentication
- [ ] authorization
- [ ] API gateway
- [ ] reliability
- [ ] OpenAPI
- [ ] API testing

### Testing

- [ ] STLC
- [ ] unit
- [ ] integration
- [ ] system
- [ ] E2E
- [ ] smoke
- [ ] sanity
- [ ] regression
- [ ] load
- [ ] stress
- [ ] spike
- [ ] soak
- [ ] contract testing

### Git / delivery

- [ ] Git basics
- [ ] merge vs rebase
- [ ] branching
- [ ] pull requests
- [ ] code review
- [ ] CI
- [ ] CD
- [ ] pipeline
- [ ] environments
- [ ] rolling
- [ ] blue-green
- [ ] canary

### Architecture

- [ ] monolith
- [ ] modular monolith
- [ ] microservices
- [ ] layered architecture
- [ ] event-driven architecture
- [ ] queues
- [ ] Pub/Sub
- [ ] separation of concerns
- [ ] coupling/cohesion
- [ ] SOLID
- [ ] DRY
- [ ] KISS
- [ ] YAGNI

### Production

- [ ] logging
- [ ] metrics
- [ ] tracing
- [ ] health checks
- [ ] timeouts
- [ ] retries
- [ ] backoff
- [ ] circuit breaker
- [ ] graceful shutdown
- [ ] performance
- [ ] caching
- [ ] connection pooling
- [ ] Docker

### Security

- [ ] authentication vs authorization
- [ ] sessions
- [ ] JWT
- [ ] OAuth2
- [ ] RBAC
- [ ] CORS
- [ ] CSRF
- [ ] XSS
- [ ] secrets
- [ ] least privilege

### Final answer framework

For theory:

```
Definition
    ↓
Why it exists
    ↓
Simple example
    ↓
Practical project example
    ↓
Trade-off
    ↓
Follow-up
```

For API questions:

```
What is it?
    ↓
How does communication work?
    ↓
Where is it useful?
    ↓
Trade-offs
    ↓
Security / reliability
    ↓
Project connection
```

For project questions:

```
Problem
    ↓
Architecture
    ↓
Request / data flow
    ↓
What I implemented
    ↓
Why
    ↓
Failure handling
    ↓
Security
    ↓
Scaling
```

### Final goal

> Be able to discuss software as an engineer, not merely as someone who knows individual technologies.

[Back to Table of Contents](#table-of-contents)
