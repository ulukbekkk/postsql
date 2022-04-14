# Slash commands
* `\с` - показывает в какой бд мы находимся и через какого юзера

* `\с name_of_db` - переключается к этой бд

* `\l` - показывает все бд

* `\dt` - показывает все таблицы в бд

* `\du` - показывает всех юзеров

* `\q` - выход


# Создание бд и таблиц
```sql
CREATE DATABASE name_of_db; 
-- создает базу данных
```

```sql
CREATE TABLE name_of_table (
    name_of_column1 data_type constraint,
    name_of_column2 data_type constraint,
    ...
); 
-- создает таблицу с полями
```
# Заполнение таблиц
```sql
INSERT INTO name_of_table (name_of_column1, name_of_column2) 
VALUES (val1, val2);
-- добавляет запись в таблицу
```
# вывод данных из таблицы
```sql
SELECT * FROM name_of_table; 
-- достает все поля и записи из таблицы

SELECT name_of_column1, name_of_column2 FROM name_of_table; 
-- достает только указанные столбцы из таблицы
```

# связи
## pk fk
> primary key (pk) - первичный ключ
> это ограничение, которое мы указываем на те поля,которые должны быть уникальными для того, чтобы потом их использовать в связях (например id)

> foreign key (fk) - внешний ключ
> это ограничение, которое мы указываем на те поля, которые будут ссылаться на pk в другой таблице, для создания связи

```sql
CREATE TABLE author (
    id serial primary key,
    first_name varchar(50),
    last_name varchar(50)
)

CREATE TABLE book (
    id serial,
    title varchar(100),
    published year,
    author_id int foreign key referenses author (id)
)
```

## Виды связи (Теория)
> One to one  - (один к одному)
например:
* Один автор - одна страна
* Один флаг - одна срана
* Один человек - одно сердце

> one to many (один ко многим)
Например: 

* Один человек - много клетокб, но у одной клетки только одни человек
* один родитнль - много детей, но у одного поста только одни родители
* Один аккаунт - много постов, но у одного поста только один автор(аккаунт) 
* Один makers - много maker`ов, но у одной maker`a только один makers

>many to many - (многие ко многим)
Например:

* У человека много друзей и у одного друга много других друзей
* У доктора много пациентов и у пациента много  докторов
* У пользователя много соц сетей и у одной соц сети мног пользователей

## Виды связей (практика)

### one to one
```sql
create table flag (
   id serial primary key,
   photo text
)

create table country (
   id serial primary key,
   title varchar(50),
   gimn text,
   glag_id int unique,
   constraint fk_country_flag 
   foreign key (flag_id) references flag(id)
)
```

### one to mane

```sql
CREATE TABLE acount (
   id serial primary key,
   nickname varchar(25) unique,
   u_password varchar(255)
)
CREATE TABLE post(
   id serial primary key,
   title varchar(100),
   body text,
   photo_text,
   accound_id int,
   constraint fk_acc_post 
   foreign key (accound_id) references account(id) 
);

```

### Many to many
```sql
create table doctor (
   id serial primary key,
   first_name varchar(25),
   last_name varchar(50)

);

Create Table patient (
   id serial primary key,
   first_name varchar(15),
   last_name varchar(50)
);


create table doctor_patient (
   doctor_id int,
   patient_id int,

   constraint fk_doctor
   foreign key (doctor_id) references doctor(id),

   constraint fk_patient
   foreign key (patient_id) references patient(id)
);

```




## joins (теория)
> JOIN - инструкция, которая позволяет в запросах SELECT брать данные из нескольких таблиц

> INNER JOIN (JOIN) - когда достаются только те записи, у которых есть полная связь

> FULL JOIN - когда достаются абсолютно все записи со всех таблиц

> LEFT JOIN - когда достаются все записи с 'левой' таблицы и так же те записи с полной связью

> RIGHT JOIN - когда достаются все записи с 'правой' таблицы и так же те записи с полной связью


## Join (Практиа)

### one to one
```sql
select country.title, country.gimn, flag.photo
from country
join flag
on country.flag_id = glag.id;
```

### one to many
```sql
select account.nickname, post.title, post.photo
from account 
join post
on account.id = post.account_id;


``` 

### many to many
```sql
select doctor.first_name as Doctor, 
      patient.first_name as Patient
from doctor
join doctor_patient as dp on doctor.id = dp.doctor_id
join patient on patient.id = dp.patient_id;

```


```sql
SELECT author.first_name, book.title 
FROM author
JOIN book ON author.id = book.author_id
```

# Import export данных
write from file to db
```bash
psql db_name < file.sql
```
write from db to file
```bash
pg_dump db_name > file.sql


