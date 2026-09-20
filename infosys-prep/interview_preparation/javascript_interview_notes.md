# JavaScript Interview Notes

## Table of Contents

- [JavaScript Fundamentals](#javascript-fundamentals)
- [Runtime and Engine](#runtime-and-engine)
- [Execution Context and Call Stack](#execution-context-and-call-stack)
- [Memory and Garbage Collection](#memory-and-garbage-collection)
- [Variables and Data Types](#variables-and-data-types)
- [Coercion and Equality](#coercion-and-equality)
- [Scope, Hoisting and TDZ](#scope-hoisting-and-tdz)
- [Closures](#closures)
- [this, call, apply and bind](#this-call-apply-and-bind)
- [Arrow Functions](#arrow-functions)
- [Functions and Higher-Order Functions](#functions-and-higher-order-functions)
- [Objects](#objects)
- [Prototype Chain](#prototype-chain)
- [Classes and Inheritance](#classes-and-inheritance)
- [Destructuring, Spread and Rest](#destructuring-spread-and-rest)
- [Optional Chaining and Nullish Coalescing](#optional-chaining-and-nullish-coalescing)
- [Arrays and Array Methods](#arrays-and-array-methods)
- [Map, Set, WeakMap and WeakSet](#map-set-weakmap-and-weakset)
- [Iterators and Generators](#iterators-and-generators)
- [Promises](#promises)
- [Async and Await](#async-and-await)
- [Event Loop](#event-loop)
- [Microtasks and Tasks](#microtasks-and-tasks)
- [Timers](#timers)
- [Browser Events](#browser-events)
- [Event Bubbling, Capturing and Delegation](#event-bubbling-capturing-and-delegation)
- [DOM](#dom)
- [Fetch and AbortController](#fetch-and-abortcontroller)
- [CORS and Cookies](#cors-and-cookies)
- [Browser Storage](#browser-storage)
- [Modules](#modules)
- [ES Modules vs CommonJS](#es-modules-vs-commonjs)
- [npm, Bundlers and Babel](#npm-bundlers-and-babel)
- [Tree Shaking](#tree-shaking)
- [Immutability and Copying](#immutability-and-copying)
- [Debouncing and Throttling](#debouncing-and-throttling)
- [Functional Programming](#functional-programming)
- [Memoization](#memoization)
- [Web Workers](#web-workers)
- [Error Handling](#error-handling)
- [JSON](#json)
- [Security](#security)
- [Performance](#performance)
- [JavaScript with React](#javascript-with-react)
- [JavaScript with FastAPI](#javascript-with-fastapi)
- [JavaScript in SceneFlow](#javascript-in-sceneflow)
- [JavaScript in ScoreHub](#javascript-in-scorehub)
- [JavaScript in the URL Shortener](#javascript-in-the-url-shortener)
- [Generic Interview Q&A](#generic-interview-qa)
- [Runtime and Internals Q&A](#runtime-and-internals-qa)
- [Async JavaScript Q&A](#async-javascript-qa)
- [Objects and Prototype Q&A](#objects-and-prototype-qa)
- [Browser Q&A](#browser-qa)
- [Coding Interview Drills](#coding-interview-drills)
- [Project-Based Q&A](#project-based-qa)
- [Interview Traps](#interview-traps)
- [Final Checklist](#final-checklist)

<a id="javascript-fundamentals"></a>
## JavaScript Fundamentals

JavaScript is a dynamically typed, prototype-based language with first-class functions. ECMAScript specifies the language; browsers and Node.js provide host APIs.

Interview answer:

“JavaScript is a dynamically typed language with first-class functions, prototype-based object behavior and an event-driven concurrency model. ECMAScript defines the language, while the host environment provides APIs.”

Important distinction:

- ECMAScript = language specification.
- JavaScript engine = executes JavaScript.
- Host environment = provides APIs such as DOM, timers, fetch, filesystem APIs, etc.

<a id="runtime-and-engine"></a>
## Runtime and Engine

A simplified browser runtime model:

~~~text
JavaScript
   |
   v
JavaScript Engine
   |
   +-- Call Stack
   +-- Heap
   |
   v
Host APIs
   |
   v
Task / Microtask queues
   |
   v
Event Loop
~~~

Common engines:

- V8 — Chrome and Node.js
- SpiderMonkey — Firefox
- JavaScriptCore — Safari

A modern engine may parse source, build internal representations, execute bytecode/intermediate representations and optimize hot code with JIT techniques.

Do not answer only “JavaScript is interpreted.” Modern engines use both interpretation-like execution and compilation/optimization techniques.

<a id="execution-context-and-call-stack"></a>
## Execution Context and Call Stack

An execution context is the runtime environment in which JavaScript code executes.

Common contexts:

- global execution context
- function execution context
- eval execution context

A function call creates an execution context containing the bindings and lexical environment needed for that invocation.

The call stack tracks active execution.

~~~js
function first() {
  second();
}

function second() {
  console.log("hello");
}

first();
~~~

A stack overflow occurs when the call stack grows without returning, commonly through uncontrolled recursion.

<a id="memory-and-garbage-collection"></a>
## Memory and Garbage Collection

JavaScript automatically manages memory.

Simplified lifecycle:

~~~text
allocate → use → become unreachable → garbage collection
~~~

Garbage collection is primarily based on reachability. Do not say that an object is collected immediately when a variable goes out of scope.

Avoid the oversimplification “primitives are always on the stack and objects are always on the heap.” JavaScript engines can optimize representations internally.

Common memory-leak sources:

- forgotten event listeners
- uncleared timers
- subscriptions
- large objects retained by closures
- unbounded caches
- detached DOM structures that remain referenced

<a id="variables-and-data-types"></a>
## Variables and Data Types

Declarations:

- var
- let
- const

Use const by default and let when reassignment is required. var is function-scoped; let and const are block-scoped.

Primitive types:

- string
- number
- bigint
- boolean
- undefined
- symbol
- null

Objects are non-primitive values. Functions are callable objects.

~~~js
typeof null       // "object" - historical behavior
typeof undefined  // "undefined"
typeof function() {} // "function"
~~~

const prevents reassignment of a binding; it does not freeze an object.

<a id="coercion-and-equality"></a>
## Coercion and Equality

JavaScript performs implicit type conversion.

~~~js
"5" + 2  // "52"
"5" - 2  // 3
true + 1  // 2
~~~

Use explicit conversion when clarity matters.

Equality:

~~~js
5 == "5"   // true
5 === "5"  // false
~~~

Use strict equality === by default.

Objects compare by identity:

~~~js
{} === {}  // false
~~~

Falsy values include false, 0, -0, 0n, "", null, undefined and NaN.

Arrays and objects are truthy even when empty.

<a id="scope-hoisting-and-tdz"></a>
## Scope, Hoisting and TDZ

Scope determines where a binding can be accessed.

Main scopes:

- global
- function
- block
- module

Lexical scope is determined by where code is written.

Hoisting is an informal term for declaration/binding behavior before execution. Do not say JavaScript physically moves all declarations to the top.

~~~js
console.log(a); // undefined
var a = 10;
~~~

Function declarations can be called before their textual declaration.

let and const have a Temporal Dead Zone before initialization:

~~~js
console.log(x); // ReferenceError
let x = 10;
~~~

Classes also cannot be accessed before their initialization.

<a id="closures"></a>
## Closures

A closure is a function together with access to its surrounding lexical environment.

~~~js
function counter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const next = counter();

next(); // 1
next(); // 2
~~~

Uses:

- data privacy
- factories
- callbacks
- event handlers
- memoization
- React Hooks

<a id="this-call-apply-and-bind"></a>
## this, call, apply and bind

For ordinary functions, this is strongly affected by the call form.

~~~js
const user = {
  name: "Sai",
  greet() {
    return this.name;
  }
};

user.greet(); // "Sai"
~~~

call and apply invoke immediately with a chosen receiver.

bind returns a new function with a bound receiver and optionally bound arguments.

~~~js
function greet(city) {
  console.log(this.name, city);
}

const user = { name: "Sai" };

greet.call(user, "Kadapa");
greet.apply(user, ["Kadapa"]);

const bound = greet.bind(user, "Kadapa");
bound();
~~~

<a id="arrow-functions"></a>
## Arrow Functions

Arrow functions have lexical this. They do not create their own dynamic this.

They also do not have their own arguments object and cannot be used as constructors with new.

~~~js
const obj = {
  value: 10,
  method() {
    const inner = () => this.value;
    return inner();
  }
};
~~~

This is a major interview distinction between arrow functions and ordinary functions.

<a id="functions-and-higher-order-functions"></a>
## Functions and Higher-Order Functions

Functions are first-class values: they can be assigned, passed, returned and stored.

A higher-order function accepts a function, returns one, or both.

~~~js
function multiplyBy(factor) {
  return number => number * factor;
}

const double = multiplyBy(2);
double(5); // 10
~~~

Callbacks are functions supplied to another function to be called later or during an operation.

IIFEs are immediately invoked function expressions and were historically used for private scope before modules and block scoping.

<a id="objects"></a>
## Objects

Objects contain properties and methods.

~~~js
const user = {
  name: "Sai",
  age: 22,
  greet() {
    return "Hello " + this.name;
  }
};

user.name;
user["name"];
~~~

Know:

- computed properties
- property existence
- enumerable properties
- own vs inherited properties
- Object.keys
- Object.values
- Object.entries
- Object.assign
- Object.freeze
- Object.defineProperty
- property descriptors

Property descriptors include value, writable, enumerable, configurable, get and set.

<a id="prototype-chain"></a>
## Prototype Chain

JavaScript uses prototype-based inheritance.

~~~js
const parent = {
  greet() {
    return "hello";
  }
};

const child = Object.create(parent);

child.greet();
~~~

Property lookup first checks the object and then follows its prototype chain.

Useful APIs:

~~~js
Object.getPrototypeOf(obj);
Object.setPrototypeOf(obj, parent);
Object.create(parent);
~~~

Prefer standard prototype APIs rather than relying on the legacy __proto__ accessor.

<a id="classes-and-inheritance"></a>
## Classes and Inheritance

Classes provide syntax for constructing objects and defining methods.

~~~js
class User {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return "Hello " + this.name;
  }
}

class Admin extends User {
  deleteUser() {
    return "deleted";
  }
}
~~~

Class methods generally live on the prototype.

Know:

- constructor
- extends
- super
- static methods
- private fields
- getters/setters
- inheritance vs composition

JavaScript classes do not replace the prototype system; they are built around it.

<a id="destructuring-spread-and-rest"></a>
## Destructuring, Spread and Rest

Destructuring extracts values:

~~~js
const user = { name: "Sai", age: 22 };
const { name, age } = user;

const [first, second] = [10, 20];
~~~

Spread expands:

~~~js
const copy = { ...user };
const combined = [...a, ...b];
~~~

Rest collects:

~~~js
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}
~~~

Spread copying is shallow.

<a id="optional-chaining-and-nullish-coalescing"></a>
## Optional Chaining and Nullish Coalescing

Optional chaining safely stops when a value is nullish:

~~~js
user?.address?.city;
~~~

Nullish coalescing uses a fallback only for null or undefined:

~~~js
const name = user.name ?? "Unknown";
~~~

This differs from ||, which also treats values such as 0 and "" as false.

<a id="arrays-and-array-methods"></a>
## Arrays and Array Methods

Know mutation vs non-mutation.

Common methods:

- push, pop
- shift, unshift
- slice, splice
- map
- filter
- reduce
- find
- some
- every
- includes
- sort

~~~js
const doubled = [1, 2, 3].map(x => x * 2);

const even = [1, 2, 3, 4].filter(x => x % 2 === 0);

const total = [1, 2, 3].reduce((sum, x) => sum + x, 0);

const first = [1, 2, 3].find(x => x > 1);
~~~

Important:

- map returns a new array.
- filter returns matching elements.
- reduce accumulates a result.
- find returns the first match.
- some checks whether at least one matches.
- every checks whether all match.
- sort mutates the array and compares as strings by default.

<a id="map-set-weakmap-and-weakset"></a>
## Map, Set, WeakMap and WeakSet

Map stores key-value pairs.

Set stores unique values.

~~~js
const map = new Map();
map.set("id", 42);

const set = new Set([1, 1, 2]);
// Set contains 1 and 2
~~~

WeakMap and WeakSet use weak references for supported object keys and are not directly iterable.

Use WeakMap when metadata should not by itself keep an object alive.

<a id="iterators-and-generators"></a>
## Iterators and Generators

An iterator has next() returning an object containing value and done.

Generators use function* and yield.

~~~js
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}

const iterator = numbers();

iterator.next();
~~~

Generators are useful for lazy sequences and custom iteration.

<a id="promises"></a>
## Promises

A Promise represents eventual completion or failure.

States:

- pending
- fulfilled
- rejected

~~~js
fetch("/api/users")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
~~~

A Promise settles only once.

Important methods:

- Promise.all
- Promise.allSettled
- Promise.race
- Promise.any
- Promise.resolve
- Promise.reject

<a id="async-and-await"></a>
## Async and Await

An async function always returns a Promise.

~~~js
async function getUser() {
  const response = await fetch("/api/user");

  if (!response.ok) {
    throw new Error("Request failed");
  }

  return response.json();
}
~~~

await suspends that async function's continuation until the Promise settles. It does not block the whole JavaScript execution thread.

For independent operations:

~~~js
const [users, projects] = await Promise.all([
  getUsers(),
  getProjects()
]);
~~~

Do not write sequential awaits when operations are independent and should run concurrently.

<a id="event-loop"></a>
## Event Loop

The event loop coordinates JavaScript execution with queued asynchronous work.

~~~text
Current task
   |
   v
Call Stack
   |
   v
Microtasks
   |
   v
Next eligible task
~~~

The exact browser event-loop model is richer, but the interview rule is:

1. synchronous JavaScript runs first
2. microtasks are processed at the appropriate checkpoint
3. later tasks are selected by the host event loop

The event loop does not make CPU-heavy JavaScript automatically parallel.

<a id="microtasks-and-tasks"></a>
## Microtasks and Tasks

Promise reactions are microtasks.

Timers such as setTimeout schedule tasks.

~~~js
console.log("A");

setTimeout(() => console.log("B"), 0);

Promise.resolve().then(() => console.log("C"));

console.log("D");
~~~

Output:

~~~text
A
D
C
B
~~~

Reason:

- A and D are synchronous.
- C is a Promise microtask.
- B is a later timer task.

<a id="timers"></a>
## Timers

setTimeout(fn, 0) does not mean immediate execution.

It means the callback becomes eligible after the timer delay and after currently required work is processed.

~~~js
setTimeout(() => console.log("later"), 0);
console.log("now");
~~~

Output:

~~~text
now
later
~~~

Know setInterval, clearTimeout and clearInterval.

<a id="browser-events"></a>
## Browser Events

Events can be registered with addEventListener.

~~~js
function handler(event) {
  console.log(event.type);
}

button.addEventListener("click", handler);
button.removeEventListener("click", handler);
~~~

Removing an event listener generally requires the same function reference and compatible listener options.

<a id="event-bubbling-capturing-and-delegation"></a>
## Event Bubbling, Capturing and Delegation

Event propagation is commonly explained as:

~~~text
capture: window → document → ancestors → target
target
bubble: target → ancestors → document → window
~~~

Capture listener:

~~~js
element.addEventListener("click", handler, { capture: true });
~~~

Event delegation uses one ancestor listener:

~~~js
list.addEventListener("click", event => {
  const item = event.target.closest("[data-id]");

  if (!item) return;

  console.log(item.dataset.id);
});
~~~

Delegation is useful for dynamic lists and reducing listener count.

<a id="dom"></a>
## DOM

The DOM represents an HTML document as an object tree.

Know:

~~~js
document.querySelector(".card");
document.createElement("div");
element.appendChild(child);
element.remove();
~~~

React abstracts most direct DOM manipulation, but DOM knowledge remains important for frontend interviews.

<a id="fetch-and-abortcontroller"></a>
## Fetch and AbortController

fetch returns a Promise for a Response.

~~~js
const response = await fetch("/api/users");

if (!response.ok) {
  throw new Error("HTTP " + response.status);
}

const data = await response.json();
~~~

Important trap: HTTP 4xx/5xx responses do not automatically reject fetch. Network failures can reject it.

AbortController can cancel an abortable operation:

~~~js
const controller = new AbortController();

fetch("/api/data", {
  signal: controller.signal
});

controller.abort();
~~~

This is useful for search, component cleanup and obsolete requests.

<a id="cors-and-cookies"></a>
## CORS and Cookies

An origin is:

~~~text
scheme + host + port
~~~

For example, localhost:3000 and localhost:8000 are different origins.

CORS controls whether browser JavaScript can access cross-origin responses according to server-provided policy.

CORS is not authentication or authorization.

Cookie attributes to know:

- HttpOnly
- Secure
- SameSite
- Domain
- Path
- Max-Age
- Expires

HttpOnly prevents normal JavaScript access to the cookie.

<a id="browser-storage"></a>
## Browser Storage

Know:

- localStorage
- sessionStorage
- cookies
- IndexedDB

Web Storage values are strings:

~~~js
localStorage.setItem("theme", "dark");
const theme = localStorage.getItem("theme");
~~~

Understand the security implications before storing authentication data in browser-accessible storage.

<a id="modules"></a>
## Modules

Modules provide explicit imports/exports and scoped bindings.

~~~js
export function add(a, b) {
  return a + b;
}
~~~

~~~js
import { add } from "./math.js";
~~~

Modules improve dependency clarity and support bundler optimizations.

<a id="es-modules-vs-commonjs"></a>
## ES Modules vs CommonJS

ES Modules:

- import/export
- standard JavaScript module system
- static module structure
- native browser support
- top-level await in supported environments

CommonJS:

- require
- module.exports
- historically common in Node.js

Modern Node.js supports both, with package configuration and file extensions affecting interpretation.

<a id="npm-bundlers-and-babel"></a>
## npm, Bundlers and Babel

npm manages JavaScript packages and project scripts.

Know:

- package.json
- package-lock.json
- dependencies
- devDependencies
- npm install
- npm ci
- npm run

A bundler resolves modules and builds deployable assets. Examples include Vite, webpack, Rollup and esbuild-based tooling.

A transpiler transforms source syntax. Babel is a JavaScript transformation tool often used to transform modern syntax and JSX.

Bundler and transpiler are not synonyms.

<a id="tree-shaking"></a>
## Tree Shaking

Tree shaking removes statically unreachable exports when the module/bundler semantics allow it.

ES module static structure makes this optimization practical.

Do not claim that every unused function is always removed. Dynamic behavior, side effects and package configuration affect the result.

<a id="immutability-and-copying"></a>
## Immutability and Copying

Spread creates a shallow copy.

~~~js
const copy = { ...user };
~~~

Nested objects remain shared.

~~~js
const copy = { ...user };
copy.address.city = "X";
~~~

For supported data, structuredClone can make a deep clone:

~~~js
const deepCopy = structuredClone(user);
~~~

JSON stringify/parse is not a universal deep-cloning solution because it loses or transforms some JavaScript values.

<a id="debouncing-and-throttling"></a>
## Debouncing and Throttling

Debounce waits until calls stop for a period.

~~~js
function debounce(fn, delay) {
  let timer;

  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
~~~

Typical uses:

- search
- autosave
- resize

Throttle limits execution frequency.

Typical uses:

- scroll
- mouse movement
- resize
- high-frequency UI events

Know leading/trailing behavior for production implementations.

<a id="functional-programming"></a>
## Functional Programming

JavaScript supports:

- first-class functions
- higher-order functions
- closures
- pure functions
- immutability
- composition

Pure function:

~~~js
function add(a, b) {
  return a + b;
}
~~~

A pure function gives the same result for the same inputs and has no observable side effects.

<a id="memoization"></a>
## Memoization

Memoization caches results.

~~~js
function memoize(fn) {
  const cache = new Map();

  return function (value) {
    if (cache.has(value)) {
      return cache.get(value);
    }

    const result = fn(value);
    cache.set(value, result);
    return result;
  };
}
~~~

Discuss cache invalidation, key equality, memory growth and whether the computation is expensive enough to justify caching.

<a id="web-workers"></a>
## Web Workers

Web Workers run JavaScript in a separate worker context.

Use them for CPU-heavy browser work that would otherwise block the main UI thread.

~~~js
const worker = new Worker("worker.js");

worker.postMessage({ value: 100 });

worker.onmessage = event => {
  console.log(event.data);
};
~~~

Workers communicate through messages and do not have normal DOM access.

<a id="error-handling"></a>
## Error Handling

Synchronous:

~~~js
try {
  riskyOperation();
} catch (error) {
  console.error(error);
} finally {
  cleanup();
}
~~~

Async:

~~~js
try {
  await request();
} catch (error) {
  handle(error);
}
~~~

Custom errors:

~~~js
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}
~~~

<a id="json"></a>
## JSON

JSON is a data-interchange format, not the same thing as a JavaScript object.

~~~js
const text = JSON.stringify({ name: "Sai" });
const object = JSON.parse(text);
~~~

JSON cannot directly represent every JavaScript value.

<a id="security"></a>
## Security

Frontend interview topics:

- XSS
- CSRF
- CORS
- cookies
- token handling
- input validation
- output encoding
- Content Security Policy
- dependency security

Never rely on frontend validation for authorization. The backend must independently validate and authorize sensitive operations.

Be careful with dangerous HTML APIs such as innerHTML and React's dangerouslySetInnerHTML.

<a id="performance"></a>
## Performance

Measure before optimizing.

Common techniques:

- reduce unnecessary DOM work
- code splitting
- lazy loading
- memoization where useful
- debounce/throttle high-frequency events
- avoid unnecessary allocations in hot paths
- Web Workers for CPU-heavy browser work
- efficient network requests
- caching

For React, combine JavaScript profiling with React DevTools profiling.

<a id="javascript-with-react"></a>
## JavaScript with React

React interviews often test JavaScript directly.

Connect these concepts:

- closures → callbacks, effects and Hooks
- destructuring → props
- spread → immutable state updates
- map → rendering lists
- promises/async-await → API calls
- modules → component architecture
- event loop → asynchronous UI behavior
- debounce → search
- optional chaining → safe API data access
- higher-order functions → array methods and component patterns

Strong React preparation requires strong JavaScript fundamentals.

<a id="javascript-with-fastapi"></a>
## JavaScript with FastAPI

Typical flow:

~~~text
React/JavaScript
      ↓ fetch
HTTPS
      ↓
FastAPI
      ↓
validation/business logic
      ↓
database/external services
      ↓
JSON response
      ↓
JavaScript state/UI
~~~

Know CORS, JSON, HTTP status codes, async requests, error handling, cancellation and authentication.

<a id="javascript-in-sceneflow"></a>
## JavaScript in SceneFlow

Explain:

“I use JavaScript/React for component logic, form state, API calls, scene/image transformations, asynchronous job polling, event handling and UI state.”

Important concepts:

- promises
- async/await
- closures
- array methods
- destructuring
- immutable updates
- AbortController
- debounce/throttle
- modules

For background image search, the frontend should avoid waiting indefinitely for one synchronous request. It can track a backend job and poll or subscribe to updates.

<a id="javascript-in-scorehub"></a>
## JavaScript in ScoreHub

For live scores:

~~~text
WebSocket message
      ↓
validate/shape data
      ↓
update state
      ↓
React render
~~~

Explain that independent asynchronous events can arrive rapidly, so state updates must not accidentally overwrite newer information with stale data.

<a id="javascript-in-the-url-shortener"></a>
## JavaScript in the URL Shortener

Frontend responsibilities:

- capture URL input
- validate input
- send asynchronous request
- show loading state
- process JSON response
- display short URL
- copy to clipboard
- handle API errors

Backend remains authoritative for persistence and redirect behavior.

<a id="generic-interview-qa"></a>
## Generic Interview Q&A

### What is JavaScript?

A dynamically typed, prototype-based language with first-class functions and an event-driven concurrency model.

### Is JavaScript interpreted or compiled?

Modern engines use parsing, intermediate representations and JIT optimization. Calling JavaScript simply “interpreted” is incomplete.

### var vs let vs const?

var is function-scoped. let and const are block-scoped. const prevents reassignment of the binding, not mutation of the referenced object.

### == vs ===?

== performs coercion according to JavaScript's equality rules. === uses strict equality. Prefer === by default.

### null vs undefined?

undefined commonly represents an absent/uninitialized value; null is an explicit absence value. APIs should define which they use.

### Why is typeof null object?

Historical behavior retained for compatibility.

### What is a closure?

A function together with access to its lexical environment.

### What is hoisting?

A shorthand for declaration/binding behavior before execution. Different declarations follow different rules.

### What is TDZ?

The period before a let/const binding is initialized in which access throws a ReferenceError.

### What is this?

For ordinary functions, this depends on the call form. Arrow functions use lexical this.

### call vs apply vs bind?

call invokes with individual arguments; apply invokes with an argument collection; bind returns a new bound function.

### What is prototype inheritance?

Property lookup can continue from an object to its prototype and further up the prototype chain.

### map vs forEach?

map returns a transformed array. forEach executes a callback for each item and returns undefined.

### filter vs find?

filter returns all matches. find returns the first match.

### What does reduce do?

It accumulates a collection into a result.

### Why is sort tricky?

It mutates the array and compares values as strings by default without a comparator.

<a id="runtime-and-internals-qa"></a>
## Runtime and Internals Q&A

### What is an execution context?

The runtime environment in which JavaScript code executes.

### What is the call stack?

A stack of active execution contexts/calls.

### What is the heap?

A conceptual area used for dynamically allocated runtime data; exact implementation is engine-specific.

### What is a JavaScript engine?

Software that parses, executes and optimizes JavaScript.

### What is JIT?

Runtime compilation/optimization that can turn frequently executed code into more efficient executable representations.

### Is JavaScript single-threaded?

A given JavaScript agent normally executes JavaScript on one main thread, but browser and server environments can provide concurrency through workers and other mechanisms.

### What blocks the event loop?

Long-running synchronous JavaScript, especially CPU-heavy loops.

### How do you handle CPU-heavy browser work?

Use Web Workers or move the computation to a backend/service.

<a id="async-javascript-qa"></a>
## Async JavaScript Q&A

### Promise vs callback?

A Promise represents eventual completion/failure and supports composable async operations. A callback is a function supplied for later invocation.

### Promise states?

Pending, fulfilled and rejected.

### What does async return?

Always a Promise.

### Does await block JavaScript?

No. It suspends the async function's continuation while other JavaScript work can proceed.

### Promise.all vs Promise.allSettled?

Promise.all rejects when one input rejects; Promise.allSettled waits for every input and reports each result.

### Promise.race vs Promise.any?

race settles on the first settlement; any fulfills on the first fulfillment and rejects when all inputs reject.

### Why does Promise.then run before setTimeout?

Promise reactions are microtasks; the timer callback is a later task.

<a id="objects-and-prototype-qa"></a>
## Objects and Prototype Q&A

### What is Object.create?

It creates an object with a specified prototype.

### What is prototype on a constructor function?

It is the object used as the prototype for instances created with new by that constructor.

### What happens with new?

Conceptually, new creates an object, links its prototype, invokes the constructor with that object as this, and returns the appropriate result.

### Object.freeze vs const?

const prevents rebinding. Object.freeze prevents certain mutations to an object's own properties. freeze is shallow.

### What is a property descriptor?

Metadata controlling how a property behaves, such as writable, enumerable and configurable, or getter/setter behavior.

<a id="browser-qa"></a>
## Browser Q&A

### What is the DOM?

An object representation of a document that JavaScript can inspect and modify.

### What is event bubbling?

Propagation from the target through ancestors.

### What is event delegation?

Handling descendant events from a common ancestor listener.

### What is CORS?

A browser mechanism controlling cross-origin access based on server-provided policy.

### Is CORS authentication?

No.

### localStorage vs sessionStorage?

Both store strings. localStorage generally persists across sessions; sessionStorage is associated with a page session.

### What is HttpOnly?

A cookie attribute preventing normal JavaScript access through document.cookie.

### Why AbortController?

To cancel supported asynchronous operations such as Fetch.

<a id="coding-interview-drills"></a>
## Coding Interview Drills

### Reverse a string

~~~js
function reverseString(s) {
  return [...s].reverse().join("");
}
~~~

### Character frequency

~~~js
function frequency(s) {
  const count = new Map();

  for (const ch of s) {
    count.set(ch, (count.get(ch) || 0) + 1);
  }

  return count;
}
~~~

### Remove duplicates

~~~js
function unique(arr) {
  return [...new Set(arr)];
}
~~~

### First non-repeating character

~~~js
function firstUnique(s) {
  const count = new Map();

  for (const ch of s) {
    count.set(ch, (count.get(ch) || 0) + 1);
  }

  for (const ch of s) {
    if (count.get(ch) === 1) return ch;
  }

  return null;
}
~~~

### Debounce

~~~js
function debounce(fn, delay) {
  let timer;

  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}
~~~

### EventEmitter design

Know the basic model:

~~~text
event name → collection of listeners
on       → add listener
emit     → invoke listeners
off      → remove listener
~~~

### Promise.all design

Know the invariants:

- preserve input order
- track remaining operations
- reject when an input rejects
- fulfill after every input fulfills

<a id="project-based-qa"></a>
## Project-Based Q&A

### Why use async/await in React?

“It makes asynchronous control flow readable while still using Promises underneath. I use try/catch and explicit loading/error states.”

### Where do closures appear in React?

Event handlers, callbacks, effects and custom Hooks all rely on lexical scoping and closures.

### How would you prevent stale SceneFlow results?

“Associate responses with the current query/job, abort obsolete requests where possible, and ignore stale responses that no longer belong to the current UI state.”

### How would you handle ScoreHub WebSocket events?

“Receive the event, validate its shape at the boundary, update the relevant state and ensure rapid events do not overwrite newer state with stale data.”

### How would you optimize a large scene list?

“Measure first. Then consider stable keys, reducing expensive calculations, virtualization for very large lists, memoization where useful and avoiding unnecessary network requests.”

### Why is frontend validation not enough?

“Browser code can be bypassed. The backend must independently validate input and authorize sensitive operations.”

<a id="interview-traps"></a>
## Interview Traps

- “JavaScript is purely interpreted.”
- “Everything is passed by reference.”
- “const makes objects immutable.”
- “let and const are not hoisted.”
- “Hoisting means code is physically moved to the top.”
- “Arrow functions have their own dynamic this.”
- “== and === are the same.”
- “typeof null is null.”
- “Objects are always entirely on the heap.”
- “The event loop makes CPU-heavy code asynchronous.”
- “setTimeout(fn, 0) runs immediately.”
- “Promise callbacks are tasks/macrotasks.”
- “async/await removes Promises.”
- “fetch rejects for HTTP 404.”
- “CORS authenticates users.”
- “localStorage is automatically safe for tokens.”
- “Spread creates a deep copy.”
- “sort is non-mutating.”
- “map and forEach are identical.”
- “Classes replace prototypes.”
- “React knowledge replaces JavaScript fundamentals.”
- “Frontend validation is sufficient security.”

<a id="final-checklist"></a>
## Final Checklist

Be able to explain from memory:

- JavaScript vs ECMAScript
- runtime and host environment
- execution contexts
- call stack and heap
- engine and JIT
- var, let, const
- all data types
- primitives vs objects
- coercion and equality
- truthy/falsy
- scope and lexical scope
- closures
- hoisting and TDZ
- this
- call/apply/bind
- arrow functions
- first-class functions
- higher-order functions
- objects and descriptors
- prototype chain
- classes and inheritance
- destructuring
- spread/rest
- optional chaining/nullish coalescing
- arrays and array methods
- Map/Set/WeakMap/WeakSet
- iterators/generators
- Promises
- async/await
- event loop
- microtasks/tasks
- timers
- browser events
- bubbling/capturing/delegation
- DOM
- Fetch
- AbortController
- CORS
- cookies
- browser storage
- modules
- ESM/CommonJS
- npm
- bundlers/transpilers/Babel
- tree shaking
- garbage collection
- memory leaks
- Web Workers
- error handling
- JSON
- immutability and cloning
- debounce/throttle
- functional programming
- memoization
- security
- performance
- JavaScript + React
- JavaScript + FastAPI
- SceneFlow/ScoreHub/URL Shortener explanations
- runtime/internal questions
- async questions
- browser questions
- coding drills
- interview traps

[Back to Table of Contents](#table-of-contents)
