# Infosys Mysore Pre-Test — SP/L1 Pass Roadmap

> Target: Clear the Infosys pre-test with a safe margin and maximize the chance of choosing a preferred stream.
>
> Candidate: Specialist Programmer (SP/L1)
>
> DOJ: 02 November 2026

## 1. Evidence status

### Official Infosys material

Infosys publicly describes the Foundation Program at the Global Education Center (GEC), Mysuru as a structured training program for fresh graduates. It combines generic IT training, problem-solving/algorithm thinking, professional skills and technology-stream training. Infosys' 2025-26 reporting says selected entry-level hires include System Engineering Trainees (SET), Digital Specialist Engineers (DSE) and Specialist Programmers (SP), and says campus hires undergo a 19–23 week in-house Foundation Program at GEC Mysore. The curriculum spans 45+ technology streams.

Infosys does not publish a single current public document that gives the exact pre-test question bank, complete blueprint, or guaranteed question count.

### Recent public candidate reports

Recent 2026 reports consistently mention:
- Java / problem solving
- DBMS / SQL
- Aptitude / quantitative + reasoning
- English / workplace or scenario-based questions

A very recent October 5, 2026 public report says the pre-test is conducted on the 5th day from joining, with a 65% passing threshold, and mentions Java, DBMS, LLD/English scenario-based questions and aptitude.

Other 2026 reports give different exact section counts and question totals. Some report 60 questions in 90 minutes; others report combinations such as 25 Java + 10 DBMS/SQL + 10 aptitude + 15 English/L&D. Because these public reports conflict, do not optimize around a single exact blueprint.

Working target: prepare for 75%+ performance even if the paper changes.

## 2. Difficulty

The exam is not best viewed as a hard competitive-programming contest. The difficulty appears to come from breadth, long Java snippets, unfamiliar wording and time pressure.

### P0 — Must be automatic

Java:
- Data types, operators, conditions, loops
- Arrays and strings
- Methods
- Classes, objects and constructors
- this, super, static, final
- Access modifiers
- Inheritance
- Overloading and overriding
- Runtime polymorphism
- Abstract classes and interfaces
- Encapsulation
- Basic exception handling
- String vs StringBuilder
- ArrayList, HashMap, HashSet
- Basic stack/queue concepts
- Pseudocode reading
- Output prediction
- Debugging / spotting errors

Problem solving:
- Arrays
- Strings
- Linked-list basics
- Stack
- Queue
- Hashing
- Sorting/searching basics
- Simple recursion
- Time-complexity intuition

DBMS / SQL:
- DBMS vs RDBMS
- Primary, candidate, super and foreign keys
- Constraints
- 1NF, 2NF, 3NF
- Transactions and ACID
- Joins
- Aggregations
- GROUP BY, HAVING, ORDER BY, DISTINCT
- CASE and NULL
- Nested queries
- String, numeric and basic date functions
- Basic DDL/DML

Aptitude / reasoning:
- Percentages
- Ratio and proportion
- Averages
- Profit/loss
- Simple interest
- Time and work
- Time, speed and distance
- Number system
- Number series
- Data interpretation
- Ranking
- Inequalities
- Logical deduction
- Data sufficiency

English / workplace scenarios:
- Sentence correction
- Grammar
- Vocabulary in context
- Reading comprehension
- Inference and sentence meaning
- Professional communication
- Workplace judgement / scenario selection

### P1 — Learn after P0

- Exceptions in more depth
- Inner/nested classes
- Linked-list implementation
- Recursion
- Normalization edge cases
- Isolation-level intuition
- Indexing basics
- EXISTS / IN variations
- Harder data interpretation
- More difficult reasoning

### P2 — Low priority before this test

Do not spend major preparation time on advanced Spring/Spring Boot, JVM internals, advanced concurrency, hard graph algorithms, hard DP or advanced system design unless Infosys specifically introduces them before your test.

## 3. How to handle long Java snippets

