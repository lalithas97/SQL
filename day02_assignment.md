# Day 2 Assignment: Filtering & Sorting

All exercises use **hr.employees** and **hr.departments** only.

---

## Part 1: Practice Questions (With Answers and Explanations)

### Question 1  
List employees in `department_id` 50.

**Answer:**

```sql
SELECT employee_id, first_name, last_name, department_id
FROM hr.employees
WHERE department_id = 50;
```

**Explanation:** Filter with `WHERE department_id = 50`. Only rows that satisfy the condition are returned.

---

### Question 2  
List employees whose salary is between 5000 and 10000 (inclusive).

**Answer:**

```sql
SELECT employee_id, first_name, last_name, salary
FROM hr.employees
WHERE salary BETWEEN 5000 AND 10000;
```

**Explanation:** `BETWEEN 5000 AND 10000` is equivalent to `salary >= 5000 AND salary <= 10000`. Both bounds are inclusive.

---

### Question 3  
List employees whose last name starts with 'K'.

**Answer:**

```sql
SELECT employee_id, first_name, last_name
FROM hr.employees
WHERE last_name LIKE 'K%';
```

**Explanation:** `LIKE 'K%'` matches any last name that starts with 'K' followed by any characters. `%` is the wildcard for zero or more characters.

---

### Question 4  
List the top 5 highest-paid employees (employee_id, first_name, salary).

**Answer:**

```sql
SELECT employee_id, first_name, salary
FROM hr.employees
ORDER BY salary DESC
FETCH FIRST 5 ROWS ONLY;
```

**Explanation:** Sort by `salary DESC` so highest salary first, then limit to 5 rows. In older Oracle use a subquery with `ROWNUM <= 5` instead of `FETCH FIRST`.

---

## Part 2: Self-Practice (No Answers)

Using **hr.employees** only:

1. List employees who have **no** `commission_pct` (NULL).
**Answer:**

```sql
SELECT *
FROM hr.employees
WHERE commission_pct IS NULL;
```

**Explanation:** Uses IS NULL to filter employees whose commission_pct has no value. Only rows where the column is NULL are returned.

2. List employees whose `job_id` **contains** the string `'MAN'`.

**Answer:**

```sql
SELECT *
FROM hr.employees
WHERE job_id IS '%MAN%';
```

**Explanation:** Uses LIKE '%MAN%' to filter rows where job_id contains the substring 'MAN' anywhere in the value.

3. List all employees ordered by `hire_date` **descending** (newest first).
**Answer:**

```sql
SELECT *
FROM hr.employees
ORDER BY hire_date DESC;
```

**Explanation:** Uses ORDER BY hire_date DESC to sort employees from most recently hired to earliest hired.
---

## Part 3: Additional Practice — 20 Medium + 20 Hard Questions (With Hints)

All use **hr.employees** and **hr.departments** only.

### 20 Medium Questions

1. **M1.** List employees in department_id 80 with salary greater than 8000.  
   **Hint:** WHERE department_id = 80 AND salary > 8000.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE department_id = 80 AND salary > 8000;
```

**Explanation:** 
Uses WHERE department_id = 80 AND salary > 8000 to return only employees who belong to department 80 and have a salary greater than 8000. The AND operator ensures both conditions must be true.

2. **M2.** Find employees whose last_name ends with 'n'.  
   **Hint:** WHERE last_name LIKE '%n'.
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE last_name LIKE '%n';
```

**Explanation:** 
Uses WHERE last_name LIKE '%n' to filter employees whose last name ends with the letter 'n'. The % wildcard matches any number of characters before 'n'.

3. **M3.** List employees hired after January 1, 2005.  
   **Hint:** WHERE hire_date > DATE '2005-01-01' or hire_date >= DATE '2005-01-01'.
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE hire_date > DATE '2005-01-01'
```

**Explanation:** 
Uses WHERE hire_date > DATE '2005-01-01' to return employees hired after January 1, 2005. The DATE literal ensures proper date comparison.

4. **M4.** Get employees whose job_id is either 'SA_REP' or 'SA_MAN'.  
   **Hint:** WHERE job_id IN ('SA_REP', 'SA_MAN').
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE job_id IN ('SA_REP','SA_MAN')
```

**Explanation:** 
Uses WHERE job_id IN ('SA_REP','SA_MAN') to return employees whose job_id matches either of the specified values. The IN operator allows filtering against multiple values in a single condition.

