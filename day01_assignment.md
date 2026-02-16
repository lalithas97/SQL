# Day 1 Assignment: SQL Basics & SELECT

All exercises use **hr.employees** and **hr.departments** only.

---

## Part 1: Practice Questions (With Answers and Explanations)

### Question 1  
List `employee_id`, `first_name`, and `last_name` from `hr.employees`.

**Answer:**

```sql
SELECT employee_id, first_name, last_name
FROM hr.employees;
```

**Explanation:** Use the basic `SELECT column1, column2, ... FROM table`. Only the three requested columns are selected.

---

### Question 2  
Display the full name as a single column using concatenation (e.g., "First Last").

**Answer:**

```sql
SELECT first_name || ' ' || last_name AS full_name
FROM hr.employees;
```

**Explanation:** In Oracle, `||` concatenates strings. A space is added between first and last name. `AS full_name` gives the column a clear alias.

---

### Question 3  
Calculate annual salary as `salary * 12` and give it the alias `annual_salary`.

**Answer:**

```sql
SELECT employee_id, first_name, last_name, salary, salary * 12 AS annual_salary
FROM hr.employees;
```

**Explanation:** Use an arithmetic expression in the SELECT list. The alias `annual_salary` is assigned with `AS`.

---

## Part 2: Self-Practice (No Answers)

Try these on your own using **hr.employees**.

1. List all **distinct** values of `job_id`.

**Answer:**

```sql
SELECT DISTINCT job_id from hr.EMPLOYEES;
```

**Explanation:** 
`DISTINCT` returns only unique values from a column by removing duplicate entries.

2. Show `commission_pct` and `salary` for the first 10 rows (use `FETCH FIRST 10 ROWS ONLY` or equivalent).

**Answer:**

```sql
SELECT commission_pct, salary 
from hr.EMPLOYEES
FETCH FIRST 10 ROWS ONLY;
```

**Explanation:** 
This query retrieves the `commission_pct` and `salary` columns for only the first 10 rows returned from the     `hr.employees` table.

3. Write a SELECT that returns each employee’s `employee_id` and a literal value `'HR'` in a column named `department`.

**Answer:**

```sql
SELECT employee_id, 'HR' AS department FROM hr.employees;
```

**Explanation:** 
This query selects the `employee_id` from the `hr.employees` table and adds a new column named `department` that contains the literal value `'HR'` for every row returned.
---

## Part 3: Additional Practice — 20 Medium + 20 Hard Questions (With Hints)

All questions use **hr.employees** and **hr.departments** only.

### 20 Medium Questions

1. **M1.** Display `employee_id`, `first_name`, `last_name`, and a new column `full_name` that is first_name and last_name concatenated with a comma between them (e.g., "John, Doe").  
   **Hint:** Use `first_name || ', ' || last_name` and alias it as `full_name`.

**Answer:**

```sql
SELECT employee_id,
       first_name,
       last_name,
       first_name || ', ' || last_name AS full_name
FROM hr.employees;

```

**Explanation:** 
This query selects employee details and creates a new column `full_name` by concatenating `first_name` and `last_name` with a comma and space using the concatenation operator ||.

2. **M2.** List `employee_id`, `salary`, and a column `bonus_10_pct` showing 10% of salary (salary * 0.10).  
   **Hint:** Use an arithmetic expression and alias.

**Answer:**

```sql
SELECT employee_id,
       salary,
       0.1*salary AS bonus_10_pct
FROM hr.employees;
```

**Explanation:** 
This query selects each employee’s `employee_id` and `salary`, and calculates a new column `bonus_10_pct` by multiplying the salary by 0.1 to show 10% of the salary.

3. **M3.** Show `employee_id`, `hire_date`, and a literal column `record_type` with value `'Employee'` for every row.  
   **Hint:** Add `'Employee' AS record_type` in the SELECT list.

**Answer:**

```sql
SELECT employee_id,
       hire_date,
       'Employee' AS record_type
FROM hr.employees;
```

**Explanation:** 
This query selects `employee_id` and `hire_date` and adds a constant column `record_type` that displays the literal value `Employee` for everry row returned.

4. **M4.** For each employee, display `email` and a column `email_domain` set to the literal `'@company.com'`.  
   **Hint:** Use a string literal with an alias; no concatenation required for this part.

**Answer:**

```sql
SELECT email,
       '@company.com' AS email_domain
FROM hr.employees;

```

