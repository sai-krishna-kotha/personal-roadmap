# LLD System Design Interview Notes — Infosys DSE / SP

This file is the dedicated **Low-Level Design (LLD)** preparation reference.

LLD is separate from HLD. HLD focuses on services, databases, queues, scaling, traffic, and system architecture. LLD focuses on **classes, objects, interfaces, responsibilities, relationships, extensibility, design principles, and code-level design**.

The goal is not to memorize design-pattern names. The goal is to recognize a design problem, identify the right abstraction, write a clean implementation, and explain the trade-off.

---

<a id="table-of-contents"></a>

## Table of Contents

### 1. LLD Foundations
- [How to Use These Notes](#how-to-use-these-notes)
- [What LLD Actually Means](#what-lld-actually-means)
- [HLD vs LLD](#hld-vs-lld)
- [LLD Interview Mindset](#lld-interview-mindset)
- [Requirements and Use Cases](#requirements-and-use-cases)
- [Identify Classes and Responsibilities](#identify-classes-and-responsibilities)
- [Relationships Between Objects](#relationships-between-objects)
- [Composition vs Inheritance](#composition-vs-inheritance)
- [Dependency Injection](#dependency-injection)
- [Interfaces and Abstractions](#interfaces-and-abstractions)
- [Cohesion and Coupling](#cohesion-and-coupling)
- [Immutability](#immutability)
- [Exceptions and Error Handling](#exceptions-and-error-handling)

### 2. SOLID Principles
- [SOLID Overview](#solid-overview)
- [Single Responsibility Principle](#single-responsibility-principle)
- [Open Closed Principle](#open-closed-principle)
- [Liskov Substitution Principle](#liskov-substitution-principle)
- [Interface Segregation Principle](#interface-segregation-principle)
- [Dependency Inversion Principle](#dependency-inversion-principle)
- [SOLID Trade-Offs](#solid-trade-offs)
- [SOLID Interview Traps](#solid-interview-traps)

### 3. Core Object-Oriented Design
- [Encapsulation](#encapsulation)
- [Abstraction](#abstraction)
- [Polymorphism](#polymorphism)
- [Inheritance](#inheritance)
- [Association, Aggregation and Composition](#association-aggregation-and-composition)
- [Abstract Class vs Interface](#abstract-class-vs-interface)
- [Method Overloading vs Overriding](#method-overloading-vs-overriding)
- [Static vs Dynamic Binding](#static-vs-dynamic-binding)
- [Dependency vs Association](#dependency-vs-association)
- [Tell Dont Ask](#tell-dont-ask)
- [Law of Demeter](#law-of-demeter)

### 4. Creational Design Patterns
- [Why Creational Patterns Exist](#why-creational-patterns-exist)
- [Singleton](#singleton)
- [Factory Method](#factory-method)
- [Simple Factory](#simple-factory)
- [Abstract Factory](#abstract-factory)
- [Builder](#builder)
- [Prototype](#prototype)
- [Creational Pattern Comparison](#creational-pattern-comparison)

### 5. Structural Design Patterns
- [Why Structural Patterns Exist](#why-structural-patterns-exist)
- [Adapter](#adapter)
- [Decorator](#decorator)
- [Facade](#facade)
- [Proxy](#proxy)
- [Composite](#composite)
- [Bridge](#bridge)
- [Flyweight](#flyweight)
- [Structural Pattern Comparison](#structural-pattern-comparison)

### 6. Behavioral Design Patterns
- [Why Behavioral Patterns Exist](#why-behavioral-patterns-exist)
- [Strategy](#strategy)
- [Observer](#observer)
- [Command](#command)
- [State](#state)
- [Chain of Responsibility](#chain-of-responsibility)
- [Template Method](#template-method)
- [Iterator](#iterator)
- [Mediator](#mediator)
- [Memento](#memento)
- [Visitor](#visitor)
- [Behavioral Pattern Comparison](#behavioral-pattern-comparison)

### 7. Interview-Focused Implementation Drills
- [Parking Lot](#parking-lot)
- [Library Management System](#library-management-system)
- [ATM](#atm)
- [Vending Machine](#vending-machine)
- [Elevator](#elevator)
- [Car Rental System](#car-rental-system)
- [Hotel Booking Model](#hotel-booking-model)
- [Chess](#chess)
- [Tic-Tac-Toe](#tic-tac-toe)
- [Snake and Ladder](#snake-and-ladder)
- [Splitwise](#splitwise)
- [Notification Framework](#notification-framework)
- [Payment Processing](#payment-processing)
- [Rate Limiter LLD](#rate-limiter-lld)
- [Logging Framework](#logging-framework)

### 8. Python LLD Coding Patterns
- [Python ABC](#python-abc)
- [Python Protocol](#python-protocol)
- [Dependency Injection in Python](#dependency-injection-in-python)
- [Enums and Value Objects](#enums-and-value-objects)
- [Dataclasses](#dataclasses)
- [Composition in Python](#composition-in-python)
- [Callable Strategy](#callable-strategy)
- [Testing Through Interfaces](#testing-through-interfaces)

### 9. How to Solve Any LLD Problem
- [LLD Design Workflow](#lld-design-workflow)
- [Requirement Extraction](#requirement-extraction)
- [Identify Entities](#identify-entities)
- [Assign Responsibilities](#assign-responsibilities)
- [Define Relationships](#define-relationships)
- [Define Interfaces](#define-interfaces)
- [Choose Patterns Only Where Needed](#choose-patterns-only-where-needed)
- [Implement a Minimal Working Version](#implement-a-minimal-working-version)
- [Extend the Design](#extend-the-design)
- [Review for SOLID](#review-for-solid)
- [Testing and Edge Cases](#testing-and-edge-cases)
- [Explain the Design to the Interviewer](#explain-the-design-to-the-interviewer)

### 10. Pattern Selection Guide
- [Pattern Recognition Cheat Sheet](#pattern-recognition-cheat-sheet)
- [When to Use Strategy vs State](#when-to-use-strategy-vs-state)
- [When to Use Factory vs Builder](#when-to-use-factory-vs-builder)
- [When to Use Adapter vs Facade](#when-to-use-adapter-vs-facade)
- [When to Use Decorator vs Proxy](#when-to-use-decorator-vs-proxy)
- [When to Use Observer vs Mediator](#when-to-use-observer-vs-mediator)

### 11. Common Interview Coding Expectations
- [What They May Ask You to Code](#what-they-may-ask-you-to-code)
- [Progressive Coding Strategy](#progressive-coding-strategy)
- [How to Avoid Overengineering](#how-to-avoid-overengineering)
- [Common LLD Coding Mistakes](#common-lld-coding-mistakes)
- [30-Second LLD Revision](#30-second-lld-revision)
- [Final LLD Interview Checklist](#final-lld-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

For every LLD topic, learn it in this order:

1. **Problem** — What design problem does it solve?
2. **Structure** — Which classes/interfaces participate?
3. **Collaboration** — How do the objects interact?
4. **Implementation** — Can you write a rough version?
5. **Extension** — What changes if a new requirement appears?
6. **Principles** — Which SOLID/OOP principle does the design demonstrate?
7. **Trade-off** — What complexity did the abstraction introduce?

For interviews, start with the **smallest correct design**. Then extend it when the interviewer adds requirements.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-lld-actually-means"></a>

## What LLD Actually Means

Low-Level Design translates requirements into **objects, classes, interfaces, responsibilities, and collaborations**.

Example:

```text
Requirement:
Support multiple payment methods.

Weak design:
PaymentService has a huge if/elif chain.

Better LLD:
PaymentProcessor
 ├── CardPayment
 ├── UPIPayment
 └── WalletPayment
```

The second design creates an extension point.

The interviewer is usually interested in **why the objects are shaped this way**, not only whether the code runs.

[Back to Table of Contents](#table-of-contents)

---

<a id="hld-vs-lld"></a>

## HLD vs LLD

| HLD | LLD |
|---|---|
| Services | Classes / objects |
| Databases | Object state |
| Queues | Method interactions |
| Scaling | Encapsulation |
| Replication | Inheritance / composition |
| Network flow | In-process control flow |
| Failure at service level | Error/exception behavior |
| Architecture | Code-level design |

[Back to Table of Contents](#table-of-contents)

---

<a id="lld-interview-mindset"></a>

## LLD Interview Mindset

Do not start by saying:

> “I will use Strategy, Factory, Observer and Singleton.”

Start with:

```text
What must the system do?
What changes are likely?
Which object owns each responsibility?
Which dependencies should be replaceable?
Where can behavior vary?
```

Then choose the simplest abstraction that solves that problem.

### Golden rule

> **Patterns are tools, not the design.**

[Back to Table of Contents](#table-of-contents)

---

<a id="requirements-and-use-cases"></a>

## Requirements and Use Cases

Write short use cases before classes.

Example parking lot:

```text
Vehicle enters
Vehicle gets a spot
Vehicle exits
Fee is calculated
Payment is processed
```

Then identify nouns and verbs.

Nouns often suggest objects.

Verbs often suggest responsibilities.

Do not blindly create a class for every noun.

[Back to Table of Contents](#table-of-contents)

---

<a id="identify-classes-and-responsibilities"></a>

## Identify Classes and Responsibilities

A class should have a clear purpose.

Bad:

```text
ParkingLotManager
- stores vehicles
- calculates fees
- sends notifications
- processes payments
- persists data
```

Better decomposition:

```text
ParkingLot
ParkingFloor
ParkingSpot
Vehicle
FeeCalculator
PaymentService
NotificationService
```

The goal is high cohesion.

[Back to Table of Contents](#table-of-contents)

---

<a id="relationships-between-objects"></a>

## Relationships Between Objects

Common relationships:

```text
Association
Aggregation
Composition
Inheritance
Dependency
```

### Example

```text
ParkingLot has ParkingFloor
ParkingFloor has ParkingSpot
```

The exact relationship should follow lifecycle ownership and business semantics, not UML vocabulary alone.

[Back to Table of Contents](#table-of-contents)

---

<a id="composition-vs-inheritance"></a>

## Composition vs Inheritance

### Inheritance

Use when there is a genuine substitutable **is-a** relationship.

```text
Dog is an Animal
```

### Composition

Build behavior from collaborators.

```text
Car
 ├── Engine
 └── Transmission
```

Composition usually gives more flexibility because collaborators can change independently.

### Interview rule

> Prefer composition when behavior can be modeled as a replaceable collaborator rather than a true subtype.

[Back to Table of Contents](#table-of-contents)

---

<a id="dependency-injection"></a>

## Dependency Injection

Instead of a class constructing its dependency:

```python
class OrderService:
    def __init__(self):
        self.payment = StripePayment()
```

Inject it:

```python
class OrderService:
    def __init__(self, payment):
        self.payment = payment
```

Now testing can supply a fake payment implementation.

This directly supports dependency inversion and substitution.

[Back to Table of Contents](#table-of-contents)

---

<a id="interfaces-and-abstractions"></a>

## Interfaces and Abstractions

An abstraction defines what a collaborator can do without forcing callers to depend on its implementation.

Example:

```text
PaymentGateway
    ↓
StripeGateway
RazorpayGateway
MockGateway
```

The caller depends on `PaymentGateway`, not a specific provider.

[Back to Table of Contents](#table-of-contents)

---

<a id="cohesion-and-coupling"></a>

## Cohesion and Coupling

### Cohesion

How closely related a class's responsibilities are.

High cohesion is desirable.

### Coupling

How strongly components depend on each other's implementation/details.

Low coupling is generally desirable.

Good LLD aims for:

```text
High cohesion
+
Low coupling
```

[Back to Table of Contents](#table-of-contents)

---

<a id="immutability"></a>

## Immutability

An immutable object does not change after construction.

Useful for:

- value objects
- money
- coordinates
- configuration
- IDs

Benefits:

- easier reasoning
- safer sharing
- fewer accidental state changes

[Back to Table of Contents](#table-of-contents)

---

<a id="exceptions-and-error-handling"></a>

## Exceptions and Error Handling

LLD should model invalid states deliberately.

Examples:

```text
InsufficientBalance
InvalidStateTransition
SpotUnavailable
PaymentFailed
UnsupportedOperation
```

Do not use exceptions as a substitute for normal control flow.

[Back to Table of Contents](#table-of-contents)

---

<a id="solid-overview"></a>

## SOLID Overview

```text
S → Single Responsibility
O → Open/Closed
L → Liskov Substitution
I → Interface Segregation
D → Dependency Inversion
```

Use SOLID as a design-review checklist rather than five isolated definitions.

[Back to Table of Contents](#table-of-contents)

---

<a id="single-responsibility-principle"></a>

## Single Responsibility Principle

A class should have one coherent reason to change.

Bad:

```python
class Invoice:
    def calculate_total(self): ...
    def save_to_db(self): ...
    def send_email(self): ...
```

Better:

```text
Invoice
InvoiceRepository
InvoiceEmailSender
```

SRP does not mean “one method per class”.

[Back to Table of Contents](#table-of-contents)

---

<a id="open-closed-principle"></a>

## Open Closed Principle

Software entities should be open for extension without requiring frequent modification of stable code.

Example:

Instead of:

```python
if payment_type == "card":
    ...
elif payment_type == "upi":
    ...
```

Use a common abstraction:

```text
PaymentMethod
 ├── CardPayment
 ├── UPIPayment
 └── WalletPayment
```

Then new payment behavior can be added as a new implementation.

[Back to Table of Contents](#table-of-contents)

---

<a id="liskov-substitution-principle"></a>

## Liskov Substitution Principle

A subtype should be usable wherever its abstraction is expected without breaking the client's assumptions.

Classic trap:

```text
Bird
 └── fly()

Penguin extends Bird
but cannot fly
```

If the base contract requires `fly()`, the hierarchy is wrong.

Fix the abstraction instead of adding exceptions.

[Back to Table of Contents](#table-of-contents)

---

<a id="interface-segregation-principle"></a>

## Interface Segregation Principle

Clients should not depend on methods they do not need.

Bad:

```text
Machine
- print()
- scan()
- fax()
```

A basic printer should not implement unrelated operations.

Split interfaces around client needs.

[Back to Table of Contents](#table-of-contents)

---

<a id="dependency-inversion-principle"></a>

## Dependency Inversion Principle

High-level policy should not depend directly on low-level implementation details.

Both should depend on abstractions.

```text
OrderService
    ↓
PaymentGateway
    ↑
Stripe / Mock / BankGateway
```

This is one of the most important principles for testable LLD.

[Back to Table of Contents](#table-of-contents)

---

<a id="solid-trade-offs"></a>

## SOLID Trade-Offs

SOLID is not “more abstractions = better”.

Excessive abstraction can produce:

- too many classes
- indirection
- difficult debugging
- premature generalization

A strong interview answer can say:

> “I would introduce this abstraction because this behavior is expected to vary. I would not abstract the parts that are stable.”

[Back to Table of Contents](#table-of-contents)

---

<a id="solid-interview-traps"></a>

## SOLID Interview Traps

- SRP does not mean one method per class.
- OCP does not mean never modifying existing code.
- LSP is about behavioral substitutability, not syntax.
- ISP is about client-specific contracts.
- DIP is about depending on abstractions, not simply using dependency injection.
- SOLID principles can conflict with simplicity if applied mechanically.

[Back to Table of Contents](#table-of-contents)

---

<a id="encapsulation"></a>

## Encapsulation

Encapsulation keeps an object's state and invariants under controlled access.

Example:

```python
class BankAccount:
    def __init__(self, balance: int = 0):
        self._balance = balance

    def withdraw(self, amount: int) -> None:
        if amount > self._balance:
            raise ValueError("insufficient balance")
        self._balance -= amount

    @property
    def balance(self) -> int:
        return self._balance
```

The object owns the rule.

[Back to Table of Contents](#table-of-contents)

---

<a id="abstraction"></a>

## Abstraction

Expose essential behavior while hiding implementation details.

Example:

```text
PaymentGateway
    charge(amount)
```

Callers should not need to know how a specific provider signs requests or retries HTTP calls.

[Back to Table of Contents](#table-of-contents)

---

<a id="polymorphism"></a>

## Polymorphism

Different implementations can respond through the same abstraction.

```python
class Notification:
    def send(self, message): ...

class EmailNotification(Notification):
    def send(self, message):
        print("email")

class SMSNotification(Notification):
    def send(self, message):
        print("sms")
```

The caller can work with `Notification`.

[Back to Table of Contents](#table-of-contents)

---

<a id="inheritance"></a>

## Inheritance

Inheritance reuses and specializes a base contract.

Use it carefully.

Prefer it when:

- the subtype truly is substitutable
- the abstraction is stable
- shared behavior is meaningful

Avoid inheritance just to reuse a few methods.

[Back to Table of Contents](#table-of-contents)

---

<a id="association-aggregation-and-composition"></a>

## Association, Aggregation and Composition

### Association

Objects know or interact with each other.

### Aggregation

A whole refers to parts, but part lifetime can exist independently.

### Composition

The whole strongly owns the part lifecycle.

Example:

```text
Order → LineItems
```

Depending on the domain, line items may be composition because they have little independent meaning outside the order.

[Back to Table of Contents](#table-of-contents)

---

<a id="abstract-class-vs-interface"></a>

## Abstract Class vs Interface

### Abstract class

Can combine:

- shared implementation
- shared state
- abstract operations

### Interface

Primarily defines a contract.

In Python, an interface-like abstraction can be represented with:

- `abc.ABC`
- `@abstractmethod`
- `typing.Protocol`

Choose based on whether shared implementation/state is needed.

[Back to Table of Contents](#table-of-contents)

---

<a id="method-overloading-vs-overriding"></a>

## Method Overloading vs Overriding

### Overloading

Same conceptual operation with different parameter signatures.

Python does not support Java-style signature overloading directly; common alternatives are default arguments, `*args`, `**kwargs`, or `functools.singledispatch` where appropriate.

### Overriding

Subclass provides a different implementation of an inherited method.

[Back to Table of Contents](#table-of-contents)

---

<a id="static-vs-dynamic-binding"></a>

## Static vs Dynamic Binding

Static binding resolves a method reference earlier.

Dynamic binding chooses the overridden implementation based on the runtime object.

Polymorphism relies heavily on dynamic dispatch.

[Back to Table of Contents](#table-of-contents)

---

<a id="dependency-vs-association"></a>

## Dependency vs Association

A dependency can be temporary:

```python
report.generate(formatter)
```

The method depends on `formatter`, but does not necessarily retain it as state.

An association generally represents a stronger structural relationship.

[Back to Table of Contents](#table-of-contents)

---

<a id="tell-dont-ask"></a>

## Tell Dont Ask

Instead of retrieving an object's state and performing its business rule elsewhere:

```python
if account.balance >= amount:
    account.balance -= amount
```

Prefer:

```python
account.withdraw(amount)
```

The object enforces its own invariants.

[Back to Table of Contents](#table-of-contents)

---

<a id="law-of-demeter"></a>

## Law of Demeter

An object should avoid reaching through long chains of unrelated objects.

Avoid:

```python
order.customer.address.city.name
```

Long chains often indicate excessive coupling.

[Back to Table of Contents](#table-of-contents)

---

<a id="why-creational-patterns-exist"></a>

## Why Creational Patterns Exist

Creational patterns manage **object creation** when construction becomes complex, variable, or decoupled from the caller.

The core interview question:

> “Why should this object be created through an abstraction instead of calling its constructor directly?”

[Back to Table of Contents](#table-of-contents)

---

<a id="singleton"></a>

## Singleton

Guarantees a single shared instance within the intended scope.

### Rough Python implementation

```python
class Singleton:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance
```

### Interview discussion

Singleton can simplify shared access but introduces global state and can make testing harder.

In many modern applications, dependency injection is cleaner.

[Back to Table of Contents](#table-of-contents)

---

<a id="factory-method"></a>

## Factory Method

Encapsulate object creation behind a method or factory abstraction.

```python
from abc import ABC, abstractmethod

class Notification(ABC):
    @abstractmethod
    def send(self, message: str) -> None:
        pass

class EmailNotification(Notification):
    def send(self, message: str) -> None:
        print("email:", message)

class SMSNotification(Notification):
    def send(self, message: str) -> None:
        print("sms:", message)

class NotificationFactory:
    @staticmethod
    def create(channel: str) -> Notification:
        if channel == "email":
            return EmailNotification()
        if channel == "sms":
            return SMSNotification()
        raise ValueError("unsupported channel")
```

The caller no longer needs to know the concrete class.

[Back to Table of Contents](#table-of-contents)

---

<a id="simple-factory"></a>

## Simple Factory

A simple factory centralizes creation but is not formally one of the original GoF 23 patterns.

```python
class PaymentFactory:
    @staticmethod
    def create(kind: str):
        if kind == "card":
            return CardPayment()
        if kind == "upi":
            return UPIPayment()
        raise ValueError("unsupported payment")
```

Useful for straightforward creation logic.

Trade-off: the factory itself changes when new types are added.

[Back to Table of Contents](#table-of-contents)

---

<a id="abstract-factory"></a>

## Abstract Factory

Creates a **family of related objects**.

Example:

```text
DarkThemeFactory
 ├── DarkButton
 └── DarkDialog

LightThemeFactory
 ├── LightButton
 └── LightDialog
```

Use when products must remain compatible as a family.

[Back to Table of Contents](#table-of-contents)

---

<a id="builder"></a>

## Builder

Useful when object construction has many optional parameters or construction steps.

```python
class User:
    def __init__(self, name, email, phone=None, city=None):
        self.name = name
        self.email = email
        self.phone = phone
        self.city = city

class UserBuilder:
    def __init__(self, name, email):
        self._name = name
        self._email = email
        self._phone = None
        self._city = None

    def phone(self, value):
        self._phone = value
        return self

    def city(self, value):
        self._city = value
        return self

    def build(self):
        return User(self._name, self._email, self._phone, self._city)
```

Trade-off: builder adds classes/indirection.

[Back to Table of Contents](#table-of-contents)

---

<a id="prototype"></a>

## Prototype

Create a new object by copying an existing configured object.

Useful when:

- construction is expensive
- many objects share a base configuration

Watch out for shallow vs deep copying.

[Back to Table of Contents](#table-of-contents)

---

<a id="creational-pattern-comparison"></a>

## Creational Pattern Comparison

| Pattern | Main problem |
|---|---|
| Singleton | Controlled shared instance |
| Factory Method | Vary concrete creation |
| Simple Factory | Centralize simple creation |
| Abstract Factory | Create related object families |
| Builder | Complex step-by-step construction |
| Prototype | Copy an existing object |

[Back to Table of Contents](#table-of-contents)

---

<a id="why-structural-patterns-exist"></a>

## Why Structural Patterns Exist

Structural patterns answer:

> “How can I combine objects without creating tight coupling?”

[Back to Table of Contents](#table-of-contents)

---

<a id="adapter"></a>

## Adapter

Makes one interface look like another expected interface.

```python
class LegacyPrinter:
    def print_text(self, text):
        print(text)

class Printer:
    def print(self, text):
        raise NotImplementedError

class PrinterAdapter(Printer):
    def __init__(self, legacy):
        self.legacy = legacy

    def print(self, text):
        self.legacy.print_text(text)
```

Use when integrating incompatible interfaces.

[Back to Table of Contents](#table-of-contents)

---

<a id="decorator"></a>

## Decorator

Adds behavior without changing the wrapped object's class.

```python
class Notifier:
    def send(self, message):
        print("send:", message)

class LoggingNotifier:
    def __init__(self, wrapped):
        self.wrapped = wrapped

    def send(self, message):
        print("log")
        self.wrapped.send(message)
```

Useful for:

- logging
- metrics
- authorization
- retries
- caching

[Back to Table of Contents](#table-of-contents)

---

<a id="facade"></a>

## Facade

Provides a simpler interface over a complex subsystem.

```text
OrderFacade
 ├── Inventory
 ├── Payment
 └── Shipping
```

Caller:

```python
facade.place_order(order)
```

instead of coordinating every subsystem manually.

[Back to Table of Contents](#table-of-contents)

---

<a id="proxy"></a>

## Proxy

Provides an intermediary around another object.

Common uses:

- access control
- lazy loading
- caching
- remote access
- logging

### Decorator vs Proxy

Decorator primarily **adds behavior**.

Proxy primarily **controls or mediates access**.

[Back to Table of Contents](#table-of-contents)

---

<a id="composite"></a>

## Composite

Treat individual objects and groups uniformly.

Example:

```text
File
Folder
 ├── File
 ├── Folder
 │   └── File
```

A `Folder` and `File` can both support a common operation such as `size()`.

[Back to Table of Contents](#table-of-contents)

---

<a id="bridge"></a>

## Bridge

Separates an abstraction from its implementation so both can vary independently.

Example:

```text
RemoteControl → Device
TV
Radio
```

Different remotes and devices can evolve independently.

[Back to Table of Contents](#table-of-contents)

---

<a id="flyweight"></a>

## Flyweight

Share common intrinsic state between many objects.

Useful when many logically distinct objects share expensive immutable data.

Trade-off:

External/contextual state becomes necessary.

[Back to Table of Contents](#table-of-contents)

---

<a id="structural-pattern-comparison"></a>

## Structural Pattern Comparison

| Pattern | Main problem |
|---|---|
| Adapter | Incompatible interfaces |
| Decorator | Add behavior dynamically |
| Facade | Simplify a subsystem |
| Proxy | Control/mediate access |
| Composite | Treat tree groups uniformly |
| Bridge | Separate abstraction and implementation |
| Flyweight | Share repeated immutable state |

[Back to Table of Contents](#table-of-contents)

---

<a id="why-behavioral-patterns-exist"></a>

## Why Behavioral Patterns Exist

Behavioral patterns focus on:

- changing behavior
- communication between objects
- decoupling senders and receivers
- selecting algorithms
- modeling state transitions

[Back to Table of Contents](#table-of-contents)

---

<a id="strategy"></a>

## Strategy

Encapsulate interchangeable algorithms behind a common interface.

```python
from abc import ABC, abstractmethod

class PricingStrategy(ABC):
    @abstractmethod
    def calculate(self, amount: float) -> float:
        pass

class RegularPricing(PricingStrategy):
    def calculate(self, amount):
        return amount

class DiscountPricing(PricingStrategy):
    def calculate(self, amount):
        return amount * 0.9

class Checkout:
    def __init__(self, strategy):
        self.strategy = strategy

    def total(self, amount):
        return self.strategy.calculate(amount)
```

Use when the **algorithm varies**.

[Back to Table of Contents](#table-of-contents)

---

<a id="observer"></a>

## Observer

One object publishes changes to multiple subscribers.

```python
class Subject:
    def __init__(self):
        self._observers = []

    def subscribe(self, observer):
        self._observers.append(observer)

    def notify(self, event):
        for observer in self._observers:
            observer.update(event)
```

Useful for:

- notifications
- event handling
- UI updates

Trade-off:

Subscriber failures and event ordering need consideration.

[Back to Table of Contents](#table-of-contents)

---

<a id="command"></a>

## Command

Encapsulate an operation as an object.

```python
class Command:
    def execute(self):
        raise NotImplementedError

class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.on()
```

Useful for:

- undo/redo
- queues
- task execution
- audit logs

[Back to Table of Contents](#table-of-contents)

---

<a id="state"></a>

## State

Allow an object to change behavior based on its internal state.

Example vending machine:

```text
NoCoin
HasCoin
Dispensing
OutOfStock
```

State pattern makes transitions explicit instead of creating huge conditional blocks.

[Back to Table of Contents](#table-of-contents)

---

<a id="chain-of-responsibility"></a>

## Chain of Responsibility

Pass a request through a sequence of handlers until one handles it.

```text
Request
 ↓
Auth → RateLimit → Validation → BusinessLogic
```

Useful for pipelines and middleware-like processing.

[Back to Table of Contents](#table-of-contents)

---

<a id="template-method"></a>

## Template Method

Base class defines the algorithm skeleton while subclasses customize selected steps.

Useful when:

- process order stays fixed
- certain steps vary

Prefer Strategy when the whole algorithm should be swapped at runtime.

[Back to Table of Contents](#table-of-contents)

---

<a id="iterator"></a>

## Iterator

Provides sequential access to a collection without exposing its internal representation.

Python's iterator protocol is a direct real-world example.

[Back to Table of Contents](#table-of-contents)

---

<a id="mediator"></a>

## Mediator

Centralizes complex communication between many objects.

Instead of:

```text
A ↔ B ↔ C ↔ D
```

use:

```text
A → Mediator ← B
C → Mediator ← D
```

Useful when object-to-object interactions become tangled.

[Back to Table of Contents](#table-of-contents)

---

<a id="memento"></a>

## Memento

Capture and restore an object's state without exposing implementation details.

Useful for undo functionality.

[Back to Table of Contents](#table-of-contents)

---

<a id="visitor"></a>

## Visitor

Separate operations from object structures.

Useful when:

- object structure is stable
- many operations change independently

Often more complex than necessary for beginner interviews.

[Back to Table of Contents](#table-of-contents)

---

<a id="behavioral-pattern-comparison"></a>

## Behavioral Pattern Comparison

| Pattern | Main problem |
|---|---|
| Strategy | Interchangeable algorithms |
| Observer | One-to-many notification |
| Command | Encapsulate requests |
| State | Behavior changes with state |
| Chain of Responsibility | Sequential request handling |
| Template Method | Fixed algorithm skeleton |
| Iterator | Sequential traversal |
| Mediator | Centralize collaboration |
| Memento | Save/restore state |
| Visitor | Add operations to stable structures |

[Back to Table of Contents](#table-of-contents)

---

<a id="parking-lot"></a>

## Parking Lot

### Core objects

```text
ParkingLot
ParkingFloor
ParkingSpot
Vehicle
Ticket
FeeCalculator
Payment
```

### Extension point

Vehicle types:

```python
from enum import Enum

class VehicleType(Enum):
    BIKE = "bike"
    CAR = "car"
    TRUCK = "truck"
```

Spot matching should be a policy rather than a giant `if` chain.

### Interview focus

- inheritance vs composition
- spot allocation
- fee strategy
- state transitions
- extensibility

[Back to Table of Contents](#table-of-contents)

---

<a id="library-management-system"></a>

## Library Management System

Core objects:

```text
Book
BookCopy
Member
Librarian
Loan
Reservation
Catalog
```

Important distinction:

**Book** represents the title/metadata.

**BookCopy** represents a physical copy that can be borrowed.

That distinction prevents a common modeling mistake.

[Back to Table of Contents](#table-of-contents)

---

<a id="atm"></a>

## ATM

Core states:

```text
Idle
CardInserted
Authenticated
Transaction
Ejecting
```

The State pattern fits naturally because behavior changes according to ATM state.

Potential services:

```text
CardReader
CashDispenser
AccountService
TransactionRepository
```

Interview follow-ups:

- invalid PIN attempts
- insufficient cash
- transaction rollback
- hardware failures

[Back to Table of Contents](#table-of-contents)

---

<a id="vending-machine"></a>

## Vending Machine

Good for demonstrating State + Strategy.

```text
NoCoin
HasCoin
ProductSelected
Dispensing
```

Policies can handle:

- pricing
- payment validation
- change calculation

The core lesson is avoiding a giant state-dependent conditional method.

[Back to Table of Contents](#table-of-contents)

---

<a id="elevator"></a>

## Elevator

Core objects:

```text
Elevator
Floor
Request
Scheduler
Door
Motor
```

Possible strategy:

```text
Nearest-request-first
SCAN-like scheduling
```

The scheduling rule can be represented as a replaceable strategy.

[Back to Table of Contents](#table-of-contents)

---

<a id="car-rental-system"></a>

## Car Rental System

Core objects:

```text
Vehicle
VehicleInventory
Customer
Reservation
Rental
PricingStrategy
Payment
```

Interesting interview discussion:

- availability
- reservation state
- pricing strategy
- vehicle categories
- cancellation
- payment failure

[Back to Table of Contents](#table-of-contents)

---

<a id="hotel-booking-model"></a>

## Hotel Booking Model

Core objects:

```text
Hotel
Room
RoomType
Guest
Reservation
Payment
```

Potential state:

```text
AVAILABLE
HELD
BOOKED
```

Important concurrency requirement:

Two users cannot successfully book the same room for overlapping dates.

[Back to Table of Contents](#table-of-contents)

---

<a id="chess"></a>

## Chess

Core objects:

```text
Board
Game
Player
Piece
Move
Position
```

Pieces share a common abstraction but implement different movement rules.

Good for:

- polymorphism
- composition
- validation
- state management

[Back to Table of Contents](#table-of-contents)

---

<a id="tic-tac-toe"></a>

## Tic-Tac-Toe

Small enough for a live coding interview.

Possible classes:

```text
Game
Board
Player
Move
```

Keep the design simple.

Do not introduce ten patterns for a 3×3 board.

[Back to Table of Contents](#table-of-contents)

---

<a id="snake-and-ladder"></a>

## Snake and Ladder

Core objects:

```text
Game
Board
Player
Dice
Snake
Ladder
```

Dice behavior can be injected for deterministic testing.

[Back to Table of Contents](#table-of-contents)

---

<a id="splitwise"></a>

## Splitwise

Core objects:

```text
User
Expense
Split
Group
Balance
Settlement
```

Split calculation strategies:

```text
Equal
Exact
Percentage
```

Strategy is a natural fit.

[Back to Table of Contents](#table-of-contents)

---

<a id="notification-framework"></a>

## Notification Framework

Strong Strategy + Factory example.

```python
class NotificationSender:
    def send(self, recipient, message):
        raise NotImplementedError

class EmailSender(NotificationSender):
    def send(self, recipient, message):
        print("email")

class SMSSender(NotificationSender):
    def send(self, recipient, message):
        print("sms")

class NotificationService:
    def __init__(self, sender):
        self.sender = sender

    def notify(self, recipient, message):
        self.sender.send(recipient, message)
```

Adding WhatsApp should not require rewriting `NotificationService`.

[Back to Table of Contents](#table-of-contents)

---

<a id="payment-processing"></a>

## Payment Processing

Good interview design:

```text
PaymentProcessor
   ↓
PaymentGateway
 ├── Stripe
 ├── Razorpay
 └── MockGateway
```

Use abstraction + dependency injection.

### Follow-ups

- retry
- duplicate payment request
- timeout
- provider failure
- refund
- idempotency

[Back to Table of Contents](#table-of-contents)

---

<a id="rate-limiter-lld"></a>

## Rate Limiter LLD

Define:

```python
class RateLimiter:
    def allow(self, key: str) -> bool:
        raise NotImplementedError
```

Implementations:

```text
FixedWindowRateLimiter
SlidingWindowRateLimiter
TokenBucketRateLimiter
```

This combines Strategy + interface-based design.

[Back to Table of Contents](#table-of-contents)

---

<a id="logging-framework"></a>

## Logging Framework

Possible objects:

```text
Logger
LogHandler
Formatter
Appender
LogLevel
```

A logger can delegate output to handlers:

```text
Logger
 ├── ConsoleHandler
 ├── FileHandler
 └── RemoteHandler
```

Useful patterns:

- Chain of Responsibility
- Strategy
- Factory

[Back to Table of Contents](#table-of-contents)

---

<a id="python-abc"></a>

## Python ABC

Use `ABC` when subclasses are expected to honor an explicit abstract contract.

```python
from abc import ABC, abstractmethod

class PaymentGateway(ABC):
    @abstractmethod
    def charge(self, amount: int) -> str:
        pass
```

[Back to Table of Contents](#table-of-contents)

---

<a id="python-protocol"></a>

## Python Protocol

`Protocol` supports structural typing.

```python
from typing import Protocol

class Sender(Protocol):
    def send(self, message: str) -> None:
        ...
```

A class can satisfy the protocol without explicitly inheriting from it.

Useful for flexible dependency boundaries and testing.

[Back to Table of Contents](#table-of-contents)

---

<a id="dependency-injection-in-python"></a>

## Dependency Injection in Python

Constructor injection is usually the clearest form:

```python
class OrderService:
    def __init__(self, payment_gateway):
        self.payment_gateway = payment_gateway
```

For interviews, explain that the dependency can be replaced with a fake or mock.

[Back to Table of Contents](#table-of-contents)

---

<a id="enums-and-value-objects"></a>

## Enums and Value Objects

Enums are useful for fixed states/types.

```python
from enum import Enum

class OrderStatus(Enum):
    CREATED = "created"
    PAID = "paid"
    CANCELLED = "cancelled"
```

Value objects represent small domain concepts:

```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Money:
    amount: int
    currency: str
```

[Back to Table of Contents](#table-of-contents)

---

<a id="dataclasses"></a>

## Dataclasses

Useful for simple data-bearing domain objects.

```python
from dataclasses import dataclass

@dataclass
class User:
    id: int
    name: str
```

Do not use a dataclass as a substitute for every domain class; behavior and invariants still matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="composition-in-python"></a>

## Composition in Python

```python
class CheckoutService:
    def __init__(self, pricing, payment):
        self.pricing = pricing
        self.payment = payment
```

The service delegates variable behavior to collaborators.

This is one of the most reusable Python LLD patterns.

[Back to Table of Contents](#table-of-contents)

---

<a id="callable-strategy"></a>

## Callable Strategy

Python can sometimes avoid a strategy class entirely.

```python
def regular_price(amount):
    return amount

def discounted_price(amount):
    return amount * 0.9

class Checkout:
    def __init__(self, pricing):
        self.pricing = pricing

    def total(self, amount):
        return self.pricing(amount)
```

For tiny algorithms, functions can be clearer than classes.

This is a useful trade-off to mention in interviews.

[Back to Table of Contents](#table-of-contents)

---

<a id="testing-through-interfaces"></a>

## Testing Through Interfaces

Example:

```python
class FakePaymentGateway:
    def charge(self, amount):
        return "fake-payment-id"
```

Inject it:

```python
service = OrderService(FakePaymentGateway())
```

The system can be tested without calling a real payment provider.

[Back to Table of Contents](#table-of-contents)

---

<a id="lld-design-workflow"></a>

## LLD Design Workflow

Use this sequence:

```text
Requirements
↓
Use cases
↓
Entities
↓
Responsibilities
↓
Relationships
↓
Interfaces
↓
Variable behavior
↓
Pattern selection
↓
Implementation
↓
Extension
↓
SOLID review
↓
Tests / edge cases
```

[Back to Table of Contents](#table-of-contents)

---

<a id="requirement-extraction"></a>

## Requirement Extraction

Ask:

- What operations exist?
- What states exist?
- What varies?
- What must be extensible?
- What must remain consistent?
- What failures are possible?

This determines the design.

[Back to Table of Contents](#table-of-contents)

---

<a id="identify-entities"></a>

## Identify Entities

Extract important domain objects.

Example:

```text
Parking Lot
→ Vehicle
→ Spot
→ Ticket
→ Payment
```

Then eliminate nouns that are merely attributes.

[Back to Table of Contents](#table-of-contents)

---

<a id="assign-responsibilities"></a>

## Assign Responsibilities

Use:

> “Which object has the information needed to perform this operation?”

This is often more useful than asking:

> “What class sounds like this feature?”

[Back to Table of Contents](#table-of-contents)

---

<a id="define-relationships"></a>

## Define Relationships

Ask:

```text
Is-a?
Has-a?
Uses?
Owns?
Depends-on?
```

Then choose inheritance, composition, association, or dependency.

[Back to Table of Contents](#table-of-contents)

---

<a id="define-interfaces"></a>

## Define Interfaces

Create abstractions only where:

- implementations may vary
- tests benefit from substitution
- the caller should not know concrete details

Avoid interface-per-class.

[Back to Table of Contents](#table-of-contents)

---

<a id="choose-patterns-only-where-needed"></a>

## Choose Patterns Only Where Needed

Pattern selection should follow the problem.

```text
Algorithm varies
→ Strategy

Creation varies
→ Factory

Construction is complex
→ Builder

Incompatible API
→ Adapter

Add behavior around object
→ Decorator

Complex subsystem
→ Facade

One-to-many notification
→ Observer

Behavior depends on state
→ State

Request moves through handlers
→ Chain of Responsibility
```

[Back to Table of Contents](#table-of-contents)

---

<a id="implement-a-minimal-working-version"></a>

## Implement a Minimal Working Version

Interview implementation order:

```text
1. Core entities
2. Core interfaces
3. Main use case
4. One concrete implementation
5. Add second implementation
6. Refactor toward abstraction
7. Handle edge cases
```

This demonstrates design evolution instead of premature abstraction.

[Back to Table of Contents](#table-of-contents)

---

<a id="extend-the-design"></a>

## Extend the Design

Interviewers commonly add a requirement:

> “Now support another payment provider.”

or:

> “Now add another notification channel.”

Your design should show where the new behavior fits.

This is where OCP, DIP, Strategy, Factory, and composition become visible.

[Back to Table of Contents](#table-of-contents)

---

<a id="review-for-solid"></a>

## Review for SOLID

Ask:

```text
Does one class have too many reasons to change?
Can I add a new behavior without editing stable code?
Can every subtype satisfy its contract?
Are interfaces too broad?
Do high-level classes depend on concrete details?
```

[Back to Table of Contents](#table-of-contents)

---

<a id="testing-and-edge-cases"></a>

## Testing and Edge Cases

Test:

- invalid input
- unavailable resources
- duplicate operations
- state transitions
- dependency failure
- boundary values
- concurrent-looking operations where relevant

For external dependencies, inject fakes/mocks.

[Back to Table of Contents](#table-of-contents)

---

<a id="explain-the-design-to-the-interviewer"></a>

## Explain the Design to the Interviewer

Use this order:

```text
1. Requirements
2. Main entities
3. Responsibilities
4. Relationships
5. Extension points
6. Pattern choice
7. Code
8. Trade-offs
9. Possible future extensions
```

Do not merely read class names.

Explain why each class exists.

[Back to Table of Contents](#table-of-contents)

---

<a id="pattern-recognition-cheat-sheet"></a>

## Pattern Recognition Cheat Sheet

| Problem signal | Likely pattern |
|---|---|
| Algorithm can change | Strategy |
| Object creation varies | Factory |
| Many optional constructor values | Builder |
| Incompatible interface | Adapter |
| Add behavior without modifying class | Decorator |
| Simplify complex subsystem | Facade |
| Control access to object | Proxy |
| One object broadcasts events | Observer |
| Behavior changes by state | State |
| Request passes through handlers | Chain of Responsibility |
| Encapsulate an action | Command |
| Tree of objects | Composite |
| Avoid subclass explosion across dimensions | Bridge |

These are recognition clues, not automatic answers.

[Back to Table of Contents](#table-of-contents)

---

<a id="when-to-use-strategy-vs-state"></a>

## When to Use Strategy vs State

Both can look similar because both delegate behavior.

### Strategy

Behavior is selected because the **algorithm/policy** varies.

```text
Checkout
 └── PricingStrategy
```

### State

Behavior changes because the **object's internal state** changes.

```text
VendingMachine
 └── CurrentState
```

Memory rule:

> Strategy = “Which algorithm should I use?”

> State = “What behavior is valid in my current state?”

[Back to Table of Contents](#table-of-contents)

---

<a id="when-to-use-factory-vs-builder"></a>

## When to Use Factory vs Builder

### Factory

Question:

> Which object should I create?

### Builder

Question:

> How do I construct this complicated object?

[Back to Table of Contents](#table-of-contents)

---

<a id="when-to-use-adapter-vs-facade"></a>

## When to Use Adapter vs Facade

### Adapter

Changes one interface into another compatible interface.

### Facade

Creates a simpler interface over several operations/components.

[Back to Table of Contents](#table-of-contents)

---

<a id="when-to-use-decorator-vs-proxy"></a>

## When to Use Decorator vs Proxy

### Decorator

Add responsibilities around an object.

### Proxy

Stand in front of an object to control or mediate access.

The implementation can look similar; the **intent** is different.

[Back to Table of Contents](#table-of-contents)

---

<a id="when-to-use-observer-vs-mediator"></a>

## When to Use Observer vs Mediator

### Observer

One publisher notifies multiple subscribers.

### Mediator

A central object coordinates many peers to reduce direct coupling.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-they-may-ask-you-to-code"></a>

## What They May Ask You to Code

LLD interviews can turn into live coding around:

```text
Parking lot
Vending machine
ATM
Elevator
Tic-Tac-Toe
Snake and Ladder
Chess
Payment system
Notification system
Rate limiter
Logging framework
Library system
Booking system
```

The transferable skills are:

- class modeling
- interface design
- state management
- polymorphism
- composition
- extensibility
- clean code
- edge-case handling

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-coding-strategy"></a>

## Progressive Coding Strategy

When coding live:

### Level 1 — Make it work

Create the simplest correct model.

### Level 2 — Introduce variability

Find behavior that will change.

### Level 3 — Extract abstraction

Use interface/strategy/composition where justified.

### Level 4 — Handle edge cases

Invalid state, unavailable resource, duplicate operation.

### Level 5 — Explain trade-offs

Say what the abstraction costs.

This is safer than writing a massive framework before the requirements are fully known.

[Back to Table of Contents](#table-of-contents)

---

<a id="how-to-avoid-overengineering"></a>

## How to Avoid Overengineering

Do not automatically add:

- Factory
- Abstract Factory
- Singleton
- Observer
- Builder
- ten interfaces

Start with the direct model.

Introduce a pattern only when a concrete problem appears.

[Back to Table of Contents](#table-of-contents)

---

<a id="common-lld-coding-mistakes"></a>

## Common LLD Coding Mistakes

- God classes
- deep inheritance hierarchies
- mutable global state
- giant `if/elif` type switches
- interfaces containing unrelated methods
- classes exposing all internal state
- mixing business logic with persistence
- no clear ownership of state
- ignoring invalid transitions
- using patterns because they sound impressive
- writing code before clarifying requirements

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-lld-revision"></a>

## 30-Second LLD Revision

```text
Requirements
↓
Entities
↓
Responsibilities
↓
Relationships
↓
Abstractions
↓
Variable behavior
↓
Patterns
↓
Implementation
↓
Extensions
↓
SOLID review
↓
Edge cases
```

### Pattern memory

```text
Strategy    → interchangeable algorithm
Factory     → choose object creation
Builder     → complex construction
Adapter     → incompatible interface
Decorator   → add behavior
Facade      → simplify subsystem
Proxy       → control access
Observer    → notify subscribers
State       → behavior changes with state
Command     → encapsulate action
Composite   → tree structure
Chain       → sequential handlers
Mediator    → central coordination
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-lld-interview-checklist"></a>

## Final LLD Interview Checklist

### OOP

- [ ] encapsulation
- [ ] abstraction
- [ ] inheritance
- [ ] polymorphism
- [ ] composition
- [ ] association
- [ ] aggregation
- [ ] dependency
- [ ] interface
- [ ] abstract class
- [ ] method overriding
- [ ] method overloading
- [ ] dynamic dispatch
- [ ] cohesion
- [ ] coupling
- [ ] immutability
- [ ] Tell Dont Ask
- [ ] Law of Demeter

### SOLID

- [ ] SRP
- [ ] OCP
- [ ] LSP
- [ ] ISP
- [ ] DIP
- [ ] SOLID trade-offs

### Creational

- [ ] Singleton
- [ ] Factory Method
- [ ] Simple Factory
- [ ] Abstract Factory
- [ ] Builder
- [ ] Prototype

### Structural

- [ ] Adapter
- [ ] Decorator
- [ ] Facade
- [ ] Proxy
- [ ] Composite
- [ ] Bridge
- [ ] Flyweight

### Behavioral

- [ ] Strategy
- [ ] Observer
- [ ] Command
- [ ] State
- [ ] Chain of Responsibility
- [ ] Template Method
- [ ] Iterator
- [ ] Mediator
- [ ] Memento
- [ ] Visitor

### Coding readiness

- [ ] design classes from requirements
- [ ] identify responsibilities
- [ ] define interfaces
- [ ] use composition
- [ ] inject dependencies
- [ ] write a rough implementation
- [ ] extend the implementation
- [ ] handle state transitions
- [ ] explain trade-offs
- [ ] test with fakes/mocks

### Practice problems

- [ ] Parking lot
- [ ] Library management
- [ ] ATM
- [ ] Vending machine
- [ ] Elevator
- [ ] Car rental
- [ ] Hotel booking
- [ ] Chess
- [ ] Tic-Tac-Toe
- [ ] Snake and Ladder
- [ ] Splitwise
- [ ] Notification system
- [ ] Payment system
- [ ] Rate limiter
- [ ] Logging framework

### Interview execution

- [ ] Clarify requirements first.
- [ ] Start with a minimal design.
- [ ] Explain why each class exists.
- [ ] Use patterns only when they solve a real problem.
- [ ] Show extension points.
- [ ] Apply SOLID deliberately.
- [ ] Code the core flow before edge cases.
- [ ] Explain trade-offs and complexity.
- [ ] Be ready to add a new requirement live.
- [ ] Be able to explain every line of the implementation.

[Back to Table of Contents](#table-of-contents)