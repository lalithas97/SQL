# Day 4 Assignment: DML – Insert, Update, Delete

Use a backup or copy of **hr.employees** (e.g. **hr_emp_backup**) for DML so you do not change production data. If needed, create it with CREATE TABLE hr_emp_backup AS SELECT * FROM hr.employees WHERE 1=0; plus required columns, or use your Day 3 table.

---

## Part 1: Practice Questions (With Answers and Explanations)

### Question 1
Insert one row into your backup table. Use a new employee_id (e.g. 999), set first_name, last_name, email, hire_date, job_id, salary, department_id to valid values.

**Answer (adjust column list to match your table):**

```sql
INSERT INTO hr_emp_backup (employee_id, first_name, last_name, email, hire_date, job_id, salary, department_id)
VALUES (999, 'John', 'Doe', 'JDOE', SYSDATE, 'SA_REP', 5000, 50);
```

**Explanation:** List the columns you are supplying, then provide the same number of values in the same order. Use SYSDATE for current date. Ensure department_id and job_id exist in the schema if there are FKs.

---

### Question 2
Update salary by 10% for all employees in department_id 60 in your backup table.

**Answer:**

```sql
UPDATE hr_emp_backup
SET salary = salary * 1.10
WHERE department_id = 60;
```

**Explanation:** SET salary = salary * 1.10 increases salary by 10%. The WHERE clause limits the update to department 60 only. Check row count before committing.

---

### Question 3
Delete all rows from your backup table where department_id is NULL.

**Answer:**

```sql
DELETE FROM hr_emp_backup
WHERE department_id IS NULL;
```

**Explanation:** Use WHERE department_id IS NULL to target only rows with no department. NULL must be tested with IS NULL, not = NULL.

---

## Part 2: Self-Practice (No Answers)

1. Bulk insert into your backup table from hr.employees only for employees whose salary is greater than 10000.
```sql
INSERT INTO emp_backup
SELECT *
FROM hr.employees
WHERE salary > 10000

```
**Explanation:** This statement inserts multiple rows into emp_backup by selecting all employees from hr.employees whose salary is greater than 10000.

<!-- THis above code works only if both tables have same number of columns, columns are in same order,data types are compatible.
ONE MISMATCH -> ERROR(Not enough values error) 

INSERT INTO emp_backup (emp_id, name, salary, department_id)
SELECT emp_id, name, salary, department_id
FROM hr.employees
WHERE salary > 10000;

Use this instead!
-->

2. Update job_id for a specific employee_id in your backup table (choose an id and a valid job_id).
```sql
UPDATE emp_backup
SET job_id = 'ST_MAN'
WHERE employee_id = 110;

```
**Explanation:** This statement modifies the job_id to 'ST_MAN' for the row in emp_backup where employee_id equals 110.

3. Delete rows from your backup table that you inserted for testing (e.g. where employee_id = 999).
```sql
DELETE FROM emp_backup
WHERE employee_id = 999;

```
**Explanation:** This statement removes the row from emp_backup where employee_id equals 999.
---

## Part 3: Additional Practice — 20 Medium + 20 Hard Questions (With Hints)

Use **hr_emp_backup** or similar copy tables; do not modify **hr.employees** or **hr.departments** directly unless instructed.

### 20 Medium Questions

1. **M1.** Insert one row into hr_emp_backup with employee_id 990, first_name 'Test', last_name 'User', salary 4000, department_id 50.  
   **Hint:** INSERT INTO hr_emp_backup (employee_id, first_name, last_name, salary, department_id) VALUES (990, 'Test', 'User', 4000, 50);
```sql
insert into HR_EMP_BACKUP 
    (employee_id,first_name,last_name,email,salary,department_id, hire_date,job_id)
values 
    (990, 'Test', 'User','test.user@gmail.com', 4000, 50,sysdate,'IT_PROG'); 
```
**Explanation:** This statement inserts a new row into the hr_emp_backup table with employee_id = 990, first_name = 'Test', last_name = 'User', salary = 4000, and department_id = 50.