**Explanation:** 
This query selects each employee's `email` and adds a constant column `email_domain` containing the literal `@company.com` for every row.

5. **M5.** List `employee_id`, `salary`, `commission_pct`, and `effective_commission` where effective_commission is NVL(commission_pct, 0).  
   **Hint:** Use `NVL(commission_pct, 0) AS effective_commission`.

**Answer:**

```sql
SELECT employee_id,
       salary,
       commission_pct,
       NVL(commission_pct, 0) AS effective_commission
FROM hr.employees;
```

**Explanation:** 
This query selects employee details and replaces any NULL value in `commission_pct` with 0 using the `NVL` function, displaying it as `effective_commission`.

6. **M6.** Display `first_name`, `last_name`, and a column `initials` formed by the first character of first_name and the first character of last_name (e.g., "JD").  
   **Hint:** Use SUBSTR(first_name, 1, 1) and SUBSTR(last_name, 1, 1) concatenated.

**Answer:**

```sql
SELECT first_name, last_name, 
(SUBSTR(first_name, 1, 1) || SUBSTR(last_name, 1, 1)) AS initials 
FROM hr.employees;
```

**Explanation:** 
Concatenates the first letter of `first_name` and the first letter of `last_name` to generate each employee's initials.

7. **M7.** Show `employee_id`, `salary`, and `annual_salary` as salary * 12, and also `annual_plus_bonus` as salary * 12 * 1.1 (10% bonus).  
   **Hint:** Two calculated columns with aliases.

**Answer:**

```sql
SELECT employee_id, salary, 
salary*12 AS annual_salary,
salary*12*1.1 AS annual_plus_bonus 
FROM hr.employees;
```

**Explanation:** 
Retrieves each `employee_id` and `salary`, calculates their `annya salary` (salary * 12), and then computes a 10% increased annual amount as `annual_plus_bonus` (salary * 12 * 1.1).

8. **M8.** List all columns from `hr.departments` using explicit column names (department_id, department_name, manager_id, location_id).  
   **Hint:** SELECT each column name from hr.departments; no *.

**Answer:**

```sql
SELECT department_id, department_name, manager_id, location_id FROM hr.departments;
```

**Explanation:** 
This query explicitly selects all four columns from the hr.departments instead of SELECT *.

9. **M9.** From `hr.employees`, select `employee_id` and a column `description` that is the literal `'Emp#'` concatenated with employee_id (cast to string if needed: use TO_CHAR(employee_id)).  
   **Hint:** `'Emp#' || TO_CHAR(employee_id) AS description`.

**Answer:**

```sql
SELECT employee_id, 
       'Emp#' || TO_CHAR(employee_id) AS description
FROM hr.employees;
```

**Explanation:** 
This query selects each employee's ID and creates a new column `description` by concatenating the literal `'Emp#'` with the employee_id converted to a string using `TO_CHAR`.

10. **M10.** Display `job_id`, `salary`, and a column `salary_band` that is the literal `'Standard'` for every row.  
    **Hint:** Add `'Standard' AS salary_band` in SELECT.

**Answer:**

```sql
SELECT job_id, salary, 
'Standard' AS salary_band
FROM hr.employees;
```

**Explanation:** 
This query retrieves each employee's `job_id` and `salary`, and adds a new column `salary_band` that displays the fixed literal value `'Standard'` for every row.

11. **M11.** List `employee_id`, `first_name`, `last_name`, and a column `display_name` as "Last, First" (last_name, comma space, first_name).  
    **Hint:** `last_name || ', ' || first_name AS display_name`.

**Answer:**

```sql
SELECT employee_id, first_name, last_name, 
(LAST_NAME || ', ' || FIRST_NAME) AS display_name
FROM hr.employees;
```

**Explanation:** 
This query selects each employee's ID and constructs a `display_name` column by concatenating `last_name`, a comma and space, and `first_name` in the format "LastName, FirstName" for every row.

12. **M12.** Show `department_id` from `hr.departments` and a literal `1` as column `sort_order`.  
    **Hint:** SELECT department_id, 1 AS sort_order FROM hr.departments.

**Answer:**

```sql
SELECT department_id,
1 as sort_order
FROM hr.DEPARTMENTS;
```

**Explanation:** 
This query retrieves each `department_id` from `hr.departments` and adds a new column `sort_order` that displays the fixed numeric literal value `1` for every row.

13. **M13.** From `hr.employees`, display `salary` and `monthly_net` as salary * 0.85 (assuming 15% tax).  
    **Hint:** salary * 0.85 AS monthly_net.

