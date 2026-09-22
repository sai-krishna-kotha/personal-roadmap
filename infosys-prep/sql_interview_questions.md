# SQL Interview Patterns & Questions — MNC / SBC / PBC

## Table of Contents

- [1. Filtering, CASE, NULL & Basic Retrieval](#1-filtering-case-null--basic-retrieval)
  - [Q1. Employees above department average salary](#q1-employees-above-department-average-salary)
  - [Q2. Employees hired in a date range](#q2-employees-hired-in-a-date-range)
  - [Q3. NULL-safe salary classification](#q3-null-safe-salary-classification)
  - [Q4. Conditional sorting](#q4-conditional-sorting)
- [2. GROUP BY, HAVING & Aggregation](#2-group-by-having--aggregation)
  - [Q5. Department-wise employee count](#q5-department-wise-employee-count)
  - [Q6. Departments with average salary above threshold](#q6-departments-with-average-salary-above-threshold)
  - [Q7. Second highest salary](#q7-second-highest-salary)
  - [Q8. Highest and lowest salary per department](#q8-highest-and-lowest-salary-per-department)
  - [Q9. Salary contribution percentage](#q9-salary-contribution-percentage)
- [3. JOIN Patterns](#3-join-patterns)
  - [Q10. Employees with department names](#q10-employees-with-department-names)
  - [Q11. Employees without departments](#q11-employees-without-departments)
  - [Q12. Customers with no orders](#q12-customers-with-no-orders)
  - [Q13. Orders with customer and product information](#q13-orders-with-customer-and-product-information)
  - [Q14. Self join — employee and manager](#q14-self-join--employee-and-manager)
  - [Q15. Many-to-many student-course report](#q15-many-to-many-student-course-report)
- [4. Subqueries, EXISTS & Anti-JOIN](#4-subqueries-exists--anti-join)
  - [Q16. Employees earning more than company average](#q16-employees-earning-more-than-company-average)
  - [Q17. Employees earning more than their department average](#q17-employees-earning-more-than-their-department-average)
  - [Q18. Customers who placed at least one order](#q18-customers-who-placed-at-least-one-order)
  - [Q19. Customers who never ordered](#q19-customers-who-never-ordered)
  - [Q20. Products ordered by every active customer](#q20-products-ordered-by-every-active-customer)
- [5. CTE Patterns](#5-cte-patterns)
  - [Q21. Multi-step employee salary analysis](#q21-multi-step-employee-salary-analysis)
  - [Q22. Customers whose monthly spend exceeds average monthly spend](#q22-customers-whose-monthly-spend-exceeds-average-monthly-spend)
  - [Q23. Recursive CTE for employee hierarchy](#q23-recursive-cte-for-employee-hierarchy)
  - [Q24. Deduplicate records with a CTE](#q24-deduplicate-records-with-a-cte)
- [6. Window Function Patterns](#6-window-function-patterns)
  - [Q25. Rank employees by salary](#q25-rank-employees-by-salary)
  - [Q26. Department-wise top 3 salaries](#q26-department-wise-top-3-salaries)
  - [Q27. Running salary total](#q27-running-salary-total)
  - [Q28. Previous salary using LAG](#q28-previous-salary-using-lag)
  - [Q29. Salary growth percentage](#q29-salary-growth-percentage)
  - [Q30. FIRST_VALUE and LAST_VALUE](#q30-first_value-and-last_value)
  - [Q31. Compare employee salary with department average](#q31-compare-employee-salary-with-department-average)
  - [Q32. Find consecutive login days](#q32-find-consecutive-login-days)
- [7. Top-N, Nth-Highest & Per-Group Ranking](#7-top-n-nth-highest--per-group-ranking)
  - [Q33. Nth highest salary](#q33-nth-highest-salary)
  - [Q34. Highest-paid employee in each department](#q34-highest-paid-employee-in-each-department)
  - [Q35. Top 2 products by revenue in each category](#q35-top-2-products-by-revenue-in-each-category)
  - [Q36. Top 3 customers by total spend](#q36-top-3-customers-by-total-spend)
  - [Q37. Latest order for each customer](#q37-latest-order-for-each-customer)
- [8. Date & Time Patterns](#8-date--time-patterns)
  - [Q38. Orders placed in the last 30 days](#q38-orders-placed-in-the-last-30-days)
  - [Q39. Monthly revenue](#q39-monthly-revenue)
  - [Q40. Employees with work anniversaries in the current month](#q40-employees-with-work-anniversaries-in-the-current-month)
  - [Q41. Customers active in consecutive months](#q41-customers-active-in-consecutive-months)
  - [Q42. Difference between current and previous order](#q42-difference-between-current-and-previous-order)
- [9. Duplicate Detection & Data Quality](#9-duplicate-detection--data-quality)
  - [Q43. Find duplicate emails](#q43-find-duplicate-emails)
  - [Q44. Keep one row per duplicate](#q44-keep-one-row-per-duplicate)
  - [Q45. Detect impossible salary values](#q45-detect-impossible-salary-values)
  - [Q46. Find orphan foreign keys](#q46-find-orphan-foreign-keys)
- [10. Gaps & Islands](#10-gaps--islands)
  - [Q47. Consecutive attendance days](#q47-consecutive-attendance-days)
  - [Q48. Longest consecutive login streak](#q48-longest-consecutive-login-streak)
  - [Q49. Group consecutive status periods](#q49-group-consecutive-status-periods)
  - [Q50. Missing dates in a sequence](#q50-missing-dates-in-a-sequence)
- [11. Running Totals, Moving Averages & Time-Series Metrics](#11-running-totals-moving-averages--time-series-metrics)
  - [Q51. Running monthly revenue](#q51-running-monthly-revenue)
  - [Q52. 7-day moving average](#q52-7-day-moving-average)
  - [Q53. Month-over-month growth](#q53-month-over-month-growth)
  - [Q54. First and last purchase amount per customer](#q54-first-and-last-purchase-amount-per-customer)
- [12. Conditional Aggregation & Pivoting](#12-conditional-aggregation--pivoting)
  - [Q55. Male/female employee counts](#q55-malefemale-employee-counts)
  - [Q56. Revenue by payment method](#q56-revenue-by-payment-method)
  - [Q57. Pass/fail counts by subject](#q57-passfail-counts-by-subject)
  - [Q58. Pivot monthly sales into columns](#q58-pivot-monthly-sales-into-columns)
- [13. Set Operations & Relational Division](#13-set-operations--relational-division)
  - [Q59. Employees in either department set](#q59-employees-in-either-department-set)
  - [Q60. Customers in A but not B](#q60-customers-in-a-but-not-b)
  - [Q61. Products bought by all required customers](#q61-products-bought-by-all-required-customers)
  - [Q62. Common records across two systems](#q62-common-records-across-two-systems)
- [14. Recursive & Hierarchical SQL](#14-recursive--hierarchical-sql)
  - [Q63. Full employee hierarchy](#q63-full-employee-hierarchy)
  - [Q64. Count direct and indirect reports](#q64-count-direct-and-indirect-reports)
  - [Q65. Category tree path](#q65-category-tree-path)
- [15. SQL Theory Interview Patterns](#15-sql-theory-interview-patterns)
  - [Q66. WHERE vs HAVING](#q66-where-vs-having)
  - [Q67. DELETE vs TRUNCATE vs DROP](#q67-delete-vs-truncate-vs-drop)
  - [Q68. PRIMARY KEY vs UNIQUE](#q68-primary-key-vs-unique)
  - [Q69. INNER JOIN vs LEFT JOIN](#q69-inner-join-vs-left-join)
  - [Q70. UNION vs UNION ALL](#q70-union-vs-union-all)
  - [Q71. EXISTS vs IN](#q71-exists-vs-in)
  - [Q72. GROUP BY vs window functions](#q72-group-by-vs-window-functions)
  - [Q73. Composite index and column order](#q73-composite-index-and-column-order)
  - [Q74. Why indexes can hurt writes](#q74-why-indexes-can-hurt-writes)
  - [Q75. Normalization vs denormalization](#q75-normalization-vs-denormalization)
- [16. Mixed MNC-Style SQL Case Studies](#16-mixed-mnc-style-sql-case-studies)
  - [Q76. Employees earning above team average and ranked](#q76-employees-earning-above-team-average-and-ranked)
  - [Q77. Customer retention after first purchase](#q77-customer-retention-after-first-purchase)
  - [Q78. Monthly active users](#q78-monthly-active-users)
  - [Q79. Conversion from signup to purchase](#q79-conversion-from-signup-to-purchase)
  - [Q80. Highest revenue product excluding returns](#q80-highest-revenue-product-excluding-returns)
  - [Q81. Detect users with 3+ failed logins before success](#q81-detect-users-with-3-failed-logins-before-success)
  - [Q82. Inventory stockout intervals](#q82-inventory-stockout-intervals)

---

# 1. Filtering, CASE, NULL & Basic Retrieval

## Q1. Employees above department average salary

**Schema**
```text
employees(employee_id, employee_name, department_id, salary, hire_date)
departments(department_id, department_name)
```

**Question**  
Return employees whose salary is greater than the average salary of their department.

**Optimized SQL**
```sql
SELECT e.employee_id,
       e.employee_name,
       e.department_id,
       e.salary
FROM employees e
JOIN (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) d
  ON d.department_id = e.department_id
WHERE e.salary > d.avg_salary;
```

**Progression**
```text
1. Correlated subquery
2. GROUP BY department averages
3. JOIN the aggregated result back once
```

[Back to TOC](#table-of-contents)

## Q2. Employees hired in a date range

**Schema**
```text
employees(employee_id, employee_name, hire_date, salary)
```

**Question**  
Find employees hired from `2024-01-01` through `2024-12-31`, inclusive.

**Optimized SQL**
```sql
SELECT employee_id, employee_name, hire_date
FROM employees
WHERE hire_date >= DATE '2024-01-01'
  AND hire_date <  DATE '2025-01-01';
```

**Why**
Using a half-open range is safer when `hire_date` is a timestamp and avoids time-of-day boundary issues.

[Back to TOC](#table-of-contents)

## Q3. NULL-safe salary classification

**Schema**
```text
employees(employee_id, employee_name, salary)
```

**Question**  
Classify employees as `HIGH` (`>= 100000`), `MEDIUM` (`>= 60000`), `LOW`, or `UNKNOWN` for NULL salary.

**Optimized SQL**
```sql
SELECT employee_id,
       employee_name,
       CASE
           WHEN salary IS NULL THEN 'UNKNOWN'
           WHEN salary >= 100000 THEN 'HIGH'
           WHEN salary >= 60000 THEN 'MEDIUM'
           ELSE 'LOW'
       END AS salary_band
FROM employees;
```

[Back to TOC](#table-of-contents)

## Q4. Conditional sorting

**Schema**
```text
employees(employee_id, employee_name, status, salary)
```

**Question**  
Show active employees first, then inactive employees; within each group sort by salary descending.

**Optimized SQL**
```sql
SELECT employee_id, employee_name, status, salary
FROM employees
ORDER BY CASE WHEN status = 'ACTIVE' THEN 0 ELSE 1 END,
         salary DESC;
```

[Back to TOC](#table-of-contents)

---

# 2. GROUP BY, HAVING & Aggregation

## Q5. Department-wise employee count

**Schema**
```text
employees(employee_id, department_id)
departments(department_id, department_name)
```

**Question**  
Return every department and its employee count, including empty departments.

**Optimized SQL**
```sql
SELECT d.department_id,
       d.department_name,
       COUNT(e.employee_id) AS employee_count
FROM departments d
LEFT JOIN employees e
  ON e.department_id = d.department_id
GROUP BY d.department_id, d.department_name;
```

[Back to TOC](#table-of-contents)

## Q6. Departments with average salary above threshold

**Schema**
```text
employees(employee_id, department_id, salary)
```

**Question**  
Return departments whose average salary is greater than `80000`.

**Optimized SQL**
```sql
SELECT department_id,
       AVG(salary) AS avg_salary
FROM employees
GROUP BY department_id
HAVING AVG(salary) > 80000;
```

**Pattern**
```text
WHERE  -> filter rows before grouping
HAVING -> filter groups after grouping
```

[Back to TOC](#table-of-contents)

## Q7. Second highest salary

**Schema**
```text
employees(employee_id, employee_name, salary)
```

**Question**  
Return the second distinct highest salary.

**Optimized SQL**
```sql
SELECT MAX(salary) AS second_highest_salary
FROM employees
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
);
```

**Progression**
```text
MAX(MAX()) -> DISTINCT ORDER BY -> DENSE_RANK
```

For interview robustness, this solution correctly handles duplicate highest salaries.

[Back to TOC](#table-of-contents)

## Q8. Highest and lowest salary per department

**Schema**
```text
employees(employee_id, department_id, salary)
```

**Question**  
Return each department's highest and lowest salary.

**Optimized SQL**
```sql
SELECT department_id,
       MAX(salary) AS max_salary,
       MIN(salary) AS min_salary
FROM employees
GROUP BY department_id;
```

[Back to TOC](#table-of-contents)

## Q9. Salary contribution percentage

**Schema**
```text
employees(employee_id, department_id, salary)
```

**Question**  
For every employee, calculate their percentage contribution to the total company salary.

**Optimized SQL**
```sql
SELECT employee_id,
       salary,
       ROUND(
           100.0 * salary / SUM(salary) OVER (),
           2
       ) AS salary_pct
FROM employees;
```

[Back to TOC](#table-of-contents)

---

# 3. JOIN Patterns

## Q10. Employees with department names

**Schema**
```text
employees(employee_id, employee_name, department_id)
departments(department_id, department_name)
```

**Question**  
Return employee name and department name.

**Optimized SQL**
```sql
SELECT e.employee_name,
       d.department_name
FROM employees e
JOIN departments d
  ON d.department_id = e.department_id;
```

[Back to TOC](#table-of-contents)

## Q11. Employees without departments

**Schema**
```text
employees(employee_id, employee_name, department_id)
departments(department_id, department_name)
```

**Question**  
Find employees whose department reference does not match a department.

**Optimized SQL**
```sql
SELECT e.employee_id,
       e.employee_name
FROM employees e
LEFT JOIN departments d
  ON d.department_id = e.department_id
WHERE d.department_id IS NULL;
```

[Back to TOC](#table-of-contents)

## Q12. Customers with no orders

**Schema**
```text
customers(customer_id, customer_name)
orders(order_id, customer_id, order_date)
```

**Question**  
Find customers who never placed an order.

**Optimized SQL**
```sql
SELECT c.customer_id,
       c.customer_name
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id
WHERE o.customer_id IS NULL;
```

[Back to TOC](#table-of-contents)

## Q13. Orders with customer and product information

**Schema**
```text
customers(customer_id, customer_name)
orders(order_id, customer_id, order_date)
order_items(order_id, product_id, quantity, unit_price)
products(product_id, product_name)
```

**Question**  
Return order id, customer name, product name, quantity and line amount.

**Optimized SQL**
```sql
SELECT o.order_id,
       c.customer_name,
       p.product_name,
       oi.quantity,
       oi.quantity * oi.unit_price AS line_amount
FROM orders o
JOIN customers c
  ON c.customer_id = o.customer_id
JOIN order_items oi
  ON oi.order_id = o.order_id
JOIN products p
  ON p.product_id = oi.product_id;
```

[Back to TOC](#table-of-contents)

## Q14. Self join — employee and manager

**Schema**
```text
employees(employee_id, employee_name, manager_id)
```

**Question**  
Show every employee with their manager's name.

**Optimized SQL**
```sql
SELECT e.employee_name AS employee,
       m.employee_name AS manager
FROM employees e
LEFT JOIN employees m
  ON m.employee_id = e.manager_id;
```

[Back to TOC](#table-of-contents)

## Q15. Many-to-many student-course report

**Schema**
```text
students(student_id, student_name)
courses(course_id, course_name)
enrollments(student_id, course_id)
```

**Question**  
Return every student and all courses they are enrolled in.

**Optimized SQL**
```sql
SELECT s.student_name,
       c.course_name
FROM students s
JOIN enrollments e
  ON e.student_id = s.student_id
JOIN courses c
  ON c.course_id = e.course_id
ORDER BY s.student_name, c.course_name;
```

[Back to TOC](#table-of-contents)

---

# 4. Subqueries, EXISTS & Anti-JOIN

## Q16. Employees earning more than company average

**Schema**
```text
employees(employee_id, employee_name, salary)
```

**Question**  
Return employees whose salary is above the company average.

**Optimized SQL**
```sql
SELECT employee_id,
       employee_name,
       salary
FROM employees
WHERE salary > (
    SELECT AVG(salary)
    FROM employees
);
```

[Back to TOC](#table-of-contents)

## Q17. Employees earning more than their department average

**Schema**
```text
employees(employee_id, department_id, salary)
```

**Question**  
Return employees whose salary is above their own department average.

**Optimized SQL**
```sql
SELECT e.employee_id,
       e.department_id,
       e.salary
FROM employees e
JOIN (
    SELECT department_id,
           AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
) d
  ON d.department_id = e.department_id
WHERE e.salary > d.avg_salary;
```

[Back to TOC](#table-of-contents)

## Q18. Customers who placed at least one order

**Schema**
```text
customers(customer_id, customer_name)
orders(order_id, customer_id)
```

**Question**  
Return customers who have at least one order.

**Optimized SQL**
```sql
SELECT c.customer_id,
       c.customer_name
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

**Why**
`EXISTS` is directly expressing the existence test and avoids accidental row multiplication.

[Back to TOC](#table-of-contents)

## Q19. Customers who never ordered

**Schema**
```text
customers(customer_id, customer_name)
orders(order_id, customer_id)
```

**Question**  
Return customers who have never ordered.

**Optimized SQL**
```sql
SELECT c.customer_id,
       c.customer_name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

[Back to TOC](#table-of-contents)

## Q20. Products ordered by every active customer

**Schema**
```text
customers(customer_id, status)
orders(order_id, customer_id)
order_items(order_id, product_id)
products(product_id, product_name)
```

**Question**  
Find products purchased by every active customer.

**Optimized SQL**
```sql
WITH active_customers AS (
    SELECT customer_id
    FROM customers
    WHERE status = 'ACTIVE'
),
product_customers AS (
    SELECT DISTINCT o.customer_id, oi.product_id
    FROM orders o
    JOIN order_items oi
      ON oi.order_id = o.order_id
    JOIN active_customers ac
      ON ac.customer_id = o.customer_id
)
SELECT p.product_id,
       p.product_name
FROM products p
JOIN product_customers pc
  ON pc.product_id = p.product_id
GROUP BY p.product_id, p.product_name
HAVING COUNT(*) = (SELECT COUNT(*) FROM active_customers);
```

**Pattern**
```text
"for every" -> count matched entities and compare with required entity count
```

[Back to TOC](#table-of-contents)

---

# 5. CTE Patterns

## Q21. Multi-step employee salary analysis

**Schema**
```text
employees(employee_id, employee_name, department_id, salary)
departments(department_id, department_name)
```

**Question**  
Return employees whose salary is above their department average, including department name and salary difference.

**Optimized SQL**
```sql
WITH dept_avg AS (
    SELECT department_id,
           AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT e.employee_id,
       e.employee_name,
       d.department_name,
       e.salary,
       ROUND(e.salary - da.avg_salary, 2) AS above_avg_by
FROM employees e
JOIN dept_avg da
  ON da.department_id = e.department_id
JOIN departments d
  ON d.department_id = e.department_id
WHERE e.salary > da.avg_salary;
```

[Back to TOC](#table-of-contents)

## Q22. Customers whose monthly spend exceeds average monthly spend

**Schema**
```text
orders(order_id, customer_id, order_date, total_amount)
```

**Question**  
Find customer-month combinations whose spend is above the average customer-month spend for that month.

**Optimized SQL**
```sql
WITH customer_month AS (
    SELECT customer_id,
           DATE_TRUNC('month', order_date) AS month_start,
           SUM(total_amount) AS spend
    FROM orders
    GROUP BY customer_id, DATE_TRUNC('month', order_date)
),
monthly_avg AS (
    SELECT month_start,
           AVG(spend) AS avg_spend
    FROM customer_month
    GROUP BY month_start
)
SELECT cm.customer_id,
       cm.month_start,
       cm.spend
FROM customer_month cm
JOIN monthly_avg ma
  ON ma.month_start = cm.month_start
WHERE cm.spend > ma.avg_spend;
```

[Back to TOC](#table-of-contents)

## Q23. Recursive CTE for employee hierarchy

**Schema**
```text
employees(employee_id, employee_name, manager_id)
```

**Question**  
Return each employee's hierarchy level starting from top-level managers.

**Optimized SQL**
```sql
WITH RECURSIVE org AS (
    SELECT employee_id,
           employee_name,
           manager_id,
           0 AS level
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT e.employee_id,
           e.employee_name,
           e.manager_id,
           o.level + 1
    FROM employees e
    JOIN org o
      ON e.manager_id = o.employee_id
)
SELECT employee_id,
       employee_name,
       manager_id,
       level
FROM org
ORDER BY level, employee_id;
```

[Back to TOC](#table-of-contents)

## Q24. Deduplicate records with a CTE

**Schema**
```text
customers(customer_row_id, email, customer_name, updated_at)
```

**Question**  
Keep only the latest row for every email.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT customer_row_id,
           ROW_NUMBER() OVER (
               PARTITION BY email
               ORDER BY updated_at DESC, customer_row_id DESC
           ) AS rn
    FROM customers
)
SELECT customer_row_id
FROM ranked
WHERE rn = 1;
```

For a delete, use the CTE to identify `rn > 1` rows before deleting.

[Back to TOC](#table-of-contents)

---

# 6. Window Function Patterns

## Q25. Rank employees by salary

**Schema**
```text
employees(employee_id, employee_name, department_id, salary)
```

**Question**  
Rank employees by salary within each department.

**Optimized SQL**
```sql
SELECT employee_id,
       employee_name,
       department_id,
       salary,
       DENSE_RANK() OVER (
           PARTITION BY department_id
           ORDER BY salary DESC
       ) AS salary_rank
FROM employees;
```

[Back to TOC](#table-of-contents)

## Q26. Department-wise top 3 salaries

**Schema**
```text
employees(employee_id, employee_name, department_id, salary)
```

**Question**  
Return all employees whose salary is in the top 3 distinct salary levels in their department.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT employee_id,
       employee_name,
       department_id,
       salary
FROM ranked
WHERE rnk <= 3;
```

[Back to TOC](#table-of-contents)

## Q27. Running salary total

**Schema**
```text
employees(employee_id, hire_date, salary)
```

**Question**  
Calculate cumulative salary ordered by hire date.

**Optimized SQL**
```sql
SELECT employee_id,
       hire_date,
       salary,
       SUM(salary) OVER (
           ORDER BY hire_date, employee_id
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
       ) AS running_salary
FROM employees;
```

[Back to TOC](#table-of-contents)

## Q28. Previous salary using LAG

**Schema**
```text
employee_salary_history(employee_id, effective_date, salary)
```

**Question**  
For each salary record, show the previous salary for that employee.

**Optimized SQL**
```sql
SELECT employee_id,
       effective_date,
       salary,
       LAG(salary) OVER (
           PARTITION BY employee_id
           ORDER BY effective_date
       ) AS previous_salary
FROM employee_salary_history;
```

[Back to TOC](#table-of-contents)

## Q29. Salary growth percentage

**Schema**
```text
employee_salary_history(employee_id, effective_date, salary)
```

**Question**  
Calculate salary growth percentage compared with the previous salary.

**Optimized SQL**
```sql
WITH x AS (
    SELECT employee_id,
           effective_date,
           salary,
           LAG(salary) OVER (
               PARTITION BY employee_id
               ORDER BY effective_date
           ) AS previous_salary
    FROM employee_salary_history
)
SELECT employee_id,
       effective_date,
       salary,
       previous_salary,
       ROUND(
           100.0 * (salary - previous_salary) / NULLIF(previous_salary, 0),
           2
       ) AS growth_pct
FROM x;
```

[Back to TOC](#table-of-contents)

## Q30. FIRST_VALUE and LAST_VALUE

**Schema**
```text
orders(order_id, customer_id, order_date, total_amount)
```

**Question**  
For every order, show the customer's first and latest order amount.

**Optimized SQL**
```sql
SELECT order_id,
       customer_id,
       order_date,
       total_amount,
       FIRST_VALUE(total_amount) OVER (
           PARTITION BY customer_id
           ORDER BY order_date, order_id
       ) AS first_order_amount,
       FIRST_VALUE(total_amount) OVER (
           PARTITION BY customer_id
           ORDER BY order_date DESC, order_id DESC
       ) AS latest_order_amount
FROM orders;
```

[Back to TOC](#table-of-contents)

## Q31. Compare employee salary with department average

**Schema**
```text
employees(employee_id, department_id, salary)
```

**Question**  
Show salary difference from department average for every employee.

**Optimized SQL**
```sql
SELECT employee_id,
       department_id,
       salary,
       ROUND(
           salary - AVG(salary) OVER (PARTITION BY department_id),
           2
       ) AS difference_from_dept_avg
FROM employees;
```

[Back to TOC](#table-of-contents)

## Q32. Find consecutive login days

**Schema**
```text
user_logins(user_id, login_date)
```

**Question**  
Return each user with their maximum consecutive login streak.

**Optimized SQL**
```sql
WITH days AS (
    SELECT DISTINCT user_id, CAST(login_date AS DATE) AS login_day
    FROM user_logins
),
numbered AS (
    SELECT user_id,
           login_day,
           ROW_NUMBER() OVER (
               PARTITION BY user_id
               ORDER BY login_day
           ) AS rn
    FROM days
),
grouped AS (
    SELECT user_id,
           login_day,
           login_day - (rn * INTERVAL '1 day') AS grp
    FROM numbered
)
SELECT user_id,
       MAX(streak_length) AS max_streak
FROM (
    SELECT user_id,
           grp,
           COUNT(*) AS streak_length
    FROM grouped
    GROUP BY user_id, grp
) s
GROUP BY user_id;
```

**Pattern**
```text
dedupe dates -> ROW_NUMBER -> date - row_number -> GROUP BY island
```

[Back to TOC](#table-of-contents)

---

# 7. Top-N, Nth-Highest & Per-Group Ranking

## Q33. Nth highest salary

**Schema**
```text
employees(employee_id, salary)
```

**Question**  
Return the 4th highest distinct salary.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT salary,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS rnk
    FROM employees
)
SELECT MAX(salary) AS fourth_highest_salary
FROM ranked
WHERE rnk = 4;
```

**Pattern**
```text
Nth distinct value -> DENSE_RANK
Nth physical row   -> ROW_NUMBER
Top N with ties    -> DENSE_RANK / RANK
```

[Back to TOC](#table-of-contents)

## Q34. Highest-paid employee in each department

**Schema**
```text
employees(employee_id, employee_name, department_id, salary)
```

**Question**  
Return all employees tied for the highest salary in each department.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT e.*,
           DENSE_RANK() OVER (
               PARTITION BY department_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees e
)
SELECT employee_id,
       employee_name,
       department_id,
       salary
FROM ranked
WHERE rnk = 1;
```

[Back to TOC](#table-of-contents)

## Q35. Top 2 products by revenue in each category

**Schema**
```text
products(product_id, product_name, category_id)
order_items(order_id, product_id, quantity, unit_price)
```

**Question**  
Find the top 2 products by total revenue within every category.

**Optimized SQL**
```sql
WITH product_revenue AS (
    SELECT p.product_id,
           p.product_name,
           p.category_id,
           SUM(oi.quantity * oi.unit_price) AS revenue
    FROM products p
    JOIN order_items oi
      ON oi.product_id = p.product_id
    GROUP BY p.product_id, p.product_name, p.category_id
),
ranked AS (
    SELECT *,
           DENSE_RANK() OVER (
               PARTITION BY category_id
               ORDER BY revenue DESC
           ) AS rnk
    FROM product_revenue
)
SELECT product_id,
       product_name,
       category_id,
       revenue
FROM ranked
WHERE rnk <= 2;
```

[Back to TOC](#table-of-contents)

## Q36. Top 3 customers by total spend

**Schema**
```text
orders(order_id, customer_id, total_amount)
```

**Question**  
Return the top 3 customers by total spend.

**Optimized SQL**
```sql
WITH spend AS (
    SELECT customer_id,
           SUM(total_amount) AS total_spend
    FROM orders
    GROUP BY customer_id
)
SELECT customer_id,
       total_spend
FROM spend
ORDER BY total_spend DESC
FETCH FIRST 3 ROWS ONLY;
```

[Back to TOC](#table-of-contents)

## Q37. Latest order for each customer

**Schema**
```text
orders(order_id, customer_id, order_date, total_amount)
```

**Question**  
Return the latest order row for every customer.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT o.*,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date DESC, order_id DESC
           ) AS rn
    FROM orders o
)
SELECT order_id,
       customer_id,
       order_date,
       total_amount
FROM ranked
WHERE rn = 1;
```

[Back to TOC](#table-of-contents)

---

# 8. Date & Time Patterns

## Q38. Orders placed in the last 30 days

**Schema**
```text
orders(order_id, order_date, total_amount)
```

**Question**  
Find orders from the previous 30 days relative to the current timestamp.

**Optimized SQL**
```sql
SELECT order_id,
       order_date,
       total_amount
FROM orders
WHERE order_date >= CURRENT_TIMESTAMP - INTERVAL '30 days';
```

[Back to TOC](#table-of-contents)

## Q39. Monthly revenue

**Schema**
```text
orders(order_id, order_date, total_amount, status)
```

**Question**  
Calculate monthly revenue for completed orders.

**Optimized SQL**
```sql
SELECT DATE_TRUNC('month', order_date) AS month_start,
       SUM(total_amount) AS revenue
FROM orders
WHERE status = 'COMPLETED'
GROUP BY DATE_TRUNC('month', order_date)
ORDER BY month_start;
```

[Back to TOC](#table-of-contents)

## Q40. Employees with work anniversaries in the current month

**Schema**
```text
employees(employee_id, employee_name, hire_date)
```

**Question**  
Return employees whose work anniversary falls in the current month.

**Optimized SQL**
```sql
SELECT employee_id,
       employee_name,
       hire_date
FROM employees
WHERE EXTRACT(MONTH FROM hire_date) =
      EXTRACT(MONTH FROM CURRENT_DATE);
```

[Back to TOC](#table-of-contents)

## Q41. Customers active in consecutive months

**Schema**
```text
orders(order_id, customer_id, order_date)
```

**Question**  
Find customers who placed orders in at least two consecutive calendar months.

**Optimized SQL**
```sql
WITH months AS (
    SELECT DISTINCT
           customer_id,
           DATE_TRUNC('month', order_date) AS month_start
    FROM orders
),
with_prev AS (
    SELECT customer_id,
           month_start,
           LAG(month_start) OVER (
               PARTITION BY customer_id
               ORDER BY month_start
           ) AS prev_month
    FROM months
)
SELECT DISTINCT customer_id
FROM with_prev
WHERE month_start = prev_month + INTERVAL '1 month';
```

[Back to TOC](#table-of-contents)

## Q42. Difference between current and previous order

**Schema**
```text
orders(order_id, customer_id, order_date, total_amount)
```

**Question**  
For each customer, calculate the number of days since their previous order.

**Optimized SQL**
```sql
WITH x AS (
    SELECT customer_id,
           order_id,
           order_date,
           LAG(order_date) OVER (
               PARTITION BY customer_id
               ORDER BY order_date, order_id
           ) AS previous_order_date
    FROM orders
)
SELECT customer_id,
       order_id,
       order_date,
       previous_order_date,
       order_date - previous_order_date AS gap
FROM x;
```

[Back to TOC](#table-of-contents)

---

# 9. Duplicate Detection & Data Quality

## Q43. Find duplicate emails

**Schema**
```text
customers(customer_id, email)
```

**Question**  
Find emails appearing more than once.

**Optimized SQL**
```sql
SELECT email,
       COUNT(*) AS occurrences
FROM customers
GROUP BY email
HAVING COUNT(*) > 1;
```

[Back to TOC](#table-of-contents)

## Q44. Keep one row per duplicate

**Schema**
```text
customers(customer_id, email, created_at)
```

**Question**  
Identify duplicate rows while keeping the earliest record for each email.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT customer_id,
           email,
           created_at,
           ROW_NUMBER() OVER (
               PARTITION BY email
               ORDER BY created_at, customer_id
           ) AS rn
    FROM customers
)
SELECT customer_id,
       email,
       created_at
FROM ranked
WHERE rn > 1;
```

[Back to TOC](#table-of-contents)

## Q45. Detect impossible salary values

**Schema**
```text
employees(employee_id, employee_name, salary, min_salary, max_salary)
```

**Question**  
Return employees whose salary falls outside the allowed range.

**Optimized SQL**
```sql
SELECT employee_id,
       employee_name,
       salary
FROM employees
WHERE salary < min_salary
   OR salary > max_salary;
```

[Back to TOC](#table-of-contents)

## Q46. Find orphan foreign keys

**Schema**
```text
orders(order_id, customer_id)
customers(customer_id)
```

**Question**  
Find orders whose customer_id does not exist in customers.

**Optimized SQL**
```sql
SELECT o.order_id,
       o.customer_id
FROM orders o
WHERE NOT EXISTS (
    SELECT 1
    FROM customers c
    WHERE c.customer_id = o.customer_id
);
```

[Back to TOC](#table-of-contents)

---

# 10. Gaps & Islands

## Q47. Consecutive attendance days

**Schema**
```text
attendance(employee_id, attendance_date)
```

**Question**  
Find each employee's longest consecutive attendance streak.

**Optimized SQL**
```sql
WITH days AS (
    SELECT DISTINCT employee_id, attendance_date
    FROM attendance
),
numbered AS (
    SELECT employee_id,
           attendance_date,
           ROW_NUMBER() OVER (
               PARTITION BY employee_id
               ORDER BY attendance_date
           ) AS rn
    FROM days
),
islands AS (
    SELECT employee_id,
           attendance_date,
           attendance_date - (rn * INTERVAL '1 day') AS grp
    FROM numbered
)
SELECT employee_id,
       MAX(streak_length) AS longest_streak
FROM (
    SELECT employee_id,
           grp,
           COUNT(*) AS streak_length
    FROM islands
    GROUP BY employee_id, grp
) x
GROUP BY employee_id;
```

[Back to TOC](#table-of-contents)

## Q48. Longest consecutive login streak

**Schema**
```text
logins(user_id, login_date)
```

**Question**  
Return the start date, end date and length of each user's longest login streak.

**Optimized SQL**
```sql
WITH days AS (
    SELECT DISTINCT user_id, CAST(login_date AS DATE) AS d
    FROM logins
),
numbered AS (
    SELECT user_id,
           d,
           ROW_NUMBER() OVER (
               PARTITION BY user_id
               ORDER BY d
           ) AS rn
    FROM days
),
islands AS (
    SELECT user_id,
           d,
           d - (rn * INTERVAL '1 day') AS grp
    FROM numbered
),
streaks AS (
    SELECT user_id,
           MIN(d) AS start_date,
           MAX(d) AS end_date,
           COUNT(*) AS streak_length
    FROM islands
    GROUP BY user_id, grp
),
ranked AS (
    SELECT *,
           ROW_NUMBER() OVER (
               PARTITION BY user_id
               ORDER BY streak_length DESC, end_date DESC
           ) AS rn
    FROM streaks
)
SELECT user_id,
       start_date,
       end_date,
       streak_length
FROM ranked
WHERE rn = 1;
```

[Back to TOC](#table-of-contents)

## Q49. Group consecutive status periods

**Schema**
```text
device_status(device_id, status_date, status)
```

**Question**  
Compress consecutive rows with the same status into periods.

**Optimized SQL**
```sql
WITH x AS (
    SELECT device_id,
           status_date,
           status,
           CASE
               WHEN LAG(status) OVER (
                        PARTITION BY device_id
                        ORDER BY status_date
                    ) = status
               THEN 0
               ELSE 1
           END AS new_group
    FROM device_status
),
g AS (
    SELECT *,
           SUM(new_group) OVER (
               PARTITION BY device_id
               ORDER BY status_date
               ROWS UNBOUNDED PRECEDING
           ) AS grp
    FROM x
)
SELECT device_id,
       status,
       MIN(status_date) AS start_date,
       MAX(status_date) AS end_date
FROM g
GROUP BY device_id, status, grp
ORDER BY device_id, start_date;
```

[Back to TOC](#table-of-contents)

## Q50. Missing dates in a sequence

**Schema**
```text
calendar(date_value)
sales(sale_date)
```

**Question**  
Find calendar dates with no sales.

**Optimized SQL**
```sql
SELECT c.date_value
FROM calendar c
LEFT JOIN sales s
  ON s.sale_date = c.date_value
WHERE s.sale_date IS NULL
ORDER BY c.date_value;
```

[Back to TOC](#table-of-contents)

---

# 11. Running Totals, Moving Averages & Time-Series Metrics

## Q51. Running monthly revenue

**Schema**
```text
orders(order_date, total_amount, status)
```

**Question**  
Show monthly completed revenue and cumulative revenue.

**Optimized SQL**
```sql
WITH monthly AS (
    SELECT DATE_TRUNC('month', order_date) AS month_start,
           SUM(total_amount) AS revenue
    FROM orders
    WHERE status = 'COMPLETED'
    GROUP BY DATE_TRUNC('month', order_date)
)
SELECT month_start,
       revenue,
       SUM(revenue) OVER (
           ORDER BY month_start
       ) AS cumulative_revenue
FROM monthly
ORDER BY month_start;
```

[Back to TOC](#table-of-contents)

## Q52. 7-day moving average

**Schema**
```text
daily_sales(sale_date, revenue)
```

**Question**  
Calculate the 7-row moving average.

**Optimized SQL**
```sql
SELECT sale_date,
       revenue,
       AVG(revenue) OVER (
           ORDER BY sale_date
           ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
       ) AS moving_avg_7
FROM daily_sales
ORDER BY sale_date;
```

[Back to TOC](#table-of-contents)

## Q53. Month-over-month growth

**Schema**
```text
monthly_revenue(month_start, revenue)
```

**Question**  
Calculate month-over-month revenue growth percentage.

**Optimized SQL**
```sql
WITH x AS (
    SELECT month_start,
           revenue,
           LAG(revenue) OVER (
               ORDER BY month_start
           ) AS previous_revenue
    FROM monthly_revenue
)
SELECT month_start,
       revenue,
       ROUND(
           100.0 * (revenue - previous_revenue)
           / NULLIF(previous_revenue, 0),
           2
       ) AS mom_growth_pct
FROM x;
```

[Back to TOC](#table-of-contents)

## Q54. First and last purchase amount per customer

**Schema**
```text
orders(order_id, customer_id, order_date, total_amount)
```

**Question**  
Return each customer with the amount of their first and latest purchase.

**Optimized SQL**
```sql
WITH ranked AS (
    SELECT customer_id,
           order_id,
           order_date,
           total_amount,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date, order_id
           ) AS first_rn,
           ROW_NUMBER() OVER (
               PARTITION BY customer_id
               ORDER BY order_date DESC, order_id DESC
           ) AS last_rn
    FROM orders
)
SELECT customer_id,
       MAX(CASE WHEN first_rn = 1 THEN total_amount END) AS first_purchase,
       MAX(CASE WHEN last_rn = 1 THEN total_amount END) AS last_purchase
FROM ranked
GROUP BY customer_id;
```

[Back to TOC](#table-of-contents)

---

# 12. Conditional Aggregation & Pivoting

## Q55. Male/female employee counts

**Schema**
```text
employees(employee_id, gender, department_id)
```

**Question**  
Return employee counts by department split by gender.

**Optimized SQL**
```sql
SELECT department_id,
       SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS male_count,
       SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS female_count
FROM employees
GROUP BY department_id;
```

[Back to TOC](#table-of-contents)

## Q56. Revenue by payment method

**Schema**
```text
payments(payment_id, payment_method, amount, status)
```

**Question**  
Return successful revenue from card, UPI and cash as separate columns.

**Optimized SQL**
```sql
SELECT
    SUM(CASE WHEN payment_method = 'CARD' THEN amount ELSE 0 END) AS card_revenue,
    SUM(CASE WHEN payment_method = 'UPI' THEN amount ELSE 0 END) AS upi_revenue,
    SUM(CASE WHEN payment_method = 'CASH' THEN amount ELSE 0 END) AS cash_revenue
FROM payments
WHERE status = 'SUCCESS';
```

[Back to TOC](#table-of-contents)

## Q57. Pass/fail counts by subject

**Schema**
```text
results(student_id, subject, marks)
```

**Question**  
Return passed and failed student counts for every subject.

**Optimized SQL**
```sql
SELECT subject,
       SUM(CASE WHEN marks >= 40 THEN 1 ELSE 0 END) AS pass_count,
       SUM(CASE WHEN marks < 40 THEN 1 ELSE 0 END) AS fail_count
FROM results
GROUP BY subject;
```

[Back to TOC](#table-of-contents)

## Q58. Pivot monthly sales into columns

**Schema**
```text
sales(sale_date, amount)
```

**Question**  
Return annual revenue with January, February and March as separate columns.

**Optimized SQL**
```sql
SELECT EXTRACT(YEAR FROM sale_date) AS year,
       SUM(CASE WHEN EXTRACT(MONTH FROM sale_date) = 1 THEN amount ELSE 0 END) AS jan,
       SUM(CASE WHEN EXTRACT(MONTH FROM sale_date) = 2 THEN amount ELSE 0 END) AS feb,
       SUM(CASE WHEN EXTRACT(MONTH FROM sale_date) = 3 THEN amount ELSE 0 END) AS mar
FROM sales
GROUP BY EXTRACT(YEAR FROM sale_date)
ORDER BY year;
```

[Back to TOC](#table-of-contents)

---

# 13. Set Operations & Relational Division

## Q59. Employees in either department set

**Schema**
```text
employees(employee_id, employee_name, department_id)
```

**Question**  
Return employees from department 10 or department 20 without duplicates.

**Optimized SQL**
```sql
SELECT employee_id, employee_name
FROM employees
WHERE department_id = 10

UNION

SELECT employee_id, employee_name
FROM employees
WHERE department_id = 20;
```

[Back to TOC](#table-of-contents)

## Q60. Customers in A but not B

**Schema**
```text
customer_segments_a(customer_id)
customer_segments_b(customer_id)
```

**Question**  
Return customers present in A but not B.

**Optimized SQL**
```sql
SELECT customer_id
FROM customer_segments_a

EXCEPT

SELECT customer_id
FROM customer_segments_b;
```

[Back to TOC](#table-of-contents)

## Q61. Products bought by all required customers

**Schema**
```text
required_customers(customer_id)
purchases(customer_id, product_id)
products(product_id, product_name)
```

**Question**  
Find products purchased by every customer in `required_customers`.

**Optimized SQL**
```sql
SELECT p.product_id,
       p.product_name
FROM products p
JOIN purchases pu
  ON pu.product_id = p.product_id
JOIN required_customers rc
  ON rc.customer_id = pu.customer_id
GROUP BY p.product_id, p.product_name
HAVING COUNT(DISTINCT pu.customer_id) = (
    SELECT COUNT(*)
    FROM required_customers
);
```

[Back to TOC](#table-of-contents)

## Q62. Common records across two systems

**Schema**
```text
system_a_users(user_id, email)
system_b_users(user_id, email)
```

**Question**  
Find emails appearing in both systems.

**Optimized SQL**
```sql
SELECT email
FROM system_a_users

INTERSECT

SELECT email
FROM system_b_users;
```

[Back to TOC](#table-of-contents)

---

# 14. Recursive & Hierarchical SQL

## Q63. Full employee hierarchy

**Schema**
```text
employees(employee_id, employee_name, manager_id)
```

**Question**  
Return every employee with their hierarchy depth.

**Optimized SQL**
```sql
WITH RECURSIVE org AS (
    SELECT employee_id,
           employee_name,
           manager_id,
           0 AS depth
    FROM employees
    WHERE manager_id IS NULL

    UNION ALL

    SELECT e.employee_id,
           e.employee_name,
           e.manager_id,
           o.depth + 1
    FROM employees e
    JOIN org o
      ON e.manager_id = o.employee_id
)
SELECT *
FROM org
ORDER BY depth, employee_id;
```

[Back to TOC](#table-of-contents)

## Q64. Count direct and indirect reports

**Schema**
```text
employees(employee_id, employee_name, manager_id)
```

**Question**  
For each manager, count all direct and indirect reports.

**Optimized SQL**
```sql
WITH RECURSIVE hierarchy AS (
    SELECT employee_id AS manager_id,
           employee_id AS employee_id
    FROM employees

    UNION ALL

    SELECT h.manager_id,
           e.employee_id
    FROM hierarchy h
    JOIN employees e
      ON e.manager_id = h.employee_id
)
SELECT manager_id,
       COUNT(*) - 1 AS total_reports
FROM hierarchy
GROUP BY manager_id;
```

[Back to TOC](#table-of-contents)

## Q65. Category tree path

**Schema**
```text
categories(category_id, category_name, parent_id)
```

**Question**  
Build the path from root category to every category.

**Optimized SQL**
```sql
WITH RECURSIVE tree AS (
    SELECT category_id,
           category_name,
           parent_id,
           category_name AS path
    FROM categories
    WHERE parent_id IS NULL

    UNION ALL

    SELECT c.category_id,
           c.category_name,
           c.parent_id,
           t.path || ' > ' || c.category_name
    FROM categories c
    JOIN tree t
      ON c.parent_id = t.category_id
)
SELECT category_id,
       category_name,
       path
FROM tree;
```

[Back to TOC](#table-of-contents)

---

# 15. SQL Theory Interview Patterns

## Q66. WHERE vs HAVING

**Question**  
Explain the difference.

**Answer**
```text
WHERE  -> filters individual rows before GROUP BY.
HAVING -> filters grouped results after GROUP BY.
```

**Example**
```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM employees
WHERE status = 'ACTIVE'
GROUP BY department_id
HAVING AVG(salary) > 80000;
```

[Back to TOC](#table-of-contents)

## Q67. DELETE vs TRUNCATE vs DROP

**Question**  
Explain the difference.

**Answer**
```text
DELETE
- Removes selected rows.
- Supports WHERE.
- Row-by-row logging/trigger behavior depends on database.

TRUNCATE
- Removes all rows.
- No WHERE.
- Usually faster for clearing a table.
- Transaction/rollback behavior depends on DBMS.

DROP
- Removes the table object itself: data + definition.
```

[Back to TOC](#table-of-contents)

## Q68. PRIMARY KEY vs UNIQUE

**Question**  
What is the difference?

**Answer**
```text
PRIMARY KEY
- Uniquely identifies each row.
- One primary key constraint per table.
- Cannot contain NULL.

UNIQUE
- Enforces uniqueness.
- Multiple UNIQUE constraints can exist.
- NULL handling depends on DBMS.
```

[Back to TOC](#table-of-contents)

## Q69. INNER JOIN vs LEFT JOIN

**Question**  
When do you use each?

**Answer**
```text
INNER JOIN -> return only rows that match both sides.
LEFT JOIN  -> return every row from the left table plus matching rows on the right.
```

**Classic interview pattern**
```sql
-- Customers with no orders
SELECT c.customer_id
FROM customers c
LEFT JOIN orders o
  ON o.customer_id = c.customer_id
WHERE o.customer_id IS NULL;
```

[Back to TOC](#table-of-contents)

## Q70. UNION vs UNION ALL

**Question**  
What is the difference?

**Answer**
```text
UNION
- Combines result sets and removes duplicates.

UNION ALL
- Combines result sets without duplicate elimination.
- Usually cheaper because it avoids the deduplication step.
```

[Back to TOC](#table-of-contents)

## Q71. EXISTS vs IN

**Question**  
When should you prefer EXISTS?

**Answer**
```text
EXISTS checks whether at least one matching row exists.
It is particularly natural for correlated existence/anti-existence checks.
```

**Interview-safe pattern**
```sql
SELECT c.customer_id
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

[Back to TOC](#table-of-contents)

## Q72. GROUP BY vs window functions

**Question**  
Explain the difference.

**Answer**
```text
GROUP BY
- Collapses rows into groups.
- Produces one result row per group.

WINDOW FUNCTION
- Keeps the original rows.
- Calculates analytics across related rows.
```

**Example**
```sql
-- One row per department
SELECT department_id, AVG(salary)
FROM employees
GROUP BY department_id;

-- Every employee row kept
SELECT employee_id,
       salary,
       AVG(salary) OVER (PARTITION BY department_id) AS dept_avg
FROM employees;
```

[Back to TOC](#table-of-contents)

## Q73. Composite index and column order

**Question**  
Why does `(department_id, salary)` differ from `(salary, department_id)`?

**Answer**
```text
B-tree composite indexes are ordered by the leading column(s).
An index on (department_id, salary) is naturally useful for:

WHERE department_id = ?
WHERE department_id = ? AND salary > ?

But it is generally less useful for filtering only by salary.
```

**Interview point**
```text
Index column order should match common filtering, joining and ordering patterns.
```

[Back to TOC](#table-of-contents)

## Q74. Why indexes can hurt writes

**Question**  
Why not create an index on every column?

**Answer**
```text
Every INSERT, UPDATE and DELETE may need index maintenance.
More indexes mean:
- more storage
- more write work
- more memory/cache pressure
- potentially more maintenance complexity
```

[Back to TOC](#table-of-contents)

## Q75. Normalization vs denormalization

**Question**  
When is each appropriate?

**Answer**
```text
Normalization
- Reduce redundancy.
- Improve update consistency.
- Common in OLTP systems.

Denormalization
- Intentionally duplicate data to reduce joins or speed read-heavy workloads.
- Common in analytics/reporting or performance-sensitive read paths.

Interview answer:
Prefer normalized design first; denormalize for a measured workload-driven reason.
```

[Back to TOC](#table-of-contents)

---

# 16. Mixed MNC-Style SQL Case Studies

## Q76. Employees earning above team average and ranked

**Schema**
```text
employees(employee_id, employee_name, team_id, salary)
```

**Question**  
Return employees above their team average salary and rank them inside the team.

**Optimized SQL**
```sql
WITH x AS (
    SELECT employee_id,
           employee_name,
           team_id,
           salary,
           AVG(salary) OVER (
               PARTITION BY team_id
           ) AS team_avg
    FROM employees
),
ranked AS (
    SELECT *,
           DENSE_RANK() OVER (
               PARTITION BY team_id
               ORDER BY salary DESC
           ) AS salary_rank
    FROM x
)
SELECT employee_id,
       employee_name,
       team_id,
       salary,
       team_avg,
       salary_rank
FROM ranked
WHERE salary > team_avg;
```

**Pattern**
```text
analytic calculation -> window function -> filter in outer query
```

[Back to TOC](#table-of-contents)

## Q77. Customer retention after first purchase

**Schema**
```text
orders(order_id, customer_id, order_date)
```

**Question**  
For every customer, determine whether they purchased again within 30 days after their first purchase.

**Optimized SQL**
```sql
WITH first_order AS (
    SELECT customer_id,
           MIN(order_date) AS first_order_date
    FROM orders
    GROUP BY customer_id
)
SELECT f.customer_id,
       f.first_order_date,
       CASE
           WHEN EXISTS (
               SELECT 1
               FROM orders o
               WHERE o.customer_id = f.customer_id
                 AND o.order_date > f.first_order_date
                 AND o.order_date <= f.first_order_date + INTERVAL '30 days'
           )
           THEN 'RETAINED'
           ELSE 'NOT_RETAINED'
       END AS retention_status
FROM first_order f;
```

[Back to TOC](#table-of-contents)

## Q78. Monthly active users

**Schema**
```text
user_activity(user_id, activity_time)
```

**Question**  
Count distinct active users per month.

**Optimized SQL**
```sql
SELECT DATE_TRUNC('month', activity_time) AS month_start,
       COUNT(DISTINCT user_id) AS mau
FROM user_activity
GROUP BY DATE_TRUNC('month', activity_time)
ORDER BY month_start;
```

[Back to TOC](#table-of-contents)

## Q79. Conversion from signup to purchase

**Schema**
```text
users(user_id, signup_date)
orders(order_id, user_id, order_date)
```

**Question**  
For each signup month, calculate the percentage of users who made at least one purchase within 30 days.

**Optimized SQL**
```sql
WITH signups AS (
    SELECT user_id,
           DATE_TRUNC('month', signup_date) AS signup_month,
           signup_date
    FROM users
),
converted AS (
    SELECT DISTINCT s.user_id
    FROM signups s
    JOIN orders o
      ON o.user_id = s.user_id
     AND o.order_date > s.signup_date
     AND o.order_date <= s.signup_date + INTERVAL '30 days'
)
SELECT s.signup_month,
       COUNT(*) AS signups,
       COUNT(c.user_id) AS converted_users,
       ROUND(
           100.0 * COUNT(c.user_id) / NULLIF(COUNT(*), 0),
           2
       ) AS conversion_pct
FROM signups s
LEFT JOIN converted c
  ON c.user_id = s.user_id
GROUP BY s.signup_month
ORDER BY s.signup_month;
```

[Back to TOC](#table-of-contents)

## Q80. Highest revenue product excluding returns

**Schema**
```text
order_items(order_id, product_id, quantity, unit_price)
orders(order_id, status)
products(product_id, product_name)
```

**Question**  
Find the product with the highest realized revenue when returned/cancelled orders are excluded.

**Optimized SQL**
```sql
WITH revenue AS (
    SELECT oi.product_id,
           SUM(oi.quantity * oi.unit_price) AS revenue
    FROM order_items oi
    JOIN orders o
      ON o.order_id = oi.order_id
    WHERE o.status = 'COMPLETED'
    GROUP BY oi.product_id
),
ranked AS (
    SELECT *,
           DENSE_RANK() OVER (ORDER BY revenue DESC) AS rnk
    FROM revenue
)
SELECT p.product_id,
       p.product_name,
       r.revenue
FROM ranked r
JOIN products p
  ON p.product_id = r.product_id
WHERE r.rnk = 1;
```

[Back to TOC](#table-of-contents)

## Q81. Detect users with 3+ failed logins before success

**Schema**
```text
login_events(user_id, event_time, event_type)
```

**Question**  
Find login attempts where a successful login was preceded by at least 3 failed attempts.

**Optimized SQL**
```sql
WITH x AS (
    SELECT user_id,
           event_time,
           event_type,
           SUM(
               CASE WHEN event_type = 'SUCCESS' THEN 1 ELSE 0 END
           ) OVER (
               PARTITION BY user_id
               ORDER BY event_time
               ROWS BETWEEN UNBOUNDED PRECEDING AND 1 PRECEDING
           ) AS success_count_before
    FROM login_events
),
attempt_groups AS (
    SELECT user_id,
           event_time,
           event_type,
           success_count_before
    FROM x
)
SELECT user_id,
       MIN(event_time) AS first_success_time
FROM attempt_groups
WHERE event_type = 'SUCCESS'
GROUP BY user_id, success_count_before
HAVING SUM(
           CASE
               WHEN event_type = 'SUCCESS' THEN 0
               ELSE 1
           END
       ) >= 3;
```

**Interview note**
This is a strong follow-up problem because it tests event ordering, windows and state-like grouping. In an interview, clarify whether failed attempts must be consecutive immediately before the success.

[Back to TOC](#table-of-contents)

## Q82. Inventory stockout intervals

**Schema**
```text
inventory_snapshots(product_id, snapshot_date, stock_qty)
```

**Question**  
Find every continuous interval where a product had zero stock.

**Optimized SQL**
```sql
WITH x AS (
    SELECT product_id,
           snapshot_date,
           stock_qty,
           CASE
               WHEN stock_qty = 0
                    AND COALESCE(
                        LAG(stock_qty) OVER (
                            PARTITION BY product_id
                            ORDER BY snapshot_date
                        ), 1
                    ) <> 0
               THEN 1
               ELSE 0
           END AS new_group
    FROM inventory_snapshots
),
g AS (
    SELECT *,
           SUM(new_group) OVER (
               PARTITION BY product_id
               ORDER BY snapshot_date
               ROWS UNBOUNDED PRECEDING
           ) AS grp
    FROM x
)
SELECT product_id,
       MIN(snapshot_date) AS stockout_start,
       MAX(snapshot_date) AS stockout_end,
       COUNT(*) AS snapshot_days
FROM g
WHERE stock_qty = 0
GROUP BY product_id, grp
ORDER BY product_id, stockout_start;
```

[Back to TOC](#table-of-contents)

---

# High-Frequency Pattern Recognition Cheat Sheet

| Interview wording | SQL pattern |
|---|---|
| "second/third/Nth highest" | `DENSE_RANK()` |
| "top N in each department/category" | `DENSE_RANK() OVER (PARTITION BY ...)` |
| "latest row per customer" | `ROW_NUMBER() OVER (...)` |
| "previous row/value" | `LAG()` |
| "next row/value" | `LEAD()` |
| "running total" | `SUM() OVER (ORDER BY ...)` |
| "moving average" | `AVG() OVER (... ROWS BETWEEN ...)` |
| "compare with group average" | window `AVG()` or aggregated JOIN |
| "customers who never..." | `NOT EXISTS` / `LEFT JOIN ... IS NULL` |
| "customers who have at least one..." | `EXISTS` |
| "for every customer/product..." | relational division / `COUNT(DISTINCT ...)` |
| "duplicates" | `GROUP BY ... HAVING COUNT(*) > 1` |
| "keep latest duplicate" | `ROW_NUMBER()` |
| "consecutive days" | gaps-and-islands |
| "consecutive same status" | `LAG()` + cumulative group id |
| "monthly revenue" | `DATE_TRUNC()` + `GROUP BY` |
| "month-over-month" | aggregate + `LAG()` |
| "pivot" | conditional aggregation |
| "hierarchy/tree" | recursive CTE |
| "above company average" | scalar subquery / CTE |
| "above department average" | window average or aggregate JOIN |
| "missing records" | calendar LEFT JOIN / anti-join |
| "A but not B" | `EXCEPT` / `NOT EXISTS` |
| "common A and B" | `INTERSECT` |
| "combine and deduplicate" | `UNION` |
| "combine preserving duplicates" | `UNION ALL` |

---

# SQL Interview Progression

## Level 1 — Must Solve First

```text
SELECT
WHERE
ORDER BY
DISTINCT
CASE
NULL handling
GROUP BY
HAVING
INNER JOIN
LEFT JOIN
COUNT / SUM / AVG / MIN / MAX
```

## Level 2 — Core MNC Interview

```text
Subqueries
EXISTS / NOT EXISTS
SELF JOIN
CTE
UNION / UNION ALL
Top N
Nth highest
Duplicate detection
Conditional aggregation
```

## Level 3 — Strong SDE / SP / PBC Interview

```text
ROW_NUMBER
RANK
DENSE_RANK
LAG / LEAD
Running totals
Moving averages
Month-over-month
Top N per group
Latest row per group
Gaps & islands
Relational division
```

## Level 4 — Advanced Follow-ups

```text
Recursive CTE
Hierarchy problems
Retention
Conversion
Funnel analysis
Sessionization
Event-stream problems
Complex anti-joins
Time-series analytics
Index / query-plan reasoning
```

---

# Back to TOC

[Go to Table of Contents](#table-of-contents)