2. **M2.** Update salary to 6000 for employee_id 990 in hr_emp_backup.  
   **Hint:** UPDATE hr_emp_backup SET salary = 6000 WHERE employee_id = 990;

```sql
UPDATE hr_emp_backup
SET salary = 6000
WHERE employee_id = 990;
```
**Explaination:** 

3. **M3.** Delete the row where employee_id = 990 from hr_emp_backup.  
   **Hint:** DELETE FROM hr_emp_backup WHERE employee_id = 990;
```sql
DELETE FROM hr_emp_backup
WHERE employee_id = 990;
```
**Explaination:** 

4. **M4.** Insert into hr_emp_backup from hr.employees only for department_id 80.  
   **Hint:** INSERT INTO hr_emp_backup SELECT * FROM hr.employees WHERE department_id = 80; (match column list if needed)
```sql
insert into HR_EMP_BACKUP (employee_id, first_name, last_name, email, salary, department_id,hire_date,job_id)
select employee_id, first_name, last_name, email, salary, department_id,hire_date, job_id
from hr.EMPLOYEES
where department_id = 80;
```
**Explaination:** 

5. **M5.** Update first_name to 'Updated' for employee_id 100 in hr_emp_backup.  
   **Hint:** UPDATE hr_emp_backup SET first_name = 'Updated' WHERE employee_id = 100;
```sql
update HR_EMP_BACKUP
set FIRST_NAME = 'Updated'
where employee_id = 100;
```
**Explaination:** 

6. **M6.** Delete all rows from hr_emp_backup where department_id = 90.  
   **Hint:** DELETE FROM hr_emp_backup WHERE department_id = 90;
```sql
delete hr_emp_backup
where department_id = 90;
```
**Explaination:** 

7. **M7.** Insert two rows into hr_emp_backup (e.g. employee_id 991 and 992) using two separate INSERT statements.  
   **Hint:** Two INSERT INTO ... VALUES ... statements.
```sql
insert into hr_emp_backup
    (employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id)
values
    (991, 'Lalitha','Sowmya','ls@gmail.com', 10000, 60, sysdate, 'IT_PROG');

insert into hr_emp_backup
    (employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id)
values
    (992, 'ABC','EFG','abc@gmail.com', 1000, 80, sysdate, 'IT_PROG');
```
**Explaination:** This statements inserts two new employee records (IDs 991 and 992) into the hr_emp_backup table using two separate INSERT statements, each providing values for employee_id, first_name, last_name, salary, and department_id.

8. **M8.** Update salary by 5% for all employees in hr_emp_backup in department 50.  
   **Hint:** UPDATE hr_emp_backup SET salary = salary * 1.05 WHERE department_id = 50;
```sql
update hr_emp_backup
set salary = salary * 1.05
where department_id = 50;
```
**Explaination:** This query updates the hr_emp_backup table by increasing the salary by 5% for aall employees whose department_id is 50.
9. **M9.** Delete rows from hr_emp_backup where salary is NULL.  
   **Hint:** DELETE FROM hr_emp_backup WHERE salary IS NULL;
```sql
delete from hr_emp_backup
where salary is NULL;
```
**Explaination**  THis query deletes all rows from hr_emp_backup where the salary value is NULL

10. **M10.** Insert into hr_emp_backup from hr.employees where job_id = 'SA_REP' (all columns that exist in backup).  
    **Hint:** INSERT INTO hr_emp_backup SELECT * FROM hr.employees WHERE job_id = 'SA_REP';
```sql
insert into HR_EMP_BACKUP (employee_id, first_name, last_name, email, salary, department_id,hire_date,job_id)
select employee_id, first_name, last_name, email, salary, department_id,hire_date, job_id
from hr.EMPLOYEES
where job_id = 'SA_REP';
```
**Explaination:** 
This query inserts all employees with job_id = 'SA_REP' from hr.employees into the hr_emp_backup table.

11. **M11.** Update department_id to 60 for employee_id 105 in hr_emp_backup.  
    **Hint:** UPDATE hr_emp_backup SET department_id = 60 WHERE employee_id = 105;