Recent candidates specifically report that some Java/pseudocode questions are long.

Use a structured trace:

1. Identify classes.
2. Identify fields.
3. Identify constructors.
4. Mark inheritance.
5. Mark overridden methods.
6. Mark static members.
7. Find main().
8. Trace object creation.
9. Trace method dispatch.
10. Track only variables that affect the final output.

For two- or three-class snippets, draw the inheritance chain first. Then maintain a tiny state table with step, object, method and important value.

Your training target is execution-tracing speed, not production-level Java development.

Daily target: 10–15 Java output/pseudocode questions once the foundations are covered.

## 4. Representative practice questions

These are original practice examples, not leaked Infosys questions.

### Java
1. A superclass reference points to a subclass object. Which overridden method executes and why?
2. Two objects are created from a class containing both static and instance fields. Predict the final values.
3. Trace a program where a subclass constructor calls super(), a method is overridden and an ArrayList is modified.
4. Find the output of a three-class program using private/protected/public members and inheritance.
5. Identify the compile-time error in a program involving overloading, overriding or interface implementation.

### SQL / DBMS
1. Find departments whose average salary is above the company average.
2. Find employees without a matching department using a LEFT JOIN and NULL.
3. Find the second-highest salary using a nested query.
4. Predict the result of GROUP BY with HAVING.
5. Decide which normal form is violated by a given relation.
6. Identify which ACID property is illustrated by a transaction scenario.

### Aptitude / reasoning
1. A value rises by 20% and then falls by 20%. Compare the final value with the original.
2. Solve a time-and-work question without using brute-force trial.
3. Determine what can definitely be inferred from a chain of inequalities.
4. Interpret a small table or graph quickly.
5. Determine whether provided data is sufficient to answer a question.

### English / workplace scenario
Choose the response that best balances correctness, communication, maintainability and deadline awareness in a team situation.

## 5. 30-day roadmap

### Days 1–7 — Java foundation

Day 1:
- Syntax, data types, operators, conditions, loops
- 20 output questions
- 10 small programs

Day 2:
- Arrays and strings
- 20 output questions
- 10 easy array/string problems

Day 3:
- Methods, classes, objects, constructors
- 20 tracing questions
- 10 constructor questions

Day 4:
- Encapsulation, inheritance, this, super, access modifiers
- 20 tracing questions

Day 5:
- Overloading, overriding, polymorphism, abstract class, interface
- static and final
- 25 output questions

Day 6:
- ArrayList, HashMap, HashSet
- stack/queue concepts
- exceptions
- 25 mixed Java questions

Day 7:
- 50-question Java checkpoint
- Target: 80%+

Do not move on without reviewing every wrong answer.

### Days 8–14 — DBMS + SQL

Day 8:
- Keys, constraints, normalization

Day 9:
- Transactions, ACID, indexing basics

Day 10:
- SELECT, WHERE, DISTINCT, ORDER BY, CASE, aggregates

Day 11:
- INNER JOIN and LEFT JOIN
- 25 query-writing questions

Day 12:
- Subqueries, IN, EXISTS and correlated-subquery intuition
- 20 questions

Day 13:
- String, numeric and date functions
- NULL handling
- mixed SQL

Day 14:
- 30–40 DBMS/SQL questions
- Target: 80%+

### Days 15–20 — Speed phase

Every day:
- 20–25 Java output/pseudocode questions
- 15–20 DBMS/SQL questions
- 15 aptitude/reasoning questions
- 10 English/workplace questions

Do not spend 10 minutes stuck on one Java snippet. Learn to skip and return.

### Days 21–25 — Full mixed mocks

One complete mixed mock every day under strict timing.

Review should take at least as seriously as the test itself.

For every wrong answer record:
- Topic
- Mistake type
- Why your option was wrong
- Correct rule
- One similar question

Maintain four error buckets:
- JAVA
- DBMS/SQL
- APTITUDE/REASONING
- ENGLISH/SCENARIO

