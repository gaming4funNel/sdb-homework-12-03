# Домашнее задание к занятию «SQL. Часть 1» - Иванов Игорь

### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';

![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql1.png)

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

SELECT *
FROM payment
WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-18'
  AND amount > 10.00;

![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql2.png)

### Задание 3

Получите последние пять аренд фильмов.

SELECT * 
FROM rental 
ORDER BY rental_date DESC LIMIT 5;

![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql3.png)

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

SELECT *
FROM customer
WHERE first_name IN ('Kelly', 'Willie') AND active = 1;

![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql4.png)

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

SELECT 
    LOWER(first_name) AS first_name_modified,
    LOWER(last_name) AS last_name_modified,
    REPLACE(first_name, 'll', 'pp') AS first_name_replaced,
    REPLACE(last_name, 'll', 'pp') AS last_name_replaced
FROM 
    customer
WHERE 
    first_name IN ('Kelly', 'Willie') 
    AND active = 1;

![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql5.png)

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

SELECT 
    SUBSTRING_INDEX(email, '@', 1) AS email_prefix,
    SUBSTR(email, INSTR(email, '@') + 1) AS email_suffix
FROM 
    customer;

![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql6.png)

### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

SELECT 
    CONCAT(UPPER(SUBSTRING(email, 1, 1)), LOWER(SUBSTRING(email, 2, INSTR(email, '@') - 2))) AS email_prefix,
    CONCAT(UPPER(SUBSTRING(email, INSTR(email, '@') + 1, 1)), LOWER(SUBSTRING(email, INSTR(email, '@') + 2))) AS email_suffix
FROM 
    customer;
    
![sql](https://github.com/gaming4funNel/sdb-homework-12-03/blob/main/img/sql7.png)
