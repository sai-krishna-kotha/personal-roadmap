# Django and Django REST Framework Interview Notes

## Table of Contents

- [Django Fundamentals](#django-fundamentals)
- [Django Architecture](#django-architecture)
- [Project and App Structure](#project-and-app-structure)
- [Settings and Configuration](#settings-and-configuration)
- [Request Lifecycle](#request-lifecycle)
- [URL Routing](#url-routing)
- [Function-Based vs Class-Based Views](#function-based-vs-class-based-views)
- [Templates and Template Engine](#templates-and-template-engine)
- [Models and ORM](#models-and-orm)
- [QuerySets](#querysets)
- [Relationships and Related Objects](#relationships-and-related-objects)
- [Migrations](#migrations)
- [Transactions and Concurrency](#transactions-and-concurrency)
- [Indexes and Database Performance](#indexes-and-database-performance)
- [Django Forms](#django-forms)
- [Admin](#admin)
- [Middleware](#middleware)
- [Authentication](#authentication)
- [Authorization and Permissions](#authorization-and-permissions)
- [Sessions and Cookies](#sessions-and-cookies)
- [CSRF](#csrf)
- [Caching](#caching)
- [Signals](#signals)
- [Static and Media Files](#static-and-media-files)
- [File Uploads](#file-uploads)
- [Email and Background Work](#email-and-background-work)
- [Testing Django](#testing-django)
- [Security](#security)
- [Deployment and Production](#deployment-and-production)
- [Django REST Framework Fundamentals](#django-rest-framework-fundamentals)
- [Serializers](#serializers)
- [Serializer Validation](#serializer-validation)
- [APIView](#apiview)
- [Generic Views](#generic-views)
- [ViewSets and Routers](#viewsets-and-routers)
- [Function-Based API Views](#function-based-api-views)
- [Request and Response](#request-and-response)
- [HTTP Methods and Status Codes](#http-methods-and-status-codes)
- [Authentication in DRF](#authentication-in-drf)
- [Permissions in DRF](#permissions-in-drf)
- [Throttling](#throttling)
- [Pagination](#pagination)
- [Filtering, Search and Ordering](#filtering-search-and-ordering)
- [Versioning](#versioning)
- [Content Negotiation](#content-negotiation)
- [Exception Handling](#exception-handling)
- [Browsable API and OpenAPI](#browsable-api-and-openapi)
- [Nested Serializers and Relationships](#nested-serializers-and-relationships)
- [Custom Fields and SerializerMethodField](#custom-fields-and-serializermethodfield)
- [DRF Performance and Query Optimization](#drf-performance-and-query-optimization)
- [Idempotency and API Reliability](#idempotency-and-api-reliability)
- [Django vs DRF vs FastAPI](#django-vs-drf-vs-fastapi)
- [Django with React](#django-with-react)
- [Django with SceneFlow](#django-with-sceneflow)
- [Django with the URL Shortener](#django-with-the-url-shortener)
- [Django Project Architecture](#django-project-architecture)
- [Implementation Drills](#implementation-drills)
- [Generic Interview Q&A](#generic-interview-qa)
- [Django Q&A](#django-qa)
- [DRF Q&A](#drf-qa)
- [Database and ORM Q&A](#database-and-orm-qa)
- [Security Q&A](#security-qa)
- [Project-Based Q&A](#project-based-qa)
- [Interview Traps](#interview-traps)
- [Final Checklist](#final-checklist)

<a id="django-fundamentals"></a>
## Django Fundamentals

[Back to Table of Contents](#table-of-contents)

Django is a high-level Python web framework for building server-side web applications.

Interview answer:

"Django is a batteries-included Python web framework. It provides URL routing, views, ORM, templates, authentication, middleware, forms, admin and security features so applications can be built with a consistent architecture."

Django follows an MVC-like architecture, but Django commonly describes its pattern as MTV:

- Model — data and database representation.
- Template — presentation.
- View — request handling and application logic.

The framework also provides many cross-cutting features around the MTV core.

<a id="django-architecture"></a>
## Django Architecture

[Back to Table of Contents](#table-of-contents)

A simplified request path:

```text
Client
  |
  v
Web Server / ASGI or WSGI
  |
  v
Middleware
  |
  v
URL Resolver
  |
  v
View
  |
  v
ORM / Services / External APIs
  |
  v
Template or JSON Response
  |
  v
Middleware
  |
  v
Client
```

For a REST API, templates are usually replaced by serialized data such as JSON.

Important distinction:

- Django is the web framework.
- WSGI/ASGI is the server interface layer.
- Gunicorn/Uvicorn/Daphne are server processes commonly used in deployment.

<a id="project-and-app-structure"></a>
## Project and App Structure

[Back to Table of Contents](#table-of-contents)

A typical project:

```text
project/
├── manage.py
├── project/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
└── users/
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── serializers.py
    ├── urls.py
    ├── views.py
    ├── tests.py
    └── migrations/
```

Interview distinction:

- Project = overall Django configuration.
- App = reusable domain or feature module.

Do not say every Django application must contain exactly these files. Structure depends on the project.

<a id="settings-and-configuration"></a>
## Settings and Configuration

[Back to Table of Contents](#table-of-contents)

Know:

- INSTALLED_APPS
- MIDDLEWARE
- DATABASES
- ROOT_URLCONF
- TEMPLATES
- STATIC_URL
- STATIC_ROOT
- MEDIA_ROOT
- MEDIA_URL
- ALLOWED_HOSTS
- SECRET_KEY
- DEBUG
- authentication settings
- DRF configuration

Production configuration should separate environment-specific secrets and settings from source code.

Never commit secret keys, database passwords or API credentials.

<a id="request-lifecycle"></a>
## Request Lifecycle

[Back to Table of Contents](#table-of-contents)

A simplified lifecycle:

1. Server receives an HTTP request.
2. Django creates the request object.
3. Middleware processes the request.
4. URL resolver selects a view.
5. View executes application logic.
6. Database/external services may be called.
7. View returns a response.
8. Response passes back through middleware.
9. Server sends the response.

Middleware can therefore run both before and after the view.

<a id="url-routing"></a>
## URL Routing

[Back to Table of Contents](#table-of-contents)

Django uses URL configuration to map URLs to views.

```python
from django.urls import path
from .views import UserListView

urlpatterns = [
    path("users/", UserListView.as_view(), name="user-list"),
]
```

Know:

- path()
- re_path()
- include()
- named URLs
- path converters
- namespace concepts

The URL resolver chooses a matching route and passes captured parameters to the view.

<a id="function-based-vs-class-based-views"></a>
## Function-Based vs Class-Based Views

[Back to Table of Contents](#table-of-contents)

Function-based view:

```python
from django.http import JsonResponse

def health(request):
    return JsonResponse({"status": "ok"})
```

Class-based view:

```python
from django.views import View
from django.http import JsonResponse

class HealthView(View):
    def get(self, request):
        return JsonResponse({"status": "ok"})
```

Class-based views allow reusable behavior through inheritance and mixins.

Interview point:

- FBV can be straightforward for simple flows.
- CBV can improve reuse and organization for related HTTP behaviors.
- DRF generic views and ViewSets build heavily on class-based design.

<a id="templates-and-template-engine"></a>
## Templates and Template Engine

[Back to Table of Contents](#table-of-contents)

Django templates render server-side HTML.

```html
<h1>{{ user.username }}</h1>

{% for item in items %}
  <p>{{ item.name }}</p>
{% endfor %}
```

Know:

- variables
- filters
- tags
- template inheritance
- autoescaping

The template engine is not required when Django is used purely as a backend API.

<a id="models-and-orm"></a>
## Models and ORM

[Back to Table of Contents](#table-of-contents)

Django ORM maps Python model classes to database tables.

```python
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)
```

Know:

- fields
- primary keys
- constraints
- Meta
- model methods
- managers
- migrations
- relationships

ORM does not remove the need to understand SQL. Interviews often ask you to connect ORM operations to SQL behavior.

<a id="querysets"></a>
## QuerySets

[Back to Table of Contents](#table-of-contents)

QuerySets represent database queries.

```python
active_users = User.objects.filter(is_active=True)
user = User.objects.get(pk=1)
recent = User.objects.order_by("-created_at")[:20]
```

Important property:

QuerySets are generally lazy. Building a QuerySet does not necessarily execute the database query immediately.

Evaluation can happen through operations such as:

- iteration
- list()
- len()
- bool()
- serialization
- explicit evaluation

Do not accidentally trigger repeated queries inside loops.

<a id="relationships-and-related-objects"></a>
## Relationships and Related Objects

[Back to Table of Contents](#table-of-contents)

Foreign key:

```python
class Order(models.Model):
    user = models.ForeignKey(
        User,
        on_delete=models.CASCADE,
        related_name="orders",
    )
```

Know:

- ForeignKey
- OneToOneField
- ManyToManyField
- on_delete
- related_name
- reverse relationships

Understand the SQL shape behind relationships and use query optimization deliberately.

<a id="migrations"></a>
## Migrations

[Back to Table of Contents](#table-of-contents)

Migrations track schema changes.

Common commands:

```bash
python manage.py makemigrations
python manage.py migrate
python manage.py showmigrations
```

makemigrations creates migration files from model changes.

migrate applies migrations to the database.

Migrations are versioned schema history, not simply "the database backup."

<a id="transactions-and-concurrency"></a>
## Transactions and Concurrency

[Back to Table of Contents](#table-of-contents)

Django supports transaction management:

```python
from django.db import transaction

with transaction.atomic():
    account.debit(amount)
    account.credit(amount)
```

Know:

- atomicity
- commit
- rollback
- isolation
- select_for_update()
- race conditions
- optimistic vs pessimistic approaches

Example:

```python
with transaction.atomic():
    wallet = Wallet.objects.select_for_update().get(pk=wallet_id)
    wallet.balance -= 100
    wallet.save(update_fields=["balance"])
```

The row lock helps serialize competing updates to the selected record when supported by the database.

<a id="indexes-and-database-performance"></a>
## Indexes and Database Performance

[Back to Table of Contents](#table-of-contents)

Indexes can speed reads that match the indexed access pattern, but add storage and write/update cost.

Know:

- db_index
- Meta indexes
- composite indexes
- unique constraints
- query plans
- select_related
- prefetch_related
- only()
- defer()

Do not claim that adding an index always makes every query faster.

<a id="django-forms"></a>
## Django Forms

[Back to Table of Contents](#table-of-contents)

Django Forms provide HTML form handling and validation.

Know:

- Form
- ModelForm
- field validation
- clean()
- clean_<field>()
- errors
- CSRF integration

For JSON APIs, DRF serializers usually play the validation/deserialization role instead of Django Forms.

<a id="admin"></a>
## Admin

[Back to Table of Contents](#table-of-contents)

Django admin provides an authenticated interface for model management.

```python
from django.contrib import admin
from .models import Product

@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = ("name", "price")
```

Useful concepts:

- ModelAdmin
- list_display
- list_filter
- search_fields
- ordering
- custom actions

<a id="middleware"></a>
## Middleware

[Back to Table of Contents](#table-of-contents)

Middleware is a chain of request/response hooks.

Common uses:

- authentication-related processing
- logging
- security headers
- sessions
- CORS support
- request IDs
- timing

Conceptually:

```text
request -> middleware 1 -> middleware 2 -> view
response <- middleware 2 <- middleware 1
```

Middleware ordering matters.

<a id="authentication"></a>
## Authentication

[Back to Table of Contents](#table-of-contents)

Django includes authentication primitives:

- User model
- authentication backends
- login/logout
- password hashing
- permissions
- groups
- sessions

Know the difference:

Authentication = who are you?

Authorization = what are you allowed to do?

<a id="authorization-and-permissions"></a>
## Authorization and Permissions

[Back to Table of Contents](#table-of-contents)

Django permissions can be associated with users and groups.

Application-specific authorization can also be enforced in views, services or DRF permission classes.

Always enforce authorization on the server.

Never rely on hidden UI elements to protect an operation.

<a id="sessions-and-cookies"></a>
## Sessions and Cookies

[Back to Table of Contents](#table-of-contents)

Django sessions allow server-side session state with a session identifier commonly stored in a cookie.

Know cookie attributes:

- HttpOnly
- Secure
- SameSite
- Domain
- Path

Session-backed authentication differs from stateless token-based authentication.

<a id="csrf"></a>
## CSRF

[Back to Table of Contents](#table-of-contents)

Cross-Site Request Forgery tricks a browser into sending an authenticated request that the user did not intentionally initiate.

Django includes CSRF protection for relevant cookie/session-based browser workflows.

Important distinction:

- CORS controls browser cross-origin access policy.
- CSRF protects against a class of unwanted authenticated browser requests.

They solve different problems.

<a id="caching"></a>
## Caching

[Back to Table of Contents](#table-of-contents)

Django provides a cache framework supporting configurable cache backends.

Common pattern:

```text
request
  |
  v
cache lookup
  |
  +-- hit --> response
  |
  +-- miss --> database/query --> cache set --> response
```

Know:

- cache keys
- TTL
- invalidation
- per-view caching
- low-level cache API
- Redis/Memcached concepts

Caching stale data is a correctness concern, not only a performance concern.

<a id="signals"></a>
## Signals

[Back to Table of Contents](#table-of-contents)

Signals allow decoupled code to react to framework or model events.

Examples:

- post_save
- pre_save
- post_delete

Example:

```python
from django.db.models.signals import post_save
from django.dispatch import receiver

@receiver(post_save, sender=User)
def user_saved(sender, instance, created, **kwargs):
    if created:
        create_profile(instance)
```

Interview caution:

Do not use signals for every business workflow. Hidden side effects can make execution flow difficult to trace. Explicit service-layer calls are often easier to reason about for critical business logic.

<a id="static-and-media-files"></a>
## Static and Media Files

[Back to Table of Contents](#table-of-contents)

Static files are application assets such as CSS and JavaScript.

Media files are user-uploaded content.

Know:

- STATIC_URL
- STATIC_ROOT
- MEDIA_URL
- MEDIA_ROOT
- collectstatic
- object storage concepts

Production applications commonly serve static/media assets separately from the application process.

<a id="file-uploads"></a>
## File Uploads

[Back to Table of Contents](#table-of-contents)

Django handles uploaded files through request data and model fields such as FileField/ImageField.

Production considerations:

- validate file type and size
- generate safe names
- do not trust file extensions alone
- store user uploads safely
- use object storage when appropriate
- avoid blocking application workers with expensive processing

<a id="email-and-background-work"></a>
## Email and Background Work

[Back to Table of Contents](#table-of-contents)

Email can be sent using Django's email utilities.

Long-running work should usually be moved out of the request path.

For example:

```text
HTTP request
   |
   v
create job
   |
   v
queue
   |
   v
worker
   |
   v
email/image processing
```

Django itself does not turn arbitrary work into distributed background processing. Celery, RQ or another worker system can be used for that.

<a id="testing-django"></a>
## Testing Django

[Back to Table of Contents](#table-of-contents)

Know:

- unit tests
- integration tests
- Django TestCase
- transaction behavior
- client requests
- database isolation
- factory/fixture concepts

Example:

```python
from django.test import TestCase
from django.urls import reverse

class HealthTest(TestCase):
    def test_health(self):
        response = self.client.get(reverse("health"))
        self.assertEqual(response.status_code, 200)
```

Test business behavior, validation, permissions and important failure paths.

<a id="security"></a>
## Security

[Back to Table of Contents](#table-of-contents)

High-value Django security topics:

- CSRF
- XSS protection
- SQL injection protection through parameterized ORM operations
- clickjacking protection
- secure cookies
- HSTS
- security headers
- DEBUG=False in production
- ALLOWED_HOSTS
- secret management
- password hashing
- dependency updates

Django includes useful security defaults, but developers still need correct configuration and safe application logic.

<a id="deployment-and-production"></a>
## Deployment and Production

[Back to Table of Contents](#table-of-contents)

Know the deployment path:

```text
Internet
  |
  v
Reverse Proxy / Load Balancer
  |
  v
Gunicorn / Uvicorn / Daphne
  |
  v
Django
  |
  v
Database / Cache / Queue / Object Storage
```

Production checklist:

- DEBUG=False
- secure secrets
- allowed hosts
- HTTPS
- database backups
- static files
- logging
- monitoring
- health checks
- worker/process management
- connection pooling where appropriate
- timeouts

<a id="django-rest-framework-fundamentals"></a>
## Django REST Framework Fundamentals

[Back to Table of Contents](#table-of-contents)

Django REST Framework, or DRF, adds tools for building Web APIs on top of Django.

Core pieces:

- serializers
- API views
- generic views
- ViewSets
- routers
- authentication
- permissions
- throttling
- pagination
- filtering
- exception handling
- content negotiation

A typical DRF path:

```text
HTTP request
  |
  v
Django middleware
  |
  v
DRF view
  |
  v
authentication
  |
  v
permissions
  |
  v
validation
  |
  v
business logic
  |
  v
serializer
  |
  v
Response
```

<a id="serializers"></a>
## Serializers

[Back to Table of Contents](#table-of-contents)

Serializers convert complex Python/Django objects into representations such as JSON and validate incoming data.

Basic serializer:

```python
from rest_framework import serializers

class ProductSerializer(serializers.Serializer):
    name = serializers.CharField(max_length=200)
    price = serializers.DecimalField(max_digits=10, decimal_places=2)
```

ModelSerializer:

```python
class ProductSerializer(serializers.ModelSerializer):
    class Meta:
        model = Product
        fields = ["id", "name", "price"]
```

Interview answer:

"Serialization converts Python-side objects into transferable representations. Deserialization parses incoming primitive data into validated Python data. DRF serializers also provide field and object validation."

<a id="serializer-validation"></a>
## Serializer Validation

[Back to Table of Contents](#table-of-contents)

Field validation:

```python
def validate_price(self, value):
    if value < 0:
        raise serializers.ValidationError("Price cannot be negative.")
    return value
```

Object-level validation:

```python
def validate(self, attrs):
    if attrs["start"] > attrs["end"]:
        raise serializers.ValidationError("Invalid range.")
    return attrs
```

Then:

```python
serializer.is_valid(raise_exception=True)
serializer.validated_data
```

Do not treat request.data as trusted or already validated.

<a id="apiview"></a>
## APIView

[Back to Table of Contents](#table-of-contents)

APIView provides explicit HTTP-method handling with DRF's request/response behavior.

```python
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

class ProductList(APIView):
    def get(self, request):
        products = Product.objects.all()
        serializer = ProductSerializer(products, many=True)
        return Response(serializer.data)

    def post(self, request):
        serializer = ProductSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)
        serializer.save()
        return Response(serializer.data, status=status.HTTP_201_CREATED)
```

Use APIView when explicit control is valuable.

<a id="generic-views"></a>
## Generic Views

[Back to Table of Contents](#table-of-contents)

Generic API views reduce repeated CRUD code.

Common classes:

- ListAPIView
- CreateAPIView
- RetrieveAPIView
- UpdateAPIView
- DestroyAPIView
- ListCreateAPIView
- RetrieveUpdateDestroyAPIView

They combine behavior through generic and mixin-based abstractions.

<a id="viewsets-and-routers"></a>
## ViewSets and Routers

[Back to Table of Contents](#table-of-contents)

ViewSets group related actions.

```python
from rest_framework.viewsets import ModelViewSet

class ProductViewSet(ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
```

Router:

```python
from rest_framework.routers import DefaultRouter

router = DefaultRouter()
router.register("products", ProductViewSet)
```

ViewSets reduce URL boilerplate but can hide control flow compared with explicit APIViews.

<a id="function-based-api-views"></a>
## Function-Based API Views

[Back to Table of Contents](#table-of-contents)

DRF also supports function-based views:

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(["GET"])
def health(request):
    return Response({"status": "ok"})
```

Use the style that keeps the endpoint understandable and consistent with the surrounding codebase.

<a id="request-and-response"></a>
## Request and Response

[Back to Table of Contents](#table-of-contents)

DRF Request provides parsed request data.

Common inputs:

- request.data
- request.query_params
- request.headers
- request.user
- request.auth

Response:

```python
return Response(
    {"message": "created"},
    status=201,
)
```

DRF handles representation and content negotiation around the response.

<a id="http-methods-and-status-codes"></a>
## HTTP Methods and Status Codes

[Back to Table of Contents](#table-of-contents)

Common methods:

- GET — retrieve
- POST — create/process
- PUT — full replacement semantics
- PATCH — partial update
- DELETE — delete

Common statuses:

- 200 OK
- 201 Created
- 202 Accepted
- 204 No Content
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 409 Conflict
- 429 Too Many Requests
- 500 Internal Server Error

Important:

401 usually means authentication is required or failed.

403 means the request is understood but access is not permitted.

<a id="authentication-in-drf"></a>
## Authentication in DRF

[Back to Table of Contents](#table-of-contents)

Authentication identifies the caller.

Common approaches:

- SessionAuthentication
- TokenAuthentication
- custom authentication classes
- JWT through a third-party package

Authentication and permission checks are separate steps.

Example configuration concept:

```python
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework.authentication.SessionAuthentication",
    ],
}
```

<a id="permissions-in-drf"></a>
## Permissions in DRF

[Back to Table of Contents](#table-of-contents)

Permissions decide whether an authenticated or anonymous request may perform an action.

Common classes:

- AllowAny
- IsAuthenticated
- IsAdminUser
- IsAuthenticatedOrReadOnly

Custom permission:

```python
from rest_framework.permissions import BasePermission

class IsOwner(BasePermission):
    def has_object_permission(self, request, view, obj):
        return obj.owner_id == request.user.id
```

Do not confuse authentication with authorization.

<a id="throttling"></a>
## Throttling

[Back to Table of Contents](#table-of-contents)

DRF throttling limits request rates.

Useful for:

- abuse prevention
- expensive endpoints
- anonymous API limits
- user-specific API limits

Throttling is not a complete DDoS defense.

Use infrastructure-level controls for large-scale protection.

<a id="pagination"></a>
## Pagination

[Back to Table of Contents](#table-of-contents)

Pagination avoids returning unbounded datasets.

Common DRF styles include:

- PageNumberPagination
- LimitOffsetPagination
- CursorPagination

Interview comparison:

- Page number is intuitive.
- Limit/offset is flexible but can become inefficient at large offsets.
- Cursor pagination is suited to stable ordered streams and large datasets, but is less convenient for arbitrary page jumps.

<a id="filtering-search-and-ordering"></a>
## Filtering, Search and Ordering

[Back to Table of Contents](#table-of-contents)

API endpoints often support:

```text
GET /products/?category=books&search=python&ordering=-created_at
```

DRF can integrate with filtering backends and custom query logic.

Important practice:

Validate allowed filter and ordering fields instead of constructing arbitrary database expressions from untrusted input.

<a id="versioning"></a>
## Versioning

[Back to Table of Contents](#table-of-contents)

APIs can evolve through versioning strategies such as:

- URL versioning
- namespace versioning
- header versioning
- media-type versioning

Example:

```text
/api/v1/products/
/api/v2/products/
```

Choose a strategy consistently and define deprecation/backward-compatibility expectations.

<a id="content-negotiation"></a>
## Content Negotiation

[Back to Table of Contents](#table-of-contents)

Content negotiation determines the representation returned based on the request and supported renderers.

Know:

- JSONRenderer
- BrowsableAPIRenderer
- Accept header

DRF can support representations beyond JSON depending on configured renderers.

<a id="exception-handling"></a>
## Exception Handling

[Back to Table of Contents](#table-of-contents)

DRF has centralized exception handling for many API errors.

Common exceptions:

- ValidationError
- NotAuthenticated
- PermissionDenied
- NotFound
- Throttled

Custom handler:

```python
from rest_framework.views import exception_handler

def custom_exception_handler(exc, context):
    response = exception_handler(exc, context)

    if response is not None:
        response.data["service"] = "api"

    return response
```

Do not swallow errors and return HTTP 200 for failures.

<a id="browsable-api-and-openapi"></a>
## Browsable API and OpenAPI

[Back to Table of Contents](#table-of-contents)

DRF's browsable API helps inspect and interact with endpoints during development.

OpenAPI describes API contracts such as:

- paths
- methods
- parameters
- request bodies
- responses
- authentication schemes

Know the purpose even if the project uses a dedicated documentation package.

<a id="nested-serializers-and-relationships"></a>
## Nested Serializers and Relationships

[Back to Table of Contents](#table-of-contents)

Nested representation:

```python
class OrderSerializer(serializers.ModelSerializer):
    items = OrderItemSerializer(many=True, read_only=True)

    class Meta:
        model = Order
        fields = ["id", "items"]
```

Nested writes require explicit handling when creating or updating related objects.

Do not assume nested serialization automatically creates every related object correctly.

<a id="custom-fields-and-serializermethodfield"></a>
## Custom Fields and SerializerMethodField

[Back to Table of Contents](#table-of-contents)

SerializerMethodField can expose computed output:

```python
class ProductSerializer(serializers.ModelSerializer):
    display_name = serializers.SerializerMethodField()

    class Meta:
        model = Product
        fields = ["id", "name", "display_name"]

    def get_display_name(self, obj):
        return f"{obj.id}: {obj.name}"
```

Use it carefully on large querysets because per-object work can become expensive.

<a id="drf-performance-and-query-optimization"></a>
## DRF Performance and Query Optimization

[Back to Table of Contents](#table-of-contents)

A common DRF performance problem is N+1 queries.

Bad shape:

```python
orders = Order.objects.all()

for order in orders:
    print(order.user.email)
```

Potential fix:

```python
orders = Order.objects.select_related("user")
```

For many-valued relationships:

```python
orders = Order.objects.prefetch_related("items")
```

Interview workflow:

1. identify endpoint latency
2. inspect query count
3. find N+1 patterns
4. use select_related/prefetch_related appropriately
5. add indexes when justified
6. paginate
7. cache only where correctness permits
8. measure again

<a id="idempotency-and-api-reliability"></a>
## Idempotency and API Reliability

[Back to Table of Contents](#table-of-contents)

Network clients retry. Servers can receive duplicate requests.

For operations such as payment or order creation, idempotency can prevent duplicate side effects.

Concept:

```text
client
  |
  v
idempotency key
  |
  v
API
  |
  v
check/store request result
  |
  v
perform operation once
  |
  v
return same logical result for duplicate key
```

Also know:

- timeouts
- bounded retries
- exponential backoff
- jitter
- circuit breakers
- rate limiting
- validation
- observability

<a id="django-vs-drf-vs-fastapi"></a>
## Django vs DRF vs FastAPI

[Back to Table of Contents](#table-of-contents)

Django and FastAPI are both Python web technologies, but they solve different layers and emphasize different defaults.

Django:

- batteries-included web framework
- ORM
- admin
- templates
- authentication/session ecosystem
- mature full-stack architecture

DRF:

- API toolkit built around Django
- serializers
- API views
- ViewSets
- authentication/permissions
- pagination/filtering/throttling

FastAPI:

- API-focused Python framework
- ASGI-oriented
- type-hint-driven request validation
- automatic OpenAPI documentation
- dependency injection
- async-friendly request handlers

Interview answer:

"I choose based on requirements. Django is strong when I need a full application framework and integrated ORM/admin/auth ecosystem. DRF is natural when the backend is Django-based and exposes APIs. FastAPI is attractive for API-first services where ASGI, type hints and explicit API contracts are central."

Do not claim one framework is universally faster or better.

<a id="django-with-react"></a>
## Django with React

[Back to Table of Contents](#table-of-contents)

Common architecture:

```text
React
  |
  v
HTTPS / JSON
  |
  v
Django + DRF
  |
  v
Service layer
  |
  v
PostgreSQL / Redis / external APIs
```

Key integration topics:

- CORS
- CSRF for cookie-based authentication
- JWT/session authentication
- JSON serialization
- pagination
- error contracts
- file uploads
- API versioning

<a id="django-with-sceneflow"></a>
## Django with SceneFlow

[Back to Table of Contents](#table-of-contents)

For interview discussion, map SceneFlow concepts to Django equivalents.

Potential architecture:

```text
React frontend
   |
   v
Django / DRF API
   |
   v
authentication + validation
   |
   v
PostgreSQL
   |
   v
Redis + Celery
   |
   v
Gemini / image providers / Qdrant
```

Example project explanation:

"I would keep HTTP responsibilities in DRF views, request validation in serializers, domain logic in a service layer, persistence through the Django ORM, and expensive image-processing work in Celery workers. Redis can support queueing and caching, while PostgreSQL stores project, scene and result metadata."

The framework should not own all business logic. Keeping domain workflows in services makes testing and evolution easier.

<a id="django-with-the-url-shortener"></a>
## Django with the URL Shortener

[Back to Table of Contents](#table-of-contents)

Possible flow:

```text
Browser
 |
 v
Django/DRF
 |
 v
Redis cache lookup
 |
 +-- hit --> redirect
 |
 +-- miss --> PostgreSQL lookup --> redirect
```

For URL creation:

- validate the destination
- generate a unique short code
- store the mapping
- enforce uniqueness
- return the public URL

For high-concurrency counters or metadata updates, use atomic database operations/transactions rather than read-modify-write logic without protection.

<a id="django-project-architecture"></a>
## Django Project Architecture

[Back to Table of Contents](#table-of-contents)

For a growing Django backend:

```text
API layer
  |
  v
serializers / schemas
  |
  v
service layer
  |
  v
repositories or ORM queries
  |
  v
database
```

Supporting layers:

- authentication
- permissions
- caching
- background jobs
- external service clients
- observability

Do not force a repository layer into every small Django project. Introduce abstractions when they solve a real complexity or testing problem.

<a id="implementation-drills"></a>
## Implementation Drills

[Back to Table of Contents](#table-of-contents)

### Build a simple Django model

```python
class ShortURL(models.Model):
    code = models.CharField(max_length=32, unique=True)
    target = models.URLField()
    created_at = models.DateTimeField(auto_now_add=True)
```

### Build a DRF serializer

```python
class ShortURLSerializer(serializers.ModelSerializer):
    class Meta:
        model = ShortURL
        fields = ["id", "code", "target", "created_at"]
        read_only_fields = ["id", "code", "created_at"]
```

### Build a create endpoint

```python
class ShortURLCreate(APIView):
    def post(self, request):
        serializer = ShortURLSerializer(data=request.data)
        serializer.is_valid(raise_exception=True)

        obj = serializer.save()
        return Response(
            ShortURLSerializer(obj).data,
            status=status.HTTP_201_CREATED,
        )
```

### Build a permission

```python
class IsOwner(BasePermission):
    def has_object_permission(self, request, view, obj):
        return obj.owner_id == request.user.id
```

### Optimize related-object loading

```python
queryset = Order.objects.select_related("user").prefetch_related("items")
```

### Add an atomic update

```python
from django.db import transaction
from django.db.models import F

with transaction.atomic():
    wallet = Wallet.objects.select_for_update().get(pk=wallet_id)
    wallet.balance = F("balance") - amount
    wallet.save(update_fields=["balance"])
```

<a id="generic-interview-qa"></a>
## Generic Interview Q&A

[Back to Table of Contents](#table-of-contents)

### What is Django?

A high-level Python web framework that provides common components for building web applications.

### Why is Django called batteries-included?

Because many common web-development capabilities are integrated into the framework ecosystem instead of requiring every feature to be assembled independently.

### What is MTV?

Model, Template and View. It is Django's common terminology for its architectural pattern.

### What is ORM?

Object-Relational Mapping translates between application objects and relational database operations.

### What is middleware?

A request/response processing layer that can wrap view execution.

### What is a migration?

Versioned schema-change metadata used to bring database structure in sync with model definitions.

### What is DRF?

A toolkit built on Django for implementing Web APIs with serializers, views, authentication, permissions and related API capabilities.

### What is serialization?

Converting complex application objects into transferable primitive representations.

### What is deserialization?

Parsing incoming data into Python-side representations and validating it.

<a id="django-qa"></a>
## Django Q&A

[Back to Table of Contents](#table-of-contents)

### What is manage.py?

A command-line utility used to perform administrative tasks for a Django project.

### Why use include() in urls.py?

To split URL configuration across apps and keep the root URL configuration smaller.

### What is AppConfig?

It stores configuration and metadata for a Django application.

### What is QuerySet laziness?

QuerySets generally defer database execution until their results are needed.

### select_related vs prefetch_related?

select_related uses SQL joins for single-valued relationships such as foreign keys and one-to-one relationships. prefetch_related performs additional queries and combines the results in Python, making it suitable for many-to-many and reverse/many-valued relationships.

### What does transaction.atomic() do?

It groups database operations into an atomic transaction boundary so the database can commit or roll back the group together.

### What is select_for_update()?

It requests row-level locking for selected rows within a transaction on databases that support the relevant locking semantics.

### Why are signals controversial?

They can hide side effects and make execution flow harder to discover and test.

### What is collectstatic?

A Django management operation that gathers static files into the configured static root for serving/deployment.

<a id="drf-qa"></a>
## DRF Q&A

[Back to Table of Contents](#table-of-contents)

### Serializer vs ModelSerializer?

Serializer requires explicit fields and behavior. ModelSerializer can derive many fields and model-related behavior from a Django model.

### APIView vs GenericAPIView?

APIView gives lower-level explicit control over HTTP methods. GenericAPIView adds reusable generic behavior commonly combined with mixins.

### APIView vs ViewSet?

APIView organizes behavior around explicit HTTP methods. ViewSet organizes related resource actions and can work with routers.

### What are routers?

Routers generate URL patterns for ViewSets.

### Why use many=True?

It tells a serializer that the input or output represents a collection rather than a single object.

### What does is_valid() do?

It runs serializer validation and populates validated_data or validation errors.

### validated_data vs data?

validated_data contains validated Python-side input after is_valid(). data contains serialized output representation.

### Authentication vs permission?

Authentication identifies the requester. Permission determines whether that requester is allowed to perform the action.

### What is throttling?

A mechanism for limiting request rates.

### Why paginate?

To prevent unbounded response sizes and control database/network/application work.

### Why are 401 and 403 different?

401 indicates missing/invalid authentication in common HTTP usage. 403 indicates access is forbidden.

<a id="database-and-orm-qa"></a>
## Database and ORM Q&A

[Back to Table of Contents](#table-of-contents)

### What causes N+1 queries?

Fetching a base queryset and then triggering another database query for related data inside a loop.

### How do you fix N+1?

Use select_related for suitable single-valued relationships and prefetch_related for many-valued relationships, then verify query counts.

### Does ORM mean you do not need SQL?

No. SQL knowledge is still necessary for indexing, joins, query plans, transactions and performance reasoning.

### What is an index trade-off?

Indexes can speed some reads but require storage and can increase write/update cost.

### What is a transaction?

A boundary for a set of database operations with atomicity and consistency guarantees defined by the database and isolation level.

<a id="security-qa"></a>
## Security Q&A

[Back to Table of Contents](#table-of-contents)

### Is CORS authentication?

No. CORS is a browser cross-origin policy mechanism.

### Is CSRF the same as CORS?

No. CSRF protects against a class of unwanted authenticated browser requests; CORS governs whether browser JavaScript can access cross-origin responses.

### Is JWT encrypted?

Not by default. A common JWT is signed rather than encrypted.

### Where should authorization happen?

On the server, close to the protected resource or business operation.

### How do you protect uploaded files?

Validate content and size, use safe storage, avoid trusting filenames/extensions, and consider scanning/processing requirements.

### Why should DEBUG be false in production?

Debug mode can expose development diagnostics and sensitive information.

<a id="project-based-qa"></a>
## Project-Based Q&A

[Back to Table of Contents](#table-of-contents)

### Explain how you would design SceneFlow in Django/DRF

"I would expose project and scene APIs through DRF. Serializers validate request data and output schemas. Views handle HTTP concerns. Business workflows live in services. PostgreSQL stores durable metadata. Celery workers process expensive image-search jobs. Redis supports queueing and caching. External clients wrap Gemini, image providers and Qdrant interactions."

### How would you avoid long API requests?

"Create a job, return an accepted response or job identifier, process expensive work asynchronously, and let the frontend poll or subscribe to status."

### How would you prevent duplicate jobs?

"Use an idempotency key or unique job constraint where appropriate, make worker operations idempotent, and track job state."

### How would you explain Django ORM usage?

"I use model definitions for persistence, QuerySets for filtering and joins, select_related/prefetch_related for relationship loading, transactions for atomic workflows and indexes based on measured query patterns."

### How would you explain a URL shortener?

"Create the URL mapping through an authenticated API, generate a unique code, persist the mapping, cache hot redirects where useful, and resolve the short code through a fast lookup path."

### What would you do if a DRF endpoint becomes slow?

"Measure first. Inspect query count and timings, find N+1 queries, optimize ORM loading, check indexes, paginate, cache suitable results, inspect external service latency and measure again."

<a id="interview-traps"></a>
## Interview Traps

[Back to Table of Contents](#table-of-contents)

- "Django is only an MVC framework."
- "MTV means Django has no MVC concepts."
- "Django ORM means SQL is unnecessary."
- "Every QuerySet call immediately hits the database."
- "select_related and prefetch_related do the same thing."
- "Migrations are database backups."
- "Signals are always the best place for business logic."
- "CORS protects an API from unauthorized clients."
- "CSRF and CORS are the same."
- "JWT is automatically encrypted."
- "APIView is always better than ViewSet."
- "ViewSets are only for CRUD."
- "Serializers are only for output."
- "request.data is trusted input."
- "HTTP 401 and 403 mean the same thing."
- "Pagination is only a frontend concern."
- "Throttling is a complete DDoS solution."
- "Adding an index always fixes a slow endpoint."
- "Background work can safely run inside every HTTP request."
- "Async automatically makes database/CPU work faster."
- "Django automatically provides distributed job processing."
- "Hiding a button in React is authorization."
- "DRF replaces the need to understand HTTP."

<a id="final-checklist"></a>
## Final Checklist

[Back to Table of Contents](#table-of-contents)

Be able to explain from memory:

- Django vs DRF
- MTV architecture
- project vs app
- settings
- request lifecycle
- URL routing
- FBV vs CBV
- templates
- models and ORM
- QuerySet laziness
- relationships
- migrations
- transactions
- select_for_update
- indexes
- forms
- admin
- middleware
- authentication vs authorization
- sessions/cookies
- CSRF
- caching
- signals
- static/media files
- file uploads
- background jobs
- testing
- deployment
- Django security
- DRF request lifecycle
- serializers
- validation
- APIView
- generic views
- ViewSets
- routers
- request/response
- HTTP methods
- status codes
- authentication
- permissions
- throttling
- pagination
- filtering/search/ordering
- versioning
- content negotiation
- exception handling
- OpenAPI
- nested serializers
- custom serializer fields
- N+1 queries
- select_related/prefetch_related
- idempotency
- API reliability
- Django vs FastAPI trade-offs
- React integration
- SceneFlow architecture
- URL shortener architecture
- implementation drills
- generic Q&A
- Django Q&A
- DRF Q&A
- ORM Q&A
- security Q&A
- project answers
- interview traps

[Back to Table of Contents](#table-of-contents)