5. **M5.** List employees with salary between 4000 and 7000 (inclusive).  
   **Hint:** WHERE salary BETWEEN 4000 AND 7000.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE salary BETWEEN 4000 AND 7000
```

**Explanation:** 
Uses WHERE salary BETWEEN 4000 AND 7000 to return employees whose salary falls within the specified range.
The BETWEEN operator includes both boundary values.

6. **M6.** Find employees who have a manager (manager_id is not null).  
   **Hint:** WHERE manager_id IS NOT NULL.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE manager_id IS NOT NULL
```

**Explanation:** 
Uses WHERE manager_id IS NOT NULL to return employees who have an assigned manager. The IS NOT NULL condition filters rows where the column contains a value.

7. **M7.** List departments with department_id 10, 20, or 30 from hr.departments.  
   **Hint:** WHERE department_id IN (10, 20, 30).
```sql
SELECT * 
FROM hr.departments
WHERE department_id IN (10,20,30)
```

**Explanation:** 
Uses WHERE department_id IN (10,20,30) to return departents whose department_id matches any of the specified values. The IN operator allows filtering against multiple values in a single condition.

8. **M8.** Get the top 3 employees by hire_date (oldest first).  
   **Hint:** ORDER BY hire_date ASC then FETCH FIRST 3 ROWS ONLY.
```sql
SELECT *
FROM hr.employees
ORDER BY hire_date ASC
FETCH FIRST 3 ROWS ONLY
```

**Explanation:** 
Uses ORDER BY hire_date ASC to sort employees from earliest to latest hire date. FETCH FIRST 3 ROWS ONLY limits the result to the three oldest employees.

9. **M9.** List employees in department 50, ordered by last_name ascending.  
   **Hint:** WHERE department_id = 50 ORDER BY last_name.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE department_id = 50
ORDER BY last_name ASC
```

**Explanation:** 
Uses WHERE department_id = 50 to filter employees belonging to that department 50. ORDER BY last_name ASC sorts the result alphabetically by last name

10. **M10.** Find employees whose first_name starts with 'J'.  
    **Hint:** WHERE first_name LIKE 'J%'.
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE first_name LIKE 'J%'
```

**Explanation:** 
Uses WHERE first_name LIKE 'J%' to filter the first name starting with J. The % wildcard matches any number of characters following 'J'.

11. **M11.** List employees with salary not in the range 5000 to 10000.  
    **Hint:** WHERE salary NOT BETWEEN 5000 AND 10000, or salary < 5000 OR salary > 10000.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE salary < 5000 OR salary > 10000
```

**Explanation:** 
Uses WHERE salary < 5000 OR salary > 10000 to return employees whose salary falls outside the range of 5000 to 10000. The OR operator ensures rows satisying either condition are included.

12. **M12.** Get employees whose job_id contains 'CLERK'.  
    **Hint:** WHERE job_id LIKE '%CLERK%'.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE job_id LIKE '%CLERK%'
```

**Explanation:** 
Uses LIKE '%CLERK%' to filter employees whose job_id contains the substring 'CLERK'. The % wildcard matches any characters before or after the word.

13. **M13.** List employees with commission_pct greater than 0.2.  
    **Hint:** WHERE commission_pct > 0.2 (and optionally commission_pct IS NOT NULL).
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE commission_pct > 0.2
```

**Explanation:** 
Uses WHERE commission_pct > 0.2 to return employees whose commission percentage is greater than 0.2. Only rows meeting this condition are returned.

14. **M14.** Find the 10 most recently hired employees.  
    **Hint:** ORDER BY hire_date DESC FETCH FIRST 10 ROWS ONLY.
```sql
SELECT *
FROM hr.EMPLOYEES
ORDER BY hire_date DESC
FETCH FIRST 10 ROWS ONLY
```

**Explanation:** 
Uses ORDER BY hire_date DESC to sort employees from most recently hired to earliest. FETCH first 10 ROWS ONLY limits the result to the 10 newest employees.

15. **M15.** List employees in departments 50 or 60, ordered by department_id then salary descending.  
    **Hint:** WHERE department_id IN (50, 60) ORDER BY department_id, salary DESC.
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE department_id IN (50, 60)
ORDER BY department_id, salary DESC;
```

