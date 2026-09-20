# Cloud Computing Interview Notes

## Table of Contents
- [Cloud Computing](#cloud-computing)
- [Why Cloud](#why-cloud)
- [IaaS PaaS SaaS](#iaas-paas-saas)
- [Public Private and Hybrid Cloud](#public-private-and-hybrid-cloud)
- [Regions and Availability Zones](#regions-and-availability-zones)
- [Compute](#compute)
- [Virtual Machines](#virtual-machines)
- [Containers in Cloud](#containers-in-cloud)
- [Serverless](#serverless)
- [Storage](#storage)
- [Object vs Block vs File Storage](#object-vs-block-vs-file-storage)
- [Databases](#databases)
- [Managed Services](#managed-services)
- [Networking](#networking)
- [VPC and Subnets](#vpc-and-subnets)
- [Load Balancers](#load-balancers)
- [Auto Scaling](#auto-scaling)
- [CDN](#cdn)
- [DNS](#dns)
- [IAM](#iam)
- [Secrets and Configuration](#secrets-and-configuration)
- [Cloud Security Basics](#cloud-security-basics)
- [Reliability and Backups](#reliability-and-backups)
- [High Availability](#high-availability)
- [Scalability](#scalability)
- [Horizontal vs Vertical Scaling](#horizontal-vs-vertical-scaling)
- [Caching](#caching)
- [Queues and Events](#queues-and-events)
- [Observability](#observability)
- [Cloud Deployment Flow](#cloud-deployment-flow)
- [AWS Azure GCP](#aws-azure-gcp)
- [Important Cloud Interview Q&A](#important-cloud-interview-qa)
- [Project Connections](#project-connections)
- [Cloud Interview Traps](#cloud-interview-traps)
- [Final Checklist](#final-checklist)

<a id="table-of-contents"></a>

<a id="cloud-computing"></a>
## Cloud Computing

[Back to Table of Contents](#table-of-contents)

Cloud computing is delivering computing resources such as compute, storage, networking and managed services over a network with on-demand provisioning.

Examples:
- virtual machines
- managed databases
- object storage
- serverless functions
- managed Kubernetes

<a id="why-cloud"></a>
## Why Cloud

[Back to Table of Contents](#table-of-contents)

Typical benefits:
- elastic capacity
- fast provisioning
- managed infrastructure
- global availability options
- usage-based economics

Cloud does not automatically make an architecture scalable, secure or cheap.

<a id="iaas-paas-saas"></a>
## IaaS PaaS SaaS

[Back to Table of Contents](#table-of-contents)

IaaS:
- infrastructure resources
- more control
- example: virtual machine

PaaS:
- provider-managed runtime/platform
- less infrastructure management

SaaS:
- complete application consumed by users

Mental model:

```text
IaaS -> you manage more
PaaS -> provider manages more
SaaS -> provider manages most infrastructure
```

<a id="public-private-and-hybrid-cloud"></a>
## Public Private and Hybrid Cloud

[Back to Table of Contents](#table-of-contents)

Public cloud uses provider-owned infrastructure offered to customers.

Private cloud is dedicated to one organization.

Hybrid cloud combines environments.

<a id="regions-and-availability-zones"></a>
## Regions and Availability Zones

[Back to Table of Contents](#table-of-contents)

A region is a geographic cloud location.

An availability zone is an isolated location within a region designed to reduce correlated failure.

High-availability designs often distribute critical resources across multiple zones.

<a id="compute"></a>
## Compute

[Back to Table of Contents](#table-of-contents)

Common choices:
- virtual machines
- containers
- serverless functions
- managed application platforms

Choose based on control, startup behavior, workload pattern, scaling model and operational burden.

<a id="virtual-machines"></a>
## Virtual Machines

[Back to Table of Contents](#table-of-contents)

A VM provides a virtualized machine environment with its own guest operating system.

Useful for:
- long-running services
- custom OS/network configuration
- workloads requiring more infrastructure control

<a id="containers-in-cloud"></a>
## Containers in Cloud

[Back to Table of Contents](#table-of-contents)

Containers package applications consistently.

Cloud platforms can run containers using managed container services, managed Kubernetes or VM-based container hosts.

Containerization packages the application; cloud provides infrastructure/services to run it.

<a id="serverless"></a>
## Serverless

[Back to Table of Contents](#table-of-contents)

Serverless means the provider manages the underlying server infrastructure.

Typical characteristics:
- request/event-driven execution
- platform-managed scaling
- usage-based billing model

It does not mean servers do not exist.

<a id="storage"></a>
## Storage

[Back to Table of Contents](#table-of-contents)

Cloud storage commonly includes:
- object storage
- block storage
- file storage

Examples:
- images/videos -> object storage
- VM disk -> block storage
- shared filesystem -> file storage

<a id="object-vs-block-vs-file-storage"></a>
## Object vs Block vs File Storage

[Back to Table of Contents](#table-of-contents)

Object storage:
- objects plus metadata
- API based
- good for large unstructured data

Block storage:
- raw storage volumes
- behaves like disks attached to compute

File storage:
- shared filesystem semantics

<a id="databases"></a>
## Databases

[Back to Table of Contents](#table-of-contents)

Cloud databases include:
- managed relational databases
- NoSQL databases
- key-value stores
- analytical databases

Managed services reduce operations but do not remove the need to understand schema, indexes, transactions, backups and queries.

<a id="managed-services"></a>
## Managed Services

[Back to Table of Contents](#table-of-contents)

A managed service shifts operational responsibilities to the provider.

Example:
A managed PostgreSQL service can handle infrastructure operations such as provisioning and patching according to the service offering.

You still own application design, data model, permissions and cost decisions.

<a id="networking"></a>
## Networking

[Back to Table of Contents](#table-of-contents)

Core concepts:
- IP addresses
- subnets
- routing
- security groups/firewalls
- gateways
- load balancers
- DNS

Typical flow:

```text
Client
 ↓
DNS
 ↓
Load balancer
 ↓
Application
 ↓
Database
```

<a id="vpc-and-subnets"></a>
## VPC and Subnets

[Back to Table of Contents](#table-of-contents)

A VPC/VNet provides an isolated logical network.

Example:

```text
VPC
├── public subnet
│   └── load balancer
└── private subnet
    ├── backend
    └── database
```

Exact terminology differs across providers.

<a id="load-balancers"></a>
## Load Balancers

[Back to Table of Contents](#table-of-contents)

A load balancer distributes traffic across backend instances.

Benefits:
- scale out
- health-based routing
- availability

Common algorithms:
- round robin
- least connections
- weighted routing

<a id="auto-scaling"></a>
## Auto Scaling

[Back to Table of Contents](#table-of-contents)

Auto scaling adjusts compute capacity based on demand or policies.

Example:

```text
low traffic  -> 2 instances
high traffic -> 6 instances
```

Signals may include CPU, request count, queue depth or custom metrics.

<a id="cdn"></a>
## CDN

[Back to Table of Contents](#table-of-contents)

A CDN caches content at edge locations closer to users.

Useful for:
- images
- JS/CSS
- video
- suitable cacheable responses

Result:
- lower latency
- reduced origin load

<a id="dns"></a>
## DNS

[Back to Table of Contents](#table-of-contents)

DNS maps names to network endpoints.

Example:

```text
api.example.com
      ↓ DNS
load-balancer endpoint
```

Cloud DNS services can also support routing policies and health-aware behavior.

<a id="iam"></a>
## IAM

[Back to Table of Contents](#table-of-contents)

Identity and Access Management controls identities, resources and allowed actions.

Core ideas:
- authentication
- authorization
- roles
- policies
- least privilege

Application code should not receive broader permissions than necessary.

<a id="secrets-and-configuration"></a>
## Secrets and Configuration

[Back to Table of Contents](#table-of-contents)

Do not hardcode:
- database passwords
- API keys
- cloud credentials

Use:
- environment/configuration mechanisms
- secret managers
- workload identities/roles where supported

<a id="cloud-security-basics"></a>
## Cloud Security Basics

[Back to Table of Contents](#table-of-contents)

High-value practices:
- least privilege
- private networking for internal services
- encryption in transit
- encryption at rest
- secret rotation
- patching
- network segmentation
- logging/auditing
- MFA for humans
- backup and recovery testing

<a id="reliability-and-backups"></a>
## Reliability and Backups

[Back to Table of Contents](#table-of-contents)

Backup is not the same as availability.

Backup protects against data loss/corruption.

Availability mechanisms reduce service interruption.

Know:
- backup frequency
- retention
- restore procedure
- Recovery Point Objective (RPO)
- Recovery Time Objective (RTO)

RPO = acceptable data loss.

RTO = acceptable recovery time.

<a id="high-availability"></a>
## High Availability

[Back to Table of Contents](#table-of-contents)

High availability reduces downtime by removing or reducing single points of failure.

Example:

```text
             Load Balancer
              /        \
          App A        App B
```

The database may require its own replication/failover design.

<a id="scalability"></a>
## Scalability

[Back to Table of Contents](#table-of-contents)

Scalability is the ability to handle increased workload by adding resources or changing architecture.

Scale-out:
- add instances

Scale-up:
- add resources to an instance

<a id="horizontal-vs-vertical-scaling"></a>
## Horizontal vs Vertical Scaling

[Back to Table of Contents](#table-of-contents)

Vertical:

```text
2 CPU -> 8 CPU
```

Horizontal:

```text
1 instance -> 4 instances
```

Horizontal scaling usually benefits from stateless application design.

<a id="caching"></a>
## Caching

[Back to Table of Contents](#table-of-contents)

A cache stores frequently used data closer to the caller/application.

Examples:
- Redis
- CDN cache
- in-memory cache

Common strategies:
- cache-aside
- write-through
- write-back

Caching improves latency but introduces invalidation and consistency concerns.

<a id="queues-and-events"></a>
## Queues and Events

[Back to Table of Contents](#table-of-contents)

Queues decouple producers and consumers.

Example:

```text
API
 ↓
Queue
 ↓
Worker
 ↓
Database/external service
```

Benefits:
- smooth traffic spikes
- asynchronous processing
- retries
- workload isolation

<a id="observability"></a>
## Observability

[Back to Table of Contents](#table-of-contents)

Cloud applications should expose:
- logs
- metrics
- traces
- health checks
- alerts

Monitor:
- latency
- error rate
- resource usage
- queue depth
- database health
- availability

<a id="cloud-deployment-flow"></a>
## Cloud Deployment Flow

[Back to Table of Contents](#table-of-contents)

Typical deployment:

```text
Git push
  ↓
CI/CD
  ↓
Build/test
  ↓
Container image
  ↓
Registry
  ↓
Cloud runtime
  ↓
Load balancer
  ↓
Application
  ↓
Managed DB / Redis / object storage
```

<a id="aws-azure-gcp"></a>
## AWS Azure GCP

[Back to Table of Contents](#table-of-contents)

Similar service categories exist across major providers:

| Need | AWS | Azure | GCP |
|---|---|---|---|
| VM compute | EC2 | Virtual Machines | Compute Engine |
| Object storage | S3 | Blob Storage | Cloud Storage |
| Managed SQL | RDS | Azure SQL / managed DB options | Cloud SQL |
| Kubernetes | EKS | AKS | GKE |
| Serverless functions | Lambda | Azure Functions | Cloud Functions / Cloud Run functions |

Focus first on the category and architecture rather than memorizing every service name.

<a id="important-cloud-interview-qa"></a>
## Important Cloud Interview Q&A

[Back to Table of Contents](#table-of-contents)

### What is cloud computing?

On-demand delivery of compute, storage, networking and managed services over a network.

### IaaS vs PaaS vs SaaS?

They represent increasing levels of provider-managed infrastructure and application functionality.

### What is a region?

A geographic cloud location.

### What is an availability zone?

An isolated infrastructure location within a region used to improve resilience.

### What is serverless?

A model where the provider manages server infrastructure and the developer focuses on application code/configuration. Servers still exist underneath.

### Object storage vs block storage?

Object storage stores objects through APIs; block storage behaves like an attached disk.

### Why use a load balancer?

To distribute traffic across healthy instances and support scale/availability.

### Horizontal vs vertical scaling?

Horizontal adds instances. Vertical increases resources on an existing instance.

### What is IAM?

Identity and Access Management for identities, permissions and policies.

### RPO vs RTO?

RPO measures acceptable data loss. RTO measures acceptable recovery time.

### What is a CDN?

A distributed edge delivery/cache layer that reduces latency and origin load.

### Why use queues?

To decouple services and process work asynchronously.

<a id="project-connections"></a>
## Project Connections

[Back to Table of Contents](#table-of-contents)

SceneFlow:

```text
Frontend
  ↓
API
  ↓
Workers / Redis
  ↓
PostgreSQL
  ↓
External AI/image providers
```

Cloud discussion:
- frontend hosting
- API deployment
- worker scaling
- managed PostgreSQL
- Redis
- object storage for large assets
- CDN
- secrets
- monitoring

URL shortener:

```text
Client
 ↓
DNS
 ↓
Load Balancer
 ↓
API replicas
 ↓
Redis + PostgreSQL
```

Focus questions on scale, failure handling, caching, security and deployment.

<a id="cloud-interview-traps"></a>
## Cloud Interview Traps

[Back to Table of Contents](#table-of-contents)

- Cloud does not automatically mean serverless.
- Serverless still runs on servers.
- High availability is not the same as backup.
- Auto scaling does not guarantee application scalability.
- A managed database does not eliminate database design.
- Public subnet does not mean every resource must be publicly reachable.
- More replicas do not automatically solve stateful bottlenecks.
- CDN is not a replacement for every caching layer.
- IAM is not the same as network security.
- Lower cost is not automatically better architecture.

<a id="final-checklist"></a>
## Final Checklist

[Back to Table of Contents](#table-of-contents)

Know:
- cloud computing
- IaaS/PaaS/SaaS
- deployment models
- regions/AZs
- VM/container/serverless
- object/block/file storage
- managed services
- networking
- VPC/subnets
- load balancers
- auto scaling
- CDN
- DNS
- IAM
- secrets
- cloud security
- backups
- RPO/RTO
- high availability
- scalability
- horizontal/vertical scaling
- caching
- queues/events
- observability
- deployment flow
- AWS/Azure/GCP categories
- project architecture
