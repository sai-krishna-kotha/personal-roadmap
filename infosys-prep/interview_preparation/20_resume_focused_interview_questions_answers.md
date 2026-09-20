# Resume-Focused Interview Questions and Answers

## Table of Contents

- [How to Use This File](#how-to-use-this-file)
- [Resume Summary](#resume-summary)
- [Skills](#skills)
- [SceneFlow Project](#sceneflow-project)
- [URL Shortener Project](#url-shortener-project)
- [Internship — Wexdi Software Solutions](#internship--wexdi-software-solutions)
- [Education](#education)
- [Achievements](#achievements)
- [Cross-Resume Technical Questions](#cross-resume-technical-questions)
- [Why Questions](#why-questions)
- [Follow-Up Questions](#follow-up-questions)
- [Resume Traps](#resume-traps)
- [Final Resume Checklist](#final-resume-checklist)

<a id="table-of-contents"></a>

<a id="how-to-use-this-file"></a>
## How to Use This File

[Back to Table of Contents](#table-of-contents)

This file is based directly on the resume you plan to submit.

The rule for the interview is simple:

> Every word on your resume can become a question.

Do not claim something just because it is written on the resume. Be ready to explain:
- what you personally did
- why you chose it
- how it works
- what went wrong
- how you tested it
- what you would improve

Keep answers simple. Start with the basic idea, then add technical detail only when they ask.

---

<a id="resume-summary"></a>
## Resume Summary

[Back to Table of Contents](#table-of-contents)

Your resume summary says that you have hands-on experience with Python, FastAPI, Django, PostgreSQL and REST APIs, and that you worked with caching, asynchronous processing and authentication. fileciteturn344file0L4-L7

### They may ask: Tell me about your technical background.

**Answer:**

"My main area is backend development. I have mainly worked with Python, FastAPI and Django, along with PostgreSQL and REST APIs. I have also worked with Redis and Celery for caching and background processing. Recently I have been working more on system design, Docker and AI-related applications."

### They may ask: What do you mean by hands-on experience?

**Answer:**

"I have not only studied these technologies. I have used them in projects. For example, I used FastAPI and PostgreSQL in my URL shortener, and in SceneFlow I worked with FastAPI, PostgreSQL, Redis, Celery and Qdrant."

### Follow-up: Which area are you strongest in?

**Answer:**

"I am most comfortable with Python backend development, APIs and databases. I am also becoming stronger in system design and AI-based applications."

---

<a id="skills"></a>
## Skills

[Back to Table of Contents](#table-of-contents)

Your resume lists Python, SQL, JavaScript, React.js, FastAPI, Django, REST APIs, Pydantic, PostgreSQL, MySQL, SQLAlchemy, Alembic, Redis, Celery, Qdrant, Git, Docker, Linux and Postman. fileciteturn344file0L8-L14

### Python

### Why Python?

**Answer:**

"I like Python because the syntax is simple, it helps me build things quickly, and it has a strong ecosystem for backend development and AI."

### What is Python used for in your projects?

**Answer:**

"I used Python mainly for backend development. I used FastAPI and Django to build APIs and application logic."

### What Python feature do you use often?

**Answer:**

"I use functions, classes, exception handling, comprehensions and modules regularly. For backend projects, I also use type hints and Pydantic models."

### SQL

### How have you used SQL?

**Answer:**

"I used SQL mainly for working with PostgreSQL and MySQL, including joins, filtering, aggregation and database operations needed by my projects."

### Why PostgreSQL?

**Answer:**

"I chose PostgreSQL because it is a strong relational database and gives me transactions, constraints and good support for application data."

### JavaScript / React

### Why React?

**Answer:**

"I used React because it makes it easier to build the frontend as reusable components and manage changing application state."

### How does your frontend communicate with your backend?

**Answer:**

"Usually through HTTP REST APIs. The frontend sends a request, the backend validates it, performs the required work and returns a response, often as JSON."

### FastAPI

### Why FastAPI?

**Answer:**

"I like FastAPI because it makes API development simple, gives request validation through Pydantic and works well for building modern Python APIs."

### Django

### Why Django?

**Answer:**

"I used Django during my internship because it gives a lot of useful features such as models, authentication, routing and an ORM, which makes it practical for business applications."

### Pydantic

### Why Pydantic?

**Answer:**

"I use Pydantic to validate and structure data coming into the API. It helps make sure the backend receives the type and format I expect."

### PostgreSQL / MySQL

### PostgreSQL vs MySQL?

**Answer:**

"Both are relational databases and support SQL. PostgreSQL is the one I have used more recently in my projects, especially when I needed transactions, constraints and reliable relational data handling."

### SQLAlchemy

### Why SQLAlchemy?

**Answer:**

"SQLAlchemy lets Python code work with relational databases using Python objects and queries. It also gives me more control when I need database-specific behavior."

### Alembic

### What is Alembic?

**Answer:**

"Alembic is used to manage database schema changes. It lets me create and apply migrations in a controlled way."

### Redis

### Why Redis?

**Answer:**

"I used Redis mainly for fast caching and rate limiting. It is useful when I need very quick access to small pieces of data."

### Celery

### Why Celery?

**Answer:**

"I use Celery when a task should not block the API request. A user can start a job, and a worker can process it in the background."

### Qdrant

### What is Qdrant?

**Answer:**

"Qdrant is a vector database. I use it to store embeddings and find similar vectors, which is useful for semantic search."

### Docker

### Why Docker?

**Answer:**

"Docker helps package the application and its dependencies so I can run the same setup in different environments."

### Linux

### Why is Linux in your skill set?

**Answer:**

"I use Linux for development, running services, checking logs and working with command-line tools."

### Postman

### Why Postman?

**Answer:**

"I use Postman to test APIs quickly. It helps me check requests, responses, headers, authentication and error cases."

---

<a id="sceneflow-project"></a>
## SceneFlow Project

[Back to Table of Contents](#table-of-contents)

Your resume describes SceneFlow as a full-stack semantic asset retrieval system using React, TypeScript, FastAPI, PostgreSQL, Celery, Redis, Qdrant and Sentence Transformers. It includes a frontend workflow, an asynchronous Celery pipeline, multiple asset providers, vector retrieval, reranking, failure isolation, deduplication, authorization and idempotent job execution. fileciteturn344file0L15-L25

### Tell me about SceneFlow.

**Answer:**

"SceneFlow is a system that helps find relevant visual assets for scenes in a script. The user creates a project and scenes from the frontend. The backend creates a job, and the heavy work runs in the background. It searches different asset providers, stores the results, creates embeddings and uses Qdrant to find semantically relevant results."

### What problem does SceneFlow solve?

**Answer:**

"If someone has a script with many scenes, finding suitable images manually is slow. SceneFlow tries to automate part of that process by understanding the scene and finding visually relevant assets."

### What was your role?

**Answer:**

"I worked across the project, especially the backend flow and the integration between the frontend, API, background jobs, database and vector search."

### Why did you use FastAPI?

**Answer:**

"I needed APIs for projects, scripts, scenes and jobs. FastAPI made the API layer easy to build and validate."

### Why PostgreSQL?

**Answer:**

"I used PostgreSQL for the main application data such as projects, scenes, jobs and asset metadata."

### Why Redis?

**Answer:**

"Redis was useful for the background job system and fast temporary data."

### Why Celery?

**Answer:**

"Some work takes much longer than a normal API request, such as calling multiple providers and processing many candidate assets. I moved that work into Celery so the API could respond quickly."

### Why not do everything inside the API request?

**Answer:**

"Because long-running work can keep the request open for too long and can make the API slower. A background job lets the API return a job status and the worker can continue the work."

### Explain the job flow.

**Answer:**

"The frontend starts the search. The API validates the request and creates a job. Celery picks up the job. The worker analyzes the scene, calls the asset providers, stores candidates and runs the vector search. The frontend checks the job status and later displays the results."

### What does polling mean here?

**Answer:**

"The frontend sends requests at intervals to check whether the background job is completed. Once it is done, the frontend fetches the results."

### Why did you use Qdrant?

**Answer:**

"Qdrant lets me compare vectors efficiently. I can create an embedding for a scene or query and search for nearby vectors to find semantically similar assets."

### What is an embedding?

**Answer:**

"An embedding is a list of numbers that represents the meaning or features of some data. Similar items tend to have vectors that are close to each other."

### Why Sentence Transformers?

**Answer:**

"I needed a model that could turn text into useful vectors for similarity search. Sentence Transformers provides models designed for this kind of embedding task."

### What is cosine similarity?

**Answer:**

"It measures how similar two vectors are based mainly on their direction. In our case, a higher cosine similarity means the two embeddings are more semantically related."

### Why not use only keyword search?

**Answer:**

"Keyword search depends more on exact words. Semantic search can find related meaning even when the wording is different."

### What is reranking?

**Answer:**

"First I retrieve a set of candidates based on semantic similarity. Then I apply additional rules to order them, such as semantic relevance, image resolution and orientation."

### Why do reranking after vector search?

**Answer:**

"Vector similarity gives me a strong first filter, but similarity alone may not be enough. Reranking lets me consider other requirements before showing the final results."

### What is provider failure isolation?

**Answer:**

"If one image provider fails, I don't want the whole job to fail. I handle providers separately so the system can continue with the ones that are working."

### What is deduplication?

**Answer:**

"It means avoiding the same asset being stored or shown multiple times."

### What is idempotent job execution?

**Answer:**

"It means running the same job request again should not create incorrect duplicate work or duplicate data."

### How did you handle authorization?

**Answer:**

"I made sure a user can access only the projects and data they are allowed to access. The backend checks that before returning or changing data."

### What happens if Qdrant is unavailable?

**Answer:**

"I would treat it as a dependency failure, log the issue clearly and handle it without corrupting the main database data. Depending on the feature, I could retry or return a clear failure state."

### What happens if one asset provider is slow?

**Answer:**

"I would use timeouts so one provider does not block the entire job forever. The job can continue with other providers or retry when appropriate."

### What would you improve in SceneFlow?

**Answer:**

"I would improve monitoring, make job progress more visible, add stronger automated tests around the background pipeline and further improve retrieval quality."

---

<a id="url-shortener-project"></a>
## URL Shortener Project

[Back to Table of Contents](#table-of-contents)

Your resume describes a FastAPI, PostgreSQL, Redis, React and Docker URL shortener with layered route-service-repository design, secure 7-character Base62 codes, collision handling, cache-aside redirects, atomic click counting, fixed-window rate limiting, Alembic, Docker Compose and Railway deployment. fileciteturn344file0L26-L35

### Tell me about your URL shortener.

**Answer:**

"It is a service that converts a long URL into a short URL. When someone visits the short URL, the backend finds the original URL and redirects the user. I used FastAPI, PostgreSQL, Redis, React and Docker."

### Why did you build it?

**Answer:**

"I wanted a project where I could understand backend systems more deeply, especially caching, concurrency, rate limiting and database design."

### Explain the flow of a redirect.

**Answer:**

"The user sends the short code. The backend first checks Redis. If the URL is in the cache, it can redirect quickly. If not, it reads from PostgreSQL, returns the URL and can then cache it in Redis."

### Why Redis cache-aside?

**Answer:**

"Most redirect requests may ask for the same popular URLs repeatedly. Keeping those results in Redis reduces database reads and makes the response faster."

### What happens when Redis is down?

**Answer:**

"PostgreSQL remains the source of truth, so the application can fall back to the database. The cache failure should not completely stop redirects."

### Why use PostgreSQL as the source of truth?

**Answer:**

"The database provides durable storage and constraints. Redis is mainly a fast cache and should not be the only place where the URL exists."

### Why Base62?

**Answer:**

"Base62 uses letters and numbers, so a short code can represent many values using fewer characters."

### Why seven characters?

**Answer:**

"It gives a large enough space for the expected number of codes while keeping the URL short."

### What does collision mean here?

**Answer:**

"A collision means two generated codes point to the same code when they should be different. I handle this by keeping a database uniqueness constraint and retrying when there is a collision."

### Why is the database uniqueness constraint important?

**Answer:**

"Because application logic alone is not enough when multiple requests can happen at the same time. The database can guarantee that the code remains unique."

### What is atomic click counting?

**Answer:**

"It means incrementing the count in one safe database operation so concurrent requests do not overwrite each other's updates."

### Why rate limiting?

**Answer:**

"Without rate limiting, one client can send too many requests and affect the service. Rate limiting controls how many requests can be made in a given time."

### Why fixed-window rate limiting?

**Answer:**

"It is simple to implement and understand. For this project I used Redis to track request counts inside a fixed time window."

### What is layered architecture?

**Answer:**

"I separated the API route layer, service logic and database access. This keeps responsibilities clear and makes the code easier to test and change."

### Why Docker Compose?

**Answer:**

"It lets me run the backend, PostgreSQL and Redis together with a reproducible local setup."

---

<a id="internship--wexdi-software-solutions"></a>
## Internship — Wexdi Software Solutions

[Back to Table of Contents](#table-of-contents)

Your resume says you were a Python Developer Intern and Trainee Developer at Wexdi Software Solutions from July 2025 to September 2025. It also says you led a four-member development team for Django-based solutions for a US client and acted as a technical point of contact in client discussions. fileciteturn344file0L36-L42

The following answers use the additional work details you gave for this preparation:
- you focused on the Django backend
- you worked on employee timesheet management
- managers could approve or deny employee timesheets
- you handled creating and editing timesheets
- you worked with employee access levels
- approval requests and reviews were part of the workflow
- you also coordinated the frontend team

### Tell me about your internship.

**Answer:**

"During my internship at Wexdi Software Solutions, I worked mainly on a Django-based client application. I was focused on the backend, especially the employee timesheet part. Employees could create and edit their timesheets, managers could review them, approve or deny them, and access was controlled based on the employee and manager roles. I also coordinated a four-member frontend team and helped with debugging and delivery."

### What exactly did you work on?

**Answer:**

"My main work was the employee timesheet management flow. I worked on creating timesheets, editing them, sending approval requests, reviewing them and approving or denying them. I also worked on access levels so the right employees and managers could perform the right actions."

### What was the business flow?

**Answer:**

"The employee creates a timesheet and can edit it before submission. After submission, it goes for manager review. The manager can approve it or deny it. Based on the role and access level, different users can see and perform different actions."

### How did you control access?

**Answer:**

"I checked the user's role and the user's relationship with the timesheet before allowing an action. For example, a manager should be able to review the timesheets of their employees, while another employee should not be able to approve them."

### How did you implement approval and denial?

**Answer:**

"I treated the timesheet as having a status. The status changed as it moved through the process, such as submitted, approved or denied. The backend checked whether the current user was allowed to perform that action before changing the status."

### What if an employee tries to approve their own timesheet?

**Answer:**

"The backend should reject that request because approval is a manager action. I would never rely only on the frontend to prevent it."

### What if someone sends the API request directly?

**Answer:**

"The backend still performs the permission check. Hiding a button in the frontend is not security."

### Why Django for this project?

**Answer:**

"Django was a good fit because the application had models, user roles, authentication, database operations and business workflows. Django already provides many of the pieces needed for this type of application."

### What Django parts did you use?

**Answer:**

"I mainly worked with models, views, URLs, ORM queries, authentication/permissions and the backend business logic."

### What did you learn from the internship?

**Answer:**

"I learned how a real client requirement becomes a feature. I also learned that writing code is only part of the work. Communication, debugging, reviewing changes and understanding the business flow are equally important."

### You led a four-member team. What did that mean?

**Answer:**

"I helped divide frontend work, track progress, discuss implementation problems and help the team when someone was blocked. I also communicated updates and worked with the client side when requirements were unclear."

### Did you actually manage people or just assign tasks?

**Answer:**

"I would say I had technical coordination responsibility. I helped divide the work, followed up on progress, discussed problems and kept the implementation moving. I was still a developer myself, especially on the backend."

### How did you handle a teammate who was stuck?

**Answer:**

"I first understood where they were blocked. If it was something I knew, I helped them directly. Otherwise, I tried to break the problem into smaller parts and find the right way forward."

### How did you handle client requirements?

**Answer:**

"I first tried to understand the actual business need, not just the words in the request. Then I converted it into smaller development tasks and clarified anything that was unclear."

### Tell me about a difficult internship problem.

**Answer:**

"One difficult part was handling the timesheet workflow because several users had different permissions and the same data could move through different states. I had to make sure the backend checked both the current state and the user's role before allowing an action."

### What would you improve in that project?

**Answer:**

"I would add more automated tests around permission rules and timesheet state changes, because those are the areas where a small mistake can affect business data."

---

<a id="education"></a>
## Education

[Back to Table of Contents](#table-of-contents)

Your resume lists a B.Tech in Computer Science from Rajiv Gandhi University of Knowledge Technologies with an 8.68 CGPA, and a Pre University Course with a 9.78 CGPA. fileciteturn344file0L43-L47

### Tell me about your education.

**Answer:**

"I completed my B.Tech in Computer Science from RGUKT. My CGPA was 8.68. During college I focused on programming, computer science subjects, coding practice and projects."

### Why is your CGPA 8.68?

**Answer:**

"I maintained a good academic record while also spending time on coding, projects and technical learning. I tried to balance both."

### What did you learn from college that helped your projects?

**Answer:**

"Subjects like databases, operating systems, computer networks and programming gave me the basics. My projects helped me understand how those concepts are used in real applications."

---

<a id="achievements"></a>
## Achievements

[Back to Table of Contents](#table-of-contents)

Your resume lists GATE CS qualification, 550+ LeetCode problems and university-level football achievements including captaincy and an AIU South Zone Inter-University Tournament appearance. fileciteturn344file0L48-L52

### Tell me about GATE.

**Answer:**

"I qualified GATE CS 2025. Preparing for it helped me strengthen my computer science fundamentals and problem solving."

### Why did you prepare for GATE?

**Answer:**

"I wanted to strengthen my core computer science knowledge and also keep higher-study opportunities open."

### You solved 550+ LeetCode problems. Why did you solve so many?

**Answer:**

"Mainly to improve my problem-solving skills. I wanted to become more comfortable with different patterns instead of solving only a few familiar problems."

### What is more important: number of problems or understanding?

**Answer:**

"Understanding is more important. The number shows practice, but the real value is being able to recognize a problem pattern and explain why the solution works."

### Tell me about football.

**Answer:**

"I was the captain of the university football team. It taught me a lot about responsibility, communication and staying calm when things do not go as planned."

### What did being captain teach you?

**Answer:**

"I learned that leadership is not just giving instructions. You have to understand the team, communicate clearly and take responsibility when something goes wrong."

### How does football help you at work?

**Answer:**

"It taught me how to work with different people, handle pressure and focus on the team's result instead of only my own performance."

---

<a id="cross-resume-technical-questions"></a>
## Cross-Resume Technical Questions

[Back to Table of Contents](#table-of-contents)

### Why FastAPI in one project and Django in another?

**Answer:**

"I used Django in the internship because the application needed a larger framework with built-in features for a business application. I used FastAPI in my own projects because I wanted lightweight APIs, validation and a simple API-focused structure."

### Why Redis in both your projects?

**Answer:**

"Redis is useful when I need fast temporary data. In SceneFlow I used it around background processing, and in the URL shortener I used it for caching and rate limiting."

### Why PostgreSQL instead of only Redis?

**Answer:**

"Redis is fast but I still need durable relational storage. PostgreSQL is the source of truth, while Redis is used for speed or temporary state."

### Where does asynchronous processing help?

**Answer:**

"When work takes time and does not need to finish inside the user's request. SceneFlow is a good example because searching several providers and processing candidates can take much longer than a normal API call."

### Where did authentication/authorization appear in your work?

**Answer:**

"Authorization was important in both application design and the internship. Users should only be able to access the data and actions they are allowed to use."

### What is the difference between authentication and authorization?

**Answer:**

"Authentication is checking who the user is. Authorization is checking what that user is allowed to do."

### What is an API?

**Answer:**

"An API is a way for one piece of software to communicate with another. In my projects, the frontend calls backend API endpoints to perform operations and get data."

### Why REST APIs?

**Answer:**

"They are simple and widely used for communication between frontend and backend. They also work well with normal HTTP methods and JSON responses."

---

<a id="why-questions"></a>
## Why Questions

[Back to Table of Contents](#table-of-contents)

These are very likely because interviewers can pick almost any technology on the resume and ask "Why?"

### Why FastAPI?
"Simple API development, validation and good fit for Python backend services."

### Why Django?
"Good fit for the business application and gives many common features out of the box."

### Why PostgreSQL?
"Reliable relational data, constraints and transactions."

### Why Redis?
"Fast access for cache, rate limiting and temporary data."

### Why Celery?
"To move slow background work away from the API request."

### Why Qdrant?
"To store embeddings and perform similarity search."

### Why Docker?
"To package the app and dependencies consistently."

### Why React?
"Reusable frontend components and clear frontend structure."

### Why Sentence Transformers?
"To convert text into embeddings that can be compared semantically."

### Why cache-aside?
"Read from the cache first, then use the database when there is a miss. It is simple and works well for read-heavy data."

### Why repository-service-route separation?
"To keep API handling, business logic and database access separate so the code is easier to change and test."

---

<a id="follow-up-questions"></a>
## Follow-Up Questions

[Back to Table of Contents](#table-of-contents)

### "You wrote X on your resume. Explain it."

Use this structure:

**1. What it is**
"X is ..."

**2. Why you used it**
"I used it because ..."

**3. How you used it**
"In my project, ..."

**4. Problem it solved**
"It helped with ..."

**5. Trade-off**
"One limitation is ..."

### Example: Redis

"Redis is an in-memory data store. I used it for caching and rate limiting. In the URL shortener, it reduced repeated database reads. The trade-off is that cached data can become stale, so PostgreSQL remained the source of truth."

### "What happens internally?"

Do not immediately give a huge answer.

Start with the simple flow and wait for the next question.

Example:

"The frontend sends the request, the API validates it, the service performs the operation and the database stores the result."

Then expand only if they ask.

### "What went wrong in the project?"

Use:

"We had a problem with X. I checked the flow step by step and found Y. I changed Z, and then I tested the case again."

### "What would you do differently now?"

Use:

"Now I would add stronger tests, better monitoring and clearer failure handling around that part."

---

<a id="resume-traps"></a>
## Resume Traps

[Back to Table of Contents](#table-of-contents)

### Do not claim more than you can explain.

If you write:
- Redis -> be ready for cache, TTL and basic data structures.
- Celery -> be ready for worker, queue and background jobs.
- Qdrant -> be ready for embeddings and similarity search.
- Docker -> be ready for image, container, Dockerfile and Compose.
- PostgreSQL -> be ready for joins, indexes, transactions and constraints.
- React -> be ready for components, state, props and API calls.
- Django -> be ready for models, ORM, views, URLs and authentication.
- FastAPI -> be ready for routing, Pydantic, dependencies and async basics.

### Do not say "I designed everything."

Use:
"I worked on..."
"I implemented..."
"I handled..."
"I helped design..."

Be precise about your personal contribution.

### Do not memorize the project as a story with no technical understanding.

The interviewer can switch direction quickly:

"Why Redis?"
→ "What if Redis is down?"
→ "What if two requests update the same data?"
→ "How do you keep the database correct?"

Be ready for the next level.

---

<a id="final-resume-checklist"></a>
## Final Resume Checklist

[Back to Table of Contents](#table-of-contents)

Before the interview, be able to explain every resume item in simple English:

### Summary
- Python
- FastAPI
- Django
- PostgreSQL
- REST
- caching
- async processing
- authentication

### Skills
- Python
- SQL
- JavaScript
- React
- FastAPI
- Django
- Pydantic
- PostgreSQL
- MySQL
- SQLAlchemy
- Alembic
- Redis
- Celery
- Qdrant
- Git
- Docker
- Linux
- Postman

### SceneFlow
- problem
- architecture
- request flow
- background job
- Celery
- Redis
- PostgreSQL
- asset providers
- embeddings
- Sentence Transformers
- Qdrant
- cosine similarity
- reranking
- deduplication
- authorization
- idempotency
- failure handling
- polling

### URL Shortener
- architecture
- Base62
- collisions
- uniqueness
- Redis cache-aside
- database fallback
- atomic counter
- rate limiting
- Docker Compose
- Alembic
- deployment

### Internship
- Django
- employee timesheets
- create/edit
- submit for approval
- manager review
- approve/deny
- access levels
- backend permissions
- four-member team
- frontend coordination
- client communication

### Achievements
- GATE
- 550+ LeetCode
- football captain
- AIU tournament

### Final rule

Your resume should never contain a technology that you cannot explain at least at a basic interview level.

The interviewer does not need you to give the biggest answer.

They need to see that the things on your resume are real and that you understand what you worked on.