**Explanation:** 
Uses WHERE deaprtment_id IN (50,60) to filter employees belonging to departments 50 or 60. ORDER BY department_id, salary DESC first sorts by department_id and then by salary in descendng order within each department.

16. **M16.** Get employees whose last_name has exactly 5 characters.  
    **Hint:** WHERE last_name LIKE '_____' (5 underscores).
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE last_name LIKE '_____';
```

**Explanation:** 
WHERE last_name LIKE '_____' extracts only those employee details whose lastname has exactly 5 characters, wwhere each underscore represents one character.

17. **M17.** List departments where manager_id is not null from hr.departments.  
    **Hint:** FROM hr.departments WHERE manager_id IS NOT NULL.
```sql
SELECT *
FROM hr.DEPARTMENTS
WHERE manager_id IS NOT NULL
```

**Explanation:** 
Uses WHERE manager_id IS NOT NULL to return departments that have an assigned manager. Only rows where manager_id contains a value are included.

18. **M18.** Find employees with salary >= 10000, ordered by salary ascending.  
    **Hint:** WHERE salary >= 10000 ORDER BY salary.
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE salary >= 10000
ORDER BY salary ASC
```

**Explanation:** 
Uses WHERE salary >= 10000 to return employees having salary greater than or equal to 10000. ORDER BY salary ASC sorts the result in ascending order of salary.

19. **M19.** List employees whose email ends with '.com' or contains 'example' (if applicable; otherwise use a pattern that exists).  
    **Hint:** WHERE email LIKE '%.com' or email LIKE '%example%' depending on data.
```sql

SELECT * 
FROM hr.EMPLOYEES
WHERE email LIKE '%.com' OR email LIKE '%example%'
```

**Explanation:** 
Uses WHERE email LIKE '%.com' OR email LIKE '%example%' to check if email ends with .com or email contains substring 'example' in it. 

20. **M20.** Get distinct job_id values from employees in department 50.  
    **Hint:** SELECT DISTINCT job_id FROM hr.employees WHERE department_id = 50.
```sql
SELECT DISTINCT job_id
FROM hr.EMPLOYEES
WHERE department_id = 50
```

**Explanation:** 
Uses WHERE department_id = 50 to filter employees in department 50. SELECT DISTINCT job_id ensures only unique job_id values are returned.

### 20 Hard Questions

1. **H1.** List employees in department 80 with salary > 7000 OR job_id = 'SA_MAN', ordered by salary DESC.  
   **Hint:** WHERE (department_id = 80 AND salary > 7000) OR job_id = 'SA_MAN' ORDER BY salary DESC.
```sql
SELECT *
FROM HR.EMPLOYEES
WHERE (department_id = 80 AND salary > 7000) OR job_id = 'SA_MAN'
ORDER BY salary DESC
```

**Explanation:** 
Uses (department_id = 80 AND salary > 7000) OR job_id = 'SA_MAN' to return employees who either belong to department 80 with salary greater than 7000, or have the job_id 'SA_MAN'. ORDER BY salary DESC sorts the result from highest to lowest salary.

2. **H2.** Find employees hired between Jan 1, 2000 and Dec 31, 2005.  
   **Hint:** WHERE hire_date BETWEEN DATE '2000-01-01' AND DATE '2005-12-31'.
```sql
SELECT *
FROM hr.EMPLOYEES
WHERE hire_date BETWEEN DATE '2000-01-01' AND DATE '2005-12-31'
```

**Explanation:** 
Uses BETWEEN DATE '2000-01-01' AND DATE '2005-12-31' to filter employees hired within the specified date range. The BETWEEN operator includes both boundary dates.

3. **H3.** List employees whose last_name is 4 characters and starts with 'K'.  
   **Hint:** WHERE last_name LIKE 'K___'.
```sql
SELECT * 
FROM hr.EMPLOYEES
WHERE last_name LIKE 'K___'
```

**Explanation:** 
Uses LIKE 'K___' to return employees whose last_name starts with 'K' and has exactly four characters. Each underscore represents one character.

4. **H4.** Get top 5 highest-paid employees in department 50 only.  
   **Hint:** WHERE department_id = 50 ORDER BY salary DESC FETCH FIRST 5 ROWS ONLY.
```sql
SELECT *
FROM HR.EMPLOYEES
WHERE department_id = 50 
ORDER BY salary DESC
FETCH FIRST 5 ROWS ONLY
```