**Answer:**

```sql
SELECT salary,
       salary*0.85 AS monthly_net
FROM hr.EMPLOYEES;
```

**Explanation:** 
This query selects each employee's `salary` and calculates `monthly_net` by multiplying salary by 0.85 to represent the amount after deducting 15% tax.

14. **M14.** List `employee_id`, `commission_pct`, and `commission_display` where NULL commission_pct is shown as 0 using NVL.  
    **Hint:** NVL(commission_pct, 0) AS commission_display.

**Answer:**

```sql
select employee_id,
       commission_pct,
       NVL(commission_pct, 0) AS commission_display
FROM hr.EMPLOYEES;
```

**Explanation:** 
This query displays each employee's `employee_id` and `commission_pct` and creates `commission_display` by replacing NULL commission values with 0 using rhe `'NVL'` function.

15. **M15.** Display `first_name`, `last_name`, `salary`, and a column `compensation` that is salary * (1 + NVL(commission_pct, 0)).  
    **Hint:** Total comp = salary + salary*commission_pct; factor as salary*(1 + NVL(commission_pct,0)).

**Answer:**

```sql
SELECT first_name,
       last_name,
       salary,
       salary * (1 + NVL(commission_pct, 0)) AS compensation
FROM hr.EMPLOYEES;
```

**Explanation:** 
This query retrieves each employee's name and salary, and calculates `compensation` by multiplying salary with (1 + commission_pct), replacing NULL commission values with 0 using NVL.
If commission_pct = 0.2 -> salary X 1.2
If commission_pct = NULL -> salary X 1

16. **M16.** From `hr.departments`, list `department_name` and a literal column `region` with value `'HQ'`.  
    **Hint:** SELECT department_name, 'HQ' AS region FROM hr.departments.

**Answer:**

```sql
SELECT department_name,
       'HQ' AS region
FROM hr.DEPARTMENTS;
```

**Explanation:** 
This query retrieves each `department_name` and adds a new column `region` that displays the fixed literal value `'HQ'` for every row..

17. **M17.** Show `employee_id`, `hire_date`, and a column `years_label` with literal `'Years of service'`.  
    **Hint:** Add a string literal with alias years_label.

**Answer:**

```sql
SELECT employee_id,
       hire_date,
       'Years of Service' AS years_label
FROM hr.EMPLOYEES;
```

**Explanation:** 
This query retrieves each employee's `employee_id` and `hire_date`, and adds a new column `years_label` that displays the fixed literal value `'Years of Service'` for every row.

18. **M18.** List `employee_id`, `salary`, and `double_salary` as salary * 2.  
    **Hint:** Simple arithmetic expression with alias.

**Answer:**

```sql
SELECT  employee_id,
        salary,
        salary * 2 AS double_salary
FROM hr.EMPLOYEES;
```

**Explanation:** 
This query selects the `employee_id`, `salary` and calculates `double_salary` by multiplying the salary by 2 for each row.

19. **M19.** From `hr.employees`, display `manager_id` and a column `has_manager` that is the literal `'Yes'` when manager_id is not null and `'No'` when manager_id is null (use NVL2: NVL2(manager_id, 'Yes', 'No')).  
    **Hint:** NVL2(manager_id, 'Yes', 'No') AS has_manager.

**Answer:**

```sql
SELECT  manager_id,
        NVL2(manager_id,'Yes','No') AS has_manager
FROM hr.employees;
```

**Explanation:** 
This query displays each `manager_id` and uses `NVL2` to return `'Yes'` when `manager_id` is NOT NULL and `'No'` when it is NULL.

NVL2(expr, value_if_not_null, value_if_null)
- If expr is NOT NULL → return second argument
- If expr is NULL → return third argument

20. **M20.** Show `department_id`, `department_name` from `hr.departments`, and a calculated column `dept_code` as the first 3 characters of department_name (use SUBSTR).  
    **Hint:** SUBSTR(department_name, 1, 3) AS dept_code.

**Answer:**

```sql
SELECT  department_id,
        department_name,
        SUBSTR(DEPARTMENT_NAME,1,3) AS dept_code
FROM hr.DEPARTMENTS;
```

**Explanation:** 
This query retrieves each `department_id` and `department_name`, and creates `dept_code` by extracting the first three characters of `department_name` using the `SUBSTR` function.

