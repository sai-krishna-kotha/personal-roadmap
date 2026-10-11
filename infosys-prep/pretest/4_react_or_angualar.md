# React / Angular — Infosys SP L1 Pre-Test

[← Back to Pre-Test Roadmap](./README.md)

## Table of Contents

- [How to use this file](#how-to-use-this-file)
- [1. JavaScript foundations first](#1-javascript-foundations-first)
- [2. React: component model and JSX](#2-react-component-model-and-jsx)
- [3. React: props, state and events](#3-react-props-state-and-events)
- [4. React: rendering, keys and forms](#4-react-rendering-keys-and-forms)
- [5. React: hooks and effects](#5-react-hooks-and-effects)
- [6. React: data flow and common pitfalls](#6-react-data-flow-and-common-pitfalls)
- [7. Angular: application and component model](#7-angular-application-and-component-model)
- [8. Angular: templates and bindings](#8-angular-templates-and-bindings)
- [9. Angular: directives, pipes and forms](#9-angular-directives-pipes-and-forms)
- [10. Angular: services and dependency injection](#10-angular-services-and-dependency-injection)
- [11. Angular: lifecycle and RxJS basics](#11-angular-lifecycle-and-rxjs-basics)
- [12. React vs Angular quick comparison](#12-react-vs-angular-quick-comparison)
- [13. Practice MCQs](#13-practice-mcqs)
- [14. Study schedule and checklist](#14-study-schedule-and-checklist)
- [References](#references)

## How to use this file

Candidate reports do not establish whether your batch is assessed on React, Angular, or both. This guide gives both frameworks an initial pass so you are not caught out by uncertainty. Once official training material clarifies the stack, prioritize that framework while retaining the comparison table.

The questions here are representative practice, not verified exam questions.

## 1. JavaScript foundations first

Before framework-specific MCQs, revise:
- `const`, `let`, scope and hoisting basics;
- primitive values versus object references;
- array methods such as `map`, `filter`, `find` and `reduce`;
- destructuring, spread/rest syntax and template literals;
- function expressions, arrow functions and closures;
- promises, `async`/`await`, and error handling;
- ES modules: `import` and `export`.

```javascript
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2);
console.log(doubled);
```

Output: `[2, 4, 6]`. `map` creates a new array from callback results.

Do not confuse `map` with `forEach`: `forEach` is used for side effects and returns `undefined` in the normal case.

[↑ Back to TOC](#table-of-contents)

## 2. React: component model and JSX

React builds user interfaces from components. A function component returns React elements, often expressed using JSX. JSX resembles HTML but is JavaScript syntax with rules such as `className` instead of `class`.

```jsx
function Greeting({ name }) {
  return <h1>Hello, {name}</h1>;
}
```

Know:
- components and composition;
- JSX expressions use braces;
- components should be named with an uppercase first letter when used as JSX elements;
- a component's render result describes the UI for the current props and state;
- React uses a rendering/reconciliation process to update the UI as data changes.

**Trap:** JSX is not plain HTML and JSX attributes do not always use HTML attribute names. Keep render logic pure; avoid modifying external state during render.

[↑ Back to TOC](#table-of-contents)

## 3. React: props, state and events

**Props** are inputs passed to a component. **State** is component-managed data that can trigger a new render when updated. Do not mutate props or state directly.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <button onClick={() => setCount(c => c + 1)}>
      Count: {count}
    </button>
  );
}
```

The functional setter is useful when the next state depends on the previous state. State updates are scheduled by React; do not assume reading the state variable on the next line immediately gives the new value.

Event names use camelCase, such as `onClick`. Pass a function, e.g. `onClick={handleClick}`, rather than calling it immediately with `onClick={handleClick()}` unless an immediate call is specifically intended.

[↑ Back to TOC](#table-of-contents)

## 4. React: rendering, keys and forms

Use `map` to render arrays and supply stable keys so React can match list items between renders.

```jsx
items.map(item => <li key={item.id}>{item.name}</li>)
```

A key is a reconciliation hint and is not automatically passed as a normal prop. Prefer stable data identifiers; array indices can cause incorrect matching when a list is reordered or items are inserted/removed.

A controlled input receives its value from state and updates that state in its change handler. An uncontrolled input keeps much of its state in the DOM and may be accessed via a ref.

Conditional rendering can use `if`, ternary expressions, and logical operators. Beware of `count && <Panel />`: if `count` is zero, React can render the numeric `0` rather than render nothing.

[↑ Back to TOC](#table-of-contents)

## 5. React: hooks and effects

Hooks let function components use React features. High-yield hooks:
- `useState`: component state.
- `useEffect`: synchronize with external systems after rendering.
- `useRef`: keep a mutable reference that persists across renders without triggering a render when changed.
- `useMemo`: cache a calculated value when useful.
- `useCallback`: cache a function definition when useful.
- `useContext`: read a value from a context provider.

Hooks must be called at the top level of React function components or custom hooks, not inside loops, conditions or nested functions.

An effect may return a cleanup function. Its dependency array determines when the effect is re-synchronized; missing or incorrect dependencies can produce stale values or repeated work. Do not use an effect for every calculation—derive values during render when possible.

[↑ Back to TOC](#table-of-contents)

## 6. React: data flow and common pitfalls

- Data usually flows from parent to child through props.
- A child can notify a parent by invoking a callback passed as a prop.
- State belongs at the component that needs to coordinate the data; move it up when siblings must share it.
- Context can share values across a component subtree.
- Effects are for synchronization, such as subscriptions or browser APIs, with appropriate cleanup.

Common pitfalls:
1. Mutating an array/object in state instead of creating a new value.
2. Using an unstable key.
3. Calling an event handler during render accidentally.
4. Calling hooks conditionally.
5. Omitting required effect dependencies.
6. Assuming a state setter changes the current render's local variable immediately.
7. Treating props as mutable local state without a reasoned synchronization plan.

[↑ Back to TOC](#table-of-contents)

## 7. Angular: application and component model

Angular is a TypeScript-based web application framework. Modern Angular centers on components, templates, dependency injection, routing and reactive patterns. Different Angular versions and projects can use different configuration styles; be able to recognize the concept even when boilerplate differs.

A component connects a TypeScript class, a template and optional styles. The class holds UI logic; the template describes what is rendered. Angular's compiler/framework handles template bindings and updates.

Know the distinction:
- Component: UI unit with template and logic.
- Service: reusable class for logic/data shared across components.
- Module: a grouping mechanism in module-based applications; modern standalone components can reduce the need for NgModules.
- Router: maps URLs to views/components.

[↑ Back to TOC](#table-of-contents)

## 8. Angular: templates and bindings

Common binding styles:

- **Interpolation:** `{{ title }}` — display an expression's value as text.
- **Property binding:** `[disabled]="isSaving"` — set a DOM/component property.
- **Event binding:** `(click)="save()"` — respond to an event.
- **Two-way binding:** `[(ngModel)]="name"` where the relevant form support is imported/configured.

The “banana in a box” shorthand `[(...)]` combines a property input and matching change event convention.

Angular template syntax is not identical to React JSX. For example, React commonly uses `onClick`; Angular templates commonly use `(click)`.

[↑ Back to TOC](#table-of-contents)

## 9. Angular: directives, pipes and forms

Directives add behavior to elements or control structure:
- Attribute directives change behavior or appearance.
- Structural/control-flow syntax controls what content is rendered. Angular versions differ in support and style for built-in control flow such as `@if` / `@for` versus older structural directives.

Pipes transform values for display, such as a date or uppercase transformation. Custom pipes can be created for domain-specific formatting.

Angular forms can use template-driven or reactive forms. Reactive forms define form state and validation in TypeScript and are often a good fit for complex forms. Understand controls, validators, form groups and form submission behavior.

[↑ Back to TOC](#table-of-contents)

## 10. Angular: services and dependency injection

Dependency injection (DI) means a class receives dependencies rather than constructing every dependency directly. Angular's injector provides services according to provider configuration and scope.

```typescript
@Injectable({ providedIn: 'root' })
export class UserService {
  // shared user-related operations
}
```

A component can receive a service through constructor injection in common Angular code, or through supported injection APIs in modern Angular.

Know why services are useful: shared logic, API calls, state/data access, and testability. `providedIn: 'root'` commonly makes a service available application-wide through the root injector.

[↑ Back to TOC](#table-of-contents)

## 11. Angular: lifecycle and RxJS basics

Lifecycle hooks allow code to run at specific points in a component's lifetime. Important examples include:
- `ngOnInit`: initialization after Angular initializes data-bound properties.
- `ngOnChanges`: respond to changes in data-bound inputs.
- `ngAfterViewInit`: after component view initialization.
- `ngOnDestroy`: cleanup before destruction.

RxJS provides observables and operators for asynchronous streams. Be able to distinguish a Promise (typically one eventual result) from an Observable (a stream that can emit over time). Learn `subscribe`, `map`, `filter`, `switchMap`, and cleanup patterns at an introductory level.

Do not subscribe repeatedly in lifecycle hooks without understanding subscription lifetime. Angular provides patterns such as the async pipe and lifecycle-aware cleanup for appropriate cases.

[↑ Back to TOC](#table-of-contents)

## 12. React vs Angular quick comparison

| Concept | React | Angular |
|---|---|---|
| Main idea | UI library built around components | Full-featured application framework |
| Typical language | JavaScript or TypeScript with JSX | TypeScript and HTML-like templates |
| Inputs | Props | Input properties / bindings |
| Local UI data | State, hooks or other state solutions | Component class properties/signals and other state patterns |
| UI events | Props such as `onClick` | Template event binding such as `(click)` |
| Lifecycle/effects | Hooks such as `useEffect` | Lifecycle hooks such as `ngOnInit` / `ngOnDestroy` |
| Shared logic | Hooks, modules, context, libraries | Services and dependency injection |
| Reactive async patterns | Promises and other libraries/patterns | RxJS observables are common |
| Templates | JSX | Angular templates |

Do not say “React has no framework features” or “Angular is only a library.” The useful exam distinction is where each framework places template syntax, state/data flow, dependency injection, and application structure.

[↑ Back to TOC](#table-of-contents)

## 13. Practice MCQs

### Q1. JavaScript map

What does `[1, 2].map(n => n * 2)` return?

A. `[1, 2]`  
B. `[2, 4]`  
C. `undefined`  
D. `4`

**Answer: B.**

### Q2. React props

Which statement is best?

A. Child components should mutate props  
B. Props are inputs from a parent and should be treated as read-only  
C. Props are always numbers  
D. Props cannot contain functions

**Answer: B.**

### Q3. React state

Why might `setCount(count + 1)` be less suitable for several queued updates that each depend on the previous state?

A. It always causes a syntax error  
B. The closure can refer to a render's captured value; a functional updater expresses the dependency on previous state  
C. State setters can only accept strings  
D. It prevents rendering

**Answer: B.**

### Q4. React keys

Why are stable keys useful for list items?

A. They style the list  
B. They help React identify items across renders  
C. They are automatically passed as the `id` prop  
D. They prevent all rendering

**Answer: B.**

### Q5. React hooks

Where should hooks normally be called?

A. Inside arbitrary loops  
B. Only inside conditional branches  
C. At the top level of function components or custom hooks  
D. Inside CSS

**Answer: C.**

### Q6. Angular binding

Which syntax represents Angular event binding for a click?

A. `{{click}}`  
B. `[click]="save()"`  
C. `(click)="save()"`  
D. `onClick={save}`

**Answer: C.**

### Q7. Angular DI

What is the purpose of dependency injection?

A. Turn CSS into TypeScript  
B. Provide dependencies to a class through an injector/configuration  
C. Delete components  
D. Replace all functions

**Answer: B.**

### Q8. Angular lifecycle

Which hook is commonly used for initialization after data-bound properties are initialized?

A. `ngOnInit`  
B. `ngOnDestroy`  
C. `ngAfterViewInit` exclusively for all initialization  
D. `ngOnError`

**Answer: A.**

### Q9. React controlled input

In a controlled input, where does the displayed value come from?

A. Only the browser with no React involvement  
B. React state/props, updated via handlers  
C. A Git branch  
D. A Linux environment variable

**Answer: B.**

### Q10. Observable vs Promise

Which statement is the best general distinction?

A. A Promise commonly settles once; an Observable can emit a sequence over time  
B. They are identical  
C. Observables cannot represent async data  
D. Promises always emit infinite values

**Answer: A.**

[↑ Back to TOC](#table-of-contents)

## 14. Study schedule and checklist

### Recommended three-week pass

- **Week 1:** JavaScript refresh and React fundamentals.
- **Week 2:** React hooks/effects/list rendering and Angular components/bindings.
- **Week 3:** Angular DI/forms/lifecycle/RxJS, comparison and mixed quizzes.

### Checklist

- [ ] I can explain the JavaScript features used in UI questions.
- [ ] I can explain component, props, state and event behavior in React.
- [ ] I understand keys, controlled inputs, hooks and effect dependencies.
- [ ] I can distinguish Angular interpolation, property, event and two-way binding.
- [ ] I understand components, services, DI, pipes and directives.
- [ ] I know introductory lifecycle and Observable concepts.
- [ ] I can compare React and Angular without mixing up syntax.
- [ ] I scored at least 80% in each framework topic quiz and 85% in my target framework.
- [ ] I checked the official course platform to learn which framework is actually assessed, if specified.

[↑ Back to TOC](#table-of-contents)

## References

- [React Learn](https://react.dev/learn)
- [React reference](https://react.dev/reference/react)
- [Angular overview](https://angular.dev/overview)
- [Angular guide](https://angular.dev/guide)
- [MDN JavaScript Guide](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide)
- [MDN asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Async_JS)

[← Back to Pre-Test Roadmap](./README.md)