```sql
update hr_emp_backup
set department_id = 60
where employee_id = 105;
```
**Explaination:** 
This query updates the department_id to 60 for the employee with employee_id 105 in the hr_emp_backup table.

12. **M12.** Delete the single row with employee_id 999 from hr_emp_backup (if it exists).  
    **Hint:** DELETE FROM hr_emp_backup WHERE employee_id = 999;
```sql
delete from hr_emp_backup
where employee_id = 999;
```
**Explaination:** 
This query deletes the row from hr_emp_backup where employee_id is 999, if that row exists.

13. **M13.** Insert one row with employee_id 993, last_name 'Lee', first_name 'Amy', salary 5500, department_id 60.  
    **Hint:** INSERT with columns in any order but VALUES in same order as columns.
```sql
insert into hr_emp_backup
    (employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id)
values
    (993, 'Amy','Lee','amylee@gmail.com', 5500, 60, sysdate, 'IT_PROG');
```
**Explaination:** 
This query inserts a new employee(ID 993) into hr_emp_backup with first name Amy, last name Lee, salary 5500, and department 60.

14. **M14.** Update last_name to 'Smith' for all employees in hr_emp_backup with first_name 'John'.  
    **Hint:** UPDATE hr_emp_backup SET last_name = 'Smith' WHERE first_name = 'John';
```sql
update hr_emp_backup
set last_name = 'Smith'
where first_name = 'John';
```
**Explaination:** 
This query updates the last_name to 'Smith' for all rows in hr_emp_backup where the first_name is 'John'

15. **M15.** Delete rows from hr_emp_backup where hire_date is before 2000.  
    **Hint:** DELETE FROM hr_emp_backup WHERE hire_date < DATE '2000-01-01';
```sql
delete from hr_emp_backup
where hire_date < DATE '2000-01-01';
```
**Explaination:** 
This query deletes all rows from hr_emp_backup where the hire_date is earlier than January 1, 2000.

16. **M16.** Insert from hr.employees where salary between 5000 and 7000 into hr_emp_backup.  
    **Hint:** INSERT INTO hr_emp_backup SELECT * FROM hr.employees WHERE salary BETWEEN 5000 AND 7000;
```sql
insert into hr_emp_backup
    (employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id)
select employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id
from hr.employees 
where salary between 5000 and 7000
```
**Explaination:** 
This query inserts all employees from hr.employees into hr_emp_backup whose salary is between 5000 and 7000.

17. **M17.** Update job_id to 'IT_PROG' for one specific employee (e.g. employee_id 200) in hr_emp_backup.  
    **Hint:** UPDATE hr_emp_backup SET job_id = 'IT_PROG' WHERE employee_id = 200;
```sql
update hr_emp_backup
set job_id = 'IT_PROG'
where employee_id = 200;
```
**Explaination:** 
This query updates the job_id to 'IT_PROG' for employee with employee_id - 200 in hr_emp_backup.

18. **M18.** Delete rows from hr_emp_backup where commission_pct is not null.  
    **Hint:** DELETE FROM hr_emp_backup WHERE commission_pct IS NOT NULL;
```sql
DELETE FROM hr_emp_backup
WHERE commission_pct IS NOT NULL;
```
**Explaination:** 
This query deletes all rows from hr_emp_backup where the commission_pct column contains a value (not NULL)

19. **M19.** Insert a row with hire_date = SYSDATE for a new employee in hr_emp_backup.  
    **Hint:** Include hire_date in INSERT and use SYSDATE in VALUES.
```sql
insert into hr_emp_backup
    (employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id)
values
    (995, 'Lalitha', 'Sowmya','ls@gmail.com',10000,40,sysdate,'IT_PROG');
```
**Explaination:** 
This query inserts a new employee into hr_emp_backup with the current system date as hire_date using SYSDATE.

