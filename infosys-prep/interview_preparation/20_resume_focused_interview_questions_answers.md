# Resume-Focused Interview Questions and Answers

## Table of Contents

- [How to Use This File](#how-to-use-this-file)
- [Important Accuracy Rule](#important-accuracy-rule)
- [Resume Summary](#resume-summary)
- [Basic Technology Questions](#basic-technology-questions)
- [Skills](#skills)
- [SceneFlow Project](#sceneflow-project)
- [SceneFlow Architecture](#sceneflow-architecture)
- [SceneFlow Core Implementation](#sceneflow-core-implementation)
- [SceneFlow Trade-offs](#sceneflow-trade-offs)
- [SceneFlow Architecture Questions](#sceneflow-architecture-questions)
- [URL Shortener Project](#url-shortener-project)
- [URL Shortener Architecture](#url-shortener-architecture)
- [URL Shortener Core Implementation](#url-shortener-core-implementation)
- [URL Shortener Trade-offs](#url-shortener-trade-offs)
- [URL Shortener Architecture Questions](#url-shortener-architecture-questions)
- [Internship — Wexdi Software Solutions](#internship--wexdi-software-solutions)
- [Education](#education)
- [Achievements](#achievements)
- [Cross-Resume Technical Questions](#cross-resume-technical-questions)
- [Resume Keyword Questions](#resume-keyword-questions)
- [Resume Traps](#resume-traps)
- [Final Resume Checklist](#final-resume-checklist)

<a id="table-of-contents"></a>

<a id="how-to-use-this-file"></a>
## How to Use This File

[Back to Table of Contents](#table-of-contents)

This file is based on your submitted resume **and a direct inspection of the actual source code and project documentation in both GitHub repositories**.

The project answers below are therefore separated into:
- **Verified from code/docs** — safe to state as implemented.
- **Interview framing** — simple language for explaining the verified implementation.
- **Trade-off** — why the design was used and what another design would change.

Do not add features that are not present in the repositories during the interview.

<a id="important-accuracy-rule"></a>
## Important Accuracy Rule

[Back to Table of Contents](#table-of-contents)

There is one important detail to remember for SceneFlow:

The repository's current V2 documentation says **Authentication + Authorization is still Phase 10 and not completed**. The code has a development-only `get_current_user()` dependency based on a configured development user ID. So do not say that full JWT authentication is already implemented in the current repository.

The resume mentions authorization, so a safe explanation is:

"I designed the application with an authorization dependency point and ownership checks in the service layer, but the full JWT-based authentication phase is still a planned next phase in the repository."

That is more accurate than claiming production JWT authentication exists.

For URL Shortener, the code currently implements Redis-based rate limiting, but its behavior is intentionally **fail-open** when Redis is unavailable. That means requests are allowed through when the limiter cannot reach Redis.

<a id="resume-summary"></a>
## Resume Summary

[Back to Table of Contents](#table-of-contents)

Your resume describes your main strength as Python backend development using FastAPI, Django, PostgreSQL and REST APIs, along with caching, asynchronous processing and authentication-related work. The project source confirms substantial backend work around APIs, PostgreSQL, Redis, Celery and vector retrieval. 

### Tell me about your technical background.

**Answer:**

"My main area is backend development. I mainly work with Python, FastAPI and Django, along with PostgreSQL and REST APIs. In my projects I have also worked with Redis, Celery, Docker and vector search. I like backend work because I enjoy understanding how data moves through a system and how different parts of an application work together."

### Which area are you strongest in?

**Answer:**

"I am most comfortable with Python backend development, APIs and databases. I am also becoming stronger in system design and AI-based applications."

---

<a id="skills"></a>
<a id="basic-technology-questions"></a>
## Basic Technology Questions

[Back to Table of Contents](#table-of-contents)

These are the simple questions interviewers can ask directly from the names in your resume. Keep these answers very basic first. Go deeper only when they ask.

### What is Python?

**Answer:**

"Python is a high-level programming language. It has simple syntax and is used for backend development, automation, data work and AI. I mainly use it for backend development."

**Follow-up: What makes Python popular?**

"It is easy to read, has a large number of libraries and lets us build applications quickly."

**Follow-up: Is Python compiled or interpreted?**

"Python code is generally compiled to bytecode first and then executed by the Python virtual machine. In normal interview terms, we usually call Python an interpreted language."

### What is SQL?

**Answer:**

"SQL is a language used to work with relational databases. We use it to read, insert, update and delete data, and also to join and analyze data."

**Follow-up: Where did you use SQL?**

"I used SQL mainly with PostgreSQL and MySQL for application data and queries."

**Follow-up: SQL vs NoSQL?**

"SQL databases use a structured relational model. NoSQL is a broader category of databases that can use different models such as document, key-value or wide-column storage."

### What is FastAPI?

**Answer:**

"FastAPI is a Python web framework mainly used for building APIs. It gives request validation, routing and support for asynchronous code."

**Follow-up: Why did you choose it?**

"My projects are mainly API-based with separate React frontends, so FastAPI was a good fit."

### What is Django?

**Answer:**

"Django is a Python web framework that provides many common features for building web applications, including models, URLs, views, authentication and an ORM."

**Follow-up: Why did you use Django in the internship?**

"The client application had business workflows, users, roles and database operations, so Django was a practical fit."

### What is REST API?

**Answer:**

"A REST API is a way for applications to communicate over HTTP using resources and standard operations such as GET, POST, PUT, PATCH and DELETE."

**Follow-up: Give an example from your project.**

"For the URL shortener, the frontend sends an HTTP request to the FastAPI backend to create a short URL, and the backend returns the result as JSON."

### What is Pydantic?

**Answer:**

"Pydantic is used to define and validate data structures in Python. In FastAPI, I use it to validate request and response data."

### What is PostgreSQL?

**Answer:**

"PostgreSQL is a relational database. It stores data in tables and supports SQL, transactions, constraints and relationships between data."

### What is MySQL?

**Answer:**

"MySQL is also a relational database that uses SQL. I have used it as part of my database knowledge and application work."

### PostgreSQL vs MySQL?

**Answer:**

"Both are relational databases and support SQL. PostgreSQL is the one I have used more in my recent projects."

### What is SQLAlchemy?

**Answer:**

"SQLAlchemy is a Python library for working with relational databases. It lets the application work with database models and queries from Python."

### What is an ORM?

**Answer:**

"ORM means Object-Relational Mapping. It lets application code work with database records through programming language objects instead of writing every query manually."

### What is Alembic?

**Answer:**

"Alembic is a database migration tool commonly used with SQLAlchemy. It helps manage schema changes in a controlled way."

### What is Redis?

**Answer:**

"Redis is a fast in-memory data store. It is commonly used for caching, temporary data, counters and messaging."

**Follow-up: How did you use Redis?**

"In the URL shortener I used it for redirect caching and rate limiting. In SceneFlow it is used as the Celery message broker."

### What is Celery?

**Answer:**

"Celery is a background task system. It lets the application send a task to a worker so slow work can happen outside the normal API request."

### What is Qdrant?

**Answer:**

"Qdrant is a vector database. It stores vectors and can find vectors that are similar to a given query vector."

### What is an embedding?

**Answer:**

"An embedding is a list of numbers that represents data in a form that a model or search system can compare. Similar meanings can have nearby vectors."

### What is Docker?

**Answer:**

"Docker packages an application and its dependencies into an image that can run as a container. This helps keep the environment consistent."

### What is a Docker container?

**Answer:**

"A container is a running instance of a Docker image. It gives the application an isolated environment while sharing the host kernel."

### What is Git?

**Answer:**

"Git is a version control system. It tracks code changes and helps developers work on different versions and collaborate safely."

### What is Linux?

**Answer:**

"Linux is an operating system family widely used for servers and development. I use Linux for development, running services and command-line work."

### What is Postman?

**Answer:**

"Postman is a tool for testing APIs. I use it to send requests and check responses, headers, authentication and error cases."

### What is React?

**Answer:**

"React is a JavaScript library for building user interfaces using reusable components."

### What is JavaScript?

**Answer:**

"JavaScript is a programming language widely used for web applications. I mainly use it on the frontend with React."

### What is TypeScript?

**Answer:**

"TypeScript is JavaScript with a type system. It helps catch many mistakes earlier and makes larger frontend codebases easier to maintain."

### What is Nginx?

**Answer:**

"Nginx is a web server and reverse proxy. It can receive client requests and forward them to backend services, and it can also serve static frontend files."

### What is Docker Compose?

**Answer:**

"Docker Compose lets me define and run multiple related containers together, such as an API, PostgreSQL and Redis."

### What is async programming?

**Answer:**

"Async programming lets the application handle waiting operations, such as network or database calls, without blocking the whole flow while it waits."

### What is caching?

**Answer:**

"Caching means storing frequently used data in a faster place so we do not have to calculate or fetch it again every time."

### What is rate limiting?

**Answer:**

"Rate limiting controls how many requests a client can make in a certain time. It helps protect the service from excessive traffic."

### What is an HTTP API?

**Answer:**

"It is an API that communicates using HTTP requests and responses. The request usually contains a method, URL and optional headers/body, and the server returns a status code and response data."

### What is authentication?

**Answer:**

"Authentication checks who the user is."

### What is authorization?

**Answer:**

"Authorization checks what the authenticated user is allowed to do."

### What is background processing?

**Answer:**

"It means moving slow work out of the normal user request so the user does not have to wait for the whole operation."

---


## Skills

[Back to Table of Contents](#table-of-contents)

Your resume lists Python, SQL, JavaScript, React.js, FastAPI, Django, REST APIs, Pydantic, PostgreSQL, MySQL, SQLAlchemy, Alembic, Redis, Celery, Qdrant, Git, Docker, Linux and Postman.

## Skills — Specific Interview Questions

[Back to Table of Contents](#table-of-contents)

This section is for the exact skill names on your resume. The interviewer can point at one skill and keep asking deeper follow-ups.

### Python

**Q: Why do you use Python?**

**Answer:** "I like Python because the syntax is simple and it lets me build backend and AI applications quickly."

**Q: What are mutable and immutable objects?**

**Answer:** "Mutable objects can be changed after creation, like lists and dictionaries. Immutable objects cannot be changed after creation, like strings and tuples."

**Q: List vs tuple?**

**Answer:** "A list is mutable, while a tuple is immutable. I use a list when the data may change and a tuple when it should stay fixed."

**Q: What is a dictionary and why is lookup fast?**

**Answer:** "A dictionary stores key-value pairs. It normally gives very fast average lookup because it uses hashing."

**Q: What is a decorator?**

**Answer:** "A decorator wraps a function and adds or changes its behavior without changing the main function code."

**Q: What is a generator?**

**Answer:** "A generator produces values one at a time instead of keeping all values in memory at once. I would use it when working with large or streaming data."

### SQL

**Q: What is the difference between WHERE and HAVING?**

**Answer:** "WHERE filters rows before grouping. HAVING filters groups after GROUP BY."

**Q: INNER JOIN vs LEFT JOIN?**

**Answer:** "INNER JOIN returns matching rows from both tables. LEFT JOIN keeps every row from the left table even when there is no match on the right."

**Q: What is an index?**

**Answer:** "An index helps the database find rows faster for suitable queries, but it also takes storage and can make writes more expensive."

**Q: What is a transaction?**

**Answer:** "A transaction groups database operations so they are handled as one unit. Either the required changes succeed together or they are rolled back."

### JavaScript

**Q: let vs const?**

**Answer:** "Both are block-scoped. A let variable can be reassigned, while a const binding cannot be reassigned."

**Q: What is a Promise?**

**Answer:** "A Promise represents a value that may be available later, usually for asynchronous work."

**Q: What is async/await?**

**Answer:** "It is a cleaner way to write asynchronous code using Promises. await pauses that async function until the Promise settles."

**Q: What is the event loop?**

**Answer:** "The event loop helps JavaScript handle asynchronous work by coordinating the call stack with queues of callbacks and other tasks."

### React.js

**Q: What is a React component?**

**Answer:** "A component is a reusable part of the UI. It receives data through props and can keep changing data in state."

**Q: Props vs state?**

**Answer:** "Props come from the parent and are read by the component. State is data managed by the component that can change over time."

**Q: Why are keys used in React lists?**

**Answer:** "Keys help React identify which list items changed, were added or removed."

**Q: What is useEffect used for?**

**Answer:** "It is used for side effects such as API calls, subscriptions or other work that should happen because of a render or state change."

**Q: How does React call your backend?**

**Answer:** "Usually through HTTP requests to REST API endpoints. The response data is then stored in React state and shown in the UI."

### FastAPI

**Q: What is FastAPI?**

**Answer:** "FastAPI is a Python framework for building APIs. It gives routing, request validation and automatic API documentation."

**Q: Why Pydantic in FastAPI?**

**Answer:** "Pydantic validates and structures request and response data so the API works with predictable data."

**Q: What is dependency injection in FastAPI?**

**Answer:** "It lets a route receive things it depends on, such as a database session or current user, without creating them directly inside the route."

**Q: What is async in FastAPI?**

**Answer:** "Async helps when the application spends time waiting for things like database or network operations, so the server can handle other work while waiting."

**Q: Async vs sync?**

**Answer:** "Sync code waits for the operation to finish before continuing. Async code can give control back while waiting for an I/O operation."

### Django

**Q: What is Django?**

**Answer:** "Django is a Python web framework that provides common features such as routing, models, authentication, forms and an ORM."

**Q: What is Django ORM?**

**Answer:** "The ORM lets the application work with database records using Python objects and query methods instead of writing every SQL statement manually."

**Q: What is middleware?**

**Answer:** "Middleware is code that runs around the request and response flow. It can be used for things like authentication, logging or other common request processing."

**Q: What is a migration?**

**Answer:** "A migration is a versioned change to the database schema, such as creating a table or adding a column."

### REST APIs

**Q: GET vs POST?**

**Answer:** "GET is mainly used to retrieve data. POST is mainly used to send data to create or trigger something on the server."

**Q: PUT vs PATCH?**

**Answer:** "PUT is generally used for replacing a resource representation. PATCH is used for partial updates."

**Q: What is a status code?**

**Answer:** "It tells the client what happened to the request. For example, 200 means success, 201 means created, 400 means bad request and 404 means not found."

**Q: What is idempotency?**

**Answer:** "An operation is idempotent when repeating the same request has the same intended final effect as doing it once."

### Pydantic

**Q: Why not just use a normal Python dictionary?**

**Answer:** "A dictionary does not automatically enforce the structure and types I expect. Pydantic gives validation and a clear data model."

### PostgreSQL

**Q: PostgreSQL vs MySQL?**

**Answer:** "Both are relational databases and both support SQL. PostgreSQL is the database I have used more in my recent projects."

**Q: What is normalization?**

**Answer:** "Normalization is organizing relational data to reduce unnecessary duplication and update problems."

**Q: What is a foreign key?**

**Answer:** "A foreign key connects one table to another table and helps maintain valid relationships between records."

**Q: What is a unique constraint?**

**Answer:** "It prevents duplicate values in a column or combination of columns where uniqueness is required."

### MySQL

**Q: Have you used MySQL directly?**

**Answer:** "Yes, I have worked with MySQL, mainly around relational data and SQL queries. PostgreSQL is the database I have used more heavily in my recent projects."

**Q: What would you check when a query is slow?**

**Answer:** "I would first look at the query itself, filters, joins, indexes and the amount of data being scanned. I would use the database query plan when needed."

### SQLAlchemy

**Q: What is SQLAlchemy?**

**Answer:** "SQLAlchemy is a Python toolkit for working with SQL databases. It provides both SQL expression tools and an ORM."

**Q: ORM vs raw SQL?**

**Answer:** "ORM code is convenient for common application operations. Raw SQL can be useful when I need exact database-specific control or a complex query."

### Alembic

**Q: Why do you need Alembic if SQLAlchemy already defines models?**

**Answer:** "Models describe the application side, but the actual database schema also needs controlled versioned changes. Alembic manages those migrations."

### Redis

**Q: What data can Redis store?**

**Answer:** "Redis can store key-value data and also supports structures such as strings, lists, sets and hashes."

**Q: Why is Redis fast?**

**Answer:** "It keeps frequently accessed data in memory and is designed for very fast operations."

**Q: What is TTL?**

**Answer:** "TTL means time to live. It defines how long a key should remain before it expires."

**Q: Redis cache vs PostgreSQL?**

**Answer:** "Redis is mainly for fast temporary or cached data in my projects. PostgreSQL is the durable source of truth."

**Q: What if Redis goes down?**

**Answer:** "It depends on the use. In my URL shortener, the redirect path falls back to PostgreSQL. For SceneFlow, Redis is the Celery broker, so losing Redis affects background job processing."

### Celery

**Q: What is Celery?**

**Answer:** "Celery is a task queue system. It lets the application send work to worker processes instead of doing everything inside the API request."

**Q: Why Celery instead of a Python thread?**

**Answer:** "A task queue gives a clearer way to manage background work with separate workers, queueing and retries. A thread inside the API process is much more tied to that process."

**Q: What is a worker?**

**Answer:** "A worker is a process that takes queued tasks and executes them."

**Q: What is a broker?**

**Answer:** "The broker carries tasks from the producer to the workers. In my SceneFlow project, Redis is used for that."

### Qdrant

**Q: What is a vector database?**

**Answer:** "It stores vectors and lets us search for vectors that are close to a given query vector."

**Q: Why not a normal SQL LIKE query?**

**Answer:** "LIKE is based mainly on text matching. Vector search can compare semantic meaning."

**Q: What is an embedding?**

**Answer:** "It is a numeric vector created from data so that similar items can be compared in vector space."

**Q: What is cosine similarity?**

**Answer:** "It measures how similar two vectors are mainly by comparing their direction."

### Git

**Q: Git vs GitHub?**

**Answer:** "Git is the version control system. GitHub is a platform for hosting Git repositories and collaborating on them."

**Q: merge vs rebase?**

**Answer:** "Merge combines histories and creates a merge point when needed. Rebase moves commits onto a new base and creates a more linear history."

**Q: What is a pull request?**

**Answer:** "It is a way to propose code changes and review them before merging into another branch."

### Docker

**Q: What is Docker?**

**Answer:** "Docker packages an application and its dependencies into an image that can run as a container."

**Q: Image vs container?**

**Answer:** "An image is the packaged template. A container is a running instance of that image."

**Q: Why Docker in your projects?**

**Answer:** "It makes the environment more repeatable. I can run the backend and supporting services with the same setup instead of installing everything manually."

### Linux

**Q: What Linux commands do you use?**

**Answer:** "I commonly use commands such as ls, cd, grep, ps, top, curl, chmod, systemctl and basic networking commands."

**Q: Why Linux for backend work?**

**Answer:** "Most server environments use Linux, and it gives me a good command-line environment for running services, checking processes and reading logs."

### Postman

**Q: How do you test an API in Postman?**

**Answer:** "I choose the HTTP method, enter the URL, add the required headers or body, send the request and check the status code and response. I also test invalid input and error cases."

### Cross-Skill Follow-Ups

**Q: How do these technologies fit together in your project?**

**Answer:** "React is the frontend. FastAPI or Django handles the backend. PostgreSQL stores the main data. Redis handles caching, rate limiting or background-job messaging depending on the project. Celery handles long-running work, and Qdrant handles vector search in SceneFlow."

**Q: Which skill would you be most comfortable explaining in depth?**

**Answer:** "Python backend development, FastAPI, PostgreSQL and the backend architecture of my projects."

**Q: Which skill are you still learning more deeply?**

**Answer:** "I am still going deeper into cloud, DevOps and advanced AI systems. I know the basics and have used some of them in projects, and I am building more depth now."

### Why FastAPI?

**Answer:**

"I used FastAPI because the projects were API-focused and had separate React frontends. It gives me request validation with Pydantic and a clean way to organize API routes and services."

### Why Django?

**Answer:**

"I used Django during my internship because that application had a lot of normal business features such as models, users, permissions and database workflows. Django already gives many of those pieces."

### Why PostgreSQL?

**Answer:**

"In SceneFlow, PostgreSQL is the main relational database. The project has connected data such as users, projects, scripts, scenes, search jobs and assets, so a relational database fits the data well. The project documentation also specifically moved from SQLite to PostgreSQL because multiple workers needed reliable concurrent database access."

### Why Redis?

**Answer:**

"I used Redis for two different jobs. In SceneFlow it is the Celery message broker for background jobs. In the URL shortener it is used for redirect caching and rate limiting."

### Why Celery?

**Answer:**

"SceneFlow can take a long time to search different providers, create embeddings and process candidates. Celery moves that work out of the normal API request and lets workers process it separately."

### Why Qdrant?

**Answer:**

"Qdrant stores the asset vectors and lets the application search for similar vectors. It is useful for semantic retrieval, where exact words are not enough."

### Why Docker?

**Answer:**

"Docker packages the application and its dependencies so the setup is repeatable. The projects also use Docker Compose to run related services together during development."

---

<a id="sceneflow-project"></a>
## SceneFlow Project

[Back to Table of Contents](#table-of-contents)

### Tell me about SceneFlow.

**Answer:**

"SceneFlow is a semantic visual asset retrieval system. A user creates projects, scripts and scenes. For a scene, the system uses Gemini to turn the scene into structured visual information and visual search queries. It then searches Pexels, Pixabay and Openverse, stores the candidates in PostgreSQL, creates embeddings, uses Qdrant to retrieve similar candidates and finally ranks the results before showing them in the React frontend."

### What problem does it solve?

**Answer:**

"The problem is finding useful images for script scenes. Searching manually or using only exact keywords can miss relevant images. The system tries to understand the scene and then retrieve visually relevant candidates."

### What is the current high-level architecture?

**Answer:**

"The current V2 is a layered full-stack application. React sends requests to FastAPI. The API layer handles HTTP and validation. Services contain the application logic, and repositories handle database access. Long-running search work is sent to Celery through Redis. The worker talks to Gemini and the asset providers, stores candidates in PostgreSQL, indexes vectors in Qdrant, retrieves candidates and runs a ranking service. The frontend then reads the job state and results."

Architecture memory:

```text
React
  ↓
FastAPI Router
  ↓
Search Job
  ↓
Redis
  ↓
Celery Worker
  ├── Gemini
  ├── Pexels / Pixabay / Openverse
  ├── PostgreSQL
  └── Sentence Transformer → Qdrant
                         ↓
                   Ranking Service
                         ↓
                    Results API
                         ↓
                       React
```

### Why layered architecture?

**Answer:**

"I wanted HTTP handling, business logic and database code to stay separate. It makes the project easier to understand, test and change."

### What are the layers?

**Answer:**

"The router handles HTTP. The service layer contains the main application logic. The repository layer handles database access."

### Why not put SQL inside the router?

**Answer:**

"Then the route would have HTTP logic and database logic mixed together. Separating them makes the code easier to test and reuse."

### Why not make it microservices?

**Answer:**

"For this project, that would add more deployment and communication complexity than necessary. The current design keeps a modular backend while still separating the major responsibilities. I would split services later only when the scaling or team needs justify it."

<a id="sceneflow-architecture"></a>
## SceneFlow Architecture

[Back to Table of Contents](#table-of-contents)

### How does a search request move through the system?

**Answer:**

"The frontend starts the search. FastAPI validates the request and creates a search job. The job is sent through Redis to a Celery worker. The worker uses the stored scene analysis, calls the asset providers, saves the candidates in PostgreSQL, indexes them in Qdrant and then retrieves and ranks the candidates. The job is marked completed, and the frontend can display the results."

### Why create a SearchJob record?

**Answer:**

"It gives the system a persistent record of the work and its state. Instead of keeping the request open, the frontend can check whether the job is pending, running, completed or failed."

### Why polling?

**Answer:**

"Because the search can take longer than a normal HTTP request. The frontend can submit the job and then check the status separately."

### Why not WebSockets?

**Answer:**

"Polling is simpler for this use case and was enough for the current product flow. WebSockets could give more immediate updates, but they would add more connection management. If real-time progress became important, I could consider WebSockets or server-sent events."

### How is the job made idempotent?

**Answer:**

"The Celery task first checks the existing job status. If it is already running or completed, it stops instead of doing the same work again. The task is also designed so logical failures are marked as failed rather than blindly retried."

### What does the code actually retry?

**Answer:**

"The startup part of the Celery task retries database-related initialization failures with exponential delays. The later part does not blindly retry logical failures such as an unanalyzed scene."

### Why is that important?

**Answer:**

"A logical problem will not be fixed by repeating the same task. Retrying should be used mainly for temporary failures."

### What happens if Qdrant indexing fails?

**Answer:**

"In the current workflow, PostgreSQL persistence is kept successful and the indexing error is logged. The worker then continues to the later retrieval stage. So the design treats vector indexing as a secondary step rather than making the main database write depend on it."

### Is that a trade-off?

**Answer:**

"Yes. It improves availability of the primary data, but it also means PostgreSQL and Qdrant can become temporarily inconsistent. A production version could add an outbox or reindex job so failed indexing is repaired later."

### Why PostgreSQL plus Qdrant instead of one database?

**Answer:**

"PostgreSQL is the source of truth for structured application data. Qdrant is specialized for vector similarity search. Keeping those responsibilities separate makes each part simpler for its job."

### Could you use pgvector instead of Qdrant?

**Answer:**

"Yes. That would reduce the number of systems to operate. The trade-off is that a dedicated vector database gives a clearer separation for vector search. For a smaller system, pgvector could be a reasonable alternative."

---

<a id="sceneflow-core-implementation"></a>
## SceneFlow Core Implementation

[Back to Table of Contents](#table-of-contents)

### How does Gemini work in the current code?

**Answer:**

"Gemini is used as a scene-intelligence service. A prompt file is loaded, the scene text is inserted into it, and Gemini returns a structured Pydantic result such as a summary, subjects, actions, mood and visual queries."

### Why structured output instead of plain text?

**Answer:**

"Plain text would be harder to parse reliably. Structured output gives the backend a known shape, so the rest of the code can work with fields directly."

### Why are prompts stored separately?

**Answer:**

"It keeps prompt wording separate from Python code. That makes prompts easier to read, review and change without mixing them with application logic."

### Does Gemini search the image providers?

**Answer:**

"No. Gemini only produces the structured visual understanding and queries. A separate provider service calls Pexels, Pixabay and Openverse."

### Why separate the Gemini service from provider search?

**Answer:**

"They are different responsibilities. Gemini understands the scene; provider services retrieve images. Keeping them separate makes each part easier to change."

### How are providers handled?

**Answer:**

"The asset search service runs the configured providers concurrently using asyncio. Each provider gets its own result status, so one provider failure does not automatically fail the others."

### Why concurrent provider search?

**Answer:**

"Because the provider calls are network-bound. Running them concurrently reduces total waiting time compared with waiting for one provider and then starting the next."

### What happens if one provider fails?

**Answer:**

"The failure is stored as a failed provider result, while successful provider results are still collected."

### How are duplicate assets removed?

**Answer:**

"The provider aggregation code first checks a provider-specific asset ID and then the image URL. If either identifies an already-seen asset, it is skipped."

### What embedding flow is used?

**Answer:**

"The system converts asset information into embedding text, generates vectors with the Sentence Transformer service and upserts them into Qdrant."

### How is retrieval performed?

**Answer:**

"For each visual query, the system creates a query embedding and compares it with stored asset vectors. For each asset, it keeps the maximum similarity across the query vectors."

### Why maximum similarity across multiple queries?

**Answer:**

"A scene can produce more than one useful visual query. Maximum similarity lets an asset be strongly related to at least one of those queries without requiring it to match every query."

### How does final ranking work?

**Answer:**

"Vector similarity is the strongest signal, but the final rank also considers image resolution and orientation. The current ranking code uses 70% semantic score, 15% resolution and 15% orientation."

### Why not use only cosine similarity?

**Answer:**

"An image can be semantically correct but still be a poor result for the requested format or resolution. The extra rules make the result more useful to the actual application."

### Why deterministic ranking?

**Answer:**

"I wanted consistent results. The ranking code uses fixed weights and tie-breakers instead of another AI model, so the ordering is easier to explain and reproduce."

### What are the tie-breakers?

**Answer:**

"First final score, then semantic score, then pixel count, then provider name and provider asset ID."

<a id="sceneflow-trade-offs"></a>
## SceneFlow Trade-offs

[Back to Table of Contents](#table-of-contents)

### FastAPI vs Django

**Why FastAPI:**
"The V2 frontend is separate and the backend is mainly an API service. FastAPI fits that structure well and gives Pydantic validation and async support."

**Why not Django:**
"Django could also build this system, but the current design does not need Django templates or its full-stack web features. The project documentation explicitly chose FastAPI for the decoupled API architecture."

### PostgreSQL vs SQLite

**Why PostgreSQL:**
"The project moved to PostgreSQL because several Celery workers may read and write scene and asset data concurrently. PostgreSQL is better suited for that shared production-style workload."

**Why not SQLite:**
"It is very convenient for small local projects, but concurrent writes become a limitation for this workload."

### Celery + Redis vs FastAPI BackgroundTasks

**Why Celery:**
"The work is long-running and should be handled by a worker system. Celery also gives retries and a separate worker pool."

**Why not BackgroundTasks:**
"FastAPI BackgroundTasks is simpler, but it is tied more closely to the application process. It is not the same kind of durable distributed worker setup."

### Qdrant vs PostgreSQL-only search

**Why Qdrant:**
"The application needs vector similarity search."

**Why not PostgreSQL-only:**
"A relational database is excellent for structured data, but a dedicated vector store makes the vector-search part more focused."

### Multi-provider search vs one provider

**Why multiple providers:**
"It increases the chance of finding useful results and gives provider failure isolation."

**Trade-off:**
"More APIs mean more failure cases, rate limits, normalization work and maintenance."

### Polling vs WebSockets

**Why polling:**
"Simple and enough for the current requirement."

**Trade-off:**
"More repeated requests and less immediate updates."

### Heuristic ranking vs LLM reranking

**Why heuristic ranking:**
"Predictable, cheap, fast and easy to explain."

**Trade-off:**
"It may not capture complex semantic preferences as well as a stronger learned reranker."

### PostgreSQL write before Qdrant indexing

**Why:**
"The main application data stays persisted even if the vector index has a temporary problem."

**Trade-off:**
"The two systems can temporarily disagree, so reindexing is important."

### One Celery worker queue vs separate specialized queues

**Current style:**
"The project uses the Celery worker setup without splitting this workflow into many specialized queues."

**Trade-off:**
"Separate queues could isolate heavy jobs later, but would add configuration and deployment complexity."

---

<a id="sceneflow-architecture-questions"></a>
## SceneFlow Architecture Questions

[Back to Table of Contents](#table-of-contents)

### Draw the architecture on a whiteboard.

Say:

"React frontend → FastAPI API → SearchJob → Redis → Celery worker → Gemini/provider search → PostgreSQL and Qdrant → deterministic ranking → results."

Then explain each arrow.

### What if Gemini is down?

"Scene analysis cannot continue for a new request, so the service should return a failed job state or retry when the failure looks temporary. Existing stored scene analysis can still be reused by the later search task."

### What if Pexels is down?

"The provider result is marked failed, but Pixabay and Openverse can still return results."

### What if Redis is down?

"The Celery queue path would be affected because Redis is the broker in the current architecture. That is a more serious dependency than Redis being only a cache."

### What if PostgreSQL is down?

"The main application state cannot be safely read or written. The API and workers should fail clearly rather than pretending the operation succeeded."

### What if the same search job is delivered twice?

"The task checks the job state and stops when the job is already running or completed. That protects against duplicate work."

### How would you scale SceneFlow?

"I would add more Celery workers for background load, keep the API stateless so it can have multiple instances, scale PostgreSQL appropriately, and monitor provider latency, job queue depth and failure rates."

### What is the main bottleneck?

"The external provider calls and background processing are likely to dominate latency for a search job. Database and vector retrieval also become important as the candidate volume grows."

### How would you improve reliability?

"I would add better retry policies for temporary provider failures, a repair/reindex mechanism for Qdrant, stronger monitoring and possibly separate queues for different job types."

---

<a id="url-shortener-project"></a>
## URL Shortener Project

[Back to Table of Contents](#table-of-contents)

The repository confirms a FastAPI backend, React frontend, PostgreSQL, Redis, Docker, Docker Compose, Nginx, Alembic and Railway deployment. The application uses a layered API/service/repository structure.

### Tell me about the URL Shortener.

**Answer:**

"It is a service that converts a long URL into a short code. When the short code is requested, the backend finds the target URL and redirects the user. I focused on the parts that make a simple URL shortener work reliably under repeated requests, especially caching, uniqueness, rate limiting and concurrent click counting."

### Why build this project?

**Answer:**

"I wanted a small project where I could understand backend system design clearly. It gave me a chance to work on caching, database constraints, rate limiting and concurrency in one system."

<a id="url-shortener-architecture"></a>
## URL Shortener Architecture

[Back to Table of Contents](#table-of-contents)

### What is the architecture?

**Answer:**

"The frontend talks to the FastAPI API for creating and managing URLs. The backend has API, service and repository layers. PostgreSQL stores the URL records. Redis is used for redirect caching and rate limiting. Nginx is used in the deployed architecture, and Docker Compose runs the full local stack."

Architecture memory:

```text
React
  ↓
FastAPI
  ├── API layer
  ├── Service layer
  └── Repository layer
       ├── PostgreSQL
       └── Redis
              ├── cache
              └── rate limiter
```

### Explain a redirect request.

**Answer:**

"The user sends the short code. The service checks Redis first. If there is a cache hit, it gets the target data quickly. If there is a miss, it reads PostgreSQL and then stores the result in Redis with a TTL. It validates whether the URL is active or expired and then increments the click count using an atomic database update."

### Why PostgreSQL as source of truth?

**Answer:**

"PostgreSQL stores the durable URL record. Redis can lose cached data or become unavailable, so I don't depend on it as the main source."

### Why cache-aside?

**Answer:**

"The application checks the cache first and loads from the database on a miss. This is simple and works well for redirect traffic because the same short codes can be requested many times."

### Why TTL?

**Answer:**

"The cache should not live forever. A TTL limits how long cached information stays there. The code also reduces the TTL when the URL has an earlier expiration time."

### What happens when Redis is down?

**Answer:**

"The service catches the Redis error and falls back to PostgreSQL. The redirect still works, although it may be slower."

### Is Redis failure completely harmless?

**Answer:**

"No. The redirect path has a database fallback, but the rate limiter also uses Redis. The current rate limiter is fail-open, so if Redis is unavailable, URL creation is allowed instead of blocked."

### Why fail-open for rate limiting?

**Answer:**

"The project prioritizes keeping the core URL creation path available. The trade-off is that during Redis failure the rate limit is not enforced."

### Would you choose fail-open in a security-sensitive system?

**Answer:**

"Not always. For an endpoint where abuse itself is the main security risk, I may prefer fail-closed or another protection mechanism. It depends on what is more important: availability or strict request control."

<a id="url-shortener-core-implementation"></a>
## URL Shortener Core Implementation

[Back to Table of Contents](#table-of-contents)

### How is the short code generated?

**Answer:**

"The code uses Python's `secrets` module to generate a random seven-character string from a Base62 alphabet of uppercase letters, lowercase letters and digits."

### Why use `secrets` instead of `random`?

**Answer:**

"`secrets` is designed for stronger random values. Since short codes should not be predictable unnecessarily, it is a better choice."

### Is the seven-character code mathematically guaranteed unique?

**Answer:**

"No. There can still be a collision. That is why the database has a uniqueness constraint, and the service retries generation when an insert gets a uniqueness error."

### Why keep the uniqueness constraint if collisions are unlikely?

**Answer:**

"Because low probability is not a guarantee. The database should enforce the invariant that two records cannot use the same short code."

### Explain atomic click counting.

**Answer:**

"The repository runs an SQL update like `clicks = clicks + 1` directly in the database. It avoids reading the old value and then writing a new one in application code."

### Why is read-modify-write dangerous?

**Answer:**

"Two requests can read the same old value. Both may then write back the same incremented value, which loses one click."

### What rate limiter is implemented?

**Answer:**

"It is a Redis fixed-window limiter that allows 10 URL-creation requests per minute per client IP."

### Why fixed-window?

**Answer:**

"It is simple and easy to understand and implement. More advanced limiters can give smoother traffic control, but they also need more logic."

### What is the drawback of fixed-window rate limiting?

**Answer:**

"You can get a burst around the boundary of two windows. A sliding-window or token-bucket approach can control that more smoothly."

### Why use async SQLAlchemy?

**Answer:**

"The backend uses asynchronous FastAPI handlers and async database access. This fits a service that spends time waiting on the database and Redis."

### Why repository-service-route separation?

**Answer:**

"The route handles HTTP, the service contains the business rules and the repository handles database operations. It keeps the responsibilities separate."

<a id="url-shortener-trade-offs"></a>
## URL Shortener Trade-offs

[Back to Table of Contents](#table-of-contents)

### Random short code vs sequential ID encoded as Base62

**Current choice: random seven-character code.**

Why:
- harder to guess than simple sequential codes
- simple generation
- no direct exposure of database ID

Trade-off:
- collisions are possible
- each collision needs a database attempt and retry

Sequential ID + Base62 would give very predictable codes and simpler collision handling, but exposes ordering and makes enumeration easier.

### Redis cache vs no cache

Why cache:
- faster redirects
- fewer database reads

Trade-off:
- cache invalidation
- extra dependency
- stale data risk

The project reduces this risk using TTL and checks lifecycle information in cached data.

### Redis vs in-process cache

Redis is shared between application instances.

An in-process cache would be simpler but each API instance would have its own copy and would not share cache state.

### Fixed window vs token bucket

Fixed window is simpler.

Token bucket gives better control over bursts but is more complex.

### Nginx vs direct FastAPI exposure

Nginx can sit in front of the application and handle reverse-proxy duties.

Direct FastAPI exposure is simpler for a small deployment, but a reverse proxy gives a cleaner boundary for routing and deployment.

### PostgreSQL vs NoSQL

PostgreSQL fits because URL records, expiration and click data are simple relational data, and the project benefits from strong uniqueness and atomic updates.

A NoSQL store could also work at very large scale, but the access pattern here does not require giving up relational guarantees just for the sake of using NoSQL.

---

<a id="url-shortener-architecture-questions"></a>
## URL Shortener Architecture Questions

[Back to Table of Contents](#table-of-contents)

### What is the most important hot path?

"The redirect path. It can receive far more reads than URL-creation requests, so caching is important."

### What would you scale first?

"I would scale the API horizontally, keep redirect reads cached, and monitor PostgreSQL read load. At higher traffic, I would also consider database read replicas or a stronger caching layer."

### What if one API instance crashes?

"Another instance can continue serving if the service is behind a load balancer and shared state is in PostgreSQL and Redis."

### What if PostgreSQL is down but Redis has the URL?

"The current code can still return a cached redirect and incrementing the click count would still need database access, so the full request is not guaranteed to remain successful. I would separate redirect delivery from analytics counting if I needed the redirect path to survive a database outage."

### How would you improve click counting at very high traffic?

"I would consider buffering click events into a queue and processing them asynchronously, instead of doing a database write for every single redirect."

### Why not count clicks in Redis only?

"Redis would be faster, but then I need a reliable way to flush counts to durable storage. The current project keeps the count update simple and durable in PostgreSQL."

### How would you handle very popular URLs?

"Use Redis caching, increase API replicas and monitor database load. For very large traffic, a CDN or edge caching strategy could also be considered depending on the redirect requirements."

### How would you prevent abuse of URL creation?

"Rate limiting is the first layer. I would also consider stronger identity-based limits, abuse detection and authentication if the product requires it."

---

<a id="internship--wexdi-software-solutions"></a>
## Internship — Wexdi Software Solutions

[Back to Table of Contents](#table-of-contents)

Your resume says you worked as a Python Developer Intern and Trainee Developer at Wexdi Software Solutions, led a four-member development team for a Django-based client application and acted as a technical point of contact. Your additional interview preparation details establish that your main backend work was employee timesheet management.

### Tell me about your internship.

**Answer:**

"During my internship at Wexdi Software Solutions, I worked mainly on a Django-based client application. My main backend work was the employee timesheet workflow. Employees could create and edit timesheets and send them for approval. Managers could review, approve or deny them. I also worked on access levels so the right employees and managers could perform the right actions. Along with that, I coordinated a four-member frontend team and helped with debugging and client communication."

### What did you personally implement?

**Answer:**

"My main implementation area was the Django backend around timesheets, approval flow and access control. I also helped coordinate frontend work, but my technical focus was the backend."

### What is the timesheet workflow?

**Answer:**

"An employee creates a timesheet and can edit it before submission. After submitting it, the relevant manager reviews it. The manager can approve or deny it. The backend checks whether the user is allowed to perform the requested action."

### Why is backend permission checking important?

**Answer:**

"Because frontend buttons are not security. A user can call the API directly. The backend must check the user's role and access for every protected action."

### What if an employee tries to approve their own timesheet?

**Answer:**

"The backend should reject the action because approval is a manager operation and the user does not have that permission."

### How did the internship change your understanding of software development?

**Answer:**

"It showed me that real development is not only writing code. I also had to understand business rules, communicate requirements, coordinate with other people and debug issues that crossed different parts of the application."

---

<a id="education"></a>
## Education

[Back to Table of Contents](#table-of-contents)

Your resume lists a B.Tech in Computer Science from RGUKT with an 8.68 CGPA and a Pre University Course with a 9.78 CGPA.

### Tell me about your education.

**Answer:**

"I completed my B.Tech in Computer Science from RGUKT. I focused on programming, computer science fundamentals, coding practice and projects."

### How did academics help your projects?

**Answer:**

"Subjects like databases, operating systems, computer networks and programming gave me the basic ideas. Projects helped me connect those ideas to real software."

---

<a id="achievements"></a>
## Achievements

[Back to Table of Contents](#table-of-contents)

### Tell me about GATE.

**Answer:**

"I qualified GATE CS 2025. Preparing for it helped me strengthen my core computer science subjects and problem solving."

### Tell me about 550+ LeetCode problems.

**Answer:**

"I solved them mainly to improve problem solving and become comfortable with different patterns. I do not think the number itself is the main point. The important thing is whether I understand the problem and can explain the solution."

### Tell me about football captaincy.

**Answer:**

"I was the university football team captain. It taught me about responsibility, communication and staying calm under pressure."

### How is football relevant to software work?

**Answer:**

"It taught me that the team result matters, and that communication becomes more important when people have different roles."

---

<a id="cross-resume-technical-questions"></a>
## Cross-Resume Technical Questions

[Back to Table of Contents](#table-of-contents)

### Why FastAPI in SceneFlow and URL Shortener?

"Both projects are API-heavy and have separate React frontends. FastAPI gave me a clean way to build those APIs."

### Why PostgreSQL in both?

"It is a good fit for durable relational data and gives me constraints and transactions."

### Where is concurrency visible in your projects?

"In SceneFlow, multiple Celery workers can process jobs and multiple provider requests run concurrently. In the URL shortener, multiple redirect requests can update the same click counter, so the database update must be atomic."

### Where is caching used?

"In the URL shortener, Redis caches redirect data. SceneFlow uses Redis in a different role: as the Celery message broker."

### Where is asynchronous processing used?

"SceneFlow uses Celery for long-running search work. The URL shortener mainly uses async request/database/Redis access rather than a background job pipeline."

### What is authentication vs authorization?

"Authentication answers who the user is. Authorization answers what that user is allowed to do."

### What is the source of truth in each project?

"PostgreSQL is the source of truth for the main application records in both projects. Qdrant is for vectors in SceneFlow, and Redis is used as infrastructure rather than the main durable store."

---

<a id="resume-keyword-questions"></a>
## Resume Keyword Questions

[Back to Table of Contents](#table-of-contents)

### REST APIs

"What is REST?"

"REST is an architectural style for designing network APIs around resources and standard HTTP operations."

### Pydantic

"Why use Pydantic?"

"To validate and structure API data so the backend receives predictable input."

### SQLAlchemy

"Why use SQLAlchemy?"

"It lets the Python application work with relational database data through a Python API while still allowing explicit SQL when needed."

### Alembic

"Why use Alembic?"

"To manage database schema changes through migrations instead of manually changing production databases."

### Qdrant

"What is stored in Qdrant?"

"Vectors and related metadata used for similarity search."

### Celery

"What does a Celery worker do?"

"It picks up background tasks from the queue and executes the long-running work separately from the API process."

### Docker

"What is the difference between an image and a container?"

"An image is the package/template. A container is a running instance created from that image."

### Redis

"What happens if Redis is unavailable?"

"The answer depends on its role. In the URL shortener, the cache path falls back to PostgreSQL. In SceneFlow, Redis is the Celery broker, so losing it affects job submission and processing."

### Qdrant vs Redis

"Redis is used for fast key-value style data and the Celery broker in these projects. Qdrant is specifically used for vector similarity search."

---

<a id="resume-traps"></a>
## Resume Traps

[Back to Table of Contents](#table-of-contents)

### SceneFlow

Do not say:
- "JWT is fully implemented" — the repository says that phase is still planned.
- "Gemini searches Pexels" — it does not; Gemini produces scene intelligence and queries.
- "Qdrant is the main database" — PostgreSQL is the authoritative structured store.
- "Qdrant failure automatically fails all data persistence" — the current code logs indexing failure after PostgreSQL persistence.
- "Every provider is called sequentially" — provider search is concurrent.
- "Cosine similarity alone decides the final order" — deterministic reranking is applied afterward.

### URL Shortener

Do not say:
- "The database ID is encoded into Base62" — the current code generates a random seven-character Base62 string with `secrets`.
- "Redis is the source of truth" — PostgreSQL is.
- "Redis failure stops redirects" — redirect reads fall back to PostgreSQL.
- "Rate limiting is always enforced" — the current limiter fails open when Redis is unavailable.
- "Click counts are incremented in application memory" — the repository uses an atomic SQL update.

### General

Do not claim deeper ownership than you actually have.

Good phrases:
"I implemented..."
"I worked on..."
"In the current code..."
"The trade-off is..."
"I would improve this by..."

<a id="final-resume-checklist"></a>
## Final Resume Checklist

[Back to Table of Contents](#table-of-contents)

Before the interview, be able to explain:

### SceneFlow
- problem
- full architecture
- router/service/repository
- FastAPI
- PostgreSQL
- Celery
- Redis broker
- Gemini
- structured Pydantic scene analysis
- prompt files
- provider aggregation
- concurrent provider calls
- provider failure isolation
- asset persistence
- Sentence Transformer embeddings
- Qdrant
- query-vector similarity
- max similarity across multiple queries
- deterministic reranking
- 70/15/15 weights
- idempotent job behavior
- polling
- Qdrant failure trade-off
- PostgreSQL vs Qdrant
- Celery vs BackgroundTasks
- FastAPI vs Django
- polling vs WebSockets
- microservices vs modular monolith
- current authentication limitation

### URL Shortener
- full architecture
- API/service/repository layers
- random Base62
- `secrets`
- seven-character code
- uniqueness constraint
- collision retry
- Redis cache-aside
- TTL
- PostgreSQL fallback
- expiration and active-state checks
- atomic click counting
- fixed-window rate limiting
- fail-open trade-off
- Docker Compose
- Nginx
- Alembic
- async SQLAlchemy
- scaling the redirect path
- very high click traffic
- Redis vs in-process cache
- random code vs sequential code

### Internship
- Django backend
- timesheets
- create/edit
- submission
- approval request
- review
- approve/deny
- access levels
- backend permission checks
- four-member frontend coordination
- debugging
- client communication

The strongest project answer is not the longest answer.

It is the answer that is **accurate, simple, and backed by something you can point to in the code**.
