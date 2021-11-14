# /[блокноты](https://mmmylnikov.github.io/notebook/)/SQL

## 📝 Рецепты кода / Разметка / SQL

> Источник: [Базовый курс SQL для аналитиков и менеджеров… (юдеми)](https://www.udemy.com/course/sql-for-beginner/)


### Типы данных
```sql
-- Символьные типы данных
select 'Любое текстовое значение' as TEST from dual;
select 'Пример указания ''апострофов'' в тексте' as TEST from dual;
select 'Пример указания двойных "кавычек" в тексте' as TEST from dual;
select 'Пример соединения ' || 'двух тестовых значений' as TEST from dual;

-- Числовые типы данных
select 100 as TEST from dual;
select '100' + 10 as TEST from dual;
select 100 - 10 as TEST from dual;
select 100 / 2 as TEST from dual;

-- Типы данных даты и времени
select '01.01.2019' as TEST from dual;
select to_date('01.01.2019', 'dd.mm.yyyy') as TEST from dual;
select to_date('01.01.2019', 'dd.mm.yyyy') + 10 as TEST from dual;
select to_date('01.01.2019', 'dd.mm.yyyy') - 1 as TEST from dual;
```

### Запросы на выборку

```sql
SELECT * FROM employees;


SELECT employee_id, first_name, last_name, email, phone_number, hire_date, job_id, salary, commission_pct, manager_id, department_id
FROM employees;


SELECT
    employee_id,
    first_name,
    last_name,
    email,
    phone_number,
    hire_date,
    job_id,
    salary,
    commission_pct,
    manager_id,
    department_id
FROM
    employees;


SELECT employee_id, first_name, last_name, salary, department_id
FROM employees;


SELECT employee_id, first_name, last_name, department_id, salary
FROM employees;


SELECT employee_id, first_name, last_name, department_id, salary
FROM employees
WHERE department_id = 80;


SELECT employee_id, first_name, last_name, department_id, salary
FROM employees
WHERE department_id = 80
ORDER BY salary;


SELECT employee_id, first_name, last_name, department_id, salary
FROM employees
WHERE department_id = 80
ORDER BY salary ASC;


SELECT employee_id, first_name, last_name, department_id, salary
FROM employees
WHERE department_id = 80
ORDER BY salary DESC;


SELECT department_id, salary
FROM employees
WHERE department_id = 80;


SELECT department_id, sum(salary)
FROM employees
WHERE department_id = 80
GROUP BY department_id;


SELECT department_id, sum(salary) as total_salary
FROM employees
WHERE department_id = 80
GROUP BY department_id;
```

### Фильтрация строк в запросе Select. Работа с операторами AND, OR, IN, NOT IN
> Источник: https://www.youtube.com/watch?v=OWSRLbj1afo

```sql
SELECT * FROM employees;


SELECT * FROM employees
WHERE rownum <= 10;


SELECT * FROM employees
WHERE department_id = 80;


SELECT * FROM employees
WHERE department_id = 80 AND manager_id = 100;


SELECT * FROM employees
WHERE department_id = 80 OR manager_id = 100;


SELECT * FROM employees
WHERE
    department_id = 80
    OR (department_id = 60 AND manager_id = 103)
;


SELECT * FROM employees
WHERE
    department_id = 80
    OR (department_id = 60 AND manager_id = 103)
    OR (department_id = 90 AND manager_id = 100)
;


SELECT * FROM employees WHERE department_id = 80 OR (department_id = 60 AND manager_id = 103) OR (department_id = 90 AND manager_id = 100);


SELECT 1 + 3 * 2 FROM dual;
SELECT (1 + 3) * 2 FROM dual;


SELECT * FROM employees
WHERE department_id = 80 OR (department_id = 60 AND manager_id = 103);


SELECT * FROM employees
WHERE (department_id = 80 OR department_id = 60) AND manager_id = 103;


SELECT * FROM employees
WHERE
    employee_id = 100
    OR employee_id = 101
    OR employee_id = 102
;


SELECT * FROM employees
WHERE employee_id IN (100, 101, 102);


SELECT * FROM employees
WHERE  employee_id NOT IN (100, 101, 102);


SELECT * FROM employees
WHERE
    last_name = 'King'
    OR last_name = 'Lorentz'
;


SELECT * FROM employees
WHERE last_name IN ('King', 'Lorentz');


SELECT * FROM employees
WHERE UPPER(last_name) IN ('KING', 'LORENTZ');


SELECT
    last_name,
    UPPER(last_name) AS last_name_2,
    LOWER(last_name) AS last_name_3
FROM employees;
```

### Фильтрация строк в запросе Select. Работа с оператором BETWEEN и вложенными SQL запросами
> Источник: https://www.youtube.com/watch?v=wZSLOKnmqEc

```sql
SELECT * FROM departments;
 
SELECT * FROM employees
WHERE department_id IN (30, 90, 100);
 
SELECT * FROM departments
WHERE DEPARTMENT_NAME IN ('Purchasing', 'Executive', 'Finance');
 
SELECT * FROM employees
WHERE department_id IN 
(
     SELECT * FROM departments
     WHERE DEPARTMENT_NAME IN ('Purchasing', 'Executive', 'Finance')
);
 
SELECT * FROM employees
WHERE department_id IN 
(
     SELECT department_id FROM departments
     WHERE DEPARTMENT_NAME IN ('Purchasing', 'Executive', 'Finance')
);
 
SELECT * FROM employees
WHERE HIRE_DATE BETWEEN '01.06.05' AND '31.08.05';
 
SELECT * FROM employees
WHERE employee_id BETWEEN 100 AND 110;
```