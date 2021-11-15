# /[блокноты](https://mmmylnikov.github.io/notebook/)/SQL

## 📝 Рецепты кода / Разметка / SQL

> Источник: [Базовый курс SQL для аналитиков и менеджеров… (юдеми)](https://www.udemy.com/course/sql-for-beginner/)

## Введение
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
## Выборка, фильтрация, агрегация
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

### Фильтрация строк в запросе Select. Работа с операторами LIKE и NOT LIKE.
> Источник: https://www.youtube.com/watch?v=peuQL60RFxg

```sql
SELECT * FROM employees
WHERE JOB_ID LIKE '%ACCOUNT%';
 
SELECT * FROM employees
WHERE JOB_ID LIKE '%R%REP';
 
SELECT TABLE_NAME, column_name, data_type FROM user_tab_columns
WHERE COLUMN_NAME LIKE '%DEPARTMENT%';
 
SELECT TABLE_NAME, column_name, data_type FROM user_tab_columns
WHERE COLUMN_NAME LIKE '%department%';
 
SELECT TABLE_NAME, column_name, data_type FROM user_tab_columns
WHERE LOWER(COLUMN_NAME) LIKE '%department%';
 
SELECT TABLE_NAME, column_name, data_type FROM user_tab_columns
WHERE COLUMN_NAME NOT LIKE '%DEPARTMENT%';
```

### Фильтрация строк в запросе Select. Специфика значений NULL
> Источник: https://www.youtube.com/watch?v=5P0a5SODbEQ
 
```sql
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, MANAGER_ID, DEPARTMENT_ID 
FROM employees
WHERE 
     department_id = 90
;
 
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, MANAGER_ID, DEPARTMENT_ID 
FROM employees
WHERE 
    department_id = 90 
    AND manager_id = '(null)'
;
 
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, MANAGER_ID, DEPARTMENT_ID 
FROM employees
WHERE 
    department_id = 90 
    AND manager_id IS NULL
;
 
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, MANAGER_ID, DEPARTMENT_ID 
FROM employees
WHERE 
    department_id = 90 
    AND manager_id IS NOT NULL
;
 
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, nvl(MANAGER_ID, 0) AS MANAGER_ID, DEPARTMENT_ID 
FROM employees
WHERE 
    department_id = 90
;
```

### Агрегация данных в SQL с помощью функции COUNT
> Источник: https://www.youtube.com/watch?v=8h7JGr9loFo
 
```sql
SELECT * FROM EMPLOYEES;
 
SELECT COUNT(*) FROM EMPLOYEES;
 
SELECT COUNT(*) FROM EMPLOYEES
WHERE MANAGER_ID = 100;
 
SELECT JOB_ID, COUNT(*) FROM EMPLOYEES
GROUP BY JOB_ID;
 
SELECT JOB_ID, DEPARTMENT_ID, COUNT(*) FROM EMPLOYEES
GROUP BY JOB_ID, DEPARTMENT_ID;
 
SELECT JOB_ID, COUNT(DEPARTMENT_ID) FROM EMPLOYEES
GROUP BY JOB_ID;
 
SELECT COUNT(DEPARTMENT_ID), COUNT(*) FROM EMPLOYEES;
 
SELECT DEPARTMENT_ID, COUNT(*) FROM EMPLOYEES
GROUP BY DEPARTMENT_ID;
```

### Агрегация данных в SQL. Функции SUM, MIN, MAX, AVG
> Источник: https://www.youtube.com/watch?v=tzR4Ar6zG80
 
```sql
SELECT SUM(SALARY) 
FROM EMPLOYEES;
 
 
SELECT JOB_ID, SUM(SALARY) 
FROM EMPLOYEES
GROUP BY JOB_ID;
 
 
SELECT JOB_ID, SUM(SALARY), MIN(SALARY) 
FROM EMPLOYEES
GROUP BY JOB_ID;
 
 
SELECT JOB_ID, SUM(SALARY), MIN(SALARY), MAX(SALARY) 
FROM EMPLOYEES
GROUP BY JOB_ID;
 
 
SELECT JOB_ID, SUM(SALARY), MIN(SALARY), MAX(SALARY), avg(SALARY)  
FROM EMPLOYEES
GROUP BY JOB_ID;
 
 
SELECT 
    JOB_ID AS ДОЛЖНОСТЬ_СОТРУДНИКА, 
    SUM(SALARY) AS ОБЩАЯ_ЗП, 
    MIN(SALARY) AS МИНИМАЛЬНАЯ_ЗП, 
    MAX(SALARY) AS МАКСИМАЛЬНАЯ_ЗП, 
    avg(SALARY) AS СРЕДНЯЯ_ЗП  
FROM EMPLOYEES
GROUP BY JOB_ID;
 
 
SELECT 
    JOB_ID AS ДОЛЖНОСТЬ_СОТРУДНИКА,
    DEPARTMENT_ID AS ДЕПАРТАМЕНТ_СОТРУДНИКА,
    SUM(SALARY) AS ОБЩАЯ_ЗП, 
    MIN(SALARY) AS МИНИМАЛЬНАЯ_ЗП, 
    MAX(SALARY) AS МАКСИМАЛЬНАЯ_ЗП, 
    avg(SALARY) AS СРЕДНЯЯ_ЗП  
FROM EMPLOYEES
WHERE DEPARTMENT_ID IN (90, 100) 
GROUP BY JOB_ID, DEPARTMENT_ID
ORDER BY JOB_ID, DEPARTMENT_ID;
```

### Оператор DISTINCT. Подсчет уникальных записей и удаление дублей
> Источник https://www.youtube.com/watch?v=tPv5ZSzPWc4
 
```sql
SELECT COUNT(JOB_ID)
FROM EMPLOYEES;
 
 
SELECT COUNT(JOB_ID), COUNT(DISTINCT JOB_ID)
FROM EMPLOYEES;
 
 
SELECT DISTINCT JOB_ID
FROM EMPLOYEES;
 
 
SELECT DISTINCT JOB_ID, MANAGER_ID, DEPARTMENT_ID
FROM EMPLOYEES;
 
 
SELECT DISTINCT JOB_ID, MANAGER_ID, DEPARTMENT_ID
FROM EMPLOYEES
WHERE DEPARTMENT_ID = 50;
 
 
SELECT DISTINCT JOB_ID, MANAGER_ID, DEPARTMENT_ID
FROM EMPLOYEES
WHERE DEPARTMENT_ID = 50
ORDER BY JOB_ID, MANAGER_ID;
 
 
SELECT COUNT(DISTINCT JOB_ID, MANAGER_ID, DEPARTMENT_ID)
FROM EMPLOYEES
WHERE DEPARTMENT_ID = 50;
 
 
SELECT COUNT(DISTINCT JOB_ID || MANAGER_ID || DEPARTMENT_ID)
FROM EMPLOYEES
WHERE DEPARTMENT_ID = 50;
 
 
SELECT DISTINCT JOB_ID || MANAGER_ID || DEPARTMENT_ID
FROM EMPLOYEES
WHERE DEPARTMENT_ID = 50;
```

### Фильтрация строк с помощью предложения HAVING. Сортировка значений NULL
> Источник: https://www.youtube.com/watch?v=MS0AdDy-ThA
 
```sql
SELECT JOB_ID, DEPARTMENT_ID, COUNT(*) AS COUNT_JOB_ID
FROM EMPLOYEES
WHERE DEPARTMENT_ID IS NOT NULL
GROUP BY JOB_ID, DEPARTMENT_ID
;
 
 
SELECT JOB_ID, DEPARTMENT_ID, COUNT(*) AS COUNT_JOB_ID
FROM EMPLOYEES
WHERE DEPARTMENT_ID IS NOT NULL
GROUP BY JOB_ID, DEPARTMENT_ID
HAVING COUNT(*) >= 20
;
 
 
SELECT DEPARTMENT_NAME, MANAGER_ID 
FROM DEPARTMENTS
ORDER BY MANAGER_ID ASC
;
 
 
SELECT DEPARTMENT_NAME, MANAGER_ID 
FROM DEPARTMENTS
ORDER BY MANAGER_ID ASC NULLS FIRST 
;
```
## Создание, удаление, переименование таблиц
### Создание таблиц в базе данных
> Источник: https://www.youtube.com/watch?v=cXqZRg-pewM
 
```sql
CREATE TABLE KMV_CUSTOMERS
    ( 
        customer_id     NUMBER,
        customer_name   varchar2(20),
        city            varchar2(20)
    )
;
 
 
 
CREATE TABLE KMV_CUSTOMERS
    ( 
        customer_id     NUMBER          NOT NULL,
        customer_name   varchar2(20)    NOT NULL,
        city            varchar2(20)
    )
;
```

### Переименование и удаление таблиц в базе данных
> Источник: https://www.youtube.com/watch?v=VKhLWx7ue6A
 
```sql
CREATE TABLE KMV_CUSTOMERS
    ( 
        customer_id     NUMBER,
        customer_name   varchar2(20),
        city            varchar2(20)
    )
;
 
 
ALTER TABLE OLD_TABLE RENAME TO NEW_TABLE;
ALTER TABLE KMV_CUSTOMERS RENAME TO KMV_CUSTOMERS_NEW;
 
 
SELECT * FROM KMV_CUSTOMERS;
SELECT * FROM KMV_CUSTOMERS_NEW;
 
 
DROP TABLE TABLE_NAME;
DROP TABLE KMV_CUSTOMERS_NEW;
DROP TABLE TABLE_NAME purge;
```
## Вставка, обновление, удаление данных
### Вставка данных в таблицу
> Источник: https://www.youtube.com/watch?v=rd4ULZdOTzw

```sql 
SELECT * FROM KMV_CUSTOMERS;
 
 
CREATE TABLE KMV_CUSTOMERS
    ( 
        customer_id         NUMBER,
        customer_name   varchar2(50),
        city            varchar2(50)
    )
;
 
 
INSERT INTO KMV_CUSTOMERS 
     (customer_id, customer_name, city)
VALUES
     (991, 'Иванов Иван Иванович', 'Москва');
commit;
 
 
INSERT INTO KMV_CUSTOMERS (customer_id, customer_name, city) VALUES (992, 'Петров Иван Иванович', 'Пермь');
INSERT INTO KMV_CUSTOMERS (customer_id, customer_name, city) VALUES (993, 'Сидоров Иван Иванович', 'Краснодар');
INSERT INTO KMV_CUSTOMERS (customer_id, customer_name, city) VALUES (994, 'Скворцов Иван Иванович', 'Уфа');
commit;
 
 
INSERT ALL
  INTO KMV_CUSTOMERS (customer_id, customer_name, city) VALUES (995, 'Петров Иван Иванович', 'Мурманск')
  INTO KMV_CUSTOMERS (customer_id, customer_name, city) VALUES (996, 'Петров Иван Иванович', 'Омск')
  INTO KMV_CUSTOMERS (customer_id, customer_name, city) VALUES (997, 'Петров Иван Иванович', 'Волгоград')
SELECT * FROM dual;
commit;
 
 
SELECT
    EMPLOYEE_ID,
    FIRST_NAME ||' '|| LAST_NAME AS CUSTOMER_NAME,
    'n/a' AS CITY
FROM HR.EMPLOYEES
WHERE EMPLOYEE_ID IN (100, 105, 110, 115, 120)
ORDER BY EMPLOYEE_ID;
 
 
INSERT INTO KMV_CUSTOMERS (CUSTOMER_ID, CUSTOMER_NAME, CITY)
SELECT
    EMPLOYEE_ID,
    FIRST_NAME ||' '|| LAST_NAME AS CUSTOMER_NAME,
    'n/a' AS CITY
FROM HR.EMPLOYEES
WHERE EMPLOYEE_ID IN (100, 105, 110, 115, 120)
ORDER BY EMPLOYEE_ID;
commit;
 
 
INSERT INTO KMV_CUSTOMERS (CITY, CUSTOMER_NAME, CUSTOMER_ID)
VALUES ('Уфа', 'Скворцов Иван Иванович', 994);
commit;
 
 
INSERT INTO KMV_CUSTOMERS (CITY, CUSTOMER_ID)
VALUES ('Уфа', 994);
commit;
 
 
INSERT INTO KMV_CUSTOMERS 
VALUES  (997, 'Петров Иван Иванович', 'Волгоград');
commit;
 
 
DROP TABLE KMV_CUSTOMERS_NEW purge;
CREATE TABLE KMV_CUSTOMERS_NEW 
AS
SELECT
    EMPLOYEE_ID,
    FIRST_NAME ||' '|| LAST_NAME AS CUSTOMER_NAME,
    'n/a' AS CITY
FROM HR.EMPLOYEES
WHERE EMPLOYEE_ID IN (100, 105, 110, 115, 120)
ORDER BY EMPLOYEE_ID;
commit;
 
 
SELECT * FROM KMV_CUSTOMERS_NEW;
```

### Обновление и удаление данных в таблице
> Источник: https://www.youtube.com/watch?v=xPYxWoj8cuw

```sql 
SELECT * FROM KMV_CUSTOMERS;
 
 
CREATE TABLE KMV_CUSTOMERS AS
SELECT EMPLOYEE_ID, FIRST_NAME, LAST_NAME, HIRE_DATE
FROM HR.EMPLOYEES
WHERE EMPLOYEE_ID IN (100, 105, 110, 115, 120);
commit;
 
 
UPDATE KMV_CUSTOMERS
SET HIRE_DATE = '01.01.1999'
WHERE EMPLOYEE_ID = 105;
commit;
 
 
UPDATE KMV_CUSTOMERS
SET FIRST_NAME = 'Иван',
    LAST_NAME = 'Иванов'
WHERE EMPLOYEE_ID = 105;
commit;
 
 
UPDATE KMV_CUSTOMERS
SET FIRST_NAME = 'Иван',
    LAST_NAME = 'Иванов'
WHERE EMPLOYEE_ID IS NOT NULL;
commit;
 
 
DELETE FROM KMV_CUSTOMERS
WHERE EMPLOYEE_ID = 105;
commit;
 
 
DELETE FROM KMV_CUSTOMERS
WHERE EMPLOYEE_ID IS NOT NULL;
commit;
```

## Объединение таблиц
### INNER JOIN
> Источник: https://www.youtube.com/watch?v=uTCr_nMmQjU
 
```sql
SELECT * FROM EMPLOYEES
WHERE 
    DEPARTMENT_ID IN 
        (
            SELECT DEPARTMENT_ID
            FROM DEPARTMENTS
            WHERE DEPARTMENT_NAME IN ('IT', 'Finance') 
        )
;
 
SELECT 
    a.* 
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
WHERE 
    b.DEPARTMENT_NAME IN ('IT', 'Finance')
;
 
SELECT 
    a.* 
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
 
SELECT * FROM DEPARTMENTS_2
;
 
SELECT 
    a.* 
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
 
SELECT 
    a.*, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
 
SELECT 
    a.*, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
WHERE 
    b.DEPARTMENT_NAME IN ('IT', 'Finance')
;
 
SELECT 
    a.EMPLOYEE_ID, a.FIRST_NAME, a.LAST_NAME, a.DEPARTMENT_ID, b.DEPARTMENT_NAME, b.LOCATION_ID
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
WHERE 
    b.DEPARTMENT_NAME IN ('IT', 'Finance')
;
 
SELECT 
    b.EMPLOYEE_ID, b.FIRST_NAME, b.LAST_NAME, b.DEPARTMENT_ID, a.DEPARTMENT_NAME, a.LOCATION_ID
FROM 
    DEPARTMENTS a
    INNER JOIN EMPLOYEES b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
WHERE 
    a.DEPARTMENT_NAME IN ('IT', 'Finance')
;
```

### LEFT JOIN
> Источник: https://www.youtube.com/watch?v=O57gQ3c0aEk
 
```sql
SELECT * FROM DEPARTMENTS_2
;
 
SELECT 
    a.*, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    INNER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
 
SELECT 
    a.*, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    LEFT OUTER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
 
SELECT 
    a.*, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    LEFT OUTER JOIN DEPARTMENTS b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
```
### RIGHT JOIN
>   Источник: https://www.youtube.com/watch?v=nJmEYZgxzDU

```sql
SELECT 
    a.EMPLOYEE_ID, a.FIRST_NAME, a.LAST_NAME, a.DEPARTMENT_ID, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    LEFT OUTER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
WHERE 
    a.EMPLOYEE_ID = '109'
;
 
 
SELECT 
    a.EMPLOYEE_ID, a.FIRST_NAME, a.LAST_NAME, a.DEPARTMENT_ID, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    RIGHT OUTER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
WHERE 
    a.EMPLOYEE_ID = '109'
;
 
 
SELECT 
    a.EMPLOYEE_ID, a.FIRST_NAME, a.LAST_NAME, a.DEPARTMENT_ID, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    RIGHT OUTER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
 
 
SELECT 
    a.EMPLOYEE_ID, a.FIRST_NAME, a.LAST_NAME, a.DEPARTMENT_ID, b.DEPARTMENT_NAME
FROM 
    EMPLOYEES a
    LEFT OUTER JOIN DEPARTMENTS_2 b ON a.DEPARTMENT_ID = b.DEPARTMENT_ID
;
```

###  FULL JOIN
> Источник: https://www.youtube.com/watch?v=KsBIHB1covo
 
```sql
SELECT LOCATION_ID, STREET_ADDRESS, POSTAL_CODE, CITY, STATE_PROVINCE, COUNTRY_ID
FROM LOCATIONS
;
 
SELECT COUNTRY_ID, COUNTRY_NAME, REGION_ID
FROM COUNTRIES
;
 
SELECT DISTINCT CITY, COUNTRY_ID
FROM LOCATIONS
;
 
SELECT 
    DISTINCT a.CITY, a.COUNTRY_ID, b.COUNTRY_NAME, b.REGION_ID
FROM 
    LOCATIONS a
    FULL OUTER JOIN COUNTRIES b ON a.COUNTRY_ID = b.COUNTRY_ID
;
```

## Работа с множествами в SQL (UNION, MINUS, INTERSECT)
> Источник: https://www.youtube.com/watch?v=1n9oQE9i85c
 
```sql
SELECT * FROM DEPARTMENTS_NEW;
SELECT * FROM DEPARTMENTS_OLD;
 
 
SELECT * FROM DEPARTMENTS_NEW
UNION ALL
SELECT * FROM DEPARTMENTS_OLD
;
 
 
SELECT * FROM DEPARTMENTS_NEW
UNION
SELECT * FROM DEPARTMENTS_OLD
;
 
 
SELECT * FROM DEPARTMENTS_NEW
MINUS
SELECT * FROM DEPARTMENTS_OLD
;
 
 
SELECT * FROM DEPARTMENTS_NEW
INTERSECT 
SELECT * FROM DEPARTMENTS_OLD
;
``` 
 
## Полезные операторы и функции SQL
### Функции SQL для числовых типов данных (ROUND, ABS, TRUNC)
> Источник: https://youtu.be/m3ZeiBxkg70
 
```sql
--ROUND
SELECT ROUND(123.456, 0) FROM DUAL;
SELECT ROUND(123.456, 1) FROM DUAL;
SELECT ROUND(123.456, 2) FROM DUAL;
 
--ABS
SELECT ABS(-5) FROM DUAL;
SELECT ABS(-5.6) FROM DUAL;
SELECT ABS(5.65) FROM DUAL;
 
--TRUNC
SELECT TRUNC(123.4567, 0) FROM DUAL;
SELECT TRUNC(123.4567, 1) FROM DUAL;
SELECT TRUNC(123.4567, 2) FROM DUAL;
```

### Числовые / математические функции Oracle PL/SQL
> Источник: https://oracleplsql.ru/numeric-mathematical.html
```sql
ABS -- абсолютное значение числа.
ACOS -- арккосинус числа.
ASIN -- арксинус числа.
ATAN -- арктангенс числа.
ATAN2 -- арктангенс n и m.
AVG -- среднее значение выражения.
BITAND -- целое число, представляющее побитовую операцию AND над битами expr1 и expr2.
CEIL -- наименьшее целое число, которое больше или равно number.
COS -- косинус числа.
COSH -- гиперболический косинус числа.
COUNT -- количество возращенных запросом строк.
EXP -- e, возведенное в n-ную степень, где е = 2,71828183.
FLOOR -- наибольшее целое значение, равное или меньшее, чем число.
GREATEST -- наибольшее значение в списке выражений.
LEAST -- наименьшее значение в списке выражений.
LN -- натуральный логарифм числа.
LOG -- логарифм n по основанию m.
MAX -- максимальное значение выражения.
MEDIAN -- медиану выражения.
MIN -- минимальное значение выражения.
MOD -- остаток от деления m на n.
POWER -- возводит m в степень n.
REGEXP_COUNT -- подсчитывает количество вхождений шаблона в строку. Эта функция, введенная в Oracle 11g, позволит вам подсчитать количество раз, когда подстрока встречается в строке с использованием сопоставления шаблонов регулярных выражений.
REMAINDER -- остаток от деления m на n.
ROUND -- число, округленное до определенного количества знаков после запятой.
SIGN -- значение, определяющее знак числа.
SIN -- синус числа.
SINH -- гиперболический синус числа.
SQRT -- извлекает квадратный корень из числа.
SUM -- суммарное значение выражения.
TAN -- тангенс числа.
TANH -- гиперболический тангенс числа.
TRUNC -- число, усеченное до определенного количества знаков после запятой.
```

### Функции SQL для символьных типов данных (LOWER, UPPER, INITCAP, LENGTH, CHR, CONCAT, TRIM, TRANSLATE, REPLACE, INSTR, SUBSTR, TO_CHAR)
> Источник https://youtu.be/myYvKpjquGw

```sql
SELECT LOWER('Обучение SQL') FROM DUAL;
SELECT UPPER('Обучение SQL') FROM DUAL;
SELECT INITCAP('обучение SQL') FROM DUAL;
 
SELECT LENGTH('Обучение SQL') FROM DUAL;
 
SELECT CHR(37) FROM DUAL;
SELECT CHR(34) FROM DUAL;
SELECT CHR(12) FROM DUAL;
 
SELECT CONCAT('Значение 1', ' Значение 2') FROM dual;
SELECT CONCAT(CONCAT('Значение 1 ', 'Значение 2'), ' Значение 3 ') FROM dual;
SELECT 'Значение 1' || ' Значение 2' || ' Значение 3' FROM dual;
 
SELECT TRIM('m' FROM 'mSQL') FROM DUAL;
SELECT TRIM('П' FROM 'ПриветП') FROM DUAL;
SELECT TRIM('     Обучение SQL     ') FROM DUAL;
 
SELECT TRANSLATE('123-SQL-123', '123', '456') FROM DUAL;
 
SELECT REPLACE('Базовый курс/мастер-класс по SQL', 'мастер-класс', 'вебинар') FROM DUAL;
 
SELECT INSTR('Обучение SQL с нуля до профи', 'SQL') FROM DUAL;
 
SELECT SUBSTR('Обучение SQL с нуля', 10, 3) FROM DUAL;
 
SELECT TO_CHAR(1234.567, '9999.9') FROM DUAL;
SELECT TO_CHAR(1234.567, '9,999.99') FROM DUAL;
SELECT TO_CHAR(1234.567, '000099') FROM DUAL;
 
SELECT SYSDATE FROM DUAL;
SELECT TO_CHAR(SYSDATE, 'dd.mm.yyyy') FROM DUAL;
SELECT TO_CHAR(SYSDATE, 'yyyy.mm.dd') FROM DUAL;
SELECT TO_CHAR(SYSDATE, 'FMMonth DD, YYYY') FROM DUAL;
SELECT TO_CHAR(SYSDATE, 'YYYY') FROM DUAL;
SELECT TO_CHAR(SYSDATE, 'Q') FROM DUAL;
SELECT TO_CHAR(SYSDATE, 'DAY') FROM DUAL;
```

### Символьные / строчные функции Oracle PL/SQL
> Источник: https://oracleplsql.ru/string-character.html

```sql
ASCII  -- числовое представление крайнего левого символа строки.
ASCIISTR -- преобразует строку любого набора символов к ASCII строке, используя набор символов базы данных.
CHR -- является противоположностью функции ASCII. CHR  -- символ, который основан на числовом коде.
COMPOSE  -- строку Unicode.
CONCAT -- позволяет соединить вместе две строки.
|| -- оператор конкатенации || позволяет объединить две или более строк вместе.
DUMP  -- значение varchar2, который включает код типа данных, длину в байтах, и внутреннее представление выражения.
INITCAP -- устанавливает первый символ каждого слова в верхний регистр, а остальные в нижний регистр.
INSTR  -- n-е вхождение подстроки в строке.
INSTR2  -- вхождение подстроки в строку, используя UCS2 кодовые точки.
INSTR4  -- вхождение подстроки в строку, используя UCS4 кодовые точки.
INSTRB  -- вхождение подстроки в строку, байты вместо символов.
INSTRC  -- вхождение подстроки в строку, используя Unicode полные символов.
LENGTH  -- длину указанной строки.
LENGTH2  -- длину указанной строки, используя UCS2 кодовые точки.
LENGTH4 -- длину указанной строки, используя UCS4 кодовые точки.
LENGTHB  -- длину указанной строки, используя байты вместо символов.
LENGTHC  -- длину указанной строки, используя полные символы Unicode.
LOWER -- преобразует все символы в заданной строке в нижний регистр. Если есть символы в строке, которые не являются буквами, они не влияют на эту функцию.
LPAD -- добавляет с левой части строки определенный набор символов (при не нулевом string1).
LTRIM -- удаляет все указанные символы с левой стороны строки.
NCHR  -- символ на основе number_code в национальной кодировке.
REGEXP_INSTR -- является расширением функции INSTR. Она  -- местоположение шаблона регулярного выражения в строке. Эта функция, представленная в Oracle 10g, позволит вам найти подстроку в строке, используя сопоставление шаблонов регулярных выражений.
REGEXP_LIKE -- позволяет выполнять регулярные выражения в предложении WHERE в запросах SELECT, INSERT, UPDATE или DELETE.
REGEXP_REPLACE -- является расширением функции REPLACE. Эта функция, введенная в Oracle 10g, позволит вам заменить последовательность символов в строке другим набором символов, используя сопоставление шаблонов регулярных выражений.
REGEXP_SUBSTR -- является расширением функции SUBSTR. Эта функция, представленная в Oracle 10g, позволит вам извлечь подстроку из строки, используя сопоставление шаблонов регулярных выражений.
REPLACE -- заменяет последовательность символов в строке другим набором символов.
RPAD -- дополняет с правой части строки определенный набор символов (при не нулевом string1).
RTRIM -- удаляет все указанные символы из правой части строки.
SOUNDEX  -- фонетическое представление (так, как это звучит) строки.
SUBSTR -- позволяет извлекать подстроку из строки.
TO_CHAR -- преобразует число или дату в строку.
TRANSLATE -- заменяет последовательность символов в строке другим набором символов. Тем не менее, она заменяет один символ за один раз. Например, заменится первый символ в string_to_replace с первого символа в replacement_string. Тогда будет заменен второй символ в string_to_replace с вторым символом в replacement_string, и так далее.
TRIM -- удаляет все указанные символы с начала или окончания строки.
UPPER -- преобразует все символы строки в верхний регистр. Если есть символы в строке, которые не являются буквами, они не влияют на эту функцию.
VSIZE  -- длину в байтах для внутреннего представления выражения.
```
### Функции SQL для даты и времени (SYSDATE, TO_DATE, LAST_DAY, ADD_MONTHS, EXTRACT, TRUNC)
> Источник: https://youtu.be/_6XWUJ2zf8Y
 
```sql
SELECT SYSDATE FROM dual;
SELECT TO_CHAR(SYSDATE, 'YYYY/MM/DD HH24:MI:SS') FROM dual;
 
SELECT TO_DATE('29.12.2020', 'dd.mm.yyyy') FROM dual;
SELECT TO_DATE('29/12/2020', 'dd/mm/yyyy') FROM dual;
SELECT TO_DATE('2020/12/29', ' yyyy/mm/dd') FROM dual;
SELECT TO_DATE('29.12.2020 15:45:30', 'DD.MM.YYYY HH24:MI:SS') FROM dual;
 
SELECT LAST_DAY(TO_DATE('15.12.2020', 'dd.mm.yyyy')) FROM dual;
 
SELECT ADD_MONTHS(TO_DATE('29.12.2020', 'dd.mm.yyyy'), 1) FROM dual;
SELECT ADD_MONTHS(TO_DATE('29.12.2020', 'dd.mm.yyyy'), -1) FROM dual;
 
SELECT EXTRACT(YEAR FROM to_date('29.12.2020', 'dd.mm.yyyy')) FROM dual;
SELECT EXTRACT(MONTH FROM to_date('29.12.2020', 'dd.mm.yyyy')) FROM dual;
SELECT EXTRACT(DAY FROM to_date('29.12.2020', 'dd.mm.yyyy')) FROM dual;
 
SELECT SYSDATE FROM dual;
SELECT TRUNC(SYSDATE, 'YEAR') FROM dual;
SELECT TRUNC(SYSDATE, 'Q') FROM dual;
SELECT TRUNC(SYSDATE, 'MONTH') FROM dual;
SELECT TRUNC(SYSDATE, 'IW') FROM dual;
```

### Дата / время функции Oracle PL/SQL
> Источник: https://oracleplsql.ru/date-time.html
```sql
ADD_MONTHS -- возвращает дату плюс n месяцев.
CURRENT_DATE -- возвращает текущую дату в часовом поясе текущей сессии SQL как установлено с помощью команды ALTER SESSION.
CURRENT_TIMESTAMP -- возвращает текущую дату и время в часовом поясе текущей сессии SQL как установлено с помощью команды ALTER SESSION. возвращает дату/время со значением часового пояса.
DBTIMEZONE -- возвращает часовой пояс базы данных как смещения часового пояса (в следующем формате: '[+|-]TZH:TZM') или название региона часового пояса.
EXTRACT -- извлекает значение из даты или значения интервала.
LAST_DAY -- возвращает последний день месяца на основе значения даты.
LOCALTIMESTAMP -- возвращает текущую дату и время в часовом поясе из текущей сессии SQL, как установлено командой ALTER SESSION. Это возвратит значение TIMESTAMP.
MONTHS_BETWEEN -- возвращает количество месяцев между date1 и date2.
NEW_TIME -- возвращает дату и время часового пояса zone2 для даты и времени часового пояса zone1, заданных date.
NEXT_DAY -- возвращает первый день недели, который больше date.
ROUND -- возвращает дату округленную до определенной единицы измерения.
SESSIONTIMEZONE -- возвращает часовой пояс текущей сессии в качестве смещения часового пояса (в следующем формате: '[+|-]TZH:TZM') или наименование региона часового пояса.
SYSDATE -- возвращает текущую системную дату и время на вашей локальной базе данных.
SYSTIMESTAMP -- возвращает текущую системную дату и время (в том числе доли секунды и часового пояса) на ваше локальной базе данных.
TO_DATE преобразует строку в дату.
TRUNC -- возвращает дату, усеченную к определенной единице измерения.
TZ_OFFSET -- возвращает смещение часового пояса из значения.
```