20. **M20.** Update salary to 10000 for the employee with the highest employee_id in hr_emp_backup (use subquery: WHERE employee_id = (SELECT MAX(employee_id) FROM hr_emp_backup)).  
    **Hint:** UPDATE hr_emp_backup SET salary = 10000 WHERE employee_id = (SELECT MAX(employee_id) FROM hr_emp_backup);
```sql
update hr_emp_backup
set salary = 10000
where employee_id = (
    select max(employee_id) from hr_emp_backup
);
```
**Explaination:** 
This query updates the salary to 10000 for the employee whose employee_id is the highest in hr_emp_backup table.

### 20 Hard Questions

1. **H1.** Use MERGE to sync hr_emp_backup with hr.employees: when employee_id matches, update salary and hire_date; when not matched, insert the row from hr.employees.  
   **Hint:** MERGE INTO hr_emp_backup t USING hr.employees s ON (t.employee_id = s.employee_id) WHEN MATCHED THEN UPDATE SET t.salary = s.salary, t.hire_date = s.hire_date WHEN NOT MATCHED THEN INSERT (...) VALUES (s....);

```sql
MERGE INTO hr_emp_backup t
USING hr.employees s
ON (t.employee_id = s.employee_id)

WHEN MATCHED THEN
UPDATE SET
        t.salary = s.salary,
        t.hire_date = s.hire_date

WHEN NOT MATCHED THEN 
INSERT (employee_id, first_name, last_name, salary, department_id, hire_date)
VALUES (
    s.employee_id,
    s.first_name,
    s.last_name,
    s.salary,
    s.department_id,
    s.hire_date
)
```
**Explaination:** 
The statement updates existing employee records in hr_emp_backup and inserts new employees from hr.employees to keep the backup table synchronized.

2. **H2.** Update hr_emp_backup so that salary equals the salary from hr.employees for the same employee_id (only for employees in department 60).  
   **Hint:** UPDATE hr_emp_backup e SET e.salary = (SELECT salary FROM hr.employees WHERE employee_id = e.employee_id) WHERE e.employee_id IN (SELECT employee_id FROM hr.employees WHERE department_id = 60);

<!-- 1. Which table are we modifying? 
hr_emp_backup -->

<!-- 2. Where does the correct salary value come from? 
hr.employees -->

<!-- 3. To update a row in hr_emp_backup, we must know which row in hr.employees corresponds to it. What column connects two tables? 
employee_id -->

<!-- 4. We are not updating all employees. only department?
60 -->

<!-- Look at a row in hr_emp_backup -->
```sql
update hr_emp_backup e 
set e.salary = (
    select salary 
    from hr.employees 
    where employee_id = e.employee_id 
    )
where e.employee_id in (
    select employee_id 
    from hr.employees 
    where department_id = 60
);
```
**Explaination:** 
This query updates the salary in hr_emp_backup with the salary from hr.employees for employees who belong to department 60.

3. **H3.** Delete from hr_emp_backup all employees who do not exist in hr.employees (e.g. test rows).  
   **Hint:** DELETE FROM hr_emp_backup WHERE employee_id NOT IN (SELECT employee_id FROM hr.employees); or use NOT EXISTS.
   <!-- 
    1. Which table are we deleteing rows from ?
       hr_emp_backup 
    2. employees who do not exist in hr.employees. 
    Which column links both tables? 
    employee_id  

    We are using not exists over not in because not in breaks the logic and no rows get deleted. SQL cannot determine truth because comparisions with NULL are UNKNOWN.
    This is a classic SQL bug.

    NOT EXISTS doesn't suffer from NULL problem beccause it checks row existence not membership in a list.
   -->
```sql
delete from hr_emp_backup b
where not exists (
    select 1
    from hr.employees e
    where e.employee_id = b.employee_id
)
```
**Explaination:** 
This query deletes records from hr_emp_backup where the employee does not exist in hr.employees.

4. **H4.** Insert into hr_emp_backup only employees from hr.employees whose employee_id is not already in hr_emp_backup (use INSERT ... SELECT ... WHERE NOT EXISTS).  
   **Hint:** INSERT INTO hr_emp_backup SELECT * FROM hr.employees e WHERE NOT EXISTS (SELECT 1 FROM hr_emp_backup b WHERE b.employee_id = e.employee_id);