**Explanation:** 
Uses WHERE department_id = 50 to filter employees in department 50. ORDER BY salary DESC sorts by highest salary first, and FETCH FIRST 5 ROWS ONLY limits the result to the top five highest-paid employees.

5. **H5.** List employees with no manager and salary > 5000.  
   **Hint:** WHERE manager_id IS NULL AND salary > 5000.
```sql
SELECT *
FROM HR.EMPLOYEES
WHERE manager_id IS NULL AND salary > 5000
```

**Explanation:** 
Uses WHERE manager_id IS NULL AND salary > 5000 to return employees who do not have a manager and have a salary greater than 5000. The AND operator ensures both conditions must be true.

6. **H6.** Find employees whose first_name has an 'a' as the second character.  
   **Hint:** WHERE first_name LIKE '_a%'.
```sql
SELECT *
FROM HR.EMPLOYEES
WHERE first_name LIKE '_a%'
```

**Explanation:** 
Uses LIKE '_a%' to return employees whose first_name has 'a' as the second character. The underscore represents exactly one character before 'a'.

7. **H7.** List departments (hr.departments) with department_id between 40 and 90.  
   **Hint:** WHERE department_id BETWEEN 40 AND 90.
```sql
SELECT * 
FROM HR.departments
WHERE department_id BETWEEN 40 AND 90
```

**Explanation:** 
Uses BETWEEN 40 AND 90 to filter departments whose department_id falls within the specified range. The range is inclusive.

8. **H8.** Get employees with salary < 3000 or salary > 15000, ordered by salary.  
   **Hint:** WHERE salary < 3000 OR salary > 15000 ORDER BY salary.
```sql
SELECT *
FROM HR.EMPLOYEES
WHERE salary < 3000 OR salary > 15000
ORDER BY salary
```

**Explanation:** 
Uses salary < 3000 OR salary > 15000 to return employees whose salary falls outside the given range. ORDER BY salary sorts the result in ascending order.

9. **H9.** List employees in department 60 with job_id 'IT_PROG', or in department 100 with job_id like 'FI%'.  
   **Hint:** WHERE (department_id = 60 AND job_id = 'IT_PROG') OR (department_id = 100 AND job_id LIKE 'FI%').
```sql
SELECT * 
FROM HR.EMPLOYEES
WHERE (DEPARTMENT_ID = 60 AND job_id = 'IT_PROG') OR (DEPARTMENT_ID = 100 AND job_id LIKE 'FI%')
```

**Explanation:** 
Uses (department_id = 60 AND job_id = 'IT_PROG') OR (department_id = 100 AND job_id LIKE 'FI%') to filter employees based on grouped conditions. Parentheses ensure correct logical evaluation of AND and OR.

10. **H10.** Find employees whose hire_date is in the year 2003.  
    **Hint:** WHERE EXTRACT(YEAR FROM hire_date) = 2003 or hire_date between DATE '2003-01-01' AND DATE '2003-12-31'.
```sql
SELECT * 
FROM HR.EMPLOYEES
WHERE EXTRACT(YEAR FROM hire_date) = 2003
```

**Explanation:** 
Uses EXTRACT(YEAR FROM hire_date) = 2003 to return employees hired in the year 2003. This extracts the year portion from the hire_date column for comparison.

11. **H11.** List employees with commission_pct NULL and job_id starting with 'SA'.  
    **Hint:** WHERE commission_pct IS NULL AND job_id LIKE 'SA%'.
```sql
SELECT * 
FROM HR.employees
WHERE commission_pct IS NULL AND job_id LIKE 'SA%'
```

**Explanation:** 
Uses commission_pct IS NULL AND job_id LIKE 'SA%' to return employees who have no commission and whose job_id starts with 'SA'. The AND operator ensures both conditions are satisfied.

12. **H12.** Get the 3 oldest employees (earliest hire_date) in department 90.  
    **Hint:** WHERE department_id = 90 ORDER BY hire_date ASC FETCH FIRST 3 ROWS ONLY.
```sql
SELECT *
FROM HR.EMPLOYEES
WHERE department_id = 90 
ORDER BY hire_date ASC 
FETCH FIRST 3 ROWS ONLY
```