**NOTES**
Oracle’s `SUBSTR` does **not throw errors** for out-of-range positions.
It behaves safely:

**Rules:**

- If start > length of string → returns **NULL**

- If negative start goes beyond beginning → treated as starting from position 1

- If length exceeds remaining characters → returns until end

- If start = 0 → treated as 1

Oracle prefers returning something valid instead of failing.


### 20 Hard Questions

1. **H1.** Display `employee_id`, `first_name`, `last_name`, `salary`, and a column `salary_rank_label` that is 'High' if salary >= 10000, 'Medium' if salary >= 5000 and < 10000, else 'Low'. Use CASE.  
   **Hint:** CASE WHEN salary >= 10000 THEN 'High' WHEN salary >= 5000 THEN 'Medium' ELSE 'Low' END.

**Answer:**

```sql
SELECT  employee_id,
        first_name,
        last_name,
        salary,
        CASE 
            WHEN salary>= 10000 THEN 'HIGH'
            WHEN salary >= 5000 THEN 'MEDIUM'
            ELSE 'LOW' 
        END AS salary_rank_label
FROM hr.EMPLOYEES;
```

**Explanation:** 
This query displays employee details and uses a CASE expression to classify salary into 'High', 'Medium', or 'Low' based on defined salary ranges.

2. **H2.** List `employee_id`, `salary`, `commission_pct`, and `total_comp` as salary + (salary * NVL(commission_pct, 0)), formatted to 2 decimal places using ROUND(..., 2).  
   **Hint:** ROUND(salary * (1 + NVL(commission_pct,0)), 2) AS total_comp.

**Answer:**

```sql
SELECT  employee_id, 
        salary,
        commission_pct,
        ROUND(salary * (1 + NVL(commission_pct, 0)), 2) AS total_comp                
FROM hr.employees;
```

**Explanation:** 
This query displays employee details and calculate total_comp by adding commission to salary (treating NULL commission as 0 using NVL) and rounding the result to two decimal places using ROUND.

3. **H3.** From `hr.employees`, show `employee_id`, `email`, and `email_upper` as UPPER(email). Also show `email_length` as LENGTH(email).  
   **Hint:** Use UPPER(email) and LENGTH(email) with aliases.

**Answer:**

```sql
SELECT  employee_id,
        email,
        UPPER(email) AS email_upper,
        LENGTH(email) AS email_length
FROM hr.employees;
```

**Explanation:** 
This query displays each employee’s employee_id and email, converts the email to uppercase using UPPER, and calculates the number of characters in the email using LENGTH. .

4. **H4.** Display `department_id` from `hr.departments`, `department_name`, and a column `name_length` (number of characters in department_name).  
   **Hint:** LENGTH(department_name) AS name_length.

**Answer:**

```sql
SELECT  department_id,
        department_name,
        LENGTH(DEPARTMENT_NAME) AS name_length
FROM hr.DEPARTMENTS;
```

**Explanation:** 
This query retrieves each department’s ID and name, and calculates name_length as the number of characters in department_name using the LENGTH function..

5. **H5.** List `employee_id`, `first_name`, `last_name`, and a column `reverse_name` as last_name concatenated with first_name (no comma).  
   **Hint:** last_name || first_name AS reverse_name (add space if you want).

**Answer:**

```sql
SELECT  employee_id, 
        first_name,
        last_name,
        last_name || ' ' || FIRST_NAME AS reverse_name 
FROM hr.employees;
```

**Explanation:** 
This query displays employee details and creates reverse_name by concatenating last_name and first_name using the concatenation operator ||.

6. **H6.** Show `employee_id`, `hire_date`, and a literal column `data_source` with value `'HR.EMPLOYEES'`.  
   **Hint:** 'HR.EMPLOYEES' AS data_source.

**Answer:**

```sql
SELECT  employee_id, 
        hire_date,
        'HR.EMPLOYEES' AS data_source 
FROM hr.employees;
```

**Explanation:** 
This query displays each employee’s employee_id and hire_date, and adds a literal column data_source with the fixed value 'HR.EMPLOYEES' for every row.

7. **H7.** From `hr.employees`, display `job_id`, `salary`, and `salary_percentage` as (salary / (SELECT SUM(salary) FROM hr.employees)) * 100, rounded to 2 decimals.  
   **Hint:** Scalar subquery in SELECT: ROUND(salary * 100.0 / (SELECT SUM(salary) FROM hr.employees), 2).

**Answer:**

