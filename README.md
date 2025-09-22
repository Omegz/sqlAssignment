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




# sqlAssignment 4


```sql
CREATE TABLE leaders (
  leader_id   INT PRIMARY KEY,
  leader_name VARCHAR(30) NOT NULL
);


INSERT INTO leaders (leader_id, leader_name) VALUES
  (7839, 'KING'),   -- PRESIDENT
  (7698, 'BLAKE'),  -- MANAGER
  (7782, 'CLARK'),  -- MANAGER
  (7566, 'JONES'),  -- MANAGER
  (7902, 'FORD'),   -- ANALYST (manages SMITH)
  (7788, 'SCOTT');  -- ANALYST (manages ADAMS)


CREATE TABLE employees_leaders (
  employee_number INT NOT NULL,
  leader_id       INT NOT NULL,
  PRIMARY KEY (employee_number, leader_id),
  CONSTRAINT fk_el_employee
    FOREIGN KEY (employee_number) REFERENCES employees(employee_number)
    ON UPDATE CASCADE ON DELETE CASCADE,
  CONSTRAINT fk_el_leader
    FOREIGN KEY (leader_id) REFERENCES leaders(leader_id)
    ON UPDATE CASCADE ON DELETE CASCADE
);



INSERT INTO employees_leaders VALUES
  (7499, 7698), (7499, 7839); 
  


INSERT INTO employees_leaders VALUES
  (7698, 7839);                


INSERT INTO employees_leaders VALUES
  (7782, 7839),                
  (7934, 7782);                


INSERT INTO employees_leaders VALUES
  (7566, 7839),                
  (7788, 7566);              


SELECT e.employee_name AS employee,
       l.leader_name   AS leader
FROM employees e
JOIN employees_leaders el
  ON e.employee_number = el.employee_number
JOIN leaders l
  ON el.leader_id = l.leader_id
ORDER BY e.employee_name, l.leader_name;






```
