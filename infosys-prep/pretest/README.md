# Infosys SP L1 Pre-Test — 10-Day Sprint

> **Goal:** Maximize readiness in 10 days across Python, Linux/Unix, Git, and React/Angular. This is a focused revision and MCQ practice sprint—not an official Infosys exam blueprint.
>
> Candidate reports suggest these topics and an MCQ-style format, but exact question count, duration, framework choice, pass mark, and weightings are unconfirmed. Follow official training instructions if they differ.

## Table of Contents

- [The strategy](#the-strategy)
- [Daily time budget](#daily-time-budget)
- [10-day plan](#10-day-plan)
- [How to study each topic](#how-to-study-each-topic)
- [Question practice targets](#question-practice-targets)
- [Last 48 hours](#last-48-hours)
- [Readiness tracker](#readiness-tracker)
- [Links to subject files](#links-to-subject-files)
- [After the test: AI project](#after-the-test-ai-project)
- [Official technical references](#official-technical-references)

## The strategy

With only 10 days left, do **not** try to master every advanced feature. Cover the foundations of all four areas, practise the question patterns most likely to reveal shallow understanding, then repeatedly test yourself.

Priority order:
1. **Python:** code tracing, collections, references/mutability, functions, exceptions, OOP basics.
2. **Linux:** commands, pipes/redirection, permissions, grep/find, processes, exit codes.
3. **Git:** staging/commits, branches, fetch vs pull, merge conflicts, reset vs revert.
4. **Frontend:** JavaScript fundamentals, then React essentials and an Angular overview until official material clarifies which one is tested.

Do not spend the first several days only on Python. Broad coverage is safer when the exact subject weighting is unknown.

## Daily time budget

Aim for around **4 focused hours a day** if practical. If you have less time, preserve coverage of every subject and reduce the number of practice questions.

- 90 minutes: learn/revise the day's core topics.
- 60 minutes: hands-on practice (Python snippets, Linux terminal, Git sandbox, or frontend examples).
- 60 minutes: MCQs and explain every answer.
- 30 minutes: review yesterday's mistakes and update the error log.

Use short breaks. Protect sleep: fatigue makes code tracing and command questions much harder.

## 10-day plan

| Day | Main focus | Required output |
|---|---|---|
| 1 | Python fundamentals and collections | 30 MCQs; 15 code snippets traced by hand |
| 2 | Python traps, functions, OOP and exceptions | 35 MCQs; revisit all Day 1 mistakes |
| 3 | Linux filesystem and everyday commands | Practise 20 commands; 30 MCQs |
| 4 | Linux permissions, processes, pipes and redirection | Run examples in a safe directory; 30 MCQs |
| 5 | Git essentials: state, staging, commits, history and branches | Complete a feature-branch workflow in a sandbox; 30 MCQs |
| 6 | Git remotes, conflicts, reset/revert and recovery + mixed review | Resolve a merge conflict; 40 mixed MCQs |
| 7 | JavaScript foundations and React components, props, state, events, rendering | Trace small snippets; 35 MCQs |
| 8 | React hooks/effects and Angular components, bindings, services, DI, lifecycle | Create a one-page comparison sheet; 35 MCQs |
| 9 | Full mixed review and two timed practice blocks | 2 mixed mocks; analyse every mistake |
| 10 | Final revision and light mock | Error-log review, command sheet, one fresh mixed quiz; sleep well |

### Day 1 — Python essentials

Focus on:
- Variables, types, casting, truthiness and operators.
- Strings, slicing and common methods.
- Lists, tuples, sets, dictionaries.
- Mutation versus rebinding, aliases versus copies.
- `is` versus `==`, `sort()` versus `sorted()`, `range()`, `and`/`or`.

At the end: explain why each answer is correct. Do not only memorize the letter.

### Day 2 — Python traps

Focus on:
- Functions, positional/keyword arguments, `*args`, `**kwargs`, default argument traps.
- Scope, `lambda`, comprehensions, `enumerate`, `zip`.
- OOP basics, instance versus class attributes, inheritance and `super()`.
- Exceptions, `try/except/else/finally`, files, iterators/generators basics.

Skip deep interpreter internals unless your official module explicitly includes them.

### Day 3 — Linux basics

Focus on:
- `pwd`, `ls`, `cd`, `mkdir`, `cp`, `mv`, `rm`, `touch`.
- `cat`, `less`, `head`, `tail`, `wc`.
- Absolute/relative paths, hidden files, wildcards and quoting.
- `grep` searches content; `find` searches directory entries.

Use WSL or a Linux shell, practising only in a temporary directory.

### Day 4 — Linux operational concepts

Focus on:
- `chmod` numeric modes such as 755 and 644; read/write/execute.
- `ps`, `top`, `kill`, jobs, foreground/background, SIGTERM versus SIGKILL.
- Pipes (`|`), stdout/stderr, `>`, `>>`, `<`, `2>`, `2>&1`.
- `PATH`, `export`, `$?`, exit statuses, `df` versus `du`, basic `tar`.

Practise predicting results before running commands. Never run destructive examples outside a disposable folder.

### Day 5 — Git core

Focus on:
- Working tree versus index/staging area versus local repository versus remote.
- `init`, `clone`, `status`, `add`, `diff`, `diff --staged`, `commit`, `log`, `show`.
- Branch, HEAD, switching, merge and conflict resolution.
- Why `git commit -am` does not add untracked files.

Hands-on: make a repo, create a branch, commit changes, merge back and inspect the log.

### Day 6 — Git remote and recovery + mixed review

Focus on:
- `fetch` versus `pull` versus `push`.
- `origin/main` and remote-tracking references.
- `restore`, `reset --soft/--mixed/--hard`, `revert`, `reflog`.
- `.gitignore`, untracking with `git rm --cached`, stash basics.

Then complete a mixed quiz spanning Python, Linux and Git. Spend more review time on wrong answers than on questions answered correctly.

### Day 7 — JavaScript and React core

JavaScript:
- `const`/`let`, arrays and objects, `map`/`filter`, destructuring, spread, arrow functions, promises and async/await.

React:
- Components, JSX, props, state, event handling.
- Conditional rendering, lists and stable keys.
- Controlled inputs and parent-to-child data flow.

Trace every code snippet. Be able to explain what triggers a render and why state should not be mutated directly.

### Day 8 — React and Angular essentials

React:
- `useState`, `useEffect`, dependencies, cleanup, `useRef`, `useContext`.
- Rules of Hooks and common list/key pitfalls.

Angular:
- Components/templates, interpolation (`{{ }}`), property binding (`[prop]`), event binding (`(event)`), two-way binding.
- Directives, pipes, services, dependency injection, lifecycle hooks.
- Basic observables/RxJS and forms.

The reports do not conclusively establish whether React, Angular, or both are covered. If your official course or trainer confirms one framework, allocate roughly 70% of this day to that framework.

### Day 9 — Mixed mocks

- Take two timed mixed practice sets. Use a consistent time limit of your own choosing because the actual test duration is not verified.
- Include output questions, command selection, command effect, concept comparisons and short scenarios.
- Review all incorrect and guessed answers.
- Make a one-page sheet of Python gotchas, Linux commands/redirection, Git command distinctions and frontend concepts.

### Day 10 — Consolidate, don't cram

- Review the error log and your one-page sheets.
- Take one fresh, short mixed quiz.
- Revisit only weak concepts; avoid starting an advanced new topic.
- Confirm test access, schedule and rules using official communication.
- Eat normally and get sufficient sleep.

## How to study each topic

For every MCQ:
1. Identify what it asks: output, definition, command, side effect or comparison.
2. Predict the result before looking at options when possible.
3. Eliminate choices that contradict a language/tool rule.
4. Explain why the best option is right and each plausible distractor is wrong.
5. Write down mistakes and retest them the next day using a different example.

Error-log columns: `Day | Subject | Topic | My answer | Correct rule | Why I missed it | Review date`.

## Question practice targets

These are study targets, not official exam quantities.

- Days 1–8: target 30–40 MCQs per day plus hands-on exercises.
- Days 9–10: mixed tests, focused revision and error analysis.
- Aim for 80%+ on each subject quiz before the test, and 85%+ on mixed practice. If one subject is under 70%, give it the first study block the next day.
- Do not judge readiness by scores alone: explain concepts and solve new examples, not only familiar questions.

## Last 48 hours

- No full rewrite of notes.
- Review only the error log, command list, high-yield gotchas and framework comparison.
- Practise a small set of fresh snippets to stay sharp.
- Check official exam format and logistics. Do not assume negative marking, question count or duration without confirmation.

## Readiness tracker

- [ ] Day 1 — Python fundamentals
- [ ] Day 2 — Python traps and OOP
- [ ] Day 3 — Linux commands
- [ ] Day 4 — Linux permissions/processes/streams
- [ ] Day 5 — Git core workflow
- [ ] Day 6 — Git remote/recovery + mixed review
- [ ] Day 7 — JavaScript and React basics
- [ ] Day 8 — React hooks and Angular essentials
- [ ] Day 9 — Two mixed practice blocks
- [ ] Day 10 — Final light revision
- [ ] Reviewed every wrong/guessed answer at least once
- [ ] Verified test rules from official training communication

## Links to subject files

- [Python notes and MCQs](./1_python.md)
- [Linux / Unix notes and MCQs](./2_linux.md)
- [Git notes and MCQs](./3_git.md)
- [React / Angular notes and MCQs](./4_react_or_angualar.md)

Use the detailed files as reference. Do not attempt to read every line equally—follow the daily plan and prioritize the listed topics.

## After the test: AI project

Keep the AI project parked until the pre-test is complete. Afterwards, build an **AI Learning Companion**: upload notes, generate practice questions with explanations, track mistakes and schedule spaced repetition. A small polished project with tests and a clear README is better than beginning several large features at once.

## Official technical references

- [Python Tutorial](https://docs.python.org/3/tutorial/)
- [Linux man-pages](https://www.kernel.org/doc/man-pages/)
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/)
- [Pro Git](https://git-scm.com/book/en/v2)
- [React Learn](https://react.dev/learn)
- [Angular documentation](https://angular.dev/overview)

Candidate reports can indicate topics to review, but may refer to different batches and are not official exam specifications. Verify the actual format and scope on the Infosys learning platform or in training communication.