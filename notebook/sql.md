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