**Explanation:** 
Uses WHERE department_id = 90 to filter employees in department 90. ORDER BY hire_date ASC sorts by earliest hire date, and FETCH FIRST 3 ROWS ONLY limits the result to the three oldest employees.

13. **H13.** List employees whose last_name does not start with 'A', 'B', or 'C'.  
    **Hint:** WHERE last_name NOT LIKE 'A%' AND last_name NOT LIKE 'B%' AND last_name NOT LIKE 'C%'; or use NOT IN with SUBSTR.
```sql
SELECT *
FROM hr.employees
WHERE   last_name NOT LIKE 'A%'
        AND last_name NOT LIKE 'B%'
        AND last_name NOT LIKE 'C%';

```

**Explanation:** 
Uses NOT LIKE conditions to exclude employees whose last_name starts with 'A', 'B', or 'C'. Only rows that do not match any of these patterns are returned.

14. **H14.** Find employees with salary in (5000, 6000, 7000, 8000).  
    **Hint:** WHERE salary IN (5000, 6000, 7000, 8000).
```sql
SELECT *
FROM hr.employees
WHERE salary IN (5000, 6000, 7000, 8000);
```

**Explanation:** 
Uses IN (5000, 6000, 7000, 8000) to return employees whose salary matches any of the specified values.

15. **H15.** List employees ordered by department_id ASC, then by hire_date DESC within each department.  
    **Hint:** ORDER BY department_id, hire_date DESC.
```sql
SELECT *
FROM hr.employees
ORDER BY department_id ASC, hire_date DESC;
```

**Explanation:** 
Uses ORDER BY department_id ASC, hire_date DESC to first sort employees by department_id in ascending order, and then by hire_date in descending order within each department.

16. **H16.** Get employees whose first_name and last_name both start with the same letter (simplified: same first letter).  
    **Hint:** WHERE SUBSTR(first_name,1,1) = SUBSTR(last_name,1,1).
```sql
SELECT *
FROM hr.employees
WHERE SUBSTR(first_name, 1, 1) = SUBSTR(last_name, 1, 1);
```

**Explanation:** 
Uses SUBSTR(first_name,1,1) = SUBSTR(last_name,1,1) to return employees whose first and last names start with the same letter.

17. **H17.** List employees with manager_id not null and department_id in (50, 80, 100).  
    **Hint:** WHERE manager_id IS NOT NULL AND department_id IN (50, 80, 100).
```sql
SELECT *
FROM hr.employees
WHERE manager_id IS NOT NULL AND department_id IN (50, 80, 100);

```

**Explanation:** 
Uses manager_id IS NOT NULL AND department_id IN (50, 80, 100) to return employees who have a manager assigned and belong to any of the specified departments.

18. **H18.** Find employees with salary between 3000 and 5000 and job_id containing 'REP'.  
    **Hint:** WHERE salary BETWEEN 3000 AND 5000 AND job_id LIKE '%REP%'.
```sql
SELECT *
FROM hr.employees
WHERE salary BETWEEN 3000 AND 5000 AND job_id LIKE '%REP%';
```

**Explanation:** 
Uses salary BETWEEN 3000 AND 5000 AND job_id LIKE '%REP%' to return employees whose salary falls within the specified range and whose job_id contains 'REP'. The AND operator ensures both conditions are met.

19. **H19.** List departments (hr.departments) ordered by department_name descending.  
    **Hint:** SELECT * FROM hr.departments ORDER BY department_name DESC.
```sql
SELECT *
FROM hr.departments
ORDER BY department_name DESC;
```

**Explanation:** 
Uses ORDER BY department_name DESC to sort departments in descending alphabetical order of department_name.

20. **H20.** Get employees with hire_date not in 2004 (all years except 2004).  
    **Hint:** WHERE EXTRACT(YEAR FROM hire_date) <> 2004 or hire_date < DATE '2004-01-01' OR hire_date > DATE '2004-12-31'.
```sql
SELECT *
FROM hr.employees
WHERE EXTRACT(YEAR FROM hire_date) <> 2004;
```

**Explanation:** 
Uses EXTRACT(YEAR FROM hire_date) <> 2004 (or equivalent date conditions) to return employees whose hire_date is not in the year 2004.

---

[← Back to Learning Plan](../30-day-sql-plsql-learning-plan.md) | [Tutorial](../tutorials/day02_filtering_sorting.md)