```sql
insert into hr_emp_backup (employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id)
select employee_id, first_name, last_name, email, salary, department_id,hire_date, job_id
from hr.employees e
where not exists (
    select 1
    from hr_emp_backup b
    where e.employee_id = b.employee_id
);
```
**Explaination:** 
This query inserts employees from hr.employees into hr_emp_backup only if they do not already exist in the backup table.

5. **H5.** Update hr_emp_backup: set salary to the average salary of the department (from hr.employees) for that employee's department_id.  
   **Hint:** SET salary = (SELECT AVG(salary) FROM hr.employees WHERE department_id = hr_emp_backup.department_id); use table alias in subquery.
```sql
update hr_emp_backup b
set salary = (
    select avg(salary)
    from hr.employees e
    where department_id = b.department_id
);
```
**Explaination:** 
The query updates salaries in hr_emp_backup by assigning the department wise average salary calculated from hr.employees.

6. **H6.** Delete from hr_emp_backup the single row with the smallest employee_id.  
   **Hint:** DELETE FROM hr_emp_backup WHERE employee_id = (SELECT MIN(employee_id) FROM hr_emp_backup);
```sql
delete from hr_emp_backup 
where employee_id = (
    select min(employee_id)
    from hr_emp_backup
);
```
**Explaination:** 
Deletes the min employee_id record from the backup table.

7. **H7.** Insert into a backup table one row per department from hr.departments with department_id, department_name, and a column emp_count = 0. Then (separately) update emp_count using a subquery that counts employees per department.  
   **Hint:** INSERT from departments with 0; then UPDATE ... SET emp_count = (SELECT COUNT(*) FROM hr.employees e WHERE e.department_id = backup.department_id).
```sql
create table dept_backup(
    department_id NUMBER PRIMARY KEY,
    department_name VARCHAR2(50),
    emp_count NUMBER
);

insert into dept_backup (department_id, department_name, emp_count)
select department_id, department_name, 0
from hr.departments;

update dept_backup d
set emp_count = (
    select count(*)
    from hr.employees e
    where e.department_id = d.department_id 
);
```
**Explaination:** 
Create structure, load departments with default count, then update counts using a correlated subquery.

8. **H8.** Update hr_emp_backup: set first_name and last_name from hr.employees for the same employee_id where department_id = 50.  
   **Hint:** UPDATE hr_emp_backup e SET (first_name, last_name) = (SELECT first_name, last_name FROM hr.employees WHERE employee_id = e.employee_id) WHERE e.department_id = 50;
```sql
update hr_emp_backup b
set (first_name, last_name) = (
    select e.first_name, e.last_name
    from hr.employees e
    where e.employee_id = b.employee_id AND department_id = 50
)
where exists (
    select 1
    from hr.employees e
    where e.employee_id = b.employee_id AND department_id = 50
);
```
**Explaination:** 
This query updates first_name and last_name in hr_emp_backup by fetching values from hr.employees using a correlated subquery based on matching employee_id.

It only updates rows where a corresponding employee exists in department 50, ensured by the WHERE EXISTS clause.

The WHERE EXISTS is necessary to avoid cases where the subquery returns no rows, which would otherwise result in NULL assignments and cause errors.

9. **H9.** Delete from hr_emp_backup all rows where the employee's salary in hr.employees is less than 3000 (match on employee_id).  
   **Hint:** DELETE FROM hr_emp_backup WHERE employee_id IN (SELECT employee_id FROM hr.employees WHERE salary < 3000);
```sql
-- TO find how many rows will be deleted?
select count(*) from hr_emp_backup b
where exists(
    select 1
    from hr.employees e
    where e.employee_id = b.employee_id 
    and e.salary < 3000 
);
```
```sql
-- Correct code
delete from hr_emp_backup b
where exists (
    select 1
    from hr.employees e
    where e.employee_id = b.employee_id 
    and e.salary < 3000
);
```
**Explaination:** 
This query deletes rows from hr_emp_backup where a matching employee exists in hr.employees with the same employee_id and a salary less than 3000.