```sql
SELECT  job_id, 
        salary,
        ROUND(salary * 100.0 / (SELECT SUM(salary) FROM hr.employees), 2)
        AS salary_percentage 
FROM hr.employees;
```

**Explanation:** 
This query calculates each employee's salary as percentage of the total company salary using a scalar subquery and rounds the result to two decimal places.
1.Subquery returns single value -> allowed in SELECT
2.Total salary -> SELECT SUM(salary) FROM hr.employees
3.Percentage -> (salary / total) * 100 
4.Formatting -> wrap with ROUND(...,2)

8. **H8.** List `employee_id`, `first_name`, `last_name`, and a column `formal_name` as "Mr. " or "Ms. " (your choice) concatenated with first_name and last_name.  
   **Hint:** 'Mr. ' || first_name || ' ' || last_name AS formal_name.

**Answer:**

```sql
SELECT  employee_id,
        first_name,
        last_name,
        'Ms. ' || first_name || ' ' || last_name AS formal_name
FROM hr.employees;
```

**Explanation:** 
This query creates a formal_name by concatenating the literal 'Ms.' with the employee's first and last name seperated by spaces.

9. **H9.** Display `employee_id`, `salary`, and `annual_with_raise` as (salary * 12) * 1.05 (5% annual raise).  
   **Hint:** salary * 12 * 1.05 AS annual_with_raise.

**Answer:**

```sql
SELECT  employee_id,
        salary,
        (salary * 12) * 1.05 AS annual_with_raise
FROM hr.employees;
```

**Explanation:** 
This query calculates annual_with_raise by multiplying the monthly salary by 12 and applying 5% increase.

10. **H10.** From `hr.departments`, show `department_id`, `department_name`, and a column `id_name` that concatenates department_id and department_name with a hyphen (e.g., "10-Administration"). Use TO_CHAR(department_id) for the number.  
    **Hint:** TO_CHAR(department_id) || '-' || department_name AS id_name.

**Answer:**

```sql
SELECT  department_id,
        department_name,
        TO_CHAR(department_id) || '-' || department_name AS id_name
FROM hr.departments;
```

**Explanation:** 
This query concatenates the department_id (converted to string using TO_CHAR) with a hypen and the department_name to create id_name.

11. **H11.** List `employee_id`, `commission_pct`, and `commission_category`: 'Commissioned' if commission_pct is not null, 'Non-commissioned' if null. Use NVL2 or CASE.  
    **Hint:** NVL2(commission_pct, 'Commissioned', 'Non-commissioned') AS commission_category.

**Answer:**

```sql
SELECT  employee_id,
        commission_pct,
        NVL2(commission_pct, 'Commissioned','Non-Commissioned') 
        AS commission_category
FROM hr.employees;

```

**Explanation:** 
This query uses NVL2 to label employeees as 'commissioned' when commission_pct is not NULL and 'Non-commissioned' when it is NULL.

**NOTES**
NVL2(expression, not NULL, NULL)

12. **H12.** Show `employee_id`, `first_name`, `last_name`, `salary`, and a column `salary_expression` that is the literal string `'salary * 12'` (not the result of the calculation).  
    **Hint:** 'salary * 12' AS salary_expression — a string literal.

**Answer:**

```sql
SELECT  employee_id,
        first_name,
        last_name,
        'salary * 12' AS salary_expression
FROM hr.employees;
```

**Explanation:** 
This query displays employee details and adds a literal column salary_expression containing the string 'salary * 12', not the calculated result.

13. **H13.** From `hr.employees`, display `employee_id`, `job_id`, and a column `job_salary_label` as job_id concatenated with ':' and salary (e.g., "SA_REP:9000"). Use TO_CHAR(salary).  
    **Hint:** job_id || ':' || TO_CHAR(salary) AS job_salary_label.

**Answer:**

```sql
SELECT  employee_id,
        job_id,
        job_id || ':' || TO_CHAR(salary) AS job_salary_label
FROM hr.employees;
```

**Explanation:** 
This query creates job_salary_label by concatenating job_id, a colon, and the salary converted to string using TO_CHAR.

14. **H14.** List `employee_id`, `salary`, and `tax_bracket` as '20%' if salary >= 10000, '15%' if salary >= 5000, else '10%'. Use CASE.  
    **Hint:** CASE WHEN salary >= 10000 THEN '20%' WHEN salary >= 5000 THEN '15%' ELSE '10%' END.

**Answer:**

