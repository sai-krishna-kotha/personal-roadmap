# React Interview Notes

## Table of Contents

- [React Fundamentals](#react-fundamentals)
- [Components, Props and State](#components-props-and-state)
- [JSX](#jsx)
- [Rendering and Re-rendering](#rendering-and-re-rendering)
- [React Internals](#react-internals)
- [Reconciliation and Keys](#reconciliation-and-keys)
- [Fiber and Scheduling](#fiber-and-scheduling)
- [Events and Forms](#events-and-forms)
- [Hooks](#hooks)
- [useState Deep Dive](#usestate-deep-dive)
- [useEffect Deep Dive](#useeffect-deep-dive)
- [useRef and DOM References](#useref-and-dom-references)
- [useMemo, useCallback and memo](#usememo-usecallback-and-memo)
- [useContext and State Sharing](#usecontext-and-state-sharing)
- [useReducer](#usereducer)
- [Custom Hooks](#custom-hooks)
- [Controlled vs Uncontrolled Components](#controlled-vs-uncontrolled-components)
- [Lists and Keys](#lists-and-keys)
- [Conditional Rendering](#conditional-rendering)
- [State Management Choices](#state-management-choices)
- [Context vs Redux-style Stores](#context-vs-redux-style-stores)
- [Data Fetching](#data-fetching)
- [Error Handling](#error-handling)
- [Performance](#performance)
- [React Compiler](#react-compiler)
- [Code Splitting and Lazy Loading](#code-splitting-and-lazy-loading)
- [Suspense](#suspense)
- [Portals](#portals)
- [Strict Mode](#strict-mode)
- [React Server Components and Client Components](#react-server-components-and-client-components)
- [SSR, CSR, SSG and Hydration](#ssr-csr-ssg-and-hydration)
- [React DOM and createRoot](#react-dom-and-createroot)
- [Routing](#routing)
- [Security](#security)
- [Testing](#testing)
- [Project Architecture](#project-architecture)
- [React with FastAPI](#react-with-fastapi)
- [React in SceneFlow](#react-in-sceneflow)
- [React in ScoreHub](#react-in-scorehub)
- [React in the URL Shortener](#react-in-the-url-shortener)
- [TypeScript in React](#typescript-in-react)
- [How TypeScript Is Added to React](#how-typescript-is-added-to-react)
- [TSX and JSX Compilation](#tsx-and-jsx-compilation)
- [TypeScript Configuration](#typescript-configuration)
- [Typing Props](#typing-props)
- [Typing State and Hooks](#typing-state-and-hooks)
- [Typing Events](#typing-events)
- [Typing refs](#typing-refs)
- [Typing APIs and Async Data](#typing-apis-and-async-data)
- [Typing Children and Components](#typing-children-and-components)
- [Generics in React](#generics-in-react)
- [Union, Intersection and Discriminated Union Patterns](#union-intersection-and-discriminated-union-patterns)
- [TypeScript Utility Types for React](#typescript-utility-types-for-react)
- [Type Safety vs Runtime Validation](#type-safety-vs-runtime-validation)
- [JavaScript React vs TypeScript React](#javascript-react-vs-typescript-react)
- [Generic Interview Questions and Answers](#generic-interview-questions-and-answers)
- [Internals Interview Questions and Answers](#internals-interview-questions-and-answers)
- [Hooks Interview Questions and Answers](#hooks-interview-questions-and-answers)
- [Performance Interview Questions and Answers](#performance-interview-questions-and-answers)
- [TypeScript Interview Questions and Answers](#typescript-interview-questions-and-answers)
- [Project-Based Questions and Answers](#project-based-questions-and-answers)
- [Implementation Drills](#implementation-drills)
- [Interview Traps](#interview-traps)
- [Final Checklist](#final-checklist)

React is a library for building component-based UIs. React's current documentation emphasizes components, Hooks, React DOM, Rules of React, and the React Compiler. TypeScript supports React-specific JSX and typing patterns. citeturn675000search2turn675000search5turn675000search4turn675000search1

<a id="react-fundamentals"></a>
## React Fundamentals

React lets you describe UI declaratively using reusable components. A function component receives inputs and returns JSX describing UI.

```tsx
function MyButton() {
  return <button>Save</button>;
}
```

Interview points:
- React is primarily a UI library; complete applications commonly use additional routing, data, build and server tooling.
- Declarative UI means describing the desired UI for current data rather than manually issuing every DOM mutation.
- Component composition is more important than memorizing individual APIs.

<a id="components-props-and-state"></a>
## Components, Props and State

Props are inputs supplied by a parent. State is data owned by a component that can change over time.

```tsx
type UserCardProps = {
  name: string;
  age: number;
};

function UserCard({ name, age }: UserCardProps) {
  return <p>{name} - {age}</p>;
}
```

Remember:
- Props are read-only inputs from the component's perspective.
- State is render-driving data.
- Context provides shared values without passing props through every intermediate component.
- Refs hold mutable values without causing a render when `.current` changes.

<a id="jsx"></a>
## JSX

JSX is syntax that describes UI and is transformed into JavaScript. It is not HTML executed by the browser.

```tsx
const element = <button onClick={() => alert("Hi")}>Save</button>;
```

Modern projects commonly use the automatic JSX runtime. TypeScript documents `react-jsx`, `react-jsxdev`, `preserve`, `react-native`, and classic `react` JSX modes. citeturn675000search1turn675000search9

Lowercase JSX tags such as `<div />` are intrinsic elements. Uppercase tags such as `<UserCard />` refer to component values.

<a id="rendering-and-re-rendering"></a>
## Rendering and Re-rendering

Typical mental model:

```text
state/props/context update
        ↓
React schedules work
        ↓
render phase
        ↓
reconciliation
        ↓
commit phase
        ↓
DOM/host mutations and related work
```

A re-render means React recalculates the component output. It does not mean the browser DOM is rebuilt from scratch.

<a id="react-internals"></a>
## React Internals

Interview-level internals are easiest to explain as render, reconcile, and commit.

**Render phase:** React calculates the next UI representation. Rendering should be pure.

**Reconciliation:** React determines how the previous and next element trees relate and what work can be reused.

**Commit phase:** React applies finalized changes to the host environment such as the browser DOM.

Important nuance: modern React can schedule render work so some rendering can be interrupted or reprioritized, while the commit must apply the finalized result consistently.

Do not say “the virtual DOM is the DOM copy.” A precise answer distinguishes React elements, the Fiber tree, and host DOM nodes.

<a id="reconciliation-and-keys"></a>
## Reconciliation and Keys

React uses element type and keys to preserve identity across renders.

```tsx
{items.map(item => (
  <Row key={item.id} item={item} />
))}
```

A stable key should come from logical identity. Index keys can be problematic when siblings are inserted, deleted, or reordered because the same position can refer to a different logical item.

Key is special and is not received as a normal component prop. Pass an ID separately when the child needs it.

<a id="fiber-and-scheduling"></a>
## Fiber and Scheduling

Fiber is React's internal representation of component work. A Fiber stores relationships and update-related data that let React process work incrementally.

Know these interview points:
- Fiber is not the DOM.
- Fiber is not simply another name for the virtual DOM.
- It supports incremental work and scheduling.
- Modern React uses scheduling/concurrent rendering concepts to keep urgent UI work responsive where possible.

<a id="events-and-forms"></a>
## Events and Forms

Know React event props such as `onClick`, `onChange`, and `onSubmit`.

```tsx
function SearchBox() {
  const [query, setQuery] = useState("");
  return <input value={query} onChange={e => setQuery(e.target.value)} />;
}
```

Forms interview topics:
- controlled vs uncontrolled inputs
- validation
- submit handling
- preventing default browser behavior when needed
- file inputs
- loading and error states
- async submission

<a id="hooks"></a>
## Hooks

Hooks let function components use React features such as state, effects, context and refs.

Core Hooks to know:
- `useState`
- `useEffect`
- `useContext`
- `useReducer`
- `useRef`
- `useMemo`
- `useCallback`
- `useLayoutEffect`
- custom Hooks

Rules of Hooks: call Hooks at the top level of React components or custom Hooks, not conditionally or inside loops/nested callbacks. Stable call order lets React associate Hook state with the correct call.

<a id="usestate-deep-dive"></a>
## useState Deep Dive

```tsx
const [count, setCount] = useState(0);
```

When the next state depends on the previous state, use the functional updater:

```tsx
setCount(prev => prev + 1);
```

For object state, create a new object when updating fields:

```tsx
setUser(prev => ({ ...prev, name: "Sai" }));
```

State setters schedule updates. React may batch multiple updates so several changes can be processed together efficiently.

<a id="useeffect-deep-dive"></a>
## useEffect Deep Dive

`useEffect` is primarily for synchronizing a component with an external system such as subscriptions, timers, browser APIs, or network-related effects.

```tsx
useEffect(() => {
  const id = setInterval(refreshData, 5000);
  return () => clearInterval(id);
}, []);
```

Cleanup matters for timers, subscriptions and other resources.

Do not answer “useEffect is the lifecycle method.” A better answer is: effects synchronize React with external systems after rendering.

<a id="useref-and-dom-references"></a>
## useRef and DOM References

`useRef` returns a stable mutable object whose `.current` can change without triggering a render.

```tsx
const inputRef = useRef<HTMLInputElement | null>(null);

function focusInput() {
  inputRef.current?.focus();
}
```

Common uses:
- DOM access
- storing timer IDs
- previous values
- mutable data that should not itself trigger rendering

<a id="usememo-usecallback-and-memo"></a>
## useMemo, useCallback and memo

- `useMemo` memoizes a computed value.
- `useCallback` memoizes a function reference.
- `memo` can skip some component renders when props are unchanged according to its comparison.

```tsx
const filtered = useMemo(() => items.filter(x => x.active), [items]);
const handleSave = useCallback(() => save(id), [id]);
```

These are optimizations, not correctness tools. Current React documentation notes that React Compiler can automatically memoize many values and functions. Manual memoization remains available for cases needing precise control. citeturn675000search4turn675000search6

<a id="usecontext-and-state-sharing"></a>
## useContext and State Sharing

Context lets descendants read a shared value from an ancestor provider without threading props through every intermediate component.

Typical use cases include theme, authentication information, localization and other relatively shared values.

Context is not simply “global state.” A provider update can cause consumers to render again, so scope contexts carefully.

<a id="usereducer"></a>
## useReducer

`useReducer` is useful when related state transitions are easier to express as actions.

```tsx
type State = { count: number };
type Action =
  | { type: "increment" }
  | { type: "add"; amount: number };

function reducer(state: State, action: Action): State {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    case "add": return { count: state.count + action.amount };
  }
}
```

<a id="custom-hooks"></a>
## Custom Hooks

Custom Hooks reuse stateful logic. They do not share one instance of state between components; each call has its own Hook state.

```tsx
function useDebouncedValue<T>(value: T, delay: number) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const id = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(id);
  }, [value, delay]);
  return debounced;
}
```

<a id="controlled-vs-uncontrolled-components"></a>
## Controlled vs Uncontrolled Components

**Controlled:** React state is the source of truth.

```tsx
<input value={name} onChange={e => setName(e.target.value)} />
```

**Uncontrolled:** the DOM keeps the current value and React reads it when needed, often through a ref.

Use the approach that fits the form, validation, performance, and integration requirements.

<a id="lists-and-keys"></a>
## Lists and Keys

Know how `map`, stable keys, list identity and state preservation interact.

```tsx
<ul>
{users.map(user => <li key={user.id}>{user.name}</li>)}
</ul>
```

<a id="conditional-rendering"></a>
## Conditional Rendering

Common patterns:

```tsx
{loading && <Spinner />}
{error ? <ErrorView /> : <DataView />}
{isAdmin && <AdminPanel />}
```

Be careful with truthiness. `{count && <Badge />}` can render `0` when `count` is zero.

<a id="state-management-choices"></a>
## State Management Choices

Classify state before choosing a tool:
- local UI state
- derived state
- server state
- URL state
- shared client state
- persistent state

Do not put every value into a global store.

<a id="context-vs-redux-style-stores"></a>
## Context vs Redux-style Stores

Context solves value propagation. A dedicated state library may add a state model, subscriptions, middleware, devtools and other capabilities depending on the library.

Interview answer: “Context can share values; it is not automatically a replacement for every state management solution.”

<a id="data-fetching"></a>
## Data Fetching

Typical client flow:

```text
component → request function → HTTP API → loading/error/success state → render
```

Know loading, success, empty, error, retry, cancellation, stale data, pagination, optimistic updates and cache invalidation.

<a id="error-handling"></a>
## Error Handling

Distinguish rendering errors from API/network/validation/authentication errors.

Error boundaries handle certain rendering errors in a component subtree. They are not a replacement for handling failed HTTP requests.

<a id="performance"></a>
## Performance

Typical sources of unnecessary work include expensive render calculations, unstable props, broad context updates, large lists, repeated requests and oversized bundles.

Use a measurement-first process:

```text
measure → identify bottleneck → apply targeted optimization → measure again
```

Useful tools include React DevTools and browser performance tooling.

<a id="react-compiler"></a>
## React Compiler

React Compiler is a build-time optimization tool that can automatically memoize React code based on its analysis. React's documentation recommends understanding manual `useMemo`, `useCallback`, and `memo` while allowing the compiler to handle many optimization cases. citeturn675000search6

<a id="code-splitting-and-lazy-loading"></a>
## Code Splitting and Lazy Loading

Use `lazy` and suitable bundler/framework support to load feature code when required.

```tsx
const Settings = lazy(() => import("./Settings"));
```

Benefits include smaller initial bundles and deferred loading of less-used features.

<a id="suspense"></a>
## Suspense

Suspense provides a declarative fallback boundary for supported async/lazy rendering scenarios.

```tsx
<Suspense fallback={<Spinner />}>
  <Settings />
</Suspense>
```

Do not say Suspense is only lazy loading; modern React frameworks can use it for broader rendering/data-loading patterns.

<a id="portals"></a>
## Portals

A portal renders children into another DOM node while preserving the logical React tree relationship.

Common use cases are modals, tooltips and dropdowns.

<a id="strict-mode"></a>
## Strict Mode

Strict Mode provides development-only checks. Some code may be intentionally invoked more than once in development to expose unsafe side effects. That does not mean production runs the application twice.

<a id="react-server-components-and-client-components"></a>
## React Server Components and Client Components

Server Components are part of an architecture supported by frameworks and can execute on the server. Client Components are used when browser interactivity or client-only APIs are required.

Do not equate Server Components with traditional server-side rendering; they are related but different concepts.

<a id="ssr-csr-ssg-and-hydration"></a>
## SSR, CSR, SSG and Hydration

- CSR: the browser builds the UI from client-side JavaScript.
- SSR: HTML is generated on the server for a request.
- SSG: pages are generated ahead of time.
- Hydration: client React attaches behavior to already rendered HTML.

Hydration is not simply “render the HTML again.”

<a id="react-dom-and-createroot"></a>
## React DOM and createRoot

```tsx
import { createRoot } from "react-dom/client";
import App from "./App";

const root = createRoot(document.getElementById("root")!);
root.render(<App />);
```

`react` contains core React APIs. `react-dom` provides browser DOM integration.

<a id="routing"></a>
## Routing

Client-side routing maps URL state to rendered UI.

Know route matching, nested routes, parameters, query parameters, navigation, protected routes, lazy routes and 404 handling.

<a id="security"></a>
## Security

React escapes normal text content, but application security still depends on backend authorization, secure authentication, safe token/cookie handling, validation and careful HTML handling.

`dangerouslySetInnerHTML` requires special care because it bypasses normal escaping. CORS is a browser security mechanism, not authentication.

<a id="testing"></a>
## Testing

Know unit, component/integration and end-to-end testing.

Prefer behavior-oriented tests: click a button, submit a form, render API success/failure states, and verify user-visible outcomes.

<a id="project-architecture"></a>
## Project Architecture

A practical feature-based structure:

```text
src/
  app/
  components/
  features/
  hooks/
  services/
  types/
  utils/
```

Keep UI, feature logic, API clients, stateful Hooks and shared types separated by responsibility.

<a id="react-with-fastapi"></a>
## React with FastAPI

Typical flow:

```text
React → HTTPS → FastAPI route → service layer → DB/external service → response → React state
```

Interview topics include CORS, auth, request/response schemas, loading/error states, retries/timeouts, pagination, cancellation and WebSockets.

<a id="react-in-sceneflow"></a>
## React in SceneFlow

Explain the frontend as a UI orchestration layer:

```text
project form → FastAPI call → project persisted → scenes shown
scene image search → backend job → polling/result updates → image results rendered
```

Strong discussion points: reusable components, API service modules, polling cleanup, typed models, loading/error states, stable list keys and avoiding unnecessary refetches.

<a id="react-in-scorehub"></a>
## React in ScoreHub

React can power tournament dashboards and live match views. For real-time scores, a WebSocket connection can push server events to the UI instead of continuous polling.

Frontend should update the affected state predictably when multiple score events arrive quickly.

<a id="react-in-the-url-shortener"></a>
## React in the URL Shortener

Frontend responsibilities include URL input, validation, submit/loading state, generated short URL display, copy-to-clipboard and error handling. The backend remains authoritative for persistence and redirect behavior.

<a id="typescript-in-react"></a>
## TypeScript in React

TypeScript adds static type checking to JavaScript. In React it is commonly used for props, state, events, refs, API response contracts and reusable component APIs.

Use `.ts` for TypeScript without JSX and `.tsx` for TypeScript with JSX. TypeScript's React documentation explicitly covers React and TypeScript integration. citeturn675000search0turn675000search1

<a id="how-typescript-is-added-to-react"></a>
## How TypeScript Is Added to React

Interview mental model:

```text
TS/TSX source
   ↓
type checking + JSX transform
   ↓
JavaScript
   ↓
bundler/build pipeline
   ↓
browser
```

Typical dependencies:

```bash
npm install react react-dom
npm install -D typescript @types/react @types/react-dom
```

Type annotations are a development/build-time concern. The browser executes JavaScript after the build pipeline transforms the source.

Important nuance: modern React build tools may type-check separately from the JavaScript transform; do not assume every bundler uses the TypeScript compiler for final emission.

<a id="tsx-and-jsx-compilation"></a>
## TSX and JSX Compilation

Input:

```tsx
const Button = ({ label }: { label: string }) => <button>{label}</button>;
```

For the automatic `react-jsx` mode, TypeScript can transform JSX to calls from `react/jsx-runtime`. In the classic `react` mode, JSX is transformed to `React.createElement`. The exact output depends on compiler configuration. citeturn675000search1turn675000search9

<a id="typescript-configuration"></a>
## TypeScript Configuration

Typical project configuration:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "ESNext",
    "strict": true,
    "jsx": "react-jsx",
    "moduleResolution": "Bundler",
    "noEmit": true
  }
}
```

Know `strict`, `target`, `module`, `moduleResolution`, `jsx`, `noEmit`, path aliases and library/type definitions.

<a id="typing-props"></a>
## Typing Props

```tsx
type ButtonProps = {
  label: string;
  disabled?: boolean;
  onClick: () => void;
};

function Button({ label, disabled = false, onClick }: ButtonProps) {
  return <button disabled={disabled} onClick={onClick}>{label}</button>;
}
```

Know optional properties, function props, unions, readonly properties and reusable prop types.

<a id="typing-state-and-hooks"></a>
## Typing State and Hooks

TypeScript can infer many Hook types:

```tsx
const [count, setCount] = useState(0);
const [user, setUser] = useState<User | null>(null);
const [items, setItems] = useState<Item[]>([]);
```

Use explicit generic types when the initial value does not fully express the state shape.

<a id="typing-events"></a>
## Typing Events

```tsx
function handleChange(event: React.ChangeEvent<HTMLInputElement>) {
  setValue(event.target.value);
}

function handleSubmit(event: React.FormEvent<HTMLFormElement>) {
  event.preventDefault();
}
```

Type the event according to the actual event and DOM element.

<a id="typing-refs"></a>
## Typing refs

DOM ref:

```tsx
const inputRef = useRef<HTMLInputElement | null>(null);
```

Mutable value ref:

```tsx
const requestId = useRef<number | null>(null);
```

<a id="typing-apis-and-async-data"></a>
## Typing APIs and Async Data

Define API contracts:

```tsx
type Scene = {
  id: string;
  prompt: string;
  imageUrl: string | null;
};

type SceneResponse = {
  items: Scene[];
  total: number;
};
```

Important: TypeScript does not inspect runtime network data. For untrusted external data, runtime validation should complement static types when correctness requires it.

<a id="typing-children-and-components"></a>
## Typing Children and Components

```tsx
type CardProps = {
  children: React.ReactNode;
};

function Card({ children }: CardProps) {
  return <section>{children}</section>;
}
```

`React.ReactNode` is broader than `React.ReactElement`. Know the distinction at interview level.

<a id="generics-in-react"></a>
## Generics in React

```tsx
type SelectProps<T> = {
  options: T[];
  getLabel: (item: T) => string;
  onSelect: (item: T) => void;
};

function Select<T>({ options, getLabel, onSelect }: SelectProps<T>) {
  return (
    <select>
      {options.map((item, index) => <option key={index}>{getLabel(item)}</option>)}
    </select>
  );
}
```

Generics preserve relationships between inputs and outputs without using `any`.

<a id="union-intersection-and-discriminated-union-patterns"></a>
## Union, Intersection and Discriminated Union Patterns

Union:

```ts
type Status = "idle" | "loading" | "success" | "error";
```

Discriminated union:

```ts
type State =
  | { status: "idle" }
  | { status: "loading" }
  | { status: "success"; data: Scene[] }
  | { status: "error"; message: string };
```

This pattern is excellent for UI state because the discriminator narrows which fields are available.

<a id="typescript-utility-types-for-react"></a>
## TypeScript Utility Types for React

Useful utility types:
- `Partial<T>`
- `Pick<T, K>`
- `Omit<T, K>`
- `Record<K, T>`
- `Readonly<T>`
- `ReturnType<T>`
- `Parameters<T>`
- `Awaited<T>`

<a id="type-safety-vs-runtime-validation"></a>
## Type Safety vs Runtime Validation

Interview answer: “TypeScript catches mistakes at development time. It cannot guarantee that arbitrary runtime API data matches a declared type. Runtime validation can complement static typing at system boundaries.”

<a id="javascript-react-vs-typescript-react"></a>
## JavaScript React vs TypeScript React

```jsx
function UserCard({ name }) {
  return <p>{name}</p>;
}
```

```tsx
type UserCardProps = { name: string };

function UserCard({ name }: UserCardProps) {
  return <p>{name}</p>;
}
```

The React runtime model is not fundamentally changed by using TypeScript. TypeScript improves static correctness and tooling before the browser executes JavaScript.

<a id="generic-interview-questions-and-answers"></a>
## Generic Interview Questions and Answers

### What problem does React solve?
React provides a declarative component model for interactive UIs and updates the UI when application data changes.

### What is declarative UI?
You describe what the UI should be for current state rather than manually issuing each DOM mutation.

### Why components?
They isolate UI logic, encourage composition and improve reuse.

### What causes a component to re-render?
Common triggers include its own state update, changed props, context changes, or parent rendering. Memoization can skip some work.

### Does re-render always mean DOM change?
No. React can re-run rendering while producing no host DOM mutation.

### What is lifting state up?
Move state to the nearest common ancestor so multiple children share one source of truth.

### What is prop drilling?
Passing props through intermediate components that do not otherwise need the data.

### How do you avoid prop drilling?
Use component composition, context or an appropriate state solution.

### Props vs state?
Props are external inputs; state is component-owned render-driving data.

### Why immutable state updates?
New references make state transitions predictable and allow identity-based optimizations to work correctly.

<a id="internals-interview-questions-and-answers"></a>
## Internals Interview Questions and Answers

### What happens after a state update?
React schedules work, renders the affected tree, reconciles the result and commits the needed host changes.

### What is the render phase?
React calculates the next UI representation. It should remain pure.

### What is the commit phase?
React applies finalized changes to the host environment.

### What is Fiber?
Fiber is React's internal work representation and architecture for processing component updates incrementally.

### Why Fiber?
It lets React structure, schedule and prioritize rendering work more flexibly.

### What does a key influence?
Key influences identity matching among siblings and therefore whether a component instance can be reused.

<a id="hooks-interview-questions-and-answers"></a>
## Hooks Interview Questions and Answers

### Why can't Hooks be conditional?
React relies on stable Hook call order to associate Hook state with each call.

### useState vs useReducer?
Use state for straightforward values; use a reducer when transitions are complex or naturally action-driven.

### useEffect vs event handler?
An event handler responds to an interaction. An effect synchronizes with an external system after rendering.

### useRef vs useState?
Changing a ref does not itself trigger rendering; changing state schedules an update.

### useMemo vs useCallback?
`useMemo` memoizes a value; `useCallback` memoizes a function reference.

### Is useMemo always faster?
No. It has cost and should be used when measurement and dependency behavior justify it.

### Do custom Hooks share state?
No. They share logic; each invocation has its own Hook state.

<a id="performance-interview-questions-and-answers"></a>
## Performance Interview Questions and Answers

### How do you debug unnecessary re-renders?
Measure first with React DevTools and browser profiling, then inspect state, props, context, parent renders and expensive calculations.

### How do you optimize large lists?
Use stable keys, avoid unnecessary per-row work, consider virtualization for very large lists, and measure.

### Should every child use React.memo?
No. Memoization is situational.

### How can Context hurt performance?
Provider updates can cause consumers to render, so context boundaries and provider values should be designed thoughtfully.

### What is code splitting?
Splitting application code into chunks that can be loaded when needed.

<a id="typescript-interview-questions-and-answers"></a>
## TypeScript Interview Questions and Answers

### Why TypeScript with React?
It catches incorrect props, state shapes, event usage, API assumptions and component contracts during development.

### .ts vs .tsx?
`.tsx` supports JSX; `.ts` is for TypeScript without JSX. citeturn675000search1

### Does TypeScript run in the browser?
No. The browser executes JavaScript produced by the build pipeline.

### Does TypeScript validate API JSON?
No. Declared types do not inspect runtime payloads.

### any vs unknown?
`any` disables much type checking. `unknown` requires narrowing before use.

### interface vs type?
Both describe shapes. `interface` is common for object contracts and supports declaration merging; `type` is flexible for aliases, unions and intersections.

### never vs void?
`void` usually means a function has no useful return value; `never` represents an impossible value or a function that does not successfully return.

### Why strict true?
It enables stronger checking and catches more classes of errors earlier.

### How does TypeScript understand JSX?
Through its JSX type system and React typings, combined with the configured JSX transformation mode. citeturn675000search1

<a id="project-based-questions-and-answers"></a>
## Project-Based Questions and Answers

### Explain React architecture in SceneFlow.
“I keep reusable UI, feature-specific scene/project components, API service functions, Hooks and types separated. The UI triggers FastAPI calls, tracks loading/error state, and refreshes when background jobs produce results.”

### How did you handle long-running image search?
“The frontend should not wait indefinitely for a synchronous request. The backend can create a background job, and the client can poll job state or subscribe to updates and render results when ready.”

### How do you stop polling on unmount?
Use `useEffect` cleanup to clear the timer and abort in-flight requests when appropriate.

### How does TypeScript help SceneFlow?
Typed Project, Scene, image-result, job-status, API-response and props models catch mismatches early and improve refactoring.

### How would you handle live ScoreHub updates?
Use WebSockets or another push mechanism, process events predictably, update the relevant state and render the affected UI.

### How would you structure a URL shortener frontend?
Keep URL form state local, centralize API calls, type request/response contracts, handle loading/errors explicitly, and let the backend remain authoritative for persistence and redirects.

<a id="implementation-drills"></a>
## Implementation Drills

### Counter with functional updates

```tsx
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(prev => prev + 1)}>{count}</button>;
}
```

### Debounced search

```tsx
function Search({ onSearch }: { onSearch: (q: string) => void }) {
  const [query, setQuery] = useState("");
  useEffect(() => {
    const id = setTimeout(() => onSearch(query), 300);
    return () => clearTimeout(id);
  }, [query, onSearch]);
  return <input value={query} onChange={e => setQuery(e.target.value)} />;
}
```

### Typed fetch

```tsx
type User = { id: string; name: string };

async function fetchUsers(): Promise<User[]> {
  const response = await fetch("/api/users");
  if (!response.ok) throw new Error("Request failed");
  return response.json() as Promise<User[]>;
}
```

Production discussion should add cancellation, race-condition handling, caching and retry policy.

<a id="interview-traps"></a>
## Interview Traps

- “Virtual DOM means React copies the whole DOM every time.”
- “A re-render means the whole page is redrawn.”
- “Every state update immediately mutates the DOM.”
- “useEffect is the lifecycle.”
- “useMemo always improves performance.”
- “useCallback makes a function execute faster.”
- “Context is a global state manager.”
- “Keys are only for removing warnings.”
- “Index keys are always safe.”
- “Ref changes trigger re-renders.”
- “Custom Hooks share state between components.”
- “React Compiler means memoization is obsolete.”
- “TypeScript runs in the browser.”
- “TypeScript validates API JSON at runtime.”
- “SSR and Server Components are the same thing.”
- “Suspense is only lazy loading.”
- “CORS is authentication.”

<a id="final-checklist"></a>
## Final Checklist

Be able to explain from memory:

- React and component model
- JSX and JSX transformation
- props vs state vs context vs refs
- render vs commit
- reconciliation and keys
- Fiber and scheduling
- state batching
- Hooks and Rules of Hooks
- useState / useEffect / useRef / useMemo / useCallback / useContext / useReducer
- controlled/uncontrolled forms
- state management choices
- data fetching and errors
- performance and profiling
- React Compiler
- lazy loading, Suspense and portals
- Strict Mode
- SSR / CSR / SSG / hydration
- routing and security
- testing
- React + FastAPI architecture
- SceneFlow / ScoreHub / URL Shortener frontend explanations
- TypeScript integration
- `.ts` vs `.tsx`
- JSX compiler modes
- tsconfig
- typed props/state/events/refs/API responses
- generics and discriminated unions
- utility types
- `any` vs `unknown`
- static typing vs runtime validation

## Sources

React current documentation: Quick Start, TypeScript integration, React reference and React Compiler. TypeScript documentation: React integration, JSX and TSConfig JSX options. citeturn675000search2turn675000search4turn675000search5turn675000search6turn675000search0turn675000search1turn675000search9

[Back to Table of Contents](#table-of-contents)