The WHERE EXISTS ensures that only rows with such a matching employee are deleted, and rows without a match are ignored.

10. **H10.** Insert from hr.employees where department_id is in (10, 20, 30) and salary > 5000.  
    **Hint:** INSERT INTO hr_emp_backup SELECT * FROM hr.employees WHERE department_id IN (10,20,30) AND salary > 5000;
```sql
-- To find how many rows shall be inserted
select employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id
from hr.employees
where department_id in (10, 20, 30) and salary > 5000;
```
```sql
-- FINAL SOLUTION
insert into hr_emp_backup (
    employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id
)
select employee_id, first_name, last_name, email, salary, department_id, hire_date,job_id
from hr.employees
where department_id in (10, 20, 30) and salary > 5000;
```
**Explaination:** 
This query inserts rows into hr_emp_backup by selecting data from hr.employees. Only those rows are inserted where department_id is 10, 20, or 30 and salary is greater than 5000. The filtering is applied in the SELECT statement before insertion.

11. **H11.** Update hr_emp_backup: set department_id to 50 for all employees whose current department_id is NULL.  
    **Hint:** UPDATE hr_emp_backup SET department_id = 50 WHERE department_id IS NULL;
```sql
update hr_emp_backup 
set department_id = 50
where department_id IS NULL;
```
**Explaination:** 
This query updates hr_emp_backup by setting department_id to 50 for all rows where department_id is currently NULL.

12. **H12.** Delete from hr_emp_backup employees who have the same first_name and last_name as another row in hr_emp_backup (keep one; delete duplicates—e.g. keep min(employee_id) per name).  
    **Hint:** DELETE FROM hr_emp_backup a WHERE employee_id NOT IN (SELECT MIN(employee_id) FROM hr_emp_backup GROUP BY first_name, last_name) AND EXISTS (SELECT 1 FROM hr_emp_backup b WHERE b.first_name = a.first_name AND b.last_name = a.last_name AND b.employee_id < a.employee_id); or use ROW_NUMBER() in subquery.
```sql
delete from hr_emp_backup b 
where exists (
    select 1
    from hr_emp_backup x
    where x.first_name = b.first_name
    and x.last_name = b.last_name
    and x.employee_id < b.employee_id
); 
```
**Explaination:** 
It deletes duplicate rows in hr_emp_backup by keeping only the row with the smallest employee_id for each (first_name, last_name).

13. **H13.** MERGE: for rows in hr.employees that exist in hr_emp_backup, update salary; for rows that do not exist, insert. Use department_id 80 only.  
    **Hint:** MERGE USING (SELECT * FROM hr.employees WHERE department_id = 80) s ON ...
```sql
-- SYNTAX FOR MERGE
merge into targetTable t
using sourceTable s
on (matching condition)

when matched then
update

when unmatched then 
insert 
```
```sql
merge into hr_emp_backup b
using (
    select *
    from hr.employees
    where department_id = 80
) e
on (b.employee_id = e.employee_id)

when matched then
    update set b.salary = e.salary

when not matched then
    insert (
        employee_id, first_name, last_name, email,
        salary, department_id, hire_date, job_id
    )
    values (
        e.employee_id, e.first_name, e.last_name, e.email,
        e.salary, e.department_id, e.hire_date, e.job_id
    );
```
**Explaination:** 
It synchronizes hr_emp_backup with hr.employees (dept 80) by updating existing rows and inserting missing ones based on employee_id.

14. **H14.** Update hr_emp_backup so salary is increased by 10% only for employees whose salary in hr.employees is below the company average.  
    **Hint:** UPDATE hr_emp_backup SET salary = salary * 1.10 WHERE employee_id IN (SELECT employee_id FROM hr.employees WHERE salary < (SELECT AVG(salary) FROM hr.employees));
