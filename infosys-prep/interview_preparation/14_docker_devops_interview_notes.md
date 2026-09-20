# Docker and DevOps Interview Notes

## Table of Contents

- [Docker Fundamentals](#docker-fundamentals)
- [Containers vs Virtual Machines](#containers-vs-virtual-machines)
- [Docker Architecture](#docker-architecture)
- [Images and Containers](#images-and-containers)
- [Dockerfile](#dockerfile)
- [Dockerfile Instructions](#dockerfile-instructions)
- [Docker Build Context and .dockerignore](#docker-build-context-and-dockerignore)
- [Image Layers and Caching](#image-layers-and-caching)
- [CMD vs ENTRYPOINT](#cmd-vs-entrypoint)
- [EXPOSE and Port Publishing](#expose-and-port-publishing)
- [Environment Variables and Secrets](#environment-variables-and-secrets)
- [Volumes and Bind Mounts](#volumes-and-bind-mounts)
- [Networking](#networking)
- [Docker Compose](#docker-compose)
- [Multi-Container Architecture](#multi-container-architecture)
- [Docker Commands](#docker-commands)
- [Container Logs and Debugging](#container-logs-and-debugging)
- [Container Lifecycle and Health Checks](#container-lifecycle-and-health-checks)
- [Resource Limits](#resource-limits)
- [Docker Security](#docker-security)
- [Production Docker Practices](#production-docker-practices)
- [Dockerizing Django and FastAPI](#dockerizing-django-and-fastapi)
- [Dockerizing React](#dockerizing-react)
- [CI/CD Fundamentals](#cicd-fundamentals)
- [CI/CD Pipeline](#cicd-pipeline)
- [GitHub Actions](#github-actions)
- [Build Test Deploy Flow](#build-test-deploy-flow)
- [Deployment Strategies](#deployment-strategies)
- [DevOps Environment Management](#devops-environment-management)
- [Reverse Proxy and Load Balancer](#reverse-proxy-and-load-balancer)
- [Monitoring Logging and Observability](#monitoring-logging-and-observability)
- [Infrastructure and Configuration](#infrastructure-and-configuration)
- [Common DevOps Q&A](#common-devops-qa)
- [Docker Q&A](#docker-qa)
- [Scenario-Based Questions](#scenario-based-questions)
- [Interview Traps](#interview-traps)
- [Final Checklist](#final-checklist)

<a id="docker-fundamentals"></a>
## Docker Fundamentals

[Back to Table of Contents](#table-of-contents)

Docker packages an application and its runtime dependencies into a container image so the application can run consistently across environments.

Interview answer:

"Docker is a containerization platform. It packages an application with its dependencies into an image, and runs isolated processes from that image as containers."

Key terms:

- Image — immutable template used to create containers.
- Container — running instance of an image.
- Registry — stores and distributes images.
- Dockerfile — instructions for building an image.
- Volume — persistent storage managed separately from the container filesystem.

<a id="containers-vs-virtual-machines"></a>
## Containers vs Virtual Machines

[Back to Table of Contents](#table-of-contents)

VM:

```text
Application
Libraries
Guest OS
Hypervisor
Host OS / Hardware
```

Container:

```text
Application
Libraries
Container
Container Runtime
Host OS / Kernel
```

Containers share the host kernel, while VMs virtualize hardware and run guest operating systems.

Therefore containers are usually lighter and faster to start, while VMs provide stronger OS-level isolation boundaries.

<a id="docker-architecture"></a>
## Docker Architecture

[Back to Table of Contents](#table-of-contents)

Core concepts:

- Docker CLI
- Docker daemon / engine
- Images
- Containers
- Registries

Typical flow:

```text
docker build
     |
     v
Image
     |
     v
docker run
     |
     v
Container
```

The CLI sends requests to the Docker Engine API.

<a id="images-and-containers"></a>
## Images and Containers

[Back to Table of Contents](#table-of-contents)

An image is a packaged filesystem and metadata used as the basis for containers.

A container adds a writable layer over the image's read-only layers.

Important interview point:

Deleting a container does not delete the image automatically.

<a id="dockerfile"></a>
## Dockerfile

[Back to Table of Contents](#table-of-contents)

A Dockerfile defines how an image is built.

Example:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

For production Django, replace the development server with an appropriate production WSGI/ASGI deployment.

<a id="dockerfile-instructions"></a>
## Dockerfile Instructions

[Back to Table of Contents](#table-of-contents)

Important instructions:

- FROM — base image.
- WORKDIR — working directory.
- COPY — copy files from build context.
- ADD — copy files with additional archive/URL semantics; prefer COPY for ordinary file copying.
- RUN — execute commands while building the image.
- CMD — default command/arguments.
- ENTRYPOINT — executable entrypoint.
- ENV — environment variable in the image/container environment.
- ARG — build-time variable.
- EXPOSE — documents intended container port.
- USER — choose runtime user.
- HEALTHCHECK — define container health behavior.

<a id="docker-build-context-and-dockerignore"></a>
## Docker Build Context and .dockerignore

[Back to Table of Contents](#table-of-contents)

The build context is the set of files available to Docker during a build.

A .dockerignore should exclude unnecessary or sensitive files:

```text
.git
.env
__pycache__
node_modules
*.pyc
.venv
```

Smaller contexts improve build performance and reduce accidental inclusion.

Never use .dockerignore as your only secret-protection mechanism. Do not put secrets in the image.

<a id="image-layers-and-caching"></a>
## Image Layers and Caching

[Back to Table of Contents](#table-of-contents)

Docker images are built from layers.

Poor ordering:

```dockerfile
COPY . .
RUN pip install -r requirements.txt
```

A small source-code change can invalidate the dependency-install layer.

Better:

```dockerfile
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
```

Interview answer:

"I order Dockerfile instructions so stable dependency layers are reused and frequently changing source files come later."

<a id="cmd-vs-entrypoint"></a>
## CMD vs ENTRYPOINT

[Back to Table of Contents](#table-of-contents)

CMD provides default command or arguments.

ENTRYPOINT defines the main executable behavior.

Example:

```dockerfile
ENTRYPOINT ["python", "worker.py"]
CMD ["--queue", "default"]
```

Then:

```bash
docker run app --queue images
```

The CMD arguments can be replaced while the ENTRYPOINT remains the executable.

Interview point:

CMD is commonly used for defaults; ENTRYPOINT is useful when the container behaves like a dedicated executable.

<a id="expose-and-port-publishing"></a>
## EXPOSE and Port Publishing

[Back to Table of Contents](#table-of-contents)

EXPOSE documents a port used by the application inside the image.

It does not publish the port to the host.

Publishing:

```bash
docker run -p 8000:8000 myapp
```

means:

```text
host:8000 -> container:8000
```

This distinction is frequently asked.

<a id="environment-variables-and-secrets"></a>
## Environment Variables and Secrets

[Back to Table of Contents](#table-of-contents)

Use environment variables for configuration that varies between environments.

Example:

```bash
docker run -e DATABASE_URL=... myapp
```

Do not bake passwords or API keys into Dockerfiles.

For production, use a proper secret-management mechanism such as a cloud secret manager or orchestrator secret facility.

<a id="volumes-and-bind-mounts"></a>
## Volumes and Bind Mounts

[Back to Table of Contents](#table-of-contents)

Container filesystems are ephemeral.

Volumes provide persistent Docker-managed storage:

```bash
docker volume create postgres_data
```

Bind mounts map a host path:

```bash
docker run -v $(pwd):/app myapp
```

Use volumes for persistent application data such as databases.

Use bind mounts commonly for development workflows where host files should be visible inside the container.

<a id="networking"></a>
## Networking

[Back to Table of Contents](#table-of-contents)

Containers can communicate over Docker networks.

Example:

```text
django ----             > docker network ---> postgres
celery ----/
```

Inside the same Compose network, services normally communicate using service names.

For example:

```text
DATABASE_HOST=postgres
```

Do not use localhost to refer to another container.

Inside a container, localhost refers to that same container.

<a id="docker-compose"></a>
## Docker Compose

[Back to Table of Contents](#table-of-contents)

Docker Compose defines and runs multi-container applications.

Example:

```yaml
services:
  web:
    build: .
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis

  db:
    image: postgres:16

  redis:
    image: redis:7
```

Important concepts:

- services
- networks
- volumes
- environment
- build
- ports
- health checks
- dependency ordering

depends_on controls startup ordering/relationship but should not be treated as proof that a dependency is ready to accept traffic.

<a id="multi-container-architecture"></a>
## Multi-Container Architecture

[Back to Table of Contents](#table-of-contents)

A realistic backend:

```text
              +--> PostgreSQL
              |
React -> Nginx -> Django/FastAPI -> Redis
                                  |
                                  v
                                Celery
```

Typical separation:

- frontend container
- API container
- worker container
- database container
- cache/queue container
- reverse proxy

Each service should have a clear responsibility.

<a id="docker-commands"></a>
## Docker Commands

[Back to Table of Contents](#table-of-contents)

High-value commands:

```bash
docker build -t myapp .
docker images
docker run -d -p 8000:8000 myapp
docker ps
docker ps -a
docker logs <container>
docker exec -it <container> sh
docker stop <container>
docker rm <container>
docker rmi <image>
docker pull <image>
docker push <image>
docker inspect <container>
docker stats
docker network ls
docker volume ls
docker compose up -d
docker compose down
docker compose logs -f
```

Interview muscle memory:

- ps -> running containers
- ps -a -> all containers
- logs -> application output
- exec -> enter running container
- inspect -> configuration/details
- stats -> resource usage

<a id="container-logs-and-debugging"></a>
## Container Logs and Debugging

[Back to Table of Contents](#table-of-contents)

When a container fails:

1. Check status.
2. Read logs.
3. Inspect configuration.
4. Check environment variables.
5. Check ports.
6. Check network connectivity.
7. Check mounted files/volumes.
8. Enter the container if it stays running.
9. Verify dependency availability.

Useful:

```bash
docker logs -f api
docker inspect api
docker exec -it api sh
```

For a container that exits immediately, inspect its logs and command/entrypoint first.

<a id="container-lifecycle-and-health-checks"></a>
## Container Lifecycle and Health Checks

[Back to Table of Contents](#table-of-contents)

Common states:

```text
created -> running -> stopped -> removed
```

A health check answers whether an application is responding correctly, not merely whether its process exists.

Example:

```dockerfile
HEALTHCHECK CMD curl --fail http://localhost:8000/health || exit 1
```

Health checks become particularly useful for orchestration and load balancing decisions.

<a id="resource-limits"></a>
## Resource Limits

[Back to Table of Contents](#table-of-contents)

Containers can be constrained by CPU and memory.

Why this matters:

- prevents one workload from consuming all resources
- improves predictability
- helps capacity planning
- exposes memory leaks earlier

Know the difference between an application crash and an OOM kill.

<a id="docker-security"></a>
## Docker Security

[Back to Table of Contents](#table-of-contents)

Important practices:

- use trusted/minimal base images
- keep images updated
- run as non-root when practical
- do not bake secrets into images
- scan dependencies/images
- minimize installed packages
- use read-only filesystems where appropriate
- limit Linux capabilities
- avoid privileged containers unless required
- pin or control image versions for reproducibility

Container isolation is not a substitute for application security.

<a id="production-docker-practices"></a>
## Production Docker Practices

[Back to Table of Contents](#table-of-contents)

High-value practices:

- multi-stage builds
- small base images
- deterministic dependency installation
- non-root runtime user
- health checks
- graceful shutdown
- structured logs
- environment-based configuration
- image vulnerability scanning
- resource limits
- immutable image deployment

Example multi-stage concept:

```text
builder image
   |
   v
compiled/build artifacts
   |
   v
small runtime image
```

<a id="dockerizing-django-and-fastapi"></a>
## Dockerizing Django and FastAPI

[Back to Table of Contents](#table-of-contents)

Django/FastAPI application pattern:

```text
Docker image
  |
  +-- application dependencies
  +-- source code
  +-- production server command
```

Django:

```bash
gunicorn project.wsgi:application
```

ASGI Django/FastAPI deployments may use an ASGI server such as Uvicorn.

For SceneFlow-style workloads:

```text
API container
   |
   +--> PostgreSQL
   +--> Redis
   +--> Celery worker
   +--> external APIs
```

Do not put PostgreSQL data inside the ephemeral writable layer of an ordinary database container.

<a id="dockerizing-react"></a>
## Dockerizing React

[Back to Table of Contents](#table-of-contents)

A production React application is commonly built in one stage and served from a lightweight web server in another.

```text
Node builder
   |
   v
npm run build
   |
   v
static assets
   |
   v
Nginx/runtime server
```

This is a common multi-stage build pattern.

<a id="cicd-fundamentals"></a>
## CI/CD Fundamentals

[Back to Table of Contents](#table-of-contents)

CI = Continuous Integration.

Developers frequently integrate changes and automated checks validate them.

CD can mean Continuous Delivery or Continuous Deployment depending on the organization.

Continuous Delivery:

- software is kept in a deployable state
- production release may require approval

Continuous Deployment:

- validated changes are automatically deployed to production.

<a id="cicd-pipeline"></a>
## CI/CD Pipeline

[Back to Table of Contents](#table-of-contents)

Typical pipeline:

```text
git push
  |
  v
lint
  |
  v
unit tests
  |
  v
integration tests
  |
  v
build image
  |
  v
security scan
  |
  v
push image
  |
  v
deploy
  |
  v
health check
```

The exact stages depend on the project.

<a id="github-actions"></a>
## GitHub Actions

[Back to Table of Contents](#table-of-contents)

GitHub Actions automates repository workflows.

Basic example:

```yaml
name: CI

on:
  push:
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"
      - run: pip install -r requirements.txt
      - run: pytest
```

Know:

- workflows
- jobs
- steps
- runners
- actions
- secrets
- environment variables
- artifacts
- caching

<a id="build-test-deploy-flow"></a>
## Build Test Deploy Flow

[Back to Table of Contents](#table-of-contents)

A good interview explanation:

"On every pull request, CI runs linting and tests. After merge, the pipeline builds an immutable Docker image, scans it, pushes it to a registry and deploys the specific image version. Deployment then performs health checks before traffic is shifted."

This demonstrates reproducibility and separation between build and deployment.

<a id="deployment-strategies"></a>
## Deployment Strategies

[Back to Table of Contents](#table-of-contents)

Know these:

### Rolling deployment

Gradually replace old instances with new instances.

### Blue-green deployment

Maintain two environments and switch traffic between them.

### Canary deployment

Send a small percentage of traffic to the new version before wider rollout.

### Rollback

Return traffic/deployment to a known-good version.

Interview point:

Deployment strategy is a risk-management and availability decision, not merely a Docker feature.

<a id="devops-environment-management"></a>
## DevOps Environment Management

[Back to Table of Contents](#table-of-contents)

Common environments:

- development
- testing
- staging
- production

Keep environment-specific configuration outside application code.

Typical configuration:

```text
development -> local database
staging     -> staging database
production  -> production database
```

Never copy production secrets into source control.

<a id="reverse-proxy-and-load-balancer"></a>
## Reverse Proxy and Load Balancer

[Back to Table of Contents](#table-of-contents)

Reverse proxy:

- receives client requests
- forwards them to backend services
- can terminate TLS
- can serve static assets
- can apply routing/security policies

Load balancer:

- distributes traffic among multiple backend instances.

They can be provided by the same infrastructure component.

Common architecture:

```text
Client
  |
  v
Nginx / Load Balancer
  |
  +--> API instance 1
  +--> API instance 2
  +--> API instance 3
```

<a id="monitoring-logging-and-observability"></a>
## Monitoring Logging and Observability

[Back to Table of Contents](#table-of-contents)

Three common observability signals:

- Logs — event details.
- Metrics — numerical measurements.
- Traces — request path across services.

Important metrics:

- request latency
- error rate
- throughput
- CPU
- memory
- disk
- database latency
- queue depth

A useful production question:

"How do you know the deployment is healthy?"

Answer with metrics, logs, traces and health checks rather than only saying "the container is running."

<a id="infrastructure-and-configuration"></a>
## Infrastructure and Configuration

[Back to Table of Contents](#table-of-contents)

Important DevOps concepts:

- Infrastructure as Code
- environment configuration
- secrets management
- immutable deployments
- container registries
- artifact management
- backups
- disaster recovery
- health checks
- DNS
- TLS certificates

Terraform is a common Infrastructure-as-Code tool.

Kubernetes is a container orchestration platform; Docker and Kubernetes solve related but different problems.

<a id="common-devops-qa"></a>
## Common DevOps Q&A

[Back to Table of Contents](#table-of-contents)

### What is DevOps?

DevOps is a set of practices and culture that improves collaboration between development and operations through automation, reliable delivery, observability and feedback.

### What is CI?

Automated validation of frequently integrated code changes.

### What is CD?

A delivery/deployment practice that automates getting validated software toward release or production.

### What is containerization?

Packaging an application and its dependencies into an isolated process environment that shares the host kernel.

### What is an image registry?

A service that stores and distributes container images.

### Why use Docker in CI/CD?

It provides reproducible build/runtime artifacts and reduces environment differences between development, testing and deployment.

### Docker vs Kubernetes?

Docker provides container tooling/runtime workflows. Kubernetes orchestrates containers across machines and manages scheduling, networking, scaling and desired state.

### What is Infrastructure as Code?

Defining infrastructure through version-controlled configuration instead of manually configuring resources.

### What is a health check?

A check that determines whether a service is functioning sufficiently for traffic or orchestration decisions.

### What is observability?

The ability to understand internal system behavior from external outputs such as logs, metrics and traces.

<a id="docker-qa"></a>
## Docker Q&A

[Back to Table of Contents](#table-of-contents)

### Image vs container?

An image is the packaged template; a container is a runtime instance created from an image.

### COPY vs ADD?

COPY is the straightforward choice for copying files. ADD has additional behaviors, so COPY is generally preferred unless those behaviors are intentionally needed.

### RUN vs CMD?

RUN executes during image build. CMD defines the default runtime command/arguments.

### CMD vs ENTRYPOINT?

CMD supplies defaults. ENTRYPOINT defines the main executable behavior.

### EXPOSE vs -p?

EXPOSE documents a container port. -p publishes/maps a container port to the host.

### Volume vs bind mount?

A volume is Docker-managed persistent storage. A bind mount maps a host path into the container.

### Why does localhost fail between containers?

Because localhost inside a container refers to that container itself. Use the Docker network and service/container name.

### Why use multi-stage builds?

To separate build dependencies from runtime dependencies and produce smaller runtime images.

### Why is .dockerignore important?

It reduces build context size and prevents unnecessary files from entering the build context.

### Why run containers as non-root?

It reduces the impact of a container compromise and follows least-privilege principles.

### Why does a container exit immediately?

Usually its main process ended or crashed. Check docker logs and inspect the configured command/entrypoint.

<a id="scenario-based-questions"></a>
## Scenario-Based Questions

[Back to Table of Contents](#table-of-contents)

### Your Django container works locally but not in Docker. What do you check?

Check environment variables, dependency installation, working directory, exposed/published ports, startup command, database hostname, migrations, static files and logs.

### API container cannot connect to PostgreSQL.

Check:

1. Both services are on the same Docker network.
2. Database hostname uses the Compose service name.
3. PostgreSQL is actually ready.
4. Credentials/database name are correct.
5. Port is correct for container-to-container communication.
6. Logs show the real failure.

### Container starts and immediately exits.

Inspect:

```bash
docker ps -a
docker logs <container>
docker inspect <container>
```

Then verify the entrypoint and command.

### Docker image is very large.

Check:

- base image
- unnecessary packages
- build context
- .dockerignore
- copied source/build artifacts
- dependency caches
- multi-stage builds

### Deployment works but users still see the old version.

Check image tags/digests, deployment rollout, cache/CDN behavior, reverse proxy routing and whether traffic is actually reaching the new instances.

### CI passes but production fails.

Check differences in:

- environment variables
- secrets
- database
- network
- dependency/runtime versions
- infrastructure configuration
- migrations
- external services

This is one reason immutable artifacts and environment parity matter.

### A new deployment increases error rate.

A good response:

"Check metrics and logs, stop or pause rollout if necessary, compare the new version with the previous deployment, and roll back to the known-good artifact when appropriate. Then identify the root cause before retrying."

<a id="interview-traps"></a>
## Interview Traps

[Back to Table of Contents](#table-of-contents)

- "Docker is a virtual machine."
- "A container contains a complete guest OS."
- "EXPOSE publishes the port."
- "localhost means another container."
- "depends_on guarantees service readiness."
- "Docker automatically persists container data."
- "Containers are always secure because they are isolated."
- "CMD and ENTRYPOINT are identical."
- "RUN executes when the container starts."
- "Docker Compose is a production orchestrator in every situation."
- "A smaller image is always automatically more secure."
- "Docker image tags alone guarantee immutable deployments."
- "CI/CD always means automatic production deployment."
- "CI and CD mean exactly the same thing."
- "Kubernetes is the same thing as Docker."
- "A health check only checks whether the process exists."
- "CORS is a server-to-server security mechanism."
- "Logs alone provide complete observability."
- "Adding retries always improves reliability."
- "Rolling deployment means zero downtime automatically."

<a id="final-checklist"></a>
## Final Checklist

[Back to Table of Contents](#table-of-contents)

Be able to explain from memory:

- Docker
- container vs VM
- Docker architecture
- image vs container
- Dockerfile
- common Dockerfile instructions
- build context
- .dockerignore
- image layers
- build cache
- CMD vs ENTRYPOINT
- EXPOSE vs port publishing
- environment variables
- secrets
- volumes
- bind mounts
- networking
- Docker Compose
- service discovery
- multi-container architecture
- essential Docker commands
- logs/debugging
- container lifecycle
- health checks
- resource limits
- Docker security
- multi-stage builds
- production Docker practices
- Dockerizing Django/FastAPI
- Dockerizing React
- CI/CD
- pipeline stages
- GitHub Actions
- build/test/deploy
- rolling/blue-green/canary deployment
- environments
- reverse proxy
- load balancer
- monitoring/logging/tracing
- Infrastructure as Code
- Terraform concept
- Kubernetes vs Docker
- Docker Q&A
- DevOps Q&A
- scenario questions
- interview traps

[Back to Table of Contents](#table-of-contents)