Training targets:
- Day 21: 65%+
- Day 22: 68%+
- Day 23: 70%+
- Day 24: 73%+
- Day 25: 75%+

These are preparation targets, not official Infosys cutoffs.

### Days 26–27 — Final pre-joining revision

Day 26:
- Java OOP
- Long Java traces
- SQL joins and subqueries
- Aptitude formulas
- English errors

Day 27:
- One final mixed mock
- Target: 75–80%
- Review the error notebook
- No new topics

## 6. Four Mysore days before the pre-test

If the current public Day-5 pattern applies to your batch, treat the first four days as final preparation rather than a vacation.

Day 1:
- 45 min Java
- 30 min SQL/DBMS
- 15 min aptitude

Day 2:
- 45 min Java output/pseudocode
- 30 min DBMS
- 15 min English/scenarios

Day 3:
- 60 min mixed test
- Review weak areas

Day 4:
- 90 min final simulation
- Java long snippets
- SQL joins/subqueries
- Aptitude revision

Day 5:
- 30 min Java OOP review
- 20 min SQL
- 15 min aptitude
- 10 min error notebook
- Then stop studying new material

Adjust this campus plan based on the actual training timetable.

## 7. Performance gates

Use performance gates instead of blindly following calendar days.

Java:
- 80%+ on three consecutive mixed sets

DBMS/SQL:
- 80%+ on two consecutive sets

Aptitude/English:
- 75%+

Full mixed test:
- 75%+ twice
- At least one mock at 80% under time pressure

## 8. Test-day strategy

If the live instructions confirm no negative marking, attempt every question.

Suggested order:
1. Direct aptitude/English questions
2. Direct DBMS/SQL
3. Short Java
4. Long Java traces
5. Return to skipped questions
6. Final unanswered-option pass

Do not assume no-negative-marking without checking the actual instructions on your test screen.

The key skill is not reading every line of a long Java snippet. It is quickly identifying what concepts actually control the output.

## 9. Definition of done

Before the test:
- [ ] Java fundamentals complete
- [ ] Java OOP complete
- [ ] 200+ Java output/tracing questions
- [ ] 150+ SQL/DBMS questions
- [ ] 150+ aptitude/reasoning questions
- [ ] 100+ English/scenario questions
- [ ] 5+ full mixed mocks
- [ ] 2+ mocks at 75%+
- [ ] 1 mock at 80%+
- [ ] Java revision sheet
- [ ] SQL revision sheet
- [ ] Aptitude formula sheet
- [ ] Error notebook

## 10. Final target

Do not prepare to barely cross 65%.

Prepare to make 65% feel safe.

The working model is:

Java / problem solving
+
DBMS / SQL
+
Aptitude / reasoning
+
English / workplace scenarios
+
Fast objective-test execution

The goal is:

Long Java snippet → identify the relevant concepts → trace quickly → eliminate wrong options.

SQL problem → recognize joins/grouping/functions/subquery → answer immediately.

Aptitude problem → recognize the pattern → calculate efficiently.

That combination is much more realistic than trying to become an advanced Java developer or competitive programmer specifically for this exam.

## Public sources used

1. Infosys — Training at Infosys Global Education Center
https://www.infosys.com/careers/graduates/global-education-center.html

2. Infosys — ESG Report 2025-26, Digital Skilling / Foundation Program
https://www.infosys.com/about/esg/reports/2025-26/social-digital-talent.html

3. Infosys — Foundation Program overview
https://www.infosys.com/about/esg/social/employee-wellbeing/get-set-go-foundation-program.html

4. Recent 2026 public candidate reports were used only for practical estimates of pre-test timing, threshold, subject mix, question style and difficulty. They are not treated as official Infosys policy or a guaranteed question bank.

## Confidentiality rule

Do not collect, publish or use leaked Infosys internal questions, employee-only materials, candidate credentials, screenshots containing personal data, or other confidential company information. Prepare from public material and original practice questions.
