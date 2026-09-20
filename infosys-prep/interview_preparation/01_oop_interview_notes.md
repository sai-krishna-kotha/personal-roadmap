# OOP Interview Notes — Infosys DSE / SP

> Purpose: an interview-ready OOP reference for Infosys DSE / SP-oriented interviews.
>
> This file is deliberately separate from SOLID, UML, design patterns, and system-design notes. It focuses on OOP concepts, reasoning, comparisons, Python implementations, implementation tasks, follow-up questions, and language-level keywords that commonly become interview discussion points.
>
> Source basis: the OOP topics already listed in `infosys-prep/structure_roadmap.md`, expanded with additional interview-relevant concepts where the existing roadmap was not specific enough.

<a id="table-of-contents"></a>

## Table of Contents

- [How to Use These Notes](#how-to-use-these-notes)
- [Interview Depth Model](#interview-depth-model)
- [Class and Object](#class-and-object)
- [Constructor and Object Initialization](#constructor-and-object-initialization)
- [Encapsulation](#encapsulation)
- [Abstraction](#abstraction)
- [Inheritance](#inheritance)
- [Polymorphism](#polymorphism)
- [Overloading](#overloading)
- [Overriding](#overriding)
- [Dynamic Dispatch](#dynamic-dispatch)
- [Static and Dynamic Binding](#static-and-dynamic-binding)
- [Interface and Abstract Class](#interface-and-abstract-class)
- [Composition](#composition)
- [Association, Aggregation, and Composition](#association-aggregation-and-composition)
- [Is-a vs Has-a](#is-a-vs-has-a)
- [Access Control and Name Mangling in Python](#access-control-and-name-mangling-in-python)
- [Class Variables, Instance Variables, Class Methods, and Static Methods](#class-variables-instance-variables-class-methods-and-static-methods)
- [Special Methods and Operator Overloading](#special-methods-and-operator-overloading)
- [Method Resolution Order and super()](#method-resolution-order-and-super)
- [Multiple Inheritance](#multiple-inheritance)
- [Object Identity, Equality, and Hashing](#object-identity-equality-and-hashing)
- [Dependency Inversion in OOP](#dependency-inversion-in-oop)
- [Coupling and Cohesion](#coupling-and-cohesion)
- [Interview Implementation Tasks](#interview-implementation-tasks)
- [Progressive Implementation — Encapsulation](#progressive-implementation--encapsulation)
- [Progressive Implementation — Abstraction](#progressive-implementation--abstraction)
- [Progressive Implementation — Polymorphism](#progressive-implementation--polymorphism)
- [Progressive Implementation — Inheritance and Overriding](#progressive-implementation--inheritance-and-overriding)
- [Progressive Implementation — Composition](#progressive-implementation--composition)
- [Progressive Implementation — Interface-Based Design](#progressive-implementation--interface-based-design)
- [Project-Based OOP Examples](#project-based-oop-examples)
- [Likely Follow-Up Questions](#likely-follow-up-questions)
- [Keyword Radar](#keyword-radar)
- [Common Traps](#common-traps)
- [30-Second Revision Sheet](#30-second-revision-sheet)
- [Final OOP Interview Checklist](#final-oop-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

For each concept, skim in this order:

```text
Understanding
↓
Important points
↓
Personal / simple example
↓
Technical example
↓
Interview discussion
↓
Implementation
↓
Possible follow-up
```

Do not memorize the prose.

The target is to be able to explain:

> What is happening, why it is useful, when it is appropriate, and what trade-off it introduces.

[Back to Table of Contents](#table-of-contents)

---

<a id="interview-depth-model"></a>

## Interview Depth Model

Prepare every important concept at four depths.

### Depth 1 — One sentence

Explain the idea without textbook wording.

### Depth 2 — Example

Give one simple real-world example and one technical example.

### Depth 3 — Comparison / trade-off

Explain when it is preferable to another OOP technique.

### Depth 4 — Code

Implement the smallest useful example and explain every important line.

For implementation questions, speak while coding:

```text
I need to protect this state
→ I will hide the direct mutation
→ expose controlled methods / properties
→ validate the input at the boundary
→ keep the invariant inside the object
```

[Back to Table of Contents](#table-of-contents)

---

<a id="class-and-object"></a>

## Class and Object

### Understanding

A **class** is the design of a type of object: it describes what data the object owns and what behavior it exposes.

An **object** is one concrete instance created from that class.

Think:

```text
Class  = blueprint / type definition
Object = actual thing created from it
```

### Simple example

A class can describe a bank account.

Each account object can have a different owner and balance, while all accounts share the same behavior such as deposit and withdraw.

### Technical example

```python
class BankAccount:
    def __init__(self, owner, balance=0):
        self.owner = owner
        self.balance = balance

account = BankAccount("Sai", 5000)
```

The class defines the structure and behavior. `account` is one object.

### Interview points

- A class defines a type; an object is an instance.
- Different objects have independent instance state.
- Methods describe behavior available to objects.
- In Python, classes are themselves objects of the metaclass `type`, but that is usually beyond the core interview requirement.

### Likely follow-up

> Why not just use dictionaries?

Good direction:

- Dictionaries hold data conveniently.
- Classes combine **state + behavior + invariants**.
- A class can hide implementation details and expose controlled operations.

[Back to Table of Contents](#table-of-contents)

---

<a id="constructor-and-object-initialization"></a>

## Constructor and Object Initialization

### Understanding

In Python, `__init__` initializes an already-created object. It is not literally the low-level object-construction mechanism; `__new__` creates the instance and `__init__` initializes it.

For most application interviews, `__init__` is the practical constructor-style method to discuss.

### Example

```python
class User:
    def __init__(self, username):
        # Store the state every User must have.
        self.username = username

user = User("sai")
```

### Interview point

Be precise:

> “Python uses `__new__` for instance creation and `__init__` for initialization.”

### Follow-up

> When would you use `__new__`?

Examples include immutable types, custom instance creation, or advanced metaprogramming. Do not overuse it in normal application code.

[Back to Table of Contents](#table-of-contents)

---

<a id="encapsulation"></a>

## Encapsulation

### Understanding

Encapsulation is about keeping an object's state and the rules that protect that state together, while controlling how outside code can interact with it.

The important idea is not simply “make variables private”.

It is:

> **Protect invariants and control mutation.**

### Simple example

A bank account should not allow arbitrary code to set the balance to a negative value.

### Technical example

```python
class BankAccount:
    def __init__(self, balance=0):
        # Internal state is not intended to be modified directly.
        self.__balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        self.__balance += amount

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        if amount > self.__balance:
            raise ValueError("Insufficient balance")

        self.__balance -= amount

    def get_balance(self):
        return self.__balance
```

### What to say while coding

> “I do not want callers changing the balance directly because that could violate the business rules. So I keep the state internal and force changes through methods that validate the operation.”

### Important Python nuance

Python does not have strict private fields like Java's `private` keyword.

- `_name` = convention: internal/protected-style API.
- `__name` = name mangling.
- Name mangling discourages accidental access; it is not a security boundary.

### Follow-up implementation

A cleaner interface can use a read-only property:

```python
class BankAccount:
    def __init__(self, balance=0):
        self.__balance = balance

    @property
    def balance(self):
        # Expose a read-only view of the state.
        return self.__balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        self.__balance += amount
```

Now callers can read `account.balance` but cannot use a public setter to change it.

### Common interview trap

Do not say:

> “Encapsulation means declaring variables private.”

Better:

> “Encapsulation keeps state and its rules together and controls access so invariants are protected.”

[Back to Table of Contents](#table-of-contents)

---

<a id="abstraction"></a>

## Abstraction

### Understanding

Abstraction means exposing the part of a system that users of the component need, while hiding unnecessary implementation details.

Think:

```text
What should callers know?
        ↓
Expose that
        ↓
What should callers not care about?
        ↓
Hide that
```

### Simple example

A person drives a car using steering, accelerator, and brake. They do not need to know the internal fuel-injection algorithm.

### Technical example

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount):
        # Every payment implementation must define pay().
        pass


class CardPayment(PaymentProcessor):
    def pay(self, amount):
        return f"Charging card: {amount}"
```

The caller can depend on `PaymentProcessor` without knowing how card processing works internally.

### Abstraction vs encapsulation

| Concept | Main question |
|---|---|
| Encapsulation | How do I protect and control state? |
| Abstraction | What implementation details should I hide behind a simpler interface? |

### Likely implementation task

> “Design a payment system supporting multiple payment methods.”

First version:

```python
class PaymentProcessor:
    def pay(self, amount):
        raise NotImplementedError
```

Then improve it with `ABC` and `@abstractmethod` when you want an explicit contract.

### What to say

> “I am creating a stable contract for the caller. Different implementations can change internally without changing the caller's code.”

[Back to Table of Contents](#table-of-contents)

---

<a id="inheritance"></a>

## Inheritance

### Understanding

Inheritance lets a new class reuse or specialize behavior from an existing class.

It expresses a relationship where the child type can be treated as the parent type when that relationship is genuinely valid.

### Simple example

```text
Vehicle
  ├── Car
  └── Bike
```

A car is a vehicle.

### Technical example

```python
class Vehicle:
    def move(self):
        return "Moving"


class Car(Vehicle):
    def honk(self):
        return "Beep"
```

`Car` inherits `move`.

### Important points

- Inheritance creates coupling between parent and child.
- Child classes can add behavior.
- They can override inherited methods.
- Deep inheritance hierarchies can become difficult to maintain.
- Use inheritance when there is a genuine substitutable relationship, not merely because code looks reusable.

### Follow-up

> Why is composition often preferred?

Because composition usually gives looser coupling and lets us change collaborators without changing the inheritance hierarchy.

[Back to Table of Contents](#table-of-contents)

---

<a id="polymorphism"></a>

## Polymorphism

### Understanding

Polymorphism means code can work with a common interface while the actual object determines the behavior.

The useful interview mental model is:

```text
Same operation
+
Different object
=
Different implementation
```

### Simple example

A `pay()` operation can be implemented differently by card, UPI, or wallet payment.

### Technical example

```python
class CardPayment:
    def pay(self, amount):
        return f"Card payment: {amount}"


class UpiPayment:
    def pay(self, amount):
        return f"UPI payment: {amount}"


def process_payment(processor, amount):
    # We do not need to know the concrete processor type.
    return processor.pay(amount)


print(process_payment(CardPayment(), 100))
print(process_payment(UpiPayment(), 100))
```

The function depends on behavior, not on a concrete class name.

### Technical meaning

In object-oriented designs, polymorphism commonly appears through:

- Method overriding.
- Interface / abstract-class based design.
- Duck typing in Python.
- Dependency injection.

### Personal project connection

In SceneFlow, multiple asset providers can expose a common operation such as:

```text
search(query)
```

The application can work with Pexels, Pixabay, or Openverse without hard-coding every caller around one provider.

### Follow-up

> Why is this useful?

Because the caller depends on a stable contract rather than a specific implementation.

[Back to Table of Contents](#table-of-contents)

---

<a id="overloading"></a>

## Overloading

### Understanding

Method overloading means using the same operation name with different parameter signatures.

Python does **not** support traditional compile-time method overloading like Java or C++.

Instead, Python commonly uses:

- Default arguments.
- `*args` / `**kwargs`.
- Explicit dispatch utilities such as `functools.singledispatch` in suitable cases.

### Interview trap

Do not write:

```python
class Calculator:
    def add(self, a, b):
        return a + b

    def add(self, a, b, c):
        return a + b + c
```

The second method replaces the first one.

### Python-style implementation

```python
class Calculator:
    def add(self, *numbers):
        # Accept a variable number of operands.
        return sum(numbers)

calculator = Calculator()

print(calculator.add(2, 3))
print(calculator.add(2, 3, 4))
```

### What to say

> “Python does not have traditional compile-time method overloading by signature. The usual approach is flexible arguments or explicit dispatch.”

### Overloading vs overriding

```text
Overloading
→ same class / same operation
→ different argument forms
→ compile-time concept in languages that support it

Overriding
→ child redefines inherited behavior
→ runtime polymorphism
```

[Back to Table of Contents](#table-of-contents)

---

<a id="overriding"></a>

## Overriding

### Understanding

Overriding happens when a child class provides its own implementation of a method inherited from the parent.

### Example

```python
class Notification:
    def send(self):
        return "Sending generic notification"


class EmailNotification(Notification):
    def send(self):
        return "Sending email"
```

Calling `send()` on an `EmailNotification` object uses the child implementation.

### Interview point

Overriding is one of the common mechanisms behind runtime polymorphism.

### Follow-up

> What happens if the child still needs the parent behavior?

Use `super()`:

```python
class EmailNotification(Notification):
    def send(self):
        parent_result = super().send()
        return parent_result + " + email-specific behavior"
```

[Back to Table of Contents](#table-of-contents)

---

<a id="dynamic-dispatch"></a>

## Dynamic Dispatch

### Understanding

Dynamic dispatch means the implementation of an overridden method is selected based on the actual object involved at runtime.

### Example

```python
class Animal:
    def speak(self):
        return "Some sound"


class Dog(Animal):
    def speak(self):
        return "Bark"


class Cat(Animal):
    def speak(self):
        return "Meow"


def make_speak(animal):
    # The caller only needs the common operation.
    return animal.speak()


print(make_speak(Dog()))
print(make_speak(Cat()))
```

### What the interviewer is checking

They are usually checking whether you understand:

- Reference / variable type vs actual object.
- Method overriding.
- Runtime method selection.
- Why polymorphic code reduces branching on concrete types.

[Back to Table of Contents](#table-of-contents)

---

<a id="static-and-dynamic-binding"></a>

## Static and Dynamic Binding

### Understanding

**Binding** means connecting a call or reference to the implementation it uses.

High-level distinction:

```text
Static binding
→ decision made earlier, often at compile time

Dynamic binding
→ implementation selected at runtime
```

For Python, emphasize dynamic behavior because method calls are resolved at runtime.

### Interview-ready explanation

> “Static binding is associated with compile-time resolution in statically compiled languages, while dynamic binding selects overridden behavior at runtime. Python is highly dynamic, so runtime lookup is central to normal method dispatch.”

### Do not overstate

Do not turn this into:

> “Python has no static binding anywhere.”

The terminology is language-dependent and context-dependent.

[Back to Table of Contents](#table-of-contents)

---

<a id="interface-and-abstract-class"></a>

## Interface and Abstract Class

### Understanding

An interface is primarily a **contract**: what operations a component promises.

An abstract class can provide a contract **and** shared implementation / state.

Python does not have a Java-style `interface` keyword. Common Python approaches are:

- `abc.ABC` + `@abstractmethod`.
- `typing.Protocol` for structural typing.

### Abstract class example

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount):
        # Concrete classes must implement this.
        pass

    def log_payment(self, amount):
        # Shared behavior can live here.
        print(f"Logging payment: {amount}")


class UpiPayment(PaymentProcessor):
    def pay(self, amount):
        return f"UPI payment: {amount}"
```

### Protocol example

```python
from typing import Protocol


class SearchProvider(Protocol):
    def search(self, query: str) -> list[str]:
        ...
```

A class can satisfy the protocol by providing a compatible `search()` method without explicitly inheriting from `SearchProvider`.

### Interview comparison

| Abstract class | Interface / Protocol |
|---|---|
| Can hold shared implementation | Primarily defines expected behavior |
| Can hold state | Usually no shared state requirement |
| Strong nominal relationship possible | Protocol can use structural typing |
| Useful for common base behavior | Useful for replaceable implementations |

[Back to Table of Contents](#table-of-contents)

---

<a id="composition"></a>

## Composition

### Understanding

Composition means building an object from other objects instead of inheriting all behavior from a parent.

Think:

```text
Object A
  HAS
Object B
```

### Simple example

A car has an engine.

### Technical example

```python
class Engine:
    def start(self):
        return "Engine started"


class Car:
    def __init__(self, engine):
        # Car receives its dependency instead of creating a concrete engine internally.
        self.engine = engine

    def start(self):
        return self.engine.start()
```

This is also dependency injection.

### Why it matters

Composition can provide:

- Lower coupling.
- Easier testing.
- Replaceable collaborators.
- More flexible behavior.

### Follow-up

> Why not inherit Engine?

Because a car **has an engine**; it is not a specialized type of engine.

[Back to Table of Contents](#table-of-contents)

---

<a id="association-aggregation-and-composition"></a>

## Association, Aggregation, and Composition

These three are worth distinguishing because interviewers may ask them together.

### Association

A general relationship between objects.

Example:

```text
Teacher ↔ Student
```

They can exist independently.

### Aggregation

A weak whole-part relationship.

Example:

```text
Department
 └── Employees
```

Employees can conceptually exist independently of a particular department.

### Composition

A strong ownership relationship where the part's lifecycle is tightly coupled to the whole.

Example:

```text
Order
 └── OrderItems
```

### Important Python nuance

These are primarily **design relationships**, not special Python language keywords. The code alone does not automatically tell an interviewer whether a relationship is aggregation or composition; lifecycle and ownership are what matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="is-a-vs-has-a"></a>

## Is-a vs Has-a

A quick recognition rule:

```text
IS-A  → inheritance
HAS-A → composition / aggregation
```

Examples:

```text
Car IS-A Vehicle
Car HAS-A Engine
Order HAS-A PaymentMethod
SceneFlow HAS-A SearchProvider
```

### Interview trap

Do not automatically convert every reuse relationship into inheritance.

Ask:

> “Does the child genuinely represent a specialized form of the parent?”

If not, composition is usually worth considering.

[Back to Table of Contents](#table-of-contents)

---

<a id="access-control-and-name-mangling-in-python"></a>

## Access Control and Name Mangling in Python

Python uses conventions rather than Java-style access modifiers.

### Single underscore

```python
self._cache
```

Meaning:

> Internal-use convention.

### Double underscore

```python
self.__token
```

Python performs name mangling, roughly:

```text
ClassName + attribute
```

This mainly avoids accidental clashes in subclasses.

### Why interviewers ask

They may test whether you know that Python's “private” fields are not true security boundaries.

### Good interview statement

> “Python relies largely on conventions. A single underscore signals internal use, while double underscore activates name mangling; neither should be described as a security mechanism.”

[Back to Table of Contents](#table-of-contents)

---

<a id="class-variables-instance-variables-class-methods-and-static-methods"></a>

## Class Variables, Instance Variables, Class Methods, and Static Methods

### Instance variable

Belongs to one object.

```python
class User:
    def __init__(self, username):
        self.username = username
```

### Class variable

Shared on the class unless shadowed.

```python
class User:
    user_count = 0
```

Be careful: mutable class variables can accidentally become shared state across instances.

### Class method

Receives the class as `cls`.

```python
class User:
    def __init__(self, username):
        self.username = username

    @classmethod
    def guest(cls):
        # Alternative constructor style.
        return cls("guest")
```

### Static method

Receives neither `self` nor `cls` automatically.

```python
class URLValidator:
    @staticmethod
    def is_valid(url):
        return url.startswith(("http://", "https://"))
```

### Interview comparison

| Kind | Automatic first argument | Typical use |
|---|---|---|
| Instance method | `self` | Object state / behavior |
| Class method | `cls` | Alternative constructors / class-level behavior |
| Static method | None | Utility logically grouped with the class |

[Back to Table of Contents](#table-of-contents)

---

<a id="special-methods-and-operator-overloading"></a>

## Special Methods and Operator Overloading

Python special methods let objects participate in built-in language operations.

Examples:

- `__str__`
- `__repr__`
- `__eq__`
- `__lt__`
- `__hash__`
- `__len__`
- `__add__`

### Example

```python
class Money:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        # Define how + should behave for Money objects.
        return Money(self.amount + other.amount)

    def __eq__(self, other):
        if not isinstance(other, Money):
            return NotImplemented

        return self.amount == other.amount

    def __repr__(self):
        return f"Money({self.amount})"
```

### Interview follow-up

> Why return `NotImplemented`?

Because it gives Python a chance to try reflected operations or eventually report an appropriate unsupported-operation result.

Do not confuse `NotImplemented` with `NotImplementedError`:

- `NotImplemented` = special return value used in protocol operations.
- `NotImplementedError` = exception commonly used to mark intentionally unimplemented methods.

[Back to Table of Contents](#table-of-contents)

---

<a id="method-resolution-order-and-super"></a>

## Method Resolution Order and super()

### Understanding

When multiple inheritance is involved, Python needs a deterministic order for searching base classes. That order is the **Method Resolution Order (MRO)**.

### Example

```python
class A:
    def show(self):
        return "A"


class B(A):
    def show(self):
        return "B"


class C(A):
    def show(self):
        return "C"


class D(B, C):
    pass


print(D.mro())
```

The exact order is determined by Python's C3 linearization.

### Why `super()` matters

```python
class Parent:
    def __init__(self):
        print("Parent init")


class Child(Parent):
    def __init__(self):
        # Delegate parent initialization according to the MRO.
        super().__init__()
        print("Child init")
```

### Interview point

Avoid saying:

> “`super()` always means call the immediate parent.”

More accurate:

> “`super()` follows the MRO and delegates to the next implementation in that resolution order.”

[Back to Table of Contents](#table-of-contents)

---

<a id="multiple-inheritance"></a>

## Multiple Inheritance

Python supports a class inheriting from multiple base classes.

```python
class Camera:
    def take_photo(self):
        return "photo"


class GPS:
    def location(self):
        return "location"


class Phone(Camera, GPS):
    pass
```

### Benefits

- Reuse of independent capabilities.
- Mixin-style design.

### Risks

- Ambiguous method lookup.
- Complex MRO.
- Tight coupling to inheritance hierarchy.

### Interview connection

Know the **diamond problem** concept and explain that Python resolves multiple inheritance using MRO / C3 linearization.

[Back to Table of Contents](#table-of-contents)

---

<a id="object-identity-equality-and-hashing"></a>

## Object Identity, Equality, and Hashing

This is a useful “hidden keyword” area for Python interviews.

### Identity

`is` asks whether two references point to the same object.

### Equality

`==` asks whether two objects are considered equal according to their equality implementation.

### Example

```python
a = [1, 2]
b = [1, 2]

print(a == b)  # True: same value
print(a is b)  # False: different objects
```

### Hashing

Objects used as dictionary keys or set members need hash semantics consistent with equality.

If:

```text
a == b
```

then they should have compatible hashes.

Mutable objects need special care before making them hashable.

### Interview follow-up

> Why can overriding `__eq__` affect `__hash__`?

Because hash-based collections rely on equality and hashing being consistent. Python may make a class unhashable when equality is customized without a matching hash contract.

[Back to Table of Contents](#table-of-contents)

---

<a id="dependency-inversion-in-oop"></a>

## Dependency Inversion in OOP

SOLID is intentionally kept separate from the main notes, but the **OOP implementation connection** is worth knowing.

### Understanding

High-level business logic should not be tightly coupled to low-level infrastructure details.

Instead:

```text
Business logic
     ↓
abstraction / protocol
     ↓
concrete implementation
```

### SceneFlow example

The scene-search logic should not have to know whether the provider is Pexels, Pixabay, or Openverse.

### Technical example

```python
from typing import Protocol


class SearchProvider(Protocol):
    def search(self, query: str) -> list[str]:
        ...


class SceneSearchService:
    def __init__(self, provider: SearchProvider):
        # Inject the dependency so the service is not tied to one provider.
        self.provider = provider

    def search(self, query: str):
        return self.provider.search(query)
```

### Interview point

This is where OOP connects to:

- Abstraction.
- Polymorphism.
- Composition.
- Dependency injection.
- Testability.

Do not turn this section into a full SOLID lesson.

[Back to Table of Contents](#table-of-contents)

---

<a id="coupling-and-cohesion"></a>

## Coupling and Cohesion

### Coupling

How strongly components depend on each other.

Usually:

```text
Lower coupling
→ easier change / testing / replacement
```

### Cohesion

How closely related the responsibilities inside one component are.

Usually:

```text
Higher cohesion
→ clearer responsibility
```

### Technical example

A `URLService` that contains:

- URL business rules
- validation
- persistence
- HTTP parsing
- Redis configuration

is doing too many unrelated things.

Separating router → service → repository can improve cohesion and reduce coupling.

### Interview phrase

> “I would try to keep each class focused on a coherent responsibility and avoid making high-level business logic depend directly on infrastructure.”

[Back to Table of Contents](#table-of-contents)

---

<a id="interview-implementation-tasks"></a>

## Interview Implementation Tasks

These are the implementation exercises most worth practicing from the OOP syllabus.

### Very likely categories

1. Create a class with state and methods.
2. Implement encapsulation.
3. Implement inheritance and overriding.
4. Demonstrate runtime polymorphism.
5. Design an abstract payment / notification / shape hierarchy.
6. Use composition instead of inheritance.
7. Implement an interface-like contract.
8. Implement a simple dependency-injected service.
9. Demonstrate operator overloading in Python.
10. Show a class method / static method / alternative constructor.

### Possible follow-up tasks

- Add validation.
- Make the base class abstract.
- Add another implementation without changing the caller.
- Replace inheritance with composition.
- Add a new provider / strategy.
- Make the code testable.
- Handle invalid input.
- Explain how your design changes if requirements expand.

### Interview rule

Start with the **smallest correct implementation**.

Then improve it in stages only when the interviewer asks.

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-implementation--encapsulation"></a>

## Progressive Implementation — Encapsulation

### Level 1 — Public state

```python
class BankAccount:
    def __init__(self, balance):
        self.balance = balance
```

Problem:

> Any caller can assign an invalid value directly.

### Level 2 — Controlled methods

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        # Keep the business rule inside the class.
        if amount <= 0:
            raise ValueError("Amount must be positive")

        self.__balance += amount

    def get_balance(self):
        return self.__balance
```

### Level 3 — Read-only property

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    @property
    def balance(self):
        # Callers can read but not directly write.
        return self.__balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        self.__balance += amount
```

### What to explain

> “I started with exposed state, then moved the invariant into the class, then exposed a read-only interface. The key improvement is controlled mutation, not the double underscore itself.”

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-implementation--abstraction"></a>

## Progressive Implementation — Abstraction

### Level 1 — Concrete code

```python
class StripePayment:
    def pay(self, amount):
        return "Stripe payment"
```

Problem:

> Caller becomes coupled to Stripe.

### Level 2 — Common interface shape

```python
class PaymentProcessor:
    def pay(self, amount):
        raise NotImplementedError
```

### Level 3 — Explicit abstract contract

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):
    @abstractmethod
    def pay(self, amount):
        pass
```

### Level 4 — Multiple implementations

```python
class StripePayment(PaymentProcessor):
    def pay(self, amount):
        return f"Stripe: {amount}"


class UpiPayment(PaymentProcessor):
    def pay(self, amount):
        return f"UPI: {amount}"
```

### Level 5 — Caller depends on the abstraction

```python
def checkout(processor, amount):
    # The caller does not care which payment implementation it received.
    return processor.pay(amount)
```

### Follow-up

> “Can you add PayPal without changing checkout?”

Yes. Add another implementation of the contract.

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-implementation--polymorphism"></a>

## Progressive Implementation — Polymorphism

### Level 1 — Type-based branching

```python
def send_notification(notification_type, message):
    if notification_type == "email":
        return f"Email: {message}"

    if notification_type == "sms":
        return f"SMS: {message}"

    raise ValueError("Unsupported type")
```

Problem:

- Branches grow.
- Caller knows concrete types.
- Adding a new channel changes the central function.

### Level 2 — Common method

```python
class EmailNotification:
    def send(self, message):
        return f"Email: {message}"


class SMSNotification:
    def send(self, message):
        return f"SMS: {message}"
```

### Level 3 — Polymorphic caller

```python
def send_notification(notification, message):
    # The caller depends on the operation, not the concrete type.
    return notification.send(message)
```

### Interview explanation

> “I removed type-based branching and moved the variable behavior into the objects that own it. This makes the caller closed to those concrete implementation details.”

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-implementation--inheritance-and-overriding"></a>

## Progressive Implementation — Inheritance and Overriding

### Level 1 — Base behavior

```python
class Notification:
    def send(self):
        return "Sending notification"
```

### Level 2 — Specialized behavior

```python
class EmailNotification(Notification):
    def send(self):
        return "Sending email"
```

### Level 3 — Parent + child behavior

```python
class EmailNotification(Notification):
    def send(self):
        base_message = super().send()
        return base_message + " via email"
```

### Interview point

Explain that overriding is useful when the child genuinely specializes the parent behavior.

Do not use inheritance only to reuse a few lines of code.

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-implementation--composition"></a>

## Progressive Implementation — Composition

### Level 1 — Hard-coded dependency

```python
class Car:
    def __init__(self):
        self.engine = PetrolEngine()
```

Problem:

> Hard to replace or test the engine implementation.

### Level 2 — Inject dependency

```python
class Car:
    def __init__(self, engine):
        self.engine = engine

    def start(self):
        return self.engine.start()
```

### Level 3 — Multiple engines

```python
class PetrolEngine:
    def start(self):
        return "Petrol engine started"


class ElectricEngine:
    def start(self):
        return "Electric engine started"


class Car:
    def __init__(self, engine):
        self.engine = engine

    def start(self):
        return self.engine.start()
```

The `Car` object does not change when the engine changes.

### Interview phrase

> “The car depends on an engine abstraction/behavior rather than constructing a specific engine internally. That improves substitution and testability.”

[Back to Table of Contents](#table-of-contents)

---

<a id="progressive-implementation--interface-based-design"></a>

## Progressive Implementation — Interface-Based Design

### Level 1 — Concrete provider

```python
class PexelsProvider:
    def search(self, query):
        return ["pexels-result"]
```

### Level 2 — Another provider

```python
class PixabayProvider:
    def search(self, query):
        return ["pixabay-result"]
```

### Level 3 — Service receives a provider

```python
class AssetSearchService:
    def __init__(self, provider):
        self.provider = provider

    def search(self, query):
        return self.provider.search(query)
```

### Level 4 — Protocol contract

```python
from typing import Protocol


class AssetProvider(Protocol):
    def search(self, query: str) -> list[str]:
        ...


class AssetSearchService:
    def __init__(self, provider: AssetProvider):
        self.provider = provider

    def search(self, query: str):
        return self.provider.search(query)
```

### Interview follow-up

> “How would you test the service without calling the real image API?”

Inject a fake provider:

```python
class FakeProvider:
    def search(self, query):
        return ["fake-result"]
```

Then:

```python
service = AssetSearchService(FakeProvider())
```

This demonstrates abstraction, polymorphism, composition, dependency injection, and testability in one small example.

[Back to Table of Contents](#table-of-contents)

---

<a id="project-based-oop-examples"></a>

## Project-Based OOP Examples

### SceneFlow — provider abstraction

The most valuable OOP example in your own project is the **asset-provider boundary**.

Conceptually:

```text
Scene search service
        ↓
SearchProvider contract
   ↙       ↓        ↘
Pexels  Pixabay  Openverse
```

Interview discussion:

- Why not hard-code every provider in one service?
- How does polymorphism help?
- How would you add a new provider?
- How would you test it?
- Why is composition useful here?
- What happens when a provider API fails?

### URL Shortener — service / repository separation

Your URL Shortener has:

```text
Router
  ↓
Service
  ↓
Repository
  ↓
Database
```

OOP discussion:

- Router handles HTTP concerns.
- Service handles business rules.
- Repository handles persistence concerns.
- Dependencies can be injected.
- Business logic becomes easier to test independently.

### Important caution

Do not describe a layer as “OOP” merely because it is a Python class.

Explain the **design benefit** the class gives you.

[Back to Table of Contents](#table-of-contents)

---

<a id="likely-follow-up-questions"></a>

## Likely Follow-Up Questions

### Concept comparisons

- Encapsulation vs abstraction?
- Abstraction vs interface?
- Interface vs abstract class?
- Overloading vs overriding?
- Inheritance vs composition?
- Association vs aggregation vs composition?
- Static vs dynamic binding?
- Class method vs static method?
- `is` vs `==`?
- `@staticmethod` vs `@classmethod`?

### Design questions

- Why prefer composition?
- How would you reduce coupling?
- How would you add another implementation?
- How would you test without the real dependency?
- What happens if the requirement changes?
- Where would you put validation?
- How would you make this code extensible?

### Python-specific questions

- What does `self` represent?
- What is `__init__`?
- What is `__new__`?
- What are dunder methods?
- What is name mangling?
- What is MRO?
- What does `super()` actually do?
- What is a mutable class variable?
- What is duck typing?
- What is `Protocol`?
- What is the difference between `NotImplemented` and `NotImplementedError`?
- When is an object hashable?
- What is `__slots__` at a high level?
- What is a property?
- What is a descriptor at a high level?

### Implementation prompts

Be ready to code:

- A bank account with controlled balance mutation.
- A notification system with multiple notification types.
- A payment processor with multiple implementations.
- A shape hierarchy with area calculation.
- A vehicle hierarchy.
- A provider interface with multiple concrete providers.
- A service that accepts a dependency through its constructor.
- A class with custom `__str__`, `__repr__`, and `__eq__`.
- A class method used as an alternative constructor.
- A composition-based design replacing an inheritance hierarchy.

[Back to Table of Contents](#table-of-contents)

---

<a id="keyword-radar"></a>

## Keyword Radar

These are the words that can signal a deeper OOP follow-up.

| Keyword | What you should know |
|---|---|
| `self` | Instance reference passed to instance methods |
| `cls` | Class reference passed to class methods |
| `@classmethod` | Class-level method / alternative constructors |
| `@staticmethod` | Utility method grouped under a class |
| `@property` | Attribute-style access backed by methods |
| `@abstractmethod` | Declares an abstract method in an ABC |
| `ABC` | Base class helper for abstract contracts |
| `Protocol` | Structural interface-style typing |
| `super()` | Delegates according to MRO |
| `__init__` | Object initialization |
| `__new__` | Instance creation hook |
| `__repr__` | Developer-facing representation |
| `__str__` | Human-readable representation |
| `__eq__` | Equality behavior |
| `__hash__` | Hash behavior for hashed collections |
| `__slots__` | Restricts/stabilizes instance attribute layout in some designs |
| `NotImplemented` | Special protocol return value |
| `NotImplementedError` | Exception for intentionally missing implementation |
| MRO | Method Resolution Order |
| Duck typing | Capability-based behavior over explicit type checks |
| Name mangling | Double-underscore attribute transformation |
| Dependency injection | Supplying collaborators from outside |

### What not to do

Do not memorize the keyword table in isolation.

Connect each keyword to an example you can code.

[Back to Table of Contents](#table-of-contents)

---

<a id="common-traps"></a>

## Common Traps

### Trap 1

> Encapsulation = private variables.

Correction: encapsulation is controlled state + invariants + public behavior.

### Trap 2

> Python supports Java-style method overloading.

Correction: Python does not support signature-based method overloading in the usual sense.

### Trap 3

> `__name` is security.

Correction: name mangling is not security.

### Trap 4

> `super()` means immediate parent.

Correction: it follows MRO.

### Trap 5

> Interface means only Java's `interface` keyword.

Correction: Python uses ABCs and Protocols for interface-like contracts.

### Trap 6

> Composition is just inheritance written differently.

Correction: composition changes the dependency relationship: one object owns/uses another object instead of becoming a specialized subtype.

### Trap 7

> Polymorphism always means inheritance.

Correction: Python duck typing can provide polymorphic behavior without explicit inheritance.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-revision-sheet"></a>

## 30-Second Revision Sheet

```text
Class
→ defines a type

Object
→ instance of a class

Encapsulation
→ protect state + enforce rules

Abstraction
→ expose needed behavior, hide implementation

Inheritance
→ specialize / reuse through an IS-A relationship

Polymorphism
→ same operation, different implementation

Overloading
→ multiple call forms; Python uses flexible techniques rather than signature overloading

Overriding
→ child replaces inherited behavior

Dynamic dispatch
→ runtime selects overridden implementation

Composition
→ build objects from other objects

Association
→ objects are related

Aggregation
→ weak whole-part relationship

Composition
→ strong ownership / lifecycle relationship

Interface
→ contract

Abstract class
→ contract + possible shared implementation

MRO
→ Python's method lookup order

super()
→ follow the MRO to delegate behavior

Dependency injection
→ provide collaborators from outside

Coupling
→ degree of dependency

Cohesion
→ how focused a component's responsibilities are

is
→ identity

==
→ equality

__hash__
→ hashed-collection contract
```

[Back to Table of Contents](#table-of-contents)

---

<a id="final-oop-interview-checklist"></a>

## Final OOP Interview Checklist

### Concepts

- [ ] Class / object
- [ ] Constructor / `__init__` / `__new__`
- [ ] Encapsulation
- [ ] Abstraction
- [ ] Inheritance
- [ ] Polymorphism
- [ ] Overloading
- [ ] Overriding
- [ ] Dynamic dispatch
- [ ] Static / dynamic binding
- [ ] Interface / abstract class / Protocol
- [ ] Composition
- [ ] Association / aggregation / composition
- [ ] IS-A / HAS-A
- [ ] Coupling / cohesion

### Python

- [ ] `self` / `cls`
- [ ] `@property`
- [ ] `@classmethod`
- [ ] `@staticmethod`
- [ ] Dunder methods
- [ ] `super()`
- [ ] MRO
- [ ] Name mangling
- [ ] Duck typing
- [ ] `__eq__` / `__hash__`
- [ ] `Protocol`
- [ ] `ABC`

### Implementation

- [ ] Encapsulated class
- [ ] Abstract base class
- [ ] Multiple implementations
- [ ] Runtime polymorphism
- [ ] Overriding
- [ ] Composition
- [ ] Dependency injection
- [ ] Operator overloading
- [ ] Class method / static method

### Interview behavior

- [ ] Explain before coding
- [ ] Start with the smallest correct implementation
- [ ] State why each class exists
- [ ] Explain trade-offs
- [ ] Add complexity only when asked
- [ ] Handle a follow-up variation
- [ ] Connect at least two examples to your own projects
- [ ] Never bluff an implementation detail

[Back to Table of Contents](#table-of-contents)
