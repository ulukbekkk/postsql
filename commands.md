`\c` - показывает бд мы находимся и через какого юзера

`\c` name_of_db - переключается в этой бд

`\dt` - поакзывает все таблицы в бд

`\q` - выход


```sql
CREATE DATABASE name_of_db; -создает базу данных
```
```sql
CREATE TABLE name_of_table (
    name_of_column1 data_type constrant,
    name_of_column2 data_type constrant
```    
) - создаем таблицу с полями

INSERT INTO name_of_table (name_of_column1, name_of_column2)
VALUES (val1, val2); - добавляет запись в таблицу 

SELECT * FROM name_of_table; - достает все поля и записи из таблицы
SELECT name_of_column1, name_of_column2 FROM name_of_table; достает только указанные столбцы из таблицы

> primary key - (pk) -первичный ключ 
> его мы указываем на те поля, которые должны быть уникальными для  того, чтобы потом использовать в связах (например id) 

> foreign key (fk) - внешний ключ 
> это ограничение, которое мы указываем на те поля, которые будут ссылаться на pk в другой таблице, для создание связи

 ```sql
 CREATE TABLE author(
    id serial primary key,
    first_name varchar(50),
    last_name varchar(50)

 )


 CREATE TABLE book(
    id serial,
    title varchar(100),
    published year
    author_id int foreing key referenses author (id)
 )

 ```

 > JOIN - инструкция, которая позволяет в запрос SELECT брать данные из нескльких таблиц
 > INNER JOIN (JOIN) - когда достаются только те записи, у которых есть полная связь
 > LEFT JOIN - когда достают все записи с "левой"  таблицы и так же те записи с полноц связью
 > RIGHT JOIN - 

 ```sql
SELECT author.first_name, book.title
from  author
JOIN book ON author.id = book.author_id
 ```

 


