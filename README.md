# sqlAssignment 1


```sql

SELECT employee_number
FROM employees
WHERE employee_name = 'MARTIN';



SELECT employee_name, salary
FROM employees
WHERE salary > 1500;


SELECT employee_name,
       ROUND(salary * 0.90, 2) AS salary_after_10pct_deduction
FROM employees
WHERE job_title = 'CLERK';


SELECT employee_name
FROM employees
WHERE hire_date < '1981-05-01';


SELECT employee_name, salary
FROM employees
ORDER BY salary DESC;


SELECT department_number, department_name, office_location
FROM departments
ORDER BY office_location;

SELECT department_name
FROM departments
WHERE office_location = 'NEW YORK';

SELECT employee_name
FROM employees
WHERE employee_name LIKE 'J%S';


SELECT employee_name
FROM employees
WHERE job_title = 'MANAGER' AND employee_name LIKE 'J%S';


SELECT d.department_number, d.department_name,
       COUNT(e.employee_number) AS employee_count
FROM departments d
LEFT JOIN employees e
  ON e.department_number = d.department_number
GROUP BY d.department_number, d.department_name
ORDER BY d.department_number;


```


# sqlAssignment 2


```sql

SELECT COUNT(*) AS employee_count FROM employees;


SELECT SUM(salary) AS total_salary FROM employees;



SELECT AVG(salary) AS avg_salary_dept20
FROM employees
WHERE department_number = 20;




SELECT DISTINCT job_title
FROM employees
ORDER BY job_title;



SELECT d.department_number, d.department_name,
       COUNT(e.employee_number) AS employee_count
FROM departments d
LEFT JOIN employees e
  ON e.department_number = d.department_number
GROUP BY d.department_number, d.department_name
ORDER BY d.department_number;




SELECT d.department_number,
       MAX(e.salary) AS max_salary
FROM departments d
LEFT JOIN employees e
  ON e.department_number = d.department_number
GROUP BY d.department_number
ORDER BY max_salary DESC;



SELECT SUM(salary + COALESCE(commission,0)) AS total_comp
FROM employees;


```



# sqlAssignment 3


```sql
SELECT *
FROM employees e
INNER JOIN departments d
  ON e.department_number = d.department_number;



SELECT e.employee_name, d.department_name
FROM employees e
INNER JOIN departments d
  ON e.department_number = d.department_number
ORDER BY e.employee_name ASC;





SELECT e.employee_name, d.department_name
FROM employees e
LEFT JOIN departments d
  ON e.department_number = d.department_number
ORDER BY e.employee_name;



SELECT departments.department_name, COUNT(employees.employee_number)
FROM employees
JOIN departments
  ON departments.department_number = employees.department_number
GROUP BY department_name;



SELECT d.department_name, COUNT(e.employee_number) AS employee_count
FROM employees e
RIGHT JOIN departments d
  ON d.department_number = e.department_number
GROUP BY d.department_name
ORDER BY d.department_name;


SELECT *
FROM employees employee
JOIN employees manager
  ON employee.manager_id = manager.employee_number
ORDER BY employee.employee_name;



SELECT e.employee_name  AS employee,
       m.employee_name  AS manager
FROM employees e
LEFT JOIN employees m
  ON e.manager_id = m.employee_number
ORDER BY e.employee_name;



SELECT e.department_number,
       COUNT(*) AS number_of_employees
FROM employees e
GROUP BY e.department_number
HAVING COUNT(*) > 3;


SELECT employee_name, salary
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees)
ORDER BY salary DESC;


```