```sql
update hr_emp_backup b
set salary = salary * 1.1
where exists (
    select 1
    from hr.employees e
    where e.employee_id = b.employee_id
    and e.salary < (
        select avg(salary)
        from hr.employees
    )
```
**Explaination:** 
This query updates rows from hr_emp_backup where a matching employee exists in hr.employees with the same employee_id and a salary less than average salary of the company.

The WHERE EXISTS ensures that only rows with such a matching employee are updated, and rows without a match are ignored.

15. **H15.** Delete from hr_emp_backup where hire_date is the earliest in the table (only one row).  
    **Hint:** DELETE FROM hr_emp_backup WHERE hire_date = (SELECT MIN(hire_date) FROM hr_emp_backup);
```sql
delete from hr_emp_backup 
where hire_date = (select min(hire_date) from hr_emp_backup);
```
**Explaination:** 
This query deletes the single row who has highest experience from the backup table.

16. **H16.** Insert into hr_emp_backup from hr.employees only for employees who are managers (employee_id in (SELECT manager_id FROM hr.employees)).  
    **Hint:** INSERT ... SELECT * FROM hr.employees WHERE employee_id IN (SELECT manager_id FROM hr.employees WHERE manager_id IS NOT NULL);
```sql
insert into hr_emp_backup(employee_id, first_name, last_name, email,
         salary, department_id, hire_date, job_id)
select employee_id, first_name, last_name, email,
         salary, department_id, hire_date, job_id
from hr.employees
where employee_id in (
    select manager_id from hr.employees 
);
```
**Explaination:** 
Inserts only those rows who has same employee_id in both hr_emp_backup and hr.employees tables where they are managers in the hr.employees

17. **H17.** Update last_name in hr_emp_backup to UPPER(last_name) for all rows.  
    **Hint:** UPDATE hr_emp_backup SET last_name = UPPER(last_name);
```sql
update hr_emp_backup 
set last_name = UPPER(last_name)
```
**Explaination:** 
Updates all the rows in the backup table last_name to upper case using UPPER function.

18. **H18.** Delete from hr_emp_backup the top 5 highest salary earners (use subquery with ROWNUM or FETCH).  
    **Hint:** DELETE FROM hr_emp_backup WHERE employee_id IN (SELECT employee_id FROM (SELECT employee_id FROM hr_emp_backup ORDER BY salary DESC FETCH FIRST 5 ROWS ONLY));
```sql
delete from hr_emp_backup 
where employee_id in (select employee_id
from hr_emp_backup 
where salary IS NOT NULL
order by salary
desc fetch first 5 rows only);
```
**Explaination:** 
This query fetches the first 5 values in the table whose salaries are top 5 and deletes those rows.

19. **H19.** Insert from hr.employees where job_id like 'SA%' and commission_pct is not null.  
    **Hint:** INSERT INTO hr_emp_backup SELECT * FROM hr.employees WHERE job_id LIKE 'SA%' AND commission_pct IS NOT NULL;
```sql
insert into hr_emp_backup b(
    employee_id, first_name, last_name, email, salary, department_id, hire_date, job_id
)
select employee_id, first_name, last_name, email, salary, department_id, hire_date, job_id 
from hr.employees e
where e.job_id LIKE 'SA%' 
and e.commission_pct is not null; 
```
**Explaination:** 
inserts only those rows who satisfies job_id is 'SA%' and commission_pct is not null.

20. **H20.** Update hr_emp_backup: set salary to the max salary in the same department (from hr.employees) for each employee.  
    **Hint:** UPDATE hr_emp_backup e SET salary = (SELECT MAX(salary) FROM hr.employees WHERE department_id = e.department_id) WHERE department_id IS NOT NULL;
```sql
update hr_emp_backup b
set salary = (
    select max(salary)
    from hr.employees e 
    where b.employee_id = e.employee_id
)
where department_id is not null;
```
**Explaination:** 

---

[← Back to Learning Plan](../30-day-sql-plsql-learning-plan.md) | [Tutorial](../tutorials/day04_dml_basics.md)
