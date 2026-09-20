# Core Python Interview Notes — Infosys DSE / SP

Dedicated Core Python interview reference covering Python execution, CPython internals, objects and memory, collections, functions, closures, iterators, generators, decorators, descriptors, exceptions, imports, garbage collection, GIL, threading, multiprocessing, asyncio, performance, practical implementations, and Infosys-focused interview questions.

> **Depth target:** definition → mechanism → internal model → implementation → trade-off → follow-up.

> **Important:** distinguish Python language semantics from CPython implementation details, because some internals vary by implementation and Python version.

<a id="table-of-contents"></a>

## Table of Contents

### 1. Execution and Internals
- [How to Use These Notes](#how-to-use-these-notes)
- [What Python Actually Is](#what-python-actually-is)
- [CPython vs Python the Language](#cpython-vs-python-the-language)
- [How Python Code Runs](#how-python-code-runs)
- [Source Code to Bytecode](#source-code-to-bytecode)
- [Python Virtual Machine Mental Model](#python-virtual-machine-mental-model)
- [Disassembly with dis](#disassembly-with-dis)
- [How a Function Call Works](#how-a-function-call-works)
- [Why Python Is Called Interpreted](#why-python-is-called-interpreted)
- [Import-Time Execution](#import-time-execution)

### 2. Objects, Types and Memory
- [Names vs Objects](#names-vs-objects)
- [Identity Equality and is vs ==](#identity-equality-and-is-vs)
- [Mutability and Immutability](#mutability-and-immutability)
- [Pass-by-Object-Reference](#pass-by-object-reference)
- [Stack vs Heap in Python](#stack-vs-heap-in-python)
- [Reference Counting](#reference-counting)
- [Python Objects at the C Level](#python-objects-at-the-c-level)
- [Interning and Small Integers](#interning-and-small-integers)
- [Garbage Collection](#garbage-collection)
- [Cyclic References](#cyclic-references)
- [gc Module](#gc-module)
- [Object Lifetime and Resource Cleanup](#object-lifetime-and-resource-cleanup)

### 3. Built-in Collections
- [List Internals](#list-internals)
- [Tuple Internals](#tuple-internals)
- [Dictionary Internals](#dictionary-internals)
- [Set Internals](#set-internals)
- [String Internals](#string-internals)
- [Deque](#deque)
- [Heapq](#heapq)
- [Collection Complexity](#collection-complexity)
- [Why List Append Is Amortized O1](#why-list-append-is-amortized-o1)
- [Why Dict Lookup Is Usually O1](#why-dict-lookup-is-usually-o1)
- [Hashability](#hashability)
- [Eq and Hash Contract](#eq-and-hash-contract)

### 4. Functions, Scope and Closures
- [First-Class Functions](#first-class-functions)
- [Function Objects](#function-objects)
- [Argument Passing](#argument-passing)
- [args and kwargs](#args-and-kwargs)
- [Mutable Default Argument Trap](#mutable-default-argument-trap)
- [LEGB](#legb)
- [global and nonlocal](#global-and-nonlocal)
- [Closures](#closures)
- [Late Binding](#late-binding)
- [Lambda](#lambda)
- [Higher-Order Functions](#higher-order-functions)

### 5. Iterators and Generators
- [Iterable vs Iterator](#iterable-vs-iterator)
- [Iterator Protocol](#iterator-protocol)
- [for Loop Internals](#for-loop-internals)
- [iter and next](#iter-and-next)
- [Generator Functions](#generator-functions)
- [yield and Generator State](#yield-and-generator-state)
- [Generator Expressions](#generator-expressions)
- [Generator vs List](#generator-vs-list)
- [send throw and close](#send-throw-and-close)
- [Custom Iterator Implementation](#custom-iterator-implementation)

### 6. Decorators and Descriptors
- [What a Decorator Is](#what-a-decorator-is)
- [Decorator Execution Model](#decorator-execution-model)
- [Function Decorator Implementation](#function-decorator-implementation)
- [Parameterized Decorators](#parameterized-decorators)
- [functools.wraps](#functoolswraps)
- [Class Decorators](#class-decorators)
- [Descriptor Protocol](#descriptor-protocol)
- [get set and delete](#get-set-and-delete)
- [property as a Descriptor](#property-as-a-descriptor)
- [Method Binding](#method-binding)
- [Decorator vs Descriptor](#decorator-vs-descriptor)

### 7. Python Data Model
- [Everything Is an Object](#everything-is-an-object)
- [type and object](#type-and-object)
- [dict](#dict)
- [slots](#slots)
- [Attribute Lookup](#attribute-lookup)
- [getattr vs getattribute](#getattr-vs-getattribute)
- [new vs init](#new-vs-init)
- [str vs repr](#str-vs-repr)
- [Special Method Protocols](#special-method-protocols)
- [Operator Overloading](#operator-overloading)
- [NotImplemented vs NotImplementedError](#notimplemented-vs-notimplementederror)
- [MRO](#mro)
- [super](#super)

### 8. Exceptions and Context Managers
- [Exception Hierarchy](#exception-hierarchy)
- [try except else finally](#try-except-else-finally)
- [raise and Exception Chaining](#raise-and-exception-chaining)
- [Custom Exceptions](#custom-exceptions)
- [Context Managers](#context-managers)
- [with Statement](#with-statement)
- [contextlib](#contextlib)
- [Resource Safety](#resource-safety)

### 9. Modules and Imports
- [Module vs Package](#module-vs-package)
- [How import Works](#how-import-works)
- [sys.modules](#sysmodules)
- [Import Caching](#import-caching)
- [name main](#name-main)
- [Circular Imports](#circular-imports)
- [Virtual Environments](#virtual-environments)
- [pip and Packaging Basics](#pip-and-packaging-basics)

### 10. Copying and Serialization
- [Shallow vs Deep Copy](#shallow-vs-deep-copy)
- [copy Module](#copy-module)
- [Serialization](#serialization)
- [pickle](#pickle)
- [JSON vs Pickle](#json-vs-pickle)

### 11. Threading and Concurrency
- [Process vs Thread](#process-vs-thread)
- [Concurrency vs Parallelism](#concurrency-vs-parallelism)
- [GIL](#gil)
- [Modern GIL Changes](#modern-gil-changes)
- [Why I/O-Bound Threading Helps](#why-io-bound-threading-helps)
- [Why CPU-Bound Threading Differs](#why-cpu-bound-threading-differs)
- [Thread Lifecycle](#thread-lifecycle)
- [threading Module](#threading-module)
- [Race Conditions](#race-conditions)
- [Lock](#lock)
- [RLock](#rlock)
- [Semaphore](#semaphore)
- [Event](#event)
- [Condition](#condition)
- [Barrier](#barrier)
- [Thread-Safe Design](#thread-safe-design)
- [Deadlocks](#deadlocks)
- [Deadlock Prevention](#deadlock-prevention)
- [ThreadPoolExecutor](#threadpoolexecutor)
- [Threading Drills](#threading-drills)

### 12. Multiprocessing
- [Why Multiprocessing](#why-multiprocessing)
- [Process Creation](#process-creation)
- [multiprocessing Module](#multiprocessing-module)
- [Process Isolation](#process-isolation)
- [IPC](#ipc)
- [Queue and Pipe](#queue-and-pipe)
- [Shared Memory](#shared-memory)
- [ProcessPoolExecutor](#processpoolexecutor)
- [Multiprocessing Trade-Offs](#multiprocessing-trade-offs)

### 13. Async Python
- [Synchronous vs Asynchronous](#synchronous-vs-asynchronous)
- [async def and await](#async-def-and-await)
- [Coroutine Objects](#coroutine-objects)
- [Event Loop](#event-loop)
- [Tasks](#tasks)
- [asyncio.gather](#asynciogather)
- [Async I/O Mental Model](#async-io-mental-model)
- [Async vs Threads](#async-vs-threads)
- [Async vs Multiprocessing](#async-vs-multiprocessing)
- [Common Async Mistakes](#common-async-mistakes)
- [Simple Async Implementation](#simple-async-implementation)

### 14. Performance
- [Big O vs Runtime Constants](#big-o-vs-runtime-constants)
- [timeit](#timeit)
- [cProfile](#cprofile)
- [tracemalloc](#tracemalloc)
- [Generators for Memory Efficiency](#generators-for-memory-efficiency)
- [String join](#string-join)
- [Avoiding Unnecessary Copies](#avoiding-unnecessary-copies)
- [Native Code and Vectorization](#native-code-and-vectorization)
- [Why Python Can Be Slower](#why-python-can-be-slower)

### 15. Standard Library Radar
- [collections](#collections)
- [itertools](#itertools)
- [functools](#functools)
- [heapq Module](#heapq-module)
- [bisect](#bisect)
- [dataclasses](#dataclasses)
- [typing](#typing)
- [enum](#enum)
- [pathlib](#pathlib)

### 16. Practical Implementations
- [Custom Iterator](#custom-iterator)
- [Generator](#generator)
- [Timing Decorator](#timing-decorator)
- [Retry Decorator](#retry-decorator)
- [Context Manager](#context-manager)
- [LRU Cache Concept](#lru-cache-concept)
- [Thread Pool Downloader Pattern](#thread-pool-downloader-pattern)
- [Producer Consumer Queue](#producer-consumer-queue)
- [Thread Safe Counter](#thread-safe-counter)
- [Multiprocessing Pool](#multiprocessing-pool)
- [Async Concurrent Tasks](#async-concurrent-tasks)

### 17. Infosys SP/DSE Python Questions
- [High-Frequency Questions](#high-frequency-questions)
- [Python Internals Questions](#python-internals-questions)
- [Collections Questions](#collections-questions)
- [Functions and Decorators Questions](#functions-and-decorators-questions)
- [Iterator and Generator Questions](#iterator-and-generator-questions)
- [Concurrency Questions](#concurrency-questions)
- [Memory and GC Questions](#memory-and-gc-questions)
- [Exception and Import Questions](#exception-and-import-questions)
- [Project-Driven Questions](#project-driven-questions)
- [Explain Why Drill](#explain-why-drill)

### 18. Common Python Traps
- [Mutable Default Arguments](#mutable-default-arguments)
- [Late Binding Trap](#late-binding-trap)
- [is vs == Trap](#is-vs-equal-trap)
- [Nested List Multiplication](#nested-list-multiplication)
- [Shallow Copy Trap](#shallow-copy-trap)
- [Generator Exhaustion](#generator-exhaustion)
- [Global Mutable State](#global-mutable-state)
- [Thread Shared State](#thread-shared-state)
- [Blocking in Async Code](#blocking-in-async-code)

### 19. Final Revision
- [30-Second Python Mental Model](#30-second-python-mental-model)
- [Python Keyword Radar](#python-keyword-radar)
- [Implementation Checklist](#implementation-checklist)
- [Final Python Interview Checklist](#final-python-interview-checklist)

---

<a id="how-to-use-these-notes"></a>

## How to Use These Notes

For every important concept:

```text
Definition
↓
Example
↓
Internal mechanism
↓
Implementation
↓
Trade-off / failure mode
↓
Follow-up question
```

For internals, always say **“In CPython…”** when the fact depends on the implementation.

[Back to Table of Contents](#table-of-contents)

---

<a id="what-python-actually-is"></a>

## What Python Actually Is

Python is the language. **CPython** is the dominant implementation.

```text
Python language
→ syntax + semantics + protocols

CPython
→ runtime + interpreter machinery + C implementation
```

This distinction prevents overclaiming implementation details as universal Python behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="cpython-vs-python-the-language"></a>

## CPython vs Python the Language

Language-level concepts include:

- functions
- classes
- iterators
- generators
- exceptions
- context managers
- data-model protocols

CPython decides how these are implemented internally.

[Back to Table of Contents](#table-of-contents)

---

<a id="how-python-code-runs"></a>

## How Python Code Runs

A useful CPython mental model is:

```text
.py source
↓
parse / compile
↓
code object
↓
bytecode
↓
CPython runtime execution
↓
Python objects / native operations
↓
OS / hardware
```

### Interview answer

> “CPython parses and compiles source into code objects containing bytecode and metadata, and its runtime executes that representation.”

The exact execution machinery evolves, so prefer this stable model over memorizing one version's opcode loop.

[Back to Table of Contents](#table-of-contents)

---

<a id="source-code-to-bytecode"></a>

## Source Code to Bytecode

Example:

```python
import dis

def add():
    x = 10
    return x + 5

dis.dis(add)
```

`dis` shows CPython bytecode-level instructions. The exact opcodes can change between Python versions.

[Back to Table of Contents](#table-of-contents)

---

<a id="python-virtual-machine-mental-model"></a>

## Python Virtual Machine Mental Model

Think:

```text
Code object
↓
Instruction stream
↓
Interpreter / evaluation machinery
↓
Python objects
```

This is a language runtime model, not a hardware VM.

[Back to Table of Contents](#table-of-contents)

---

<a id="disassembly-with-dis"></a>

## Disassembly with dis

Use `dis` when an interviewer asks what Python executes internally:

```python
import dis

def square(x):
    return x * x

dis.dis(square)
```

Know that bytecode is an implementation detail, not a permanent language-level contract.

[Back to Table of Contents](#table-of-contents)

---

<a id="how-a-function-call-works"></a>

## How a Function Call Works

For:

```python
def add(a, b):
    return a + b

result = add(2, 3)
```

Conceptually:

```text
function object exists
↓
call creates execution state/frame
↓
arguments become local bindings
↓
function body executes
↓
a + b uses Python's object protocols
↓
return value goes to caller
```

The exact frame representation is CPython-version-specific.

[Back to Table of Contents](#table-of-contents)

---

<a id="why-python-is-called-interpreted"></a>

## Why Python Is Called Interpreted

“Python is interpreted” is shorthand, not a complete technical description.

CPython does compilation first:

```text
source
→ code object / bytecode
→ runtime execution
```

So a strong answer is:

> “CPython compiles source into an intermediate code representation, then its runtime executes that representation.”

[Back to Table of Contents](#table-of-contents)

---

<a id="import-time-execution"></a>

## Import-Time Execution

Importing a module can execute its module-level code.

Typical flow:

```text
find module
↓
load / compile if needed
↓
execute module-level code
↓
create module object
↓
cache in sys.modules
```

This is why expensive side effects should not casually live at module top level.

[Back to Table of Contents](#table-of-contents)

---

<a id="names-vs-objects"></a>

## Names vs Objects

Python variables are names bound to objects.

```python
a = [1, 2]
b = a
```

Mental model:

```text
a ─┐
   ├──> [1, 2]
b ─┘
```

Therefore:

```python
b.append(3)
```

changes the same list visible through `a`.

[Back to Table of Contents](#table-of-contents)

---

<a id="identity-equality-and-is-vs"></a>

## Identity Equality and is vs ==

`==` asks whether values compare equal.

`is` asks whether two references point to the same object.

```python
x = [1, 2]
y = [1, 2]
z = x

print(x == y)  # True
print(x is y)  # False
print(x is z)  # True
```

Use `is` for singleton identity checks such as `value is None`.

[Back to Table of Contents](#table-of-contents)

---

<a id="mutability-and-immutability"></a>

## Mutability and Immutability

Mutable examples:

```text
list, dict, set
```

Immutable examples:

```text
int, float, str, tuple structure
```

A tuple can still contain a mutable object:

```python
x = ([1, 2], 3)
x[0].append(4)
```

The tuple's slots did not change, but the nested list did.

[Back to Table of Contents](#table-of-contents)

---

<a id="pass-by-object-reference"></a>

## Pass-by-Object-Reference

The clearest description is **call-by-sharing**.

```python
def mutate(items):
    items.append(4)

def rebind(items):
    items = [99]
```

The first can mutate the caller-visible list. The second only changes the function's local binding.

Interview line:

> “Python passes object references by value: the parameter is a new local binding pointing to the same object.”

[Back to Table of Contents](#table-of-contents)

---

<a id="stack-vs-heap-in-python"></a>

## Stack vs Heap in Python

Avoid the oversimplified C/C++ statement “variables live on the stack and objects live on the heap.”

At interview level:

- Python objects are managed in a runtime heap in CPython.
- Function execution has frames/call state.
- Local names refer to objects rather than embedding the objects themselves.

Exact frame/allocation implementation is CPython-specific.

[Back to Table of Contents](#table-of-contents)

---

<a id="reference-counting"></a>

## Reference Counting

CPython uses reference counting as a core memory-management mechanism.

Conceptually:

```text
object
↓
number of active references changes
↓
when reference count reaches zero, object can usually be deallocated immediately
```

Example:

```python
x = []
y = x
del x
```

The object remains because `y` still references it.

Reference counting alone cannot collect reference cycles, which is why CPython also has cyclic GC. citeturn514941search10

[Back to Table of Contents](#table-of-contents)

---

<a id="python-objects-at-the-c-level"></a>

## Python Objects at the C Level

A useful CPython mental model is:

```text
Python object
├── runtime metadata
├── reference-management information
└── type-specific payload
```

Do not claim every object has one identical C structure; different object types have different layouts.

[Back to Table of Contents](#table-of-contents)

---

<a id="interning-and-small-integers"></a>

## Interning and Small Integers

CPython can reuse some immutable objects, such as commonly used small integers and interned strings.

This is an implementation optimization, not the definition of identity.

Therefore:

```text
== → equality
is → identity
```

Use `is` for `None`, not for numeric value comparison.

[Back to Table of Contents](#table-of-contents)

---

<a id="garbage-collection"></a>

## Garbage Collection

In CPython, think:

```text
reference counting
        +
cyclic garbage collector
        ↓
memory reclamation
```

Reference counting handles many objects immediately.

The cyclic collector deals with unreachable reference cycles.

This is why “Python has garbage collection” is true but incomplete.

[Back to Table of Contents](#table-of-contents)

---

<a id="cyclic-references"></a>

## Cyclic References

Example:

```python
a = []
b = [a]
a.append(b)
```

The two lists reference one another. External references can disappear while internal cycle references remain, so reference counting alone cannot reclaim them.

The cyclic collector can detect collectable cycles.

[Back to Table of Contents](#table-of-contents)

---

<a id="gc-module"></a>

## gc Module

```python
import gc

print(gc.isenabled())
gc.collect()
```

`gc.collect()` requests a garbage-collection cycle. It does not mean that every object in memory disappears immediately; still-referenced objects remain alive.

[Back to Table of Contents](#table-of-contents)

---

<a id="object-lifetime-and-resource-cleanup"></a>

## Object Lifetime and Resource Cleanup

Do not depend on garbage collection timing for external resources.

Use deterministic cleanup for:

- files
- sockets
- database connections
- locks

Context managers are usually the cleanest pattern.

[Back to Table of Contents](#table-of-contents)

---

<a id="list-internals"></a>

## List Internals

CPython lists behave like dynamic arrays of references.

```text
[ref][ref][ref][ref]...
```

When capacity is exhausted, the backing storage grows and references are copied.

Therefore:

- `append()` is amortized O(1)
- `insert(0, x)` is O(n)
- middle insertion/deletion is O(n)
- indexing is O(1)

Use `deque` for efficient two-ended queue behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="tuple-internals"></a>

## Tuple Internals

Tuple is an immutable sequence.

Advantages over a list when structure is fixed:

- cannot be structurally modified
- can be used as a dict key when all contents are hashable
- can communicate immutability intent

Do not say tuples are universally faster for every operation.

[Back to Table of Contents](#table-of-contents)

---

<a id="dictionary-internals"></a>

## Dictionary Internals

A dict is hash-table based.

Conceptually:

```text
key
↓
hash(key)
↓
candidate location
↓
key comparison if needed
↓
value
```

Average lookup is approximately O(1) under normal hashing assumptions.

The exact storage/probing implementation has evolved across CPython versions.

[Back to Table of Contents](#table-of-contents)

---

<a id="set-internals"></a>

## Set Internals

Sets are also hash-table based and store unique hashable values.

```python
seen = {1, 2, 3}
print(3 in seen)
```

Average membership is approximately O(1).

[Back to Table of Contents](#table-of-contents)

---

<a id="string-internals"></a>

## String Internals

Python strings are immutable Unicode objects.

This:

```python
s = s + "x"
```

creates a new string object conceptually rather than changing the existing one in place.

For many fragments, prefer:

```python
"".join(parts)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="deque"></a>

## Deque

`collections.deque` is designed for efficient append/pop from both ends.

```python
from collections import deque

q = deque([1, 2, 3])
q.appendleft(0)
q.append(4)
q.popleft()
```

Common use: BFS queues, buffers, sliding windows.

[Back to Table of Contents](#table-of-contents)

---

<a id="heapq"></a>

## Heapq

`heapq` provides a min-heap.

Know:

- `heappush`
- `heappop`
- `heapify`
- `nlargest`
- `nsmallest`

Common use: priority queues and scheduling.

[Back to Table of Contents](#table-of-contents)

---

<a id="collection-complexity"></a>

## Collection Complexity

| Operation | List | Dict | Set | Deque |
|---|---:|---:|---:|---:|
| Index access | O(1) | — | — | O(1) at ends |
| Append right | Amortized O(1) | — | — | O(1) |
| Pop right | O(1) | — | — | O(1) |
| Insert left | O(n) | — | — | O(1) |
| Membership | O(n) | Avg O(1) | Avg O(1) | O(n) |

These are typical/average complexity statements, not universal worst-case guarantees.

[Back to Table of Contents](#table-of-contents)

---

<a id="why-list-append-is-amortized-o1"></a>

## Why List Append Is Amortized O(1)

Most appends use already allocated capacity.

Occasionally the list grows and references are copied.

```text
many cheap appends
+
occasional expensive resize
↓
amortized O(1)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="why-dict-lookup-is-usually-o1"></a>

## Why Dict Lookup Is Usually O(1)

Hashing narrows the search to candidate storage locations instead of scanning every key.

Then equality is used to confirm the key when needed.

[Back to Table of Contents](#table-of-contents)

---

<a id="hashability"></a>

## Hashability

A hashable object has a stable hash for its lifetime and equality semantics compatible with that hash.

Hashable objects can be used as:

- dict keys
- set members

A mutable list is not hashable because its contents can change.

[Back to Table of Contents](#table-of-contents)

---

<a id="eq-and-hash-contract"></a>

## Eq and Hash Contract

If:

```python
a == b
```

then, for hashable objects participating in hashed collections:

```python
hash(a) == hash(b)
```

Design custom `__eq__` and `__hash__` together.

[Back to Table of Contents](#table-of-contents)

---

<a id="first-class-functions"></a>

## First-Class Functions

Functions are objects and can be:

- assigned
- passed
- returned
- stored

```python
def greet(name):
    return f"Hi {name}"

fn = greet
print(fn("Sai"))
```

This enables callbacks, decorators, and higher-order functions.

[Back to Table of Contents](#table-of-contents)

---

<a id="function-objects"></a>

## Function Objects

Useful function-object attributes include:

- `__name__`
- `__doc__`
- `__defaults__`
- `__annotations__`

These support introspection and tooling.

[Back to Table of Contents](#table-of-contents)

---

<a id="argument-passing"></a>

## Argument Passing

Python supports positional-only, positional-or-keyword, and keyword-only parameters.

```python
def connect(host, /, port=5432, *, timeout=5):
    ...
```

Knowing these modes helps with API design questions.

[Back to Table of Contents](#table-of-contents)

---

<a id="args-and-kwargs"></a>

## args and kwargs

```python
def f(*args, **kwargs):
    print(args)
    print(kwargs)
```

`args` collects extra positional arguments as a tuple; `kwargs` collects extra keyword arguments as a dictionary.

Common use: wrappers and decorators.

[Back to Table of Contents](#table-of-contents)

---

<a id="mutable-default-argument-trap"></a>

## Mutable Default Argument Trap

Bad:

```python
def add_item(item, items=[]):
    items.append(item)
    return items
```

The default list is created once when the function is defined.

Better:

```python
def add_item(item, items=None):
    if items is None:
        items = []
    items.append(item)
    return items
```

[Back to Table of Contents](#table-of-contents)

---

<a id="legb"></a>

## LEGB

Python name lookup is commonly explained as:

```text
Local → Enclosing → Global → Built-in
```

Understand this together with `global` and `nonlocal`.

[Back to Table of Contents](#table-of-contents)

---

<a id="global-and-nonlocal"></a>

## global and nonlocal

`global` rebinds a module-level name.

`nonlocal` rebinds a name in an enclosing function scope.

```python
def counter():
    count = 0
    def inc():
        nonlocal count
        count += 1
        return count
    return inc
```

[Back to Table of Contents](#table-of-contents)

---

<a id="closures"></a>

## Closures

A closure is a function retaining access to variables from an enclosing scope after the outer function returns.

```python
def make_multiplier(n):
    def multiply(x):
        return x * n
    return multiply

f = make_multiplier(2)
print(f(5))
```

[Back to Table of Contents](#table-of-contents)

---

<a id="late-binding"></a>

## Late Binding

Trap:

```python
funcs = []
for i in range(3):
    funcs.append(lambda: i)
```

The lambdas resolve `i` later and therefore observe the final value.

Fix:

```python
funcs = []
for i in range(3):
    funcs.append(lambda i=i: i)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="lambda"></a>

## Lambda

Lambda creates a small anonymous function:

```python
square = lambda x: x * x
```

Use it for short expressions rather than complex logic.

[Back to Table of Contents](#table-of-contents)

---

<a id="higher-order-functions"></a>

## Higher-Order Functions

A higher-order function accepts or returns another function.

Examples:

- `sorted(key=...)`
- `map`
- `filter`
- decorators
- callbacks

[Back to Table of Contents](#table-of-contents)

---

<a id="iterable-vs-iterator"></a>

## Iterable vs Iterator

Iterable:

> can produce an iterator.

Iterator:

> follows the iterator protocol and produces the next item on demand.

```python
items = [1, 2, 3]
it = iter(items)
```

Mental model:

```text
Iterable
↓ iter()
Iterator
↓ next()
Value
```

[Back to Table of Contents](#table-of-contents)

---

<a id="iterator-protocol"></a>

## Iterator Protocol

An iterator implements:

```python
__iter__()
__next__()
```

and raises `StopIteration` when exhausted.

[Back to Table of Contents](#table-of-contents)

---

<a id="for-loop-internals"></a>

## for Loop Internals

Conceptually:

```python
it = iter(iterable)
while True:
    try:
        item = next(it)
    except StopIteration:
        break
    # loop body
```

Exact CPython bytecode differs by version.

[Back to Table of Contents](#table-of-contents)

---

<a id="iter-and-next"></a>

## iter and next

```python
it = iter([10, 20])
print(next(it))
print(next(it))
```

The next call after exhaustion raises `StopIteration`.

[Back to Table of Contents](#table-of-contents)

---

<a id="generator-functions"></a>

## Generator Functions

A function containing `yield` is a generator function.

Calling it creates a generator object; execution proceeds when it is advanced.

```python
def numbers():
    yield 1
    yield 2
```

[Back to Table of Contents](#table-of-contents)

---

<a id="yield-and-generator-state"></a>

## yield and Generator State

At `yield`:

```text
produce value
↓
pause execution
↓
preserve local/control state
↓
resume later
```

This is the basis of lazy iteration.

[Back to Table of Contents](#table-of-contents)

---

<a id="generator-expressions"></a>

## Generator Expressions

```python
squares = (x * x for x in range(10))
```

The values are produced lazily.

[Back to Table of Contents](#table-of-contents)

---

<a id="generator-vs-list"></a>

## Generator vs List

List:

- full materialization
- random access
- reusable iteration

Generator:

- lazy
- one-shot
- low memory for streaming workloads

[Back to Table of Contents](#table-of-contents)

---

<a id="send-throw-and-close"></a>

## send throw and close

Advanced generator methods:

- `send(value)`
- `throw(exception)`
- `close()`

Know their existence and purpose. Detailed coroutine-style generator control is lower priority than basic `yield` mechanics for Infosys.

[Back to Table of Contents](#table-of-contents)

---

<a id="custom-iterator-implementation"></a>

## Custom Iterator Implementation

```python
class CountUp:
    def __init__(self, limit):
        self.current = 0
        self.limit = limit

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.limit:
            raise StopIteration
        self.current += 1
        return self.current
```

Interview line:

> “The iterator stores its traversal state and raises `StopIteration` when exhausted.”

[Back to Table of Contents](#table-of-contents)

---

<a id="what-a-decorator-is"></a>

## What a Decorator Is

A decorator transforms or wraps a callable/class.

```python
def decorator(fn):
    def wrapper(*args, **kwargs):
        print("before")
        result = fn(*args, **kwargs)
        print("after")
        return result
    return wrapper
```

Using:

```python
@decorator
def greet():
    print("hello")
```

is approximately:

```python
greet = decorator(greet)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="decorator-execution-model"></a>

## Decorator Execution Model

Decoration happens when the `def` statement is executed, not on every call.

```text
def function created
↓
decorator(function)
↓
returned callable assigned to function name
```

The wrapper runs each time the decorated function is called.

[Back to Table of Contents](#table-of-contents)

---

<a id="function-decorator-implementation"></a>

## Function Decorator Implementation

```python
from functools import wraps
from time import perf_counter

def timed(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        start = perf_counter()
        try:
            return fn(*args, **kwargs)
        finally:
            print(f"{fn.__name__}: {perf_counter() - start:.6f}s")
    return wrapper
```

This demonstrates closure, wrapping, arbitrary arguments, metadata preservation, and cleanup-style timing.

[Back to Table of Contents](#table-of-contents)

---

<a id="parameterized-decorators"></a>

## Parameterized Decorators

```python
def retry(times):
    def decorator(fn):
        def wrapper(*args, **kwargs):
            ...
        return wrapper
    return decorator
```

Usage:

```python
@retry(3)
def call_api():
    ...
```

Mental structure:

```text
retry(3)
↓
decorator
↓
wrapper
```

[Back to Table of Contents](#table-of-contents)

---

<a id="functoolswraps"></a>

## functools.wraps

`functools.wraps` copies useful metadata from the wrapped function onto the wrapper and improves introspection/debugging.

Use it in production-quality decorators.

[Back to Table of Contents](#table-of-contents)

---

<a id="class-decorators"></a>

## Class Decorators

A decorator can receive and return a class:

```python
def add_flag(cls):
    cls.enabled = True
    return cls
```

Usage:

```python
@add_flag
class Service:
    pass
```

[Back to Table of Contents](#table-of-contents)

---

<a id="descriptor-protocol"></a>

## Descriptor Protocol

A descriptor controls attribute access through methods such as:

```text
__get__
__set__
__delete__
```

Descriptors are the mechanism behind important Python features including `property` and bound-method behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="get-set-and-delete"></a>

## get set and delete

Minimal descriptor:

```python
class Positive:
    def __set_name__(self, owner, name):
        self.name = name

    def __get__(self, instance, owner=None):
        if instance is None:
            return self
        return instance.__dict__[self.name]

    def __set__(self, instance, value):
        if value <= 0:
            raise ValueError("must be positive")
        instance.__dict__[self.name] = value
```

This lets the class control assignment to an attribute.

[Back to Table of Contents](#table-of-contents)

---

<a id="property-as-a-descriptor"></a>

## property as a Descriptor

`property` is an example of a descriptor.

```python
class User:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name
```

The `property` object lives on the class and controls access to `name`.

[Back to Table of Contents](#table-of-contents)

---

<a id="method-binding"></a>

## Method Binding

Functions defined on a class participate in descriptor behavior.

When you access:

```python
obj.method
```

the function is bound to the instance, producing behavior conceptually equivalent to supplying `self`.

This is why:

```python
obj.method()
```

passes the instance automatically.

[Back to Table of Contents](#table-of-contents)

---

<a id="decorator-vs-descriptor"></a>

## Decorator vs Descriptor

Decorator:

> transforms/wraps a callable or class.

Descriptor:

> controls attribute access when stored on a class.

Frameworks often use both, but they solve different problems.

[Back to Table of Contents](#table-of-contents)

---

<a id="everything-is-an-object"></a>

## Everything Is an Object

Python treats values such as integers, strings, functions, classes, and modules as objects.

```python
def greet():
    pass

print(type(greet))
print(type(int))
```

Classes themselves are objects too.

[Back to Table of Contents](#table-of-contents)

---

<a id="type-and-object"></a>

## type and object

At high level, classes are objects created by metaclasses; `type` is the normal metaclass for ordinary classes.

This leads into metaclasses, but metaclasses are lower priority than ordinary object-model questions for this interview target.

[Back to Table of Contents](#table-of-contents)

---

<a id="dict"></a>

## dict

Many Python instances expose writable attributes through `__dict__`:

```python
class User:
    pass

u = User()
u.name = "Sai"
print(u.__dict__)
```

Not every object has a `__dict__`.

[Back to Table of Contents](#table-of-contents)

---

<a id="slots"></a>

## slots

`__slots__` can restrict allowed instance attributes and can reduce per-instance memory in suitable designs.

```python
class Point:
    __slots__ = ("x", "y")
```

Trade-offs include reduced dynamic flexibility and inheritance-related details.

Do not claim it universally makes programs faster.

[Back to Table of Contents](#table-of-contents)

---

<a id="attribute-lookup"></a>

## Attribute Lookup

A simplified model:

```text
obj.attr
↓
attribute lookup rules
↓
descriptor handling when applicable
↓
instance state when applicable
↓
class / MRO
```

Descriptor precedence can change which object wins.

[Back to Table of Contents](#table-of-contents)

---

<a id="getattr-vs-getattribute"></a>

## getattr vs getattribute

`__getattribute__` participates in every attribute lookup.

`__getattr__` is a fallback for attributes not found normally.

Use `__getattribute__` carefully because careless overrides can recurse indefinitely.

[Back to Table of Contents](#table-of-contents)

---

<a id="new-vs-init"></a>

## new vs init

```text
__new__
→ create / return instance

__init__
→ initialize returned instance
```

This distinction matters for advanced object-construction questions.

[Back to Table of Contents](#table-of-contents)

---

<a id="str-vs-repr"></a>

## str vs repr

`__str__` aims for human-friendly output.

`__repr__` aims for a useful developer-oriented representation.

Implement both when a domain object needs clear display/debugging behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="special-method-protocols"></a>

## Special Method Protocols

Examples:

```text
__len__       → len(obj)
__iter__      → iter(obj)
__next__      → next(obj)
__contains__  → x in obj
__getitem__   → obj[key]
```

Python relies heavily on these protocols to make language syntax work with user-defined objects.

[Back to Table of Contents](#table-of-contents)

---

<a id="operator-overloading"></a>

## Operator Overloading

```python
class Money:
    def __init__(self, amount):
        self.amount = amount

    def __add__(self, other):
        return Money(self.amount + other.amount)
```

Then `a + b` can use the defined special-method protocol.

[Back to Table of Contents](#table-of-contents)

---

<a id="notimplemented-vs-notimplementederror"></a>

## NotImplemented vs NotImplementedError

`NotImplemented` is a special value used in protocol dispatch to say an operand combination is unsupported by that implementation.

`NotImplementedError` is an exception often used to mark an intentionally missing method implementation.

Do not confuse them.

[Back to Table of Contents](#table-of-contents)

---

<a id="mro"></a>

## MRO

MRO defines the method/attribute lookup order in inheritance hierarchies.

```python
class A: pass
class B(A): pass
class C(A): pass
class D(B, C): pass

print(D.mro())
```

Python uses C3 linearization for modern class MRO.

[Back to Table of Contents](#table-of-contents)

---

<a id="super"></a>

## super

`super()` does not simply mean “call the immediate parent”.

It performs method lookup according to the relevant MRO starting after a class in the hierarchy.

This is particularly important with multiple inheritance.

[Back to Table of Contents](#table-of-contents)

---

<a id="exception-hierarchy"></a>

## Exception Hierarchy

Typical shape:

```text
BaseException
├── KeyboardInterrupt
├── SystemExit
└── Exception
    ├── ValueError
    ├── TypeError
    └── KeyError
```

Application code normally catches `Exception` subclasses rather than `BaseException` broadly.

[Back to Table of Contents](#table-of-contents)

---

<a id="try-except-else-finally"></a>

## try except else finally

```python
try:
    result = risky()
except ValueError:
    recover()
else:
    use(result)
finally:
    cleanup()
```

`else` runs when the `try` block succeeds; `finally` runs on normal exit and exception paths.

[Back to Table of Contents](#table-of-contents)

---

<a id="raise-and-exception-chaining"></a>

## raise and Exception Chaining

```python
try:
    value = int(text)
except ValueError as exc:
    raise RuntimeError("invalid configuration") from exc
```

Chaining preserves the underlying cause for debugging.

[Back to Table of Contents](#table-of-contents)

---

<a id="custom-exceptions"></a>

## Custom Exceptions

```python
class PaymentFailed(Exception):
    pass
```

Use domain-specific exceptions when callers may need different recovery behavior.

[Back to Table of Contents](#table-of-contents)

---

<a id="context-managers"></a>

## Context Managers

Context managers provide scoped setup/cleanup.

```python
with open("data.txt") as f:
    data = f.read()
```

This is preferable to relying on unpredictable object-lifetime timing for resource release.

[Back to Table of Contents](#table-of-contents)

---

<a id="with-statement"></a>

## with Statement

A class-based context manager implements `__enter__` and `__exit__`.

```python
class Managed:
    def __enter__(self):
        print("setup")
        return self

    def __exit__(self, exc_type, exc, tb):
        print("cleanup")
        return False
```

[Back to Table of Contents](#table-of-contents)

---

<a id="contextlib"></a>

## contextlib

`contextlib.contextmanager` lets a generator function define context-manager setup/cleanup around `yield`.

```python
from contextlib import contextmanager

@contextmanager
def managed():
    print("setup")
    try:
        yield
    finally:
        print("cleanup")
```

This is a neat intersection of generators, decorators, and context management.

[Back to Table of Contents](#table-of-contents)

---

<a id="resource-safety"></a>

## Resource Safety

Do not rely on garbage collection to release files, sockets, database connections, or locks.

Prefer deterministic cleanup with context managers and explicit release operations.

[Back to Table of Contents](#table-of-contents)

---

<a id="module-vs-package"></a>

## Module vs Package

A module is a Python module containing code/data definitions.

A package organizes multiple modules under a package namespace.

Modern Python packaging also supports namespace packages, so an `__init__.py` file is not the whole definition of “package”.

[Back to Table of Contents](#table-of-contents)

---

<a id="how-import-works"></a>

## How import Works

Conceptually:

```text
import name
↓
locate module
↓
load / compile if needed
↓
execute module code
↓
cache module object in sys.modules
```

[Back to Table of Contents](#table-of-contents)

---

<a id="sysmodules"></a>

## sys.modules

`sys.modules` is the import cache for modules already loaded in the current process.

```python
import sys
print("json" in sys.modules)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="import-caching"></a>

## Import Caching

Normal repeated imports reuse the module object already in `sys.modules` instead of executing the module from scratch every time.

This is one reason module-level side effects are observable during the first import.

[Back to Table of Contents](#table-of-contents)

---

<a id="name-main"></a>

## name main

A module run directly gets `__name__ == "__main__"`.

```python
if __name__ == "__main__":
    main()
```

When the file is imported, `__name__` is the module's import name.

[Back to Table of Contents](#table-of-contents)

---

<a id="circular-imports"></a>

## Circular Imports

```text
A imports B
B imports A
```

This can expose partially initialized modules.

Prefer cleaner dependency boundaries; local imports are a workaround, not always the best design.

[Back to Table of Contents](#table-of-contents)

---

<a id="virtual-environments"></a>

## Virtual Environments

A virtual environment isolates project dependencies and interpreter packages.

Benefits:

- reproducibility
- avoiding version conflicts
- project isolation

[Back to Table of Contents](#table-of-contents)

---

<a id="pip-and-packaging-basics"></a>

## pip and Packaging Basics

Know the difference between a distribution package name and the Python import name.

Useful commands:

```bash
python -m pip install package
python -m pip show package
python -m pip freeze
```

[Back to Table of Contents](#table-of-contents)

---

<a id="shallow-vs-deep-copy"></a>

## Shallow vs Deep Copy

```text
shallow copy
→ new outer object, shared nested objects

deep copy
→ recursively copied nested objects
```

```python
import copy

a = [[1], [2]]
b = copy.copy(a)
c = copy.deepcopy(a)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="copy-module"></a>

## copy Module

Useful functions:

```python
copy.copy(obj)
copy.deepcopy(obj)
```

Deep copy can be expensive and may be inappropriate for external-resource objects.

[Back to Table of Contents](#table-of-contents)

---

<a id="serialization"></a>

## Serialization

Serialization converts in-memory data into a transport/storage representation.

Examples: JSON, pickle, custom binary formats.

[Back to Table of Contents](#table-of-contents)

---

<a id="pickle"></a>

## pickle

`pickle` serializes Python object graphs.

```python
import pickle
blob = pickle.dumps({"x": 1})
obj = pickle.loads(blob)
```

**Security:** never unpickle untrusted input.

[Back to Table of Contents](#table-of-contents)

---

<a id="json-vs-pickle"></a>

## JSON vs Pickle

| JSON | Pickle |
|---|---|
| Language-independent | Python-specific |
| Human-readable | Python object-oriented serialization |
| Good for APIs/config | Not for untrusted input |
| Limited native object model | Richer Python object graphs |

[Back to Table of Contents](#table-of-contents)

---

<a id="process-vs-thread"></a>

## Process vs Thread

Process:

> independent execution context with separate memory space.

Thread:

> execution unit inside a process that shares process memory/resources.

This shared memory makes threads efficient to communicate with, but creates synchronization concerns.

[Back to Table of Contents](#table-of-contents)

---

<a id="concurrency-vs-parallelism"></a>

## Concurrency vs Parallelism

Concurrency means multiple tasks can make progress through interleaving.

Parallelism means work executes simultaneously on multiple execution resources.

Async I/O gives concurrency. Multiprocessing can provide CPU parallelism. Traditional CPython threads have a GIL constraint for Python bytecode.

[Back to Table of Contents](#table-of-contents)

---

<a id="gil"></a>

## GIL

In traditional CPython builds, the Global Interpreter Lock ensures that only one thread at a time executes Python bytecode in a process. This simplifies parts of CPython's object model but limits CPU-bound Python-thread parallelism. I/O operations can release the GIL, and some extension modules release it around native work. citeturn514941search10

**Interview line:**

> “The GIL is a CPython runtime lock that, in traditional builds, prevents multiple threads from executing Python bytecode simultaneously in the same process.”

Do not say “Python cannot use multiple cores”; multiprocessing and native extensions are counterexamples. citeturn514941search10

[Back to Table of Contents](#table-of-contents)

---

<a id="modern-gil-changes"></a>

## Modern GIL Changes

CPython 3.13 introduced a supported free-threaded build configuration that can disable the GIL. It is not the default assumption for every Python installation, so specify the interpreter/build when discussing concurrency. citeturn514941search10

Interview-safe wording:

> “For the Python build I am discussing, I would verify whether it uses the traditional GIL or a free-threaded build.”

[Back to Table of Contents](#table-of-contents)

---

<a id="why-io-bound-threading-helps"></a>

## Why I/O-Bound Threading Helps

For I/O-heavy work:

```text
Thread A → waiting for network
Thread B → runs other work
Thread A → resumes
```

Typical cases: HTTP calls, database access, file I/O.

[Back to Table of Contents](#table-of-contents)

---

<a id="why-cpu-bound-threading-differs"></a>

## Why CPU-Bound Threading Differs

In traditional CPython builds, CPU-heavy Python code in multiple threads does not execute its Python bytecode simultaneously across cores because of the GIL.

For CPU-heavy workloads consider:

- multiprocessing
- native extensions
- vectorized libraries
- appropriately configured free-threaded builds

[Back to Table of Contents](#table-of-contents)

---

<a id="thread-lifecycle"></a>

## Thread Lifecycle

Typical lifecycle:

```text
create
↓
start()
↓
running / waiting
↓
complete
↓
join()
```

[Back to Table of Contents](#table-of-contents)

---

<a id="threading-module"></a>

## threading Module

```python
from threading import Thread

def worker(name):
    print(name)

threads = [Thread(target=worker, args=(f"w{i}",)) for i in range(3)]
for t in threads:
    t.start()
for t in threads:
    t.join()
```

Interview depth is in shared state, synchronization, failure handling, and bounded concurrency.

[Back to Table of Contents](#table-of-contents)

---

<a id="race-conditions"></a>

## Race Conditions

A race condition occurs when correctness depends on timing/interleaving.

Even if a statement looks simple:

```python
counter += 1
```

conceptually there is a read/modify/write sequence that can interleave.

[Back to Table of Contents](#table-of-contents)

---

<a id="lock"></a>

## Lock

```python
from threading import Lock

lock = Lock()
counter = 0

def increment():
    global counter
    with lock:
        counter += 1
```

Keep critical sections small.

[Back to Table of Contents](#table-of-contents)

---

<a id="rlock"></a>

## RLock

`RLock` is reentrant: the same thread can acquire it multiple times and must release it the same number of times.

Useful when nested code may reacquire the same lock.

[Back to Table of Contents](#table-of-contents)

---

<a id="semaphore"></a>

## Semaphore

A semaphore controls access to a limited number of permits.

```python
from threading import Semaphore
slots = Semaphore(3)
with slots:
    ...
```

Useful for bounded concurrency, such as limiting active resource users.

[Back to Table of Contents](#table-of-contents)

---

<a id="event"></a>

## Event

`Event` is a coordination flag.

```python
ready.wait()
```

Another thread can call:

```python
ready.set()
```

Use it for signaling, not mutual exclusion.

[Back to Table of Contents](#table-of-contents)

---

<a id="condition"></a>

## Condition

A `Condition` lets threads wait for a predicate and be notified when state changes.

Classic use: producer adds work, consumer wakes, re-checks the queue, and consumes.

[Back to Table of Contents](#table-of-contents)

---

<a id="barrier"></a>

## Barrier

A barrier makes a group of threads wait until all expected participants reach the synchronization point.

Useful for staged workflows.

[Back to Table of Contents](#table-of-contents)

---

<a id="thread-safe-design"></a>

## Thread-Safe Design

Prefer, where practical:

- no shared mutable state
- immutable values
- queues for ownership transfer
- locks around invariants
- bounded pools
- clear state ownership

Thread safety is about correctness guarantees, not merely “the program did not crash.”

[Back to Table of Contents](#table-of-contents)

---

<a id="deadlocks"></a>

## Deadlocks

Classic conditions:

```text
mutual exclusion
hold and wait
no preemption
circular wait
```

Example:

```text
A holds L1 → waits L2
B holds L2 → waits L1
```

[Back to Table of Contents](#table-of-contents)

---

<a id="deadlock-prevention"></a>

## Deadlock Prevention

Practical strategies:

- global lock ordering
- short critical sections
- avoid nested locks where possible
- timeouts
- reduce shared mutable state

[Back to Table of Contents](#table-of-contents)

---

<a id="threadpoolexecutor"></a>

## ThreadPoolExecutor

Prefer bounded pools over manually creating unbounded threads.

```python
from concurrent.futures import ThreadPoolExecutor

with ThreadPoolExecutor(max_workers=8) as pool:
    results = list(pool.map(fetch_url, urls))
```

This is a strong interview example for I/O-bound concurrency.

[Back to Table of Contents](#table-of-contents)

---

<a id="threading-drills"></a>

## Threading Drills

Practice:

- thread creation + `join`
- lock-protected counter
- producer-consumer queue
- semaphore-limited workers
- thread pool
- deadlock + lock-order fix

[Back to Table of Contents](#table-of-contents)

---

<a id="why-multiprocessing"></a>

## Why Multiprocessing

Separate processes provide separate memory spaces and can provide CPU parallelism independent of the traditional GIL.

Costs:

- process startup
- IPC
- serialization
- larger memory footprint

[Back to Table of Contents](#table-of-contents)

---

<a id="process-creation"></a>

## Process Creation

```python
from multiprocessing import Process

def worker():
    print("child")

p = Process(target=worker)
p.start()
p.join()
```

Process-start behavior differs by platform and start method, so do not assume one universal mechanism.

[Back to Table of Contents](#table-of-contents)

---

<a id="multiprocessing-module"></a>

## multiprocessing Module

Know:

- `Process`
- `Queue`
- `Pipe`
- `Pool`
- shared memory
- synchronization primitives

[Back to Table of Contents](#table-of-contents)

---

<a id="process-isolation"></a>

## Process Isolation

Processes do not normally share ordinary Python object memory directly.

Communication uses IPC such as queues, pipes, sockets, files, or shared memory.

[Back to Table of Contents](#table-of-contents)

---

<a id="ipc"></a>

## IPC

Inter-process communication mechanisms in Python include:

```text
Queue
Pipe
Shared memory
Sockets
Files / database
```

Choose based on data size, synchronization needs, and latency requirements.

[Back to Table of Contents](#table-of-contents)

---

<a id="queue-and-pipe"></a>

## Queue and Pipe

Queue: higher-level producer/consumer messaging.

Pipe: lower-level connection between process endpoints.

[Back to Table of Contents](#table-of-contents)

---

<a id="shared-memory"></a>

## Shared Memory

Shared memory can reduce serialization/copying cost but increases synchronization complexity.

Use it only when the workload benefits enough to justify that complexity.

[Back to Table of Contents](#table-of-contents)

---

<a id="processpoolexecutor"></a>

## ProcessPoolExecutor

```python
from concurrent.futures import ProcessPoolExecutor

with ProcessPoolExecutor() as pool:
    results = list(pool.map(cpu_heavy_function, values))
```

Useful for CPU-bound functions with manageable argument/result serialization.

[Back to Table of Contents](#table-of-contents)

---

<a id="multiprocessing-trade-offs"></a>

## Multiprocessing Trade-Offs

Pros:

- CPU parallelism
- process isolation

Cons:

- higher startup cost
- IPC overhead
- serialization/shared-state complexity

[Back to Table of Contents](#table-of-contents)

---

<a id="synchronous-vs-asynchronous"></a>

## Synchronous vs Asynchronous

Synchronous code waits directly for each operation.

Async code can pause an I/O operation and let other tasks make progress.

This is most valuable for highly concurrent I/O-bound workloads.

[Back to Table of Contents](#table-of-contents)

---

<a id="async-def-and-await"></a>

## async def and await

```python
async def fetch(client):
    return await client.get("/data")
```

`await` yields control while the awaited operation is incomplete.

[Back to Table of Contents](#table-of-contents)

---

<a id="coroutine-objects"></a>

## Coroutine Objects

Calling an `async def` creates a coroutine object.

```python
coro = fetch(client)
```

It must be awaited or scheduled.

[Back to Table of Contents](#table-of-contents)

---

<a id="event-loop"></a>

## Event Loop

The event loop coordinates ready/waiting asynchronous tasks.

```text
Task A waits on I/O
↓
event loop runs Task B
↓
B waits
↓
A becomes ready
↓
A resumes
```

[Back to Table of Contents](#table-of-contents)

---

<a id="tasks"></a>

## Tasks

```python
import asyncio

task = asyncio.create_task(fetch())
```

A task schedules a coroutine so the event loop can manage it alongside other tasks.

[Back to Table of Contents](#table-of-contents)

---

<a id="asynciogather"></a>

## asyncio.gather

```python
results = await asyncio.gather(fetch_a(), fetch_b(), fetch_c())
```

This is a common pattern for concurrent async operations.

[Back to Table of Contents](#table-of-contents)

---

<a id="async-io-mental-model"></a>

## Async I/O Mental Model

One event loop can coordinate many waiting I/O operations without creating one OS thread per operation.

Async is concurrency, not automatic CPU parallelism.

[Back to Table of Contents](#table-of-contents)

---

<a id="async-vs-threads"></a>

## Async vs Threads

Async: best when the stack supports non-blocking I/O.

Threads: useful when existing libraries are blocking or when synchronous code is simpler.

Both can be appropriate in the same application.

[Back to Table of Contents](#table-of-contents)

---

<a id="async-vs-multiprocessing"></a>

## Async vs Multiprocessing

```text
Async → I/O concurrency
Threads → I/O concurrency around blocking code
Processes → CPU parallelism + isolation
```

[Back to Table of Contents](#table-of-contents)

---

<a id="common-async-mistakes"></a>

## Common Async Mistakes

- blocking the event loop
- forgetting `await`
- creating unbounded tasks
- missing timeouts/cancellation
- using async for CPU-bound work

[Back to Table of Contents](#table-of-contents)

---

<a id="simple-async-implementation"></a>

## Simple Async Implementation

```python
import asyncio

async def worker(name, delay):
    await asyncio.sleep(delay)
    return f"{name} done"

async def main():
    return await asyncio.gather(
        worker("A", 1),
        worker("B", 2),
        worker("C", 1),
    )

print(asyncio.run(main()))
```

[Back to Table of Contents](#table-of-contents)

---

<a id="big-o-vs-runtime-constants"></a>

## Big O vs Runtime Constants

Two solutions can have the same asymptotic complexity but very different constants.

Python-level loops often have more interpreter/runtime overhead than C-implemented built-ins.

Always preserve correct Big-O reasoning, then profile the real hotspot.

[Back to Table of Contents](#table-of-contents)

---

<a id="timeit"></a>

## timeit

Use `timeit` for small controlled benchmarks:

```python
import timeit
print(timeit.timeit("sum(range(1000))", number=10000))
```

[Back to Table of Contents](#table-of-contents)

---

<a id="cprofile"></a>

## cProfile

```bash
python -m cProfile app.py
```

Use it to identify where cumulative time is spent.

[Back to Table of Contents](#table-of-contents)

---

<a id="tracemalloc"></a>

## tracemalloc

`tracemalloc` helps trace Python memory allocations.

It is more useful for allocation analysis than `sys.getsizeof()` alone.

[Back to Table of Contents](#table-of-contents)

---

<a id="generators-for-memory-efficiency"></a>

## Generators for Memory Efficiency

List:

```python
[x for x in huge_source]
```

Generator:

```python
(x for x in huge_source)
```

The generator avoids materializing all results simultaneously.

[Back to Table of Contents](#table-of-contents)

---

<a id="string-join"></a>

## String join

For many fragments:

```python
result = "".join(parts)
```

This is typically preferable to repeated string construction in a large loop.

[Back to Table of Contents](#table-of-contents)

---

<a id="avoiding-unnecessary-copies"></a>

## Avoiding Unnecessary Copies

Copies consume CPU, memory, and allocation bandwidth.

Use views/iterators/immutable sharing where appropriate, but never share mutable state accidentally when independent ownership is required.

[Back to Table of Contents](#table-of-contents)

---

<a id="native-code-and-vectorization"></a>

## Native Code and Vectorization

Python code can delegate heavy computation to optimized native libraries.

Examples include NumPy-style vectorized operations and extension modules.

This is a key reason the statement “Python is slow” is too broad.

[Back to Table of Contents](#table-of-contents)

---

<a id="why-python-can-be-slower"></a>

## Why Python Can Be Slower

Common causes:

- dynamic dispatch
- object allocation/boxing
- interpreter/runtime overhead
- Python-level loops

But optimized built-ins, native libraries, and appropriate concurrency can change the picture significantly.

[Back to Table of Contents](#table-of-contents)

---

<a id="collections"></a>

## collections

Know:

- `deque`
- `Counter`
- `defaultdict`
- `namedtuple`
- `ChainMap`

[Back to Table of Contents](#table-of-contents)

---

<a id="itertools"></a>

## itertools

Important lazy iterator tools:

- `chain`
- `islice`
- `product`
- `permutations`
- `combinations`
- `groupby`

[Back to Table of Contents](#table-of-contents)

---

<a id="functools"></a>

## functools

Know:

- `wraps`
- `lru_cache`
- `partial`
- `reduce`
- `singledispatch`

[Back to Table of Contents](#table-of-contents)

---

<a id="heapq-module"></a>

## heapq Module

Know:

- `heappush`
- `heappop`
- `heapify`
- `nlargest`
- `nsmallest`

[Back to Table of Contents](#table-of-contents)

---

<a id="bisect"></a>

## bisect

Useful for binary-search insertion points in sorted lists:

```python
from bisect import bisect_left
idx = bisect_left([1, 3, 5, 8], 5)
```

[Back to Table of Contents](#table-of-contents)

---

<a id="dataclasses"></a>

## dataclasses

Dataclasses reduce boilerplate for data-centric classes.

Know:

- generated `__init__`
- generated `repr`
- generated `eq`
- `frozen=True`
- `default_factory`

[Back to Table of Contents](#table-of-contents)

---

<a id="typing"></a>

## typing

Know the purpose of:

- `list[str]`
- `dict[str, int]`
- `Callable`
- `Protocol`
- `TypeVar`
- `Optional`
- `Union` / `|`

Typing mainly supports static analysis; it does not turn Python into a statically typed runtime by itself.

[Back to Table of Contents](#table-of-contents)

---

<a id="enum"></a>

## enum

Use enums for controlled finite sets:

```python
from enum import Enum

class Status(Enum):
    ACTIVE = "active"
    INACTIVE = "inactive"
```

[Back to Table of Contents](#table-of-contents)

---

<a id="pathlib"></a>

## pathlib

Modern path manipulation:

```python
from pathlib import Path
path = Path("data") / "file.txt"
```

[Back to Table of Contents](#table-of-contents)

---

<a id="custom-iterator"></a>

## Custom Iterator

```python
class RangeIterator:
    def __init__(self, start, stop):
        self.current = start
        self.stop = stop

    def __iter__(self):
        return self

    def __next__(self):
        if self.current >= self.stop:
            raise StopIteration
        value = self.current
        self.current += 1
        return value
```

[Back to Table of Contents](#table-of-contents)

---

<a id="generator"></a>

## Generator

```python
def read_chunks(items, size):
    for i in range(0, len(items), size):
        yield items[i:i + size]
```

Good for streaming and batching.

[Back to Table of Contents](#table-of-contents)

---

<a id="timing-decorator"></a>

## Timing Decorator

```python
from functools import wraps
from time import perf_counter

def timed(fn):
    @wraps(fn)
    def wrapper(*args, **kwargs):
        start = perf_counter()
        try:
            return fn(*args, **kwargs)
        finally:
            print(f"{fn.__name__}: {perf_counter() - start:.6f}s")
    return wrapper
```

[Back to Table of Contents](#table-of-contents)

---

<a id="retry-decorator"></a>

## Retry Decorator

```python
from functools import wraps
import time

def retry(attempts, delay=0.1):
    def decorator(fn):
        @wraps(fn)
        def wrapper(*args, **kwargs):
            last = None
            for _ in range(attempts):
                try:
                    return fn(*args, **kwargs)
                except Exception as exc:
                    last = exc
                    time.sleep(delay)
            raise last
        return wrapper
    return decorator
```

Production follow-ups: transient-error filtering, exponential backoff, jitter, idempotency, cancellation.

[Back to Table of Contents](#table-of-contents)

---

<a id="context-manager"></a>

## Context Manager

```python
class Managed:
    def __enter__(self):
        print("open")
        return self
    def __exit__(self, exc_type, exc, tb):
        print("close")
        return False
```

[Back to Table of Contents](#table-of-contents)

---

<a id="lru-cache-concept"></a>

## LRU Cache Concept

The standard library gives you `functools.lru_cache`, but the classic interview implementation combines:

```text
dict + doubly linked list
```

Dict gives O(1)-average lookup; the linked list tracks recency for O(1) promotion/eviction.

[Back to Table of Contents](#table-of-contents)

---

<a id="thread-pool-downloader-pattern"></a>

## Thread Pool Downloader Pattern

For I/O-bound work:

```python
from concurrent.futures import ThreadPoolExecutor

with ThreadPoolExecutor(max_workers=8) as pool:
    results = list(pool.map(download, urls))
```

The interview idea is bounded concurrency around blocking I/O.

[Back to Table of Contents](#table-of-contents)

---

<a id="producer-consumer-queue"></a>

## Producer Consumer Queue

```python
from queue import Queue
from threading import Thread

q = Queue()

def producer():
    for i in range(10):
        q.put(i)
    q.put(None)

def consumer():
    while True:
        item = q.get()
        try:
            if item is None:
                return
            print("process", item)
        finally:
            q.task_done()
```

The queue synchronizes and decouples producer/consumer timing.

[Back to Table of Contents](#table-of-contents)

---

<a id="thread-safe-counter"></a>

## Thread Safe Counter

```python
from threading import Lock

class Counter:
    def __init__(self):
        self.value = 0
        self.lock = Lock()

    def increment(self):
        with self.lock:
            self.value += 1
```

[Back to Table of Contents](#table-of-contents)

---

<a id="multiprocessing-pool"></a>

## Multiprocessing Pool

```python
from concurrent.futures import ProcessPoolExecutor

with ProcessPoolExecutor() as pool:
    results = list(pool.map(cpu_task, range(10)))
```

[Back to Table of Contents](#table-of-contents)

---

<a id="async-concurrent-tasks"></a>

## Async Concurrent Tasks

```python
import asyncio

async def main():
    return await asyncio.gather(
        fetch_one(),
        fetch_two(),
        fetch_three(),
    )
```

In production, bound concurrency and timeouts matter.

[Back to Table of Contents](#table-of-contents)

---

<a id="high-frequency-questions"></a>

## High-Frequency Questions

Recent public Infosys DSE/SP reports mention Python questions such as decorators, lists/tuples, dictionaries, generators, GIL, multithreading, exception handling, and performance. Candidate reports also show the interview can move from Python into projects, OOP, Java, networking, and live coding. These are signals, not a guaranteed fixed question list. citeturn514941reddit35turn514941search0turn514941search1turn514941search7

Master these:

1. Is Python interpreted or compiled?
2. What happens when a `.py` file runs?
3. What is bytecode?
4. List vs tuple?
5. Why are dict lookups usually O(1)?
6. Mutable vs immutable?
7. `is` vs `==`?
8. How does Python pass arguments?
9. What is a decorator?
10. What is an iterator?
11. What is a generator?
12. What happens inside a `for` loop?
13. What is garbage collection?
14. Reference counting vs cyclic GC?
15. What is the GIL?
16. Is Python multithreaded?
17. Thread vs process?
18. Async vs threading?
19. What is a context manager?
20. What is a descriptor?

[Back to Table of Contents](#table-of-contents)

---

<a id="python-internals-questions"></a>

## Python Internals Questions

Be ready for:

- What is a code object?
- What does `dis` show?
- What is an execution frame?
- How does attribute lookup work?
- What is a descriptor?
- Why do methods bind to instances?
- Why does Python need cyclic GC?
- Why are `is` and `==` different?
- What is `sys.modules`?
- What is `__slots__`?
- What is `__new__` vs `__init__`?
- How does MRO affect `super()`?

[Back to Table of Contents](#table-of-contents)

---

<a id="collections-questions"></a>

## Collections Questions

- Why is list append amortized O(1)?
- Why is inserting at index 0 O(n)?
- Why is dict lookup usually O(1)?
- What is a hash collision?
- Why must dict keys be hashable?
- List vs deque?
- Set vs list for membership?
- Why can too many copies hurt performance?
- How would you implement LRU cache?

[Back to Table of Contents](#table-of-contents)

---

<a id="functions-and-decorators-questions"></a>

## Functions and Decorators Questions

- Are functions objects?
- What is LEGB?
- What does `nonlocal` do?
- What is a closure?
- Why does late binding happen?
- What is a decorator?
- When does a decorator execute?
- What does `functools.wraps` do?
- How do parameterized decorators work?

[Back to Table of Contents](#table-of-contents)

---

<a id="iterator-and-generator-questions"></a>

## Iterator and Generator Questions

- Iterable vs iterator?
- What does `iter()` return?
- What does `next()` do?
- Why does `for` stop?
- What is `StopIteration`?
- What is a generator object?
- What does `yield` preserve?
- Why does a generator save memory?
- Can a generator be reused after exhaustion?

[Back to Table of Contents](#table-of-contents)

---

<a id="concurrency-questions"></a>

## Concurrency Questions

- Process vs thread?
- Concurrency vs parallelism?
- What is the GIL?
- Why can I/O-bound threads help?
- Why are CPU-bound threads different under traditional CPython?
- Race condition?
- Lock vs semaphore?
- Event vs condition?
- Deadlock?
- ThreadPoolExecutor?
- When would you use multiprocessing?
- When would you use asyncio?

[Back to Table of Contents](#table-of-contents)

---

<a id="memory-and-gc-questions"></a>

## Memory and GC Questions

- What is reference counting?
- What happens at refcount zero?
- Why can cycles survive refcounting?
- What does `gc.collect()` do?
- Can GC release a database connection deterministically?
- What is interning?
- What is `__slots__`?
- What does `sys.getsizeof()` measure?

[Back to Table of Contents](#table-of-contents)

---

<a id="exception-and-import-questions"></a>

## Exception and Import Questions

- `try/except/else/finally`?
- `raise ... from`?
- Custom exception?
- Context manager?
- How does import work?
- What is `sys.modules`?
- Circular imports?
- `if __name__ == "__main__"`?

[Back to Table of Contents](#table-of-contents)

---

<a id="project-driven-questions"></a>

## Project-Driven Questions

### SceneFlow

Be able to explain the actual Python choices in your project:

- FastAPI and request handling
- background jobs
- Redis/Celery interaction
- external provider calls
- retries and timeouts
- concurrency around I/O
- CPU-heavy embedding work
- duplicate jobs

### URL Shortener

Be able to explain:

- router/service/repository separation
- Redis cache
- SQL access
- atomic counter behavior
- connection pooling
- concurrent requests
- idempotency

Always answer from your actual implementation when the interviewer asks project-specific questions.

[Back to Table of Contents](#table-of-contents)

---

<a id="explain-why-drill"></a>

## Explain Why Drill

Turn every definition into a chain:

```text
Why is dict lookup fast?
↓
Hash narrows candidate locations.
↓
Why must keys be hashable?
↓
The hash participates in lookup.
↓
Why must hash stay stable?
↓
Changing it can make an existing key unreachable.
```

Use this style for decorators, generators, GC, GIL, imports, descriptors, and threading.

[Back to Table of Contents](#table-of-contents)

---

<a id="mutable-default-arguments"></a>

## Mutable Default Arguments

Bad:

```python
def f(items=[]):
    items.append(1)
    return items
```

Fix with `None` and initialize inside.

[Back to Table of Contents](#table-of-contents)

---

<a id="late-binding-trap"></a>

## Late Binding Trap

```python
funcs = [lambda: i for i in range(3)]
```

The lambdas see the later value of `i`.

Fix with `lambda i=i: i`.

[Back to Table of Contents](#table-of-contents)

---

<a id="is-vs-equal-trap"></a>

## is vs == Trap

```text
is → identity
== → equality
```

Use `is None`, not `== None` as the normal identity check.

[Back to Table of Contents](#table-of-contents)

---

<a id="nested-list-multiplication"></a>

## Nested List Multiplication

Bad:

```python
matrix = [[0] * 3] * 3
```

All rows reference the same inner list.

Correct:

```python
matrix = [[0] * 3 for _ in range(3)]
```

[Back to Table of Contents](#table-of-contents)

---

<a id="shallow-copy-trap"></a>

## Shallow Copy Trap

```python
a = [[1], [2]]
b = a.copy()
b[0].append(99)
```

The nested list is shared, so `a[0]` changes too.

[Back to Table of Contents](#table-of-contents)

---

<a id="generator-exhaustion"></a>

## Generator Exhaustion

Generators are one-shot iterators.

```python
g = (x for x in range(3))
print(list(g))
print(list(g))
```

The second result is empty.

[Back to Table of Contents](#table-of-contents)

---

<a id="global-mutable-state"></a>

## Global Mutable State

Global mutable objects create hidden coupling and make testing/concurrency harder.

Prefer explicit dependencies where practical.

[Back to Table of Contents](#table-of-contents)

---

<a id="thread-shared-state"></a>

## Thread Shared State

The GIL does not make application-level invariants automatically safe.

Use locks, queues, immutable state, or ownership boundaries when shared mutable state is involved.

[Back to Table of Contents](#table-of-contents)

---

<a id="blocking-in-async-code"></a>

## Blocking in Async Code

Avoid:

```python
async def handler():
    time.sleep(5)
```

That blocks the event-loop thread.

Use async-compatible I/O or explicitly offload blocking work.

[Back to Table of Contents](#table-of-contents)

---

<a id="30-second-python-mental-model"></a>

## 30-Second Python Mental Model

```text
source
↓
compile to code object / bytecode
↓
CPython runtime executes it
↓
Python objects

names → objects

for → iter → next → StopIteration
yield → pause + preserve generator state
decorator → callable transformation
descriptor → attribute-access protocol

CPython memory
→ reference counting + cyclic GC

traditional CPython threading
→ one thread executes Python bytecode at a time

process
→ separate memory + CPU parallelism

async
→ event-loop concurrency for I/O
```

[Back to Table of Contents](#table-of-contents)

---

<a id="python-keyword-radar"></a>

## Python Keyword Radar

```text
decorator → closure / wrapper / wraps
iterator → __iter__ / __next__ / StopIteration
generator → yield / saved state
for loop → iter / next
dict → hash / equality / hashability
garbage collection → refcount / cycles / gc
GIL → CPython / bytecode / I/O vs CPU
thread → shared state / locks / race conditions
process → isolation / IPC
async → coroutine / await / event loop
property → descriptor
super → MRO
import → sys.modules / module execution
copy → shallow vs deep
performance → algorithm / built-ins / profiling
```

[Back to Table of Contents](#table-of-contents)

---

<a id="implementation-checklist"></a>

## Implementation Checklist

Be able to write from memory:

- custom iterator
- generator
- decorator
- parameterized decorator
- descriptor
- context manager
- custom exception
- lock-protected counter
- producer-consumer queue
- semaphore-limited workers
- thread pool
- process pool
- async concurrent tasks
- basic LRU cache design
- shallow/deep copy demonstration
- `__new__` / `__init__` example

[Back to Table of Contents](#table-of-contents)

---

<a id="final-python-interview-checklist"></a>

## Final Python Interview Checklist

### Fundamentals
- [ ] Python vs CPython
- [ ] dynamic typing
- [ ] names vs objects
- [ ] identity vs equality
- [ ] mutability
- [ ] argument passing
- [ ] LEGB
- [ ] closures

### Internals
- [ ] source → code object → bytecode
- [ ] `dis`
- [ ] frames/call state
- [ ] object model
- [ ] descriptors
- [ ] attribute lookup
- [ ] MRO
- [ ] `super`

### Collections
- [ ] list internals
- [ ] tuple
- [ ] dict
- [ ] set
- [ ] deque
- [ ] hashability
- [ ] complexity

### Language protocols
- [ ] iterator
- [ ] generator
- [ ] decorator
- [ ] context manager
- [ ] dunder methods
- [ ] `__new__` / `__init__`

### Memory
- [ ] refcount
- [ ] cyclic GC
- [ ] `gc`
- [ ] interning
- [ ] `__slots__`
- [ ] copy semantics
- [ ] deterministic cleanup

### Concurrency
- [ ] thread/process
- [ ] concurrency/parallelism
- [ ] GIL
- [ ] race conditions
- [ ] locks
- [ ] semaphore
- [ ] condition/event
- [ ] deadlock
- [ ] thread pool
- [ ] multiprocessing
- [ ] async/await
- [ ] event loop

### Ecosystem
- [ ] imports
- [ ] `sys.modules`
- [ ] venv
- [ ] pip
- [ ] collections
- [ ] itertools
- [ ] functools
- [ ] dataclasses
- [ ] typing
- [ ] pathlib

### Interview execution
- [ ] answer simple question first
- [ ] go deeper when pushed
- [ ] distinguish language semantics from CPython internals
- [ ] write a rough implementation
- [ ] explain trade-offs
- [ ] use real-world examples
- [ ] connect answers to your own Python projects
- [ ] never bluff implementation-specific facts

[Back to Table of Contents](#table-of-contents)
