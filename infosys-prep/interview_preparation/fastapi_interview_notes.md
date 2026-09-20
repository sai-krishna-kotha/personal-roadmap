# FastAPI Interview Notes

## Table of Contents

- [1. What is FastAPI?](#1-what-is-fastapi)
- [2. FastAPI vs Flask vs Django](#2-fastapi-vs-flask-vs-django)
- [3. ASGI, Uvicorn and Starlette](#3-asgi-uvicorn-and-starlette)
- [4. Request Lifecycle](#4-request-lifecycle)
- [5. Routing and APIRouter](#5-routing-and-apirouter)
- [6. Path Parameters](#6-path-parameters)
- [7. Query Parameters](#7-query-parameters)
- [8. Request Body and Pydantic](#8-request-body-and-pydantic)
- [9. Headers, Cookies and Request](#9-headers-cookies-and-request)
- [10. Response Models](#10-response-models)
- [11. Status Codes and Responses](#11-status-codes-and-responses)
- [12. Validation and Error Handling](#12-validation-and-error-handling)
- [13. Dependency Injection](#13-dependency-injection)
- [14. Authentication and Authorization](#14-authentication-and-authorization)
- [15. OAuth2 and JWT](#15-oauth2-and-jwt)
- [16. Middleware](#16-middleware)
- [17. CORS](#17-cors)
- [18. BackgroundTasks](#18-backgroundtasks)
- [19. Lifespan](#19-lifespan)
- [20. Async and Await](#20-async-and-await)
- [21. Blocking Code](#21-blocking-code)
- [22. Database Integration](#22-database-integration)
- [23. Sessions and Transactions](#23-sessions-and-transactions)
- [24. Service and Repository Layers](#24-service-and-repository-layers)
- [25. OpenAPI and Docs](#25-openapi-and-docs)
- [26. File Uploads and Forms](#26-file-uploads-and-forms)
- [27. WebSockets](#27-websockets)
- [28. Rate Limiting](#28-rate-limiting)
- [29. Caching](#29-caching)
- [30. Idempotency](#30-idempotency)
- [31. External APIs](#31-external-apis)
- [32. Timeouts, Retries and Circuit Breakers](#32-timeouts-retries-and-circuit-breakers)
- [33. Queues and Long-Running Jobs](#33-queues-and-long-running-jobs)
- [34. BackgroundTasks vs Celery](#34-backgroundtasks-vs-celery)
- [35. Redis](#35-redis)
- [36. Testing](#36-testing)
- [37. Configuration and Security](#37-configuration-and-security)
- [38. Production Deployment and Workers](#38-production-deployment-and-workers)
- [39. Observability and Performance](#39-observability-and-performance)
- [40. SceneFlow Connection](#40-sceneflow-connection)
- [41. URL Shortener Connection](#41-url-shortener-connection)
- [42. ScoreHub Connection](#42-scorehub-connection)
- [43. Generic Interview Q&A](#43-generic-interview-qa)
- [44. Internal Interview Q&A](#44-internal-interview-qa)
- [45. Project Questions](#45-project-questions)
- [46. Implementation Drills](#46-implementation-drills)
- [47. Interview Traps](#47-interview-traps)
- [48. Final Checklist](#48-final-checklist)

<a id="1-what-is-fastapi"></a>
## 1. What is FastAPI?

**Interview answer:** FastAPI is a Python framework for building APIs. It uses Python type hints for request parsing and validation, supports asynchronous I/O through ASGI, provides dependency injection, and generates OpenAPI documentation.

### Simple example

```python
from fastapi import FastAPI
app = FastAPI()

@app.get("/hello")
def hello():
    return {"message": "hello"}
```

### Technical example

```python
from pydantic import BaseModel

class UserCreate(BaseModel):
    name: str
    age: int

@app.post("/users")
async def create_user(user: UserCreate):
    return user.model_dump()
```

[Back to Table of Contents](#table-of-contents)

<a id="2-fastapi-vs-flask-vs-django"></a>
## 2. FastAPI vs Flask vs Django

**FastAPI:** API-oriented, ASGI, typed schemas, dependency injection, OpenAPI, async support.

**Flask:** minimal web framework with a large extension ecosystem.

**Django:** broader full-stack framework with ORM, admin, authentication, templates and more built in.

Interview answer: choose according to system requirements rather than claiming one is universally better.

[Back to Table of Contents](#table-of-contents)

<a id="3-asgi-uvicorn-and-starlette"></a>
## 3. ASGI, Uvicorn and Starlette

- **ASGI:** server/application interface for modern asynchronous Python web apps.
- **Uvicorn:** ASGI server commonly used to run FastAPI.
- **Starlette:** ASGI web toolkit underneath FastAPI for routing, middleware, requests, responses and WebSockets.

**Mental model:** Browser → Uvicorn → ASGI app → FastAPI/Starlette → endpoint.

[Back to Table of Contents](#table-of-contents)

<a id="4-request-lifecycle"></a>
## 4. Request Lifecycle

1. Client sends HTTP request.
2. Uvicorn receives it.
3. ASGI application receives request scope/events.
4. Middleware runs.
5. Router finds a path operation.
6. FastAPI resolves dependencies.
7. Parameters/body are parsed and validated.
8. Endpoint executes.
9. Return value is serialized.
10. Middleware processes the response.
11. Server sends the response.

**SceneFlow:** React → HTTPS → Uvicorn/ASGI → FastAPI → validation/dependencies → service → PostgreSQL/Redis/external APIs → response.

[Back to Table of Contents](#table-of-contents)

<a id="5-routing-and-apirouter"></a>
## 5. Routing and APIRouter

```python
from fastapi import APIRouter

router = APIRouter(prefix="/projects", tags=["projects"])

@router.get("/{project_id}")
async def get_project(project_id: int):
    return {"id": project_id}
```

Then include it with `app.include_router(router)`.

Use routers to separate domains such as users, projects, scenes and auth.

[Back to Table of Contents](#table-of-contents)

<a id="6-path-parameters"></a>
## 6. Path Parameters

```python
@app.get("/users/{user_id}")
async def get_user(user_id: int):
    return {"id": user_id}
```

`GET /users/42` passes `42` as `user_id`, and FastAPI validates it against `int`.

**Question:** Path vs query parameter?

**Answer:** A path parameter is part of the resource URL; a query parameter modifies or filters the request.

[Back to Table of Contents](#table-of-contents)

<a id="7-query-parameters"></a>
## 7. Query Parameters

```python
@app.get("/users")
async def list_users(skip: int = 0, limit: int = 20):
    return {"skip": skip, "limit": limit}
```

Request: `GET /users?skip=20&limit=10`

Validation:

```python
from typing import Annotated
from fastapi import Query

limit: Annotated[int, Query(ge=1, le=100)] = 20
```

[Back to Table of Contents](#table-of-contents)

<a id="8-request-body-and-pydantic"></a>
## 8. Request Body and Pydantic

Pydantic models make request contracts explicit.

```python
class SceneCreate(BaseModel):
    script: str
    scene_number: int
    duration: float | None = None

@app.post("/scenes")
async def create_scene(scene: SceneCreate):
    return scene.model_dump()
```

**Why Pydantic?** Validation, structured schemas, serialization and OpenAPI generation without scattering manual field checks through endpoints.

[Back to Table of Contents](#table-of-contents)

<a id="9-headers-cookies-and-request"></a>
## 9. Headers, Cookies and Request

```python
from fastapi import Header, Cookie, Request

@app.get("/demo")
async def demo(x_token: str | None = Header(default=None)):
    return {"token": x_token}
```

Cookies can be declared with `Cookie()`. Use `Request` when lower-level request information is needed.

[Back to Table of Contents](#table-of-contents)

<a id="10-response-models"></a>
## 10. Response Models

```python
class UserOut(BaseModel):
    id: int
    name: str

@app.get("/users/{user_id}", response_model=UserOut)
async def get_user(user_id: int):
    return {"id": user_id, "name": "Sai", "password_hash": "secret"}
```

A response model defines the output contract and can validate, serialize and filter returned fields.

**Interview line:** Request models protect the input contract; response models protect the output contract.

[Back to Table of Contents](#table-of-contents)

<a id="11-status-codes-and-responses"></a>
## 11. Status Codes and Responses

Know: `200 OK`, `201 Created`, `202 Accepted`, `204 No Content`, `400 Bad Request`, `401 Unauthorized`, `403 Forbidden`, `404 Not Found`, `409 Conflict`, `422 Validation Error`, `429 Too Many Requests`, `500`, `502`, `503`, `504`.

```python
@app.post("/users", status_code=201)
async def create_user(user: UserCreate):
    return user
```

For redirects use `RedirectResponse`; for custom response behavior use FastAPI/Starlette response classes.

[Back to Table of Contents](#table-of-contents)

<a id="12-validation-and-error-handling"></a>
## 12. Validation and Error Handling

```python
from fastapi import HTTPException

if user is None:
    raise HTTPException(status_code=404, detail="User not found")
```

Distinguish:

- validation error — declared input is invalid
- `HTTPException` — known HTTP-level application error
- unhandled exception — unexpected failure

Custom exception handlers are useful for a consistent error format.

[Back to Table of Contents](#table-of-contents)

<a id="13-dependency-injection"></a>
## 13. Dependency Injection

One of the most important FastAPI topics.

```python
from fastapi import Depends

def get_database():
    db = create_db()
    try:
        yield db
    finally:
        db.close()

@app.get("/users")
async def users(db=Depends(get_database)):
    return db.list_users()
```

FastAPI resolves the dependency before executing the endpoint. Dependencies can have sub-dependencies.

**Interview answer:** The endpoint declares what it needs; FastAPI constructs/resolves those dependencies and injects the results.

Uses: DB sessions, current user, settings, service objects, auth checks, reusable clients.

[Back to Table of Contents](#table-of-contents)

<a id="14-authentication-and-authorization"></a>
## 14. Authentication and Authorization

**Authentication:** Who are you?

**Authorization:** What are you allowed to do?

```python
async def get_current_user(token=Depends(oauth2_scheme)):
    return verify_token(token)

@app.get("/admin")
async def admin(user=Depends(get_current_user)):
    if not user.is_admin:
        raise HTTPException(status_code=403, detail="Forbidden")
    return {"ok": True}
```

For SceneFlow, authentication identifies the caller; authorization determines whether that caller can access a project/scene.

[Back to Table of Contents](#table-of-contents)

<a id="15-oauth2-and-jwt"></a>
## 15. OAuth2 and JWT

**OAuth2** is an authorization framework. FastAPI provides security helpers for OAuth2-style flows.

**JWT** commonly carries claims and is signed. A normal signed JWT is not automatically encrypted or secret.

**Password storage:** never store plaintext passwords; use a dedicated slow password-hashing algorithm/library.

Interview trap: authentication, token validation and authorization are different responsibilities.

[Back to Table of Contents](#table-of-contents)

<a id="16-middleware"></a>
## 16. Middleware

Middleware wraps request/response processing.

```text
request → middleware → endpoint → middleware → response
```

```python
import time

@app.middleware("http")
async def timing(request, call_next):
    start = time.perf_counter()
    response = await call_next(request)
    response.headers["X-Process-Time"] = str(time.perf_counter() - start)
    return response
```

Good uses: request IDs, logging, metrics, tracing, security headers, CORS.

[Back to Table of Contents](#table-of-contents)

<a id="17-cors"></a>
## 17. CORS

CORS controls browser cross-origin access.

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://frontend.example.com"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

**Project connection:** React frontend and FastAPI backend on different origins require appropriate CORS configuration.

**Trap:** CORS is not authentication.

[Back to Table of Contents](#table-of-contents)

<a id="18-backgroundtasks"></a>
## 18. BackgroundTasks

`BackgroundTasks` is suitable for small post-response work.

```python
@app.post("/events")
async def event(background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, "event")
    return {"accepted": True}
```

It is not a distributed durable job queue.

[Back to Table of Contents](#table-of-contents)

<a id="19-lifespan"></a>
## 19. Lifespan

Use application lifespan for startup/shutdown resource management:

- DB connection pools
- shared HTTP clients
- ML models
- initialization
- cleanup

**Interview answer:** Lifespan manages resources that live for the application lifecycle rather than for one request.

[Back to Table of Contents](#table-of-contents)

<a id="20-async-and-await"></a>
## 20. Async and Await

```python
async def endpoint():
    result = await network_call()
    return result
```

`await` suspends the current coroutine while the awaited operation is not ready, allowing other event-loop work to run.

Good: network I/O, async DB calls, WebSockets.

Bad: CPU-heavy pure Python or blocking synchronous libraries inside the event loop.

**Does async automatically make code faster?** No. It improves concurrency for operations that can yield.

[Back to Table of Contents](#table-of-contents)

<a id="21-blocking-code"></a>
## 21. Blocking Code

Bad:

```python
@app.get("/report")
async def report():
    return slow_blocking_function()
```

Options:

1. Use an async-compatible library.
2. Offload blocking work to a thread.
3. Move heavy work to a process/worker system.

This connects directly to the GIL/event-loop concepts in the Core Python notes.

[Back to Table of Contents](#table-of-contents)

<a id="22-database-integration"></a>
## 22. Database Integration

FastAPI does not force an ORM/database.

Common stack: PostgreSQL + SQLAlchemy/SQLModel + suitable DB driver.

Typical architecture:

**router → dependency/session → service → repository/ORM → PostgreSQL → response model**

SceneFlow and ScoreHub both connect this topic directly to your project experience.

[Back to Table of Contents](#table-of-contents)

<a id="23-sessions-and-transactions"></a>
## 23. Sessions and Transactions

A database session provides a working interface for database operations and transaction state.

A transaction groups operations into a unit of work.

```python
def create_user(db, user):
    db.add(user)
    db.commit()
    db.refresh(user)
    return user
```

Know `commit`, `rollback`, transaction boundaries, connection pooling and why sessions should have controlled lifecycles.

[Back to Table of Contents](#table-of-contents)

<a id="24-service-and-repository-layers"></a>
## 24. Service and Repository Layers

**Router → Service → Repository → Database**

Router: HTTP concerns.

Service: business rules.

Repository: persistence.

```python
@router.post("/scenes")
async def create_scene(payload: SceneCreate, service=Depends(get_scene_service)):
    return await service.create_scene(payload)
```

This separation improves testing and keeps routers from becoming giant business-logic files.

[Back to Table of Contents](#table-of-contents)

<a id="25-openapi-and-docs"></a>
## 25. OpenAPI and Docs

FastAPI generates an OpenAPI schema from declared routes, parameters, models, responses and security metadata.

Common endpoints:

```text
/docs
/redoc
/openapi.json
```

**Interview answer:** OpenAPI is the machine-readable API contract that powers documentation and client tooling.

[Back to Table of Contents](#table-of-contents)

<a id="26-file-uploads-and-forms"></a>
## 26. File Uploads and Forms

```python
from fastapi import File, UploadFile

@app.post("/upload")
async def upload(file: UploadFile = File(...)):
    return {"filename": file.filename}
```

Know multipart/form-data vs JSON, file-size limits, content validation, safe filenames, storage and memory usage.

[Back to Table of Contents](#table-of-contents)

<a id="27-websockets"></a>
## 27. WebSockets

WebSocket flow:

**HTTP upgrade → persistent connection → messages in both directions**

Use cases: chat, live dashboards, live scores, collaboration.

ScoreHub can use WebSockets to push score updates rather than polling continuously.

HTTP is usually request/response; WebSocket supports many messages over one persistent connection.

[Back to Table of Contents](#table-of-contents)

<a id="28-rate-limiting"></a>
## 28. Rate Limiting

Know:

- fixed window
- sliding window
- token bucket
- leaky bucket

Token bucket idea:

```python
tokens = min(capacity, tokens + refill_rate * elapsed)
if tokens >= 1:
    tokens -= 1
    allow()
else:
    reject()
```

With multiple workers, process-local counters cannot enforce a global limit. Use shared state such as Redis with atomic operations.

[Back to Table of Contents](#table-of-contents)

<a id="29-caching"></a>
## 29. Caching

Flow:

**request → cache lookup → hit → return; miss → DB/external API → cache → return**

Know cache keys, TTL, invalidation, stale data, cache stampede and local vs distributed cache.

URL Shortener: Redis can cache short-code → destination mappings.

SceneFlow: Redis can cache safely reusable results/metadata.

[Back to Table of Contents](#table-of-contents)

<a id="30-idempotency"></a>
## 30. Idempotency

Retries can deliver the same logical operation more than once.

```text
Idempotency-Key: abc123
```

The server stores/recognizes the key so repeated delivery does not cause unintended duplicate effects.

SceneFlow: prevent duplicate expensive image-search jobs caused by request retries.

[Back to Table of Contents](#table-of-contents)

<a id="31-external-apis"></a>
## 31. External APIs

```python
import httpx

async with httpx.AsyncClient(timeout=5) as client:
    response = await client.get("https://example.com/data")
    response.raise_for_status()
    data = response.json()
```

Always discuss timeout, retry policy, backoff, connection reuse, rate limits, error mapping and observability.

SceneFlow uses external AI and image APIs, so this is directly interview-relevant.

[Back to Table of Contents](#table-of-contents)

<a id="32-timeouts-retries-and-circuit-breakers"></a>
## 32. Timeouts, Retries and Circuit Breakers

**Timeout:** stop waiting indefinitely.

**Retry:** repeat a transient operation.

**Exponential backoff:** increase retry delay.

**Circuit breaker:** temporarily stop calling an unhealthy dependency after repeated failures.

Do not blindly retry permanent errors or non-idempotent operations.

[Back to Table of Contents](#table-of-contents)

<a id="33-queues-and-long-running-jobs"></a>
## 33. Queues and Long-Running Jobs

```text
POST /image-search
      ↓
create job
      ↓
enqueue
      ↓
202 + job_id
      ↓
worker
      ↓
persist result
      ↓
GET /jobs/{job_id}
```

This keeps long work outside the request latency budget.

This is the central architecture behind SceneFlow's asynchronous processing.

[Back to Table of Contents](#table-of-contents)

<a id="34-backgroundtasks-vs-celery"></a>
## 34. BackgroundTasks vs Celery

**BackgroundTasks:** lightweight post-response work in the application environment.

**Celery:** queue-backed distributed workers for long-running/retryable jobs.

**Interview answer:** I use BackgroundTasks for small work; I use Celery when jobs need independent workers, retries, queueing and scalable execution.

[Back to Table of Contents](#table-of-contents)

<a id="35-redis"></a>
## 35. Redis

Redis can support caching, rate limiting, distributed locks, counters, temporary state and queue/broker roles.

SceneFlow: Redis participates in the Celery/background-processing architecture.

URL Shortener: Redis can accelerate hot redirect lookups.

Trap: Redis is not simply "a cache".

[Back to Table of Contents](#table-of-contents)

<a id="36-testing"></a>
## 36. Testing

Separate:

- unit tests
- API tests
- integration tests

Example:

```python
def test_health(client):
    response = client.get("/health")
    assert response.status_code == 200
```

Test validation, authorization, success/error paths, DB behavior, external failures and edge cases.

[Back to Table of Contents](#table-of-contents)

<a id="37-configuration-and-security"></a>
## 37. Configuration and Security

Never hard-code secrets.

```text
DATABASE_URL
REDIS_URL
JWT_SECRET
API_KEY
```

Security concepts:

- HTTPS
- authentication
- authorization
- password hashing
- CORS
- CSRF where cookie authentication makes it relevant
- input/output validation
- SQL injection prevention
- command injection avoidance
- secret management
- rate limiting
- secure file uploads
- security headers

[Back to Table of Contents](#table-of-contents)

<a id="38-production-deployment-and-workers"></a>
## 38. Production Deployment and Workers

Typical architecture:

```text
Internet
  ↓
Reverse Proxy / Load Balancer
  ↓
Uvicorn / ASGI workers
  ↓
FastAPI
  ↓
Redis / PostgreSQL / external APIs
```

Multiple workers are generally separate processes, so ordinary Python globals are not shared between them.

Use shared state such as Redis/PostgreSQL for coordination.

[Back to Table of Contents](#table-of-contents)

<a id="39-observability-and-performance"></a>
## 39. Observability and Performance

Observability: logs, metrics and traces.

Useful metrics: request count, latency, error rate, dependency latency, queue depth and worker duration.

Performance practices:

- profile before optimizing
- reuse HTTP/database clients
- use efficient SQL/indexes
- avoid unnecessary serialization
- avoid huge in-memory payloads
- cache expensive reads
- move long work off request paths
- use async-compatible I/O
- scale horizontally

SceneFlow correlation path: request ID → job ID → Celery task → Gemini/image APIs → embeddings → Qdrant → PostgreSQL.

[Back to Table of Contents](#table-of-contents)

<a id="40-sceneflow-connection"></a>
## 40. SceneFlow Connection

### Architecture

```text
React / Vercel
      ↓ HTTPS
FastAPI / Render
      ↓
Pydantic validation
      ↓
Service / orchestration
      ├── PostgreSQL
      ├── Redis
      ├── Celery
      ├── Gemini
      ├── Pexels / Pixabay / Openverse
      └── Qdrant
```

### Flow

1. Create project.
2. Create/generate scenes.
3. Click `find images`.
4. FastAPI validates the request.
5. A job is created/dispatched.
6. Celery performs expensive work.
7. Gemini analyzes scene/query text.
8. Image providers return candidates.
9. Embeddings are generated.
10. Qdrant performs vector similarity search.
11. Metadata/results are persisted.
12. Frontend polls for results.

### Strong interview answer: Why FastAPI?

> I needed an API-focused Python backend with typed contracts, dependency injection and async-compatible I/O. It also fit naturally with the AI ecosystem. I kept expensive processing outside the HTTP request path using Celery.

### Why not process synchronously?

> External API latency, embedding generation and vector operations make request latency unpredictable. A job queue keeps the API responsive and lets worker capacity scale separately.

[Back to Table of Contents](#table-of-contents)

<a id="41-url-shortener-connection"></a>
## 41. URL Shortener Connection

### Request path

```text
Browser → DNS → TCP/TLS → GET /abc123 → Reverse Proxy → FastAPI → Redis/PostgreSQL → Redirect
```

### FastAPI implementation

```python
from fastapi.responses import RedirectResponse

@app.get("/{short_code}")
async def redirect(short_code: str):
    target = await cache.get(short_code)
    if target is None:
        target = await repository.find(short_code)
    if target is None:
        raise HTTPException(status_code=404, detail="Not found")
    return RedirectResponse(url=target, status_code=302)
```

Concepts: path parameters, response classes, dependencies, caching, errors and database fallback.

[Back to Table of Contents](#table-of-contents)

<a id="42-scorehub-connection"></a>
## 42. ScoreHub Connection

ScoreHub uses FastAPI + React + PostgreSQL.

Relevant concepts:

- REST APIs
- Pydantic schemas
- transactions
- auth/authz
- response models
- WebSockets
- concurrent updates
- idempotency

### Live scores

REST can manage durable match state; WebSockets can push live updates.

### Concurrent update question

Discuss transaction boundaries, row-level locking or optimistic concurrency, event ordering and authoritative DB state.

[Back to Table of Contents](#table-of-contents)

<a id="43-generic-interview-qa"></a>
## 43. Generic Interview Q&A

### Q1. What is FastAPI?
A Python API framework using type hints, ASGI, validation, dependency injection and OpenAPI.

### Q2. What is a path operation?
A route definition containing HTTP method, path and endpoint function.

### Q3. Path vs query parameter?
Path identifies a resource in the URL; query parameters usually filter, sort or modify retrieval.

### Q4. What is Pydantic used for?
Request/response schemas, validation and serialization.

### Q5. What is `Depends`?
A declaration that tells FastAPI to resolve and inject a dependency.

### Q6. What is middleware?
A request/response wrapper for cross-cutting behavior.

### Q7. What is CORS?
Browser-controlled cross-origin access policy.

### Q8. What is `HTTPException`?
A way to return a defined HTTP error response.

### Q9. What is `BackgroundTasks`?
Lightweight post-response work, not a distributed job queue.

### Q10. What is lifespan?
Application startup/shutdown resource management.

### Q11. FastAPI vs Flask?
FastAPI emphasizes typed API contracts, DI, OpenAPI and async support; Flask is intentionally minimal.

### Q12. FastAPI vs Django?
FastAPI is API-oriented; Django is broader/full-stack.

### Q13. What is APIRouter?
A modular group of path operations.

### Q14. What is OpenAPI?
A machine-readable description of an HTTP API.

### Q15. How should passwords be stored?
As secure password hashes, never plaintext.

### Q16. What is idempotency?
Repeating the same logical request does not create unintended additional effects.

### Q17. Why do external calls need timeouts?
To prevent a dependency from holding resources indefinitely.

### Q18. Why can retries be dangerous?
They can duplicate side effects and amplify load.

### Q19. How do workers share state?
Through external shared systems such as Redis/PostgreSQL, not normal Python globals.

### Q20. What makes an API production-ready?
Clear contracts, security, validation, timeouts, failure handling, observability, persistence and a scaling strategy.

[Back to Table of Contents](#table-of-contents)

<a id="44-internal-interview-qa"></a>
## 44. Internal Interview Q&A

### Q1. Why is FastAPI fast?
ASGI architecture plus efficient async I/O and optimized validation/serialization components.

### Q2. Is FastAPI asynchronous by default?
It supports both sync and async endpoints. Actual concurrency depends on endpoint/dependency behavior.

### Q3. What happens with `def` endpoints?
Synchronous endpoint execution can be handled in a threadpool rather than directly blocking the event loop.

### Q4. ASGI vs WSGI?
ASGI supports modern asynchronous application patterns; WSGI is the older synchronous interface.

### Q5. Uvicorn vs FastAPI?
Uvicorn runs the ASGI application; FastAPI defines the application.

### Q6. Starlette vs FastAPI?
Starlette provides core ASGI web functionality; FastAPI adds typed API/dependency/schema features.

### Q7. Why response models?
They define and control the output contract.

### Q8. Why dependency injection?
Explicit dependencies, lifecycle management, reuse and testing.

### Q9. Does async solve CPU-bound work?
No. CPU-heavy work needs appropriate process/native/worker strategies.

### Q10. How do you handle downstream failure?
Timeouts, bounded retries/backoff, appropriate circuit breaking, fallback/error mapping and observability.

[Back to Table of Contents](#table-of-contents)

<a id="45-project-questions"></a>
## 45. Project Questions

### SceneFlow

**Why FastAPI?** Typed contracts, DI, async-compatible I/O and Python AI ecosystem fit.

**How prevent long image processing from blocking?** Enqueue a job and let Celery workers process it.

**Why Redis?** Shared infrastructure for cache/queue coordination/temporary state according to subsystem.

**Why Qdrant?** Semantic vector similarity search.

**Why polling?** Simple asynchronous job-status synchronization; WebSockets are an alternative for push updates.

### URL Shortener

**What happens during redirect?** Path lookup → Redis → PostgreSQL fallback → redirect response.

**How prevent duplicate short codes?** Database unique constraint plus safe regeneration on collision.

### ScoreHub

**How support live scores?** REST for durable resources and WebSockets/events for live delivery.

**How handle simultaneous updates?** Transaction boundaries, locking/concurrency control, ordering and authoritative DB state.

[Back to Table of Contents](#table-of-contents)

<a id="46-implementation-drills"></a>
## 46. Implementation Drills

Write these without help:

1. Basic health endpoint.
2. Pydantic request + response models.
3. `Depends` database dependency with cleanup.
4. Auth dependency.
5. Request-ID middleware.
6. CORS configuration.
7. Background task.
8. `POST /jobs` + `GET /jobs/{id}`.
9. External `httpx` client with timeout.
10. WebSocket endpoint.
11. Token-bucket rate limiter, then Redis version.
12. Router → service → repository → database architecture.

[Back to Table of Contents](#table-of-contents)

<a id="47-interview-traps"></a>
## 47. Interview Traps

- "FastAPI is asynchronous." → It supports both sync and async; code beneath matters.
- "CORS is authentication." → False.
- "BackgroundTasks is Celery." → False.
- "JWT is encrypted." → Not necessarily; typical JWTs are signed/encoded.
- "Redis is just a cache." → Too narrow.
- "Workers share Python globals." → False; processes have separate memory.
- "Async makes CPU work faster." → False.
- "Response models are only documentation." → False; they control output validation/serialization/filtering.
- "Pydantic makes arbitrary business logic secure." → False; validation is only one security layer.

[Back to Table of Contents](#table-of-contents)

<a id="48-final-checklist"></a>
## 48. Final Checklist

Be able to explain from memory:

- FastAPI
- ASGI / Uvicorn / Starlette
- request lifecycle
- routing and APIRouter
- path/query/body/header/cookie parameters
- Pydantic
- response models
- status codes
- validation/errors
- dependency injection and caching
- auth vs authorization
- OAuth2/JWT/password hashing
- middleware
- CORS
- BackgroundTasks
- lifespan
- async/await and event-loop blocking
- DB sessions/transactions
- service/repository architecture
- OpenAPI
- uploads/forms/streaming
- WebSockets
- rate limiting
- caching
- idempotency
- external API handling
- timeouts/retries/circuit breakers
- queues and Celery
- Redis
- testing and dependency overrides
- configuration/security
- deployment/workers
- observability/performance
- SceneFlow architecture
- URL Shortener flow
- ScoreHub real-time design

### Final architecture muscle memory

```text
React
  ↓
HTTPS
  ↓
Reverse Proxy / Load Balancer
  ↓
Uvicorn / ASGI
  ↓
FastAPI Router
  ↓
Dependencies + Validation
  ↓
Service Layer
  ├── PostgreSQL
  ├── Redis
  ├── Celery
  ├── Gemini
  ├── Image Providers
  └── Qdrant
  ↓
Pydantic Response
  ↓
React
```

[Back to Table of Contents](#table-of-contents)