```sql
SELECT  employee_id,
        salary,
        CASE
            WHEN salary >= 10000 THEN '20%'
            WHEN salary >= 5000 THEN '15%'
            ELSE '10%'
        END
        AS tax_bracket
FROM hr.employees;
```

**Explanation:** 
This query classifies each employee's salarry into tax brackets using a CASE expression based on defined salary ranges..

15. **H15.** Display `department_id`, `department_name` from `hr.departments`, and a column `dept_info` that is "Department " followed by department_id and " - " and department_name.  
    **Hint:** 'Department ' || TO_CHAR(department_id) || ' - ' || department_name AS dept_info.

**Answer:**

```sql
SELECT  department_id,
        department_name,
        'Department '|| TO_CHAR(department_id) || ' - ' || department_name AS dept_info
FROM hr.departments;
```

**Explanation:** 
This query creates dept_info by concatenating the literal 'Department ' the department_id converted to string, and the department_name seperated by ' -'.

16. **H16.** From `hr.employees`, show `employee_id`, `first_name`, `last_name`, and `full_name_reversed` as last_name, space, first_name (e.g., "Doe John").  
    **Hint:** last_name || ' ' || first_name AS full_name_reversed.

**Answer:**

```sql
SELECT  employee_id,
        first_name,
        last_name,
        last_name || ' ' || first_name AS full_name_reversed
FROM hr.employees;
```

**Explanation:** 
This query creates full_name_reversed by concatenating last_name, a space and first_name.

17. **H17.** List `employee_id`, `salary`, `commission_pct`, and `effective_salary` as salary when commission_pct is null, otherwise salary * (1 + commission_pct). Use NVL2 or CASE.  
    **Hint:** NVL2(commission_pct, salary * (1 + commission_pct), salary) AS effective_salary.

**Answer:**

```sql
SELECT  employee_id,
        salary,
        commission_pct,
        NVL2(commission_pct, salary * (1+ commission_pct), salary) AS effective_salary
FROM hr.employees;
```

**Explanation:** 
This query uses NVL2 to calculate effective_salary as salary with commission when commission_pct is not NULL, otherwise returns the base salary.

18. **H18.** Show `employee_id`, `hire_date`, and a column `hire_year` that is the year from hire_date (use EXTRACT(YEAR FROM hire_date) in Oracle).  
    **Hint:** EXTRACT(YEAR FROM hire_date) AS hire_year.

**Answer:**

```sql
SELECT  employee_id,
        hire_date,
        EXTRACT(YEAR from hire_date) AS hire_year
FROM hr.employees;
```

**Explanation:** 
This query extracts the year component from each emplloyee's hire-date using the EXTRACT function and displays it as hire_year.

19. **H19.** From `hr.departments`, display `department_name` and a column `word_count` as the number of words (simplified: 1 + number of spaces, or use a formula based on LENGTH and REPLACE of spaces). For simplicity, use LENGTH(department_name) - LENGTH(REPLACE(department_name, ' ', '')) + 1 if names have spaces.  
    **Hint:** For single-word names, word_count can be 1; or 1 + LENGTH(REPLACE(department_name,' ','')) - LENGTH(REPLACE(REPLACE(department_name,' ',''),' ','')) — simpler: just use LENGTH(department_name) as a proxy or 1 for all.

**Answer:**

```sql
SELECT  department_name,
        LENGTH(department_name) - LENGTH(REPLACE(department_name, ' ', '')) + 1 AS word_count
FROM hr.departments;
```

**Explanation:** 
This query calculates the word_count by subtracting the length of the department name without spaces from the original length and adding 1 to count the number of words.

20. **H20.** List `employee_id`, `first_name`, `last_name`, and a column `name_with_id` as "[" || employee_id || "] " || first_name || " " || last_name (e.g., "[100] Steven King").  
    **Hint:** '[' || TO_CHAR(employee_id) || '] ' || first_name || ' ' || last_name AS name_with_id.

**Answer:**

```sql
SELECT  employee_id,
        first_name,
        last_name,
        ('[' || TO_CHAR(employee_id) || ']' || ' ' || first_name || ' ' || last_name) AS name_with_id
FROM hr.employees;
```

**Explanation:** 
This query creates name_with_id by concatenating the employee_id enclosed in brackets with the employee's full name.

---

[← Back to Learning Plan](../30-day-sql-plsql-learning-plan.md) | [Tutorial](../tutorials/day01_sql_basics.md)
