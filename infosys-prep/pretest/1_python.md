# Python — Infosys SP L1 Pre-Test

[← Back to Pre-Test Roadmap](./README.md)

## Table of Contents

- [How to use this file](#how-to-use-this-file)
- [1. Python execution and basic syntax](#1-python-execution-and-basic-syntax)
- [2. Core data types and truthiness](#2-core-data-types-and-truthiness)
- [3. Strings and slicing](#3-strings-and-slicing)
- [4. Lists, tuples, sets and dictionaries](#4-lists-tuples-sets-and-dictionaries)
- [5. Mutability, identity and equality](#5-mutability-identity-and-equality)
- [6. Operators and evaluation order](#6-operators-and-evaluation-order)
- [7. Control flow and loops](#7-control-flow-and-loops)
- [8. Functions, arguments and scope](#8-functions-arguments-and-scope)
- [9. Comprehensions and unpacking](#9-comprehensions-and-unpacking)
- [10. Object-oriented Python](#10-object-oriented-python)
- [11. Exceptions and context managers](#11-exceptions-and-context-managers)
- [12. Iterators, generators and decorators](#12-iterators-generators-and-decorators)
- [13. Imports, files and common standard-library tools](#13-imports-files-and-common-standard-library-tools)
- [14. High-yield code-tracing traps](#14-high-yield-code-tracing-traps)
- [15. Practice MCQs](#15-practice-mcqs)
- [16. Study schedule and completion checklist](#16-study-schedule-and-completion-checklist)
- [References](#references)

## How to use this file

Treat this as a structured topic list and revision guide, not a leaked or official exam paper. Candidate reports are anecdotal. Practise predicting output before running code, and explain why each distractor is wrong.

**Completion rule:** for each concept, read it, write a tiny example, solve 5–10 questions, and log mistakes. Target 85% on fresh quizzes before marking a topic complete.

## 1. Python execution and basic syntax

Python executes statements in order. Indentation defines suites such as function bodies, conditionals and loops. Names refer to objects; a variable is not a fixed-typed container.

```python
x = 10
x = "ten"
print(x)
```

Output: `ten`. The name `x` is rebound to a string object.

Know: comments, indentation, assignment, expressions, `print`, `input` (returns text), type conversion, syntax errors versus runtime exceptions, and the difference between an expression and a statement.

**Typical MCQ traps:** assuming `input()` returns an integer; confusing `=` with `==`; assuming indentation is cosmetic.

[↑ Back to TOC](#table-of-contents)

## 2. Core data types and truthiness

Know `int`, `float`, `bool`, `str`, `None`, and common collection types. `type(value)` reports its type; `isinstance(value, T)` checks membership in a type or tuple of types.

Falsy values include `False`, `None`, numeric zero, empty strings, and empty built-in collections. Most non-empty objects are truthy.

```python
print(bool([]), bool("0"), bool(0))
```

Output: `False True False`.

A common conversion pitfall: `bool("False")` is `True`, because the string is non-empty. Do not treat strings such as `"0"` or `"False"` as numeric/boolean values automatically.

[↑ Back to TOC](#table-of-contents)

## 3. Strings and slicing

Strings are immutable sequences of Unicode code points. Indexing starts at zero; negative indices count from the end. Slicing uses `sequence[start:stop:step]` and excludes `stop`.

```python
s = "PYTHON"
print(s[1:5:2])
print(s[::-1])
```

Output:
```text
YH
NOHTYP
```

Know common methods: `lower`, `upper`, `strip`, `split`, `join`, `replace`, `find`, `startswith`, `endswith`, and f-strings. Methods such as `replace` return a new string; they do not mutate the original.

[↑ Back to TOC](#table-of-contents)

## 4. Lists, tuples, sets and dictionaries

- **List:** ordered, mutable sequence; allows duplicates.
- **Tuple:** ordered, immutable sequence (though it can contain mutable objects).
- **Set:** unique hashable elements; no positional indexing.
- **Dictionary:** insertion-ordered mapping from hashable keys to values.

```python
items = [1, 2, 2]
items.append(3)
print(items)

d = {"a": 1}
d["b"] = 2
print(d)
```

Remember: `list.sort()` mutates a list and returns `None`; `sorted(iterable)` returns a new list. Dictionary lookup by a missing key raises `KeyError`; `d.get(key)` returns `None` by default when the key is absent. Set operations include union (`|`), intersection (`&`) and difference (`-`).

[↑ Back to TOC](#table-of-contents)

## 5. Mutability, identity and equality

- `==` asks whether values compare equal.
- `is` asks whether two names refer to the same object.
- Mutable objects can change in place; immutable objects cannot be changed after creation.

```python
a = [1, 2]
b = a
c = a.copy()
b.append(3)
print(a, c, a is b, a is c)
```

Output: `[1, 2, 3] [1, 2] True False`.

Be careful with nested structures: a shallow copy copies only the outer container, so nested mutable elements remain shared. Avoid predicting identity for small integers or strings based on implementation-specific interning; use `is` primarily for identity checks such as `x is None`.

[↑ Back to TOC](#table-of-contents)

## 6. Operators and evaluation order

Review arithmetic (`+`, `-`, `*`, `/`, `//`, `%`, `**`), comparison, logical operators, membership, identity, bitwise operators and augmented assignment.

```python
print(7 / 2, 7 // 2, -7 // 2, 7 % 2)
```

Output: `3.5 3 -4 1`. Floor division rounds down toward negative infinity, not toward zero.

`and` and `or` short-circuit and return one of their operands, not necessarily a Boolean.

```python
print("" or "fallback")
print(0 and 10)
```

Output: `fallback`, then `0`.

[↑ Back to TOC](#table-of-contents)

## 7. Control flow and loops

Review `if/elif/else`, `for`, `while`, `range`, `break`, `continue`, and loop `else`. A loop's `else` executes when the loop ends normally, not when it is terminated by `break`.

```python
for n in range(3):
    if n == 1:
        break
else:
    print("finished")
print("done")
```

Only `done` is printed.

`range(start, stop, step)` excludes `stop`. A zero step raises `ValueError`. When tracing nested loops, write out each iteration and update state carefully.

[↑ Back to TOC](#table-of-contents)

## 8. Functions, arguments and scope

Functions are objects. Review positional and keyword arguments, defaults, `*args`, `**kwargs`, return values, lambdas, local/global/nonlocal scope and closures.

**Mutable-default trap:**

```python
def add_item(item, bucket=[]):
    bucket.append(item)
    return bucket

print(add_item("a"))
print(add_item("b"))
```

The second call returns `['a', 'b']` because the default list is created once when the function is defined. Prefer `None` as a sentinel and create a new list inside the function.

Assignment inside a function normally creates a local name unless declared `global` or `nonlocal`. Python passes object references by assignment: mutating a passed-in list may be visible to the caller, while rebinding the parameter does not rebind the caller's variable.

[↑ Back to TOC](#table-of-contents)

## 9. Comprehensions and unpacking

List comprehensions build lists; set comprehensions build sets; dictionary comprehensions build dictionaries; generator expressions produce values lazily.

```python
squares = [n * n for n in range(5) if n % 2 == 0]
print(squares)
```

Output: `[0, 4, 16]`.

Review iterable unpacking (`a, b = pair`), extended unpacking (`first, *middle, last = values`), `enumerate`, `zip`, `any`, `all`, `map`, and `filter`. In modern Python, `zip` stops at the shortest input by default.

[↑ Back to TOC](#table-of-contents)

## 10. Object-oriented Python

Know classes, instances, `self`, instance/class attributes, instance methods, class methods, static methods, inheritance, overriding, `super()`, composition, properties, and special methods such as `__init__`, `__str__`, and `__repr__`.

- Instance attributes belong to a particular object.
- Class attributes are shared through the class unless shadowed by an instance attribute.
- Overriding provides a subclass-specific implementation.
- `super()` follows Python's method resolution order; it is not simply a hard-coded call to the parent by name.
- A property can expose a method using attribute-style access.

```python
class Counter:
    count = 0
    def __init__(self):
        Counter.count += 1

a = Counter()
b = Counter()
print(a.count, b.count, Counter.count)
```

Output: `2 2 2`.

[↑ Back to TOC](#table-of-contents)

## 11. Exceptions and context managers

Know `try`, `except`, `else`, `finally`, `raise`, custom exceptions, and `with`. The `else` block executes if no exception was raised in the `try` block. `finally` runs during normal cleanup and during exception propagation.

Catch specific exceptions where possible; a broad `except:` can hide bugs. A context manager, commonly used with `with open(...)`, helps release resources reliably.

```python
try:
    value = int("x")
except ValueError:
    print("invalid")
else:
    print("converted")
finally:
    print("cleanup")
```

Output:
```text
invalid
cleanup
```

[↑ Back to TOC](#table-of-contents)

## 12. Iterators, generators and decorators

An iterable can produce an iterator; an iterator provides `__iter__()` and `__next__()`. A generator function uses `yield` and resumes from its suspended state on the next iteration. Generators are lazy and can avoid storing all results at once.

A decorator takes a function (or other callable) and returns a replacement/wrapper. The `@` syntax applies a decorator when the function is defined. Learn `functools.wraps` at a basic level.

```python
def values():
    yield 1
    yield 2

g = values()
print(next(g), next(g))
```

Output: `1 2`. A further `next(g)` raises `StopIteration` unless a default is supplied.

[↑ Back to TOC](#table-of-contents)

## 13. Imports, files and common standard-library tools

Review module imports, aliases, `if __name__ == "__main__":`, file modes (`r`, `w`, `a`, `b`), and the role of `pathlib`, `collections`, `itertools`, `math`, `random`, `json`, and `datetime`.

- `w` truncates an existing file; `a` appends.
- Text files should be opened with an intentional encoding, commonly UTF-8.
- Use `with` to manage file lifetime.
- `json.loads` parses a JSON string; `json.dumps` serializes a Python object to a JSON string.

Do not assume `random` is appropriate for security-sensitive tokens; the `secrets` module is designed for that purpose.

[↑ Back to TOC](#table-of-contents)

## 14. High-yield code-tracing traps

Before answering, check for these patterns:

1. Shared reference versus independent copy.
2. Mutation versus rebinding.
3. Mutable default arguments.
4. `is` versus `==`.
5. `list.sort()` returning `None`.
6. `and` / `or` returning operands.
7. Floor division with negative values.
8. Slice stop-exclusive behavior.
9. Loop `else` and early `break`.
10. Exception path and `finally`.
11. Generator exhaustion.
12. Dictionary key existence and `get`.
13. Shallow copy and nested mutable values.
14. Default argument evaluation time.
15. Scope and closure behavior.

[↑ Back to TOC](#table-of-contents)

## 15. Practice MCQs

Try to answer before reading the solutions.

### Q1. List aliasing

```python
a = [1, 2]
b = a
b += [3]
print(a)
```

A. `[1, 2]`  
B. `[1, 2, 3]`  
C. `[3]`  
D. Error

**Answer: B.** The list is mutated in place.

### Q2. Sorting

What does `x = [3, 1].sort()` assign to `x`?

A. `[1, 3]`  
B. `[3, 1]`  
C. `None`  
D. Error

**Answer: C.** `sort()` mutates the list and returns `None`.

### Q3. Boolean operators

What is `"A" and 0 or "B"`?

A. `True`  
B. `0`  
C. `"B"`  
D. `"A"`

**Answer: C.** `and` returns `0`; then `or` evaluates and returns `"B"`.

### Q4. Range

How many values does `list(range(2, 8, 2))` contain?

A. 2  
B. 3  
C. 4  
D. 5

**Answer: B.** The values are `2, 4, 6`.

### Q5. Input

What type does `input()` return?

A. Always integer  
B. Always float  
C. String  
D. Depends on what the user types

**Answer: C.** Convert explicitly when a numeric value is needed.

### Q6. Dictionary lookup

What happens when `d["missing"]` is used for a missing key?

A. Returns `None`  
B. Returns `False`  
C. Raises `KeyError`  
D. Inserts the key automatically

**Answer: C.**

### Q7. Function defaults

When is a normal default argument expression evaluated?

A. Each call  
B. When the function definition executes  
C. Only on the second call  
D. When the function returns

**Answer: B.**

### Q8. Identity

Which expression is the idiomatic way to test whether `value` is `None`?

A. `value == None`  
B. `value is None`  
C. `value equals None`  
D. `type(value) == "None"`

**Answer: B.**

### Q9. Generator

What happens after a generator is exhausted?

A. It automatically restarts  
B. It returns its first element again  
C. Further `next()` calls raise `StopIteration`  
D. It turns into a list

**Answer: C.**

### Q10. Exception flow

When does a `try`-`else` block's `else` run?

A. Always  
B. Only when the try block completes without an exception  
C. Only when an exception is raised  
D. Only after `finally`

**Answer: B.**

Record your score, then explain each answer aloud. Create at least 50 additional questions over time, including unfamiliar code snippets.

[↑ Back to TOC](#table-of-contents)

## 16. Study schedule and completion checklist

### Recommended three-week pass

- **Week 1:** syntax, types, collections, strings, operators and loops.
- **Week 2:** mutability, functions, scope, comprehensions and OOP.
- **Week 3:** exceptions, iterators/generators, imports/files, traps and timed quizzes.

### Checklist

- [ ] I can explain every core collection and when to use it.
- [ ] I can trace at least 20 snippets without executing them.
- [ ] I understand aliasing, copying, mutation and rebinding.
- [ ] I understand functions, scope and mutable defaults.
- [ ] I can explain OOP basics and method lookup.
- [ ] I can reason about exceptions and generator exhaustion.
- [ ] I scored at least 85% on two different topic quizzes.
- [ ] I reviewed and retested every logged mistake.

[↑ Back to TOC](#table-of-contents)

## References

- [Official Python Tutorial](https://docs.python.org/3/tutorial/)
- [Python built-in functions](https://docs.python.org/3/library/functions.html)
- [Python data model](https://docs.python.org/3/reference/datamodel.html)
- [Python standard library](https://docs.python.org/3/library/)
- [Python FAQs](https://docs.python.org/3/faq/)

[← Back to Pre-Test Roadmap](./README.md)
