anna@anna-pc:~$ mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.7.20-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| anna               |
| mysql              |
| performance_schema |
| sys                |
| wordpress          |
+--------------------+
6 rows in set (0,05 sec)

mysql> USE anna;
Database changed
mysql> SHOW TABLES;
Empty set (0,00 sec)

mysql> CREATE TABLE movies (
    -> id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
    -> name VARCHAR (20),
    -> date_launch DATE,
    -> box_office DECIMAL (11.2),
    -> imdb_rate DECIMAL (2,1),
    -> genre_id VARCHAR (10))
    -> ;
Query OK, 0 rows affected (0,16 sec)

mysql> ALTER TABLE movies MODIFY COLUMN box_office DECIMAL (11,2);
Query OK, 0 rows affected (0,57 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE movies;
+-------------+---------------+------+-----+---------+----------------+
| Field       | Type          | Null | Key | Default | Extra          |
+-------------+---------------+------+-----+---------+----------------+
| id          | int(11)       | NO   | PRI | NULL    | auto_increment |
| name        | varchar(20)   | YES  |     | NULL    |                |
| date_launch | date          | YES  |     | NULL    |                |
| box_office  | decimal(11,2) | YES  |     | NULL    |                |
| imdb_rate   | decimal(2,1)  | YES  |     | NULL    |                |
| genre_id    | varchar(10)   | YES  |     | NULL    |                |
+-------------+---------------+------+-----+---------+----------------+
6 rows in set (0,00 sec)

mysql> ALTER TABLE movies MODIFY COLUMN genre_id INT;
Query OK, 0 rows affected (4,97 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> DESCRIBE movies;
+-------------+---------------+------+-----+---------+----------------+
| Field       | Type          | Null | Key | Default | Extra          |
+-------------+---------------+------+-----+---------+----------------+
| id          | int(11)       | NO   | PRI | NULL    | auto_increment |
| name        | varchar(20)   | YES  |     | NULL    |                |
| date_launch | date          | YES  |     | NULL    |                |
| box_office  | decimal(11,2) | YES  |     | NULL    |                |
| imdb_rate   | decimal(2,1)  | YES  |     | NULL    |                |
| genre_id    | int(11)       | YES  |     | NULL    |                |
+-------------+---------------+------+-----+---------+----------------+
6 rows in set (0,00 sec)

mysql> CREATE TABLE genre 
    -> (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    -> name VARCHAR (10));
Query OK, 0 rows affected (0,16 sec)

mysql> DESCRIBE genre;
+-------+-------------+------+-----+---------+----------------+
| Field | Type        | Null | Key | Default | Extra          |
+-------+-------------+------+-----+---------+----------------+
| id    | int(11)     | NO   | PRI | NULL    | auto_increment |
| name  | varchar(10) | YES  |     | NULL    |                |
+-------+-------------+------+-----+---------+----------------+
2 rows in set (0,01 sec)

mysql> INSERT INTO genre (name) VALUES ('драма', ' комедия', 'триллер', 'фантастика');
ERROR 1136 (21S01): Column count doesn't match value count at row 1
mysql> INSERT INTO genre (name) VALUES ('драма'), (' комедия') , ('триллер') , ('фантастика');
Query OK, 4 rows affected (0,09 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM genre;
+----+----------------------+
| id | name                 |
+----+----------------------+
|  1 | драма                |
|  2 |  комедия             |
|  3 | триллер              |
|  4 | фантастика           |
+----+----------------------+
4 rows in set (0,00 sec)

mysql> DESCRIBE movies;
+-------------+---------------+------+-----+---------+----------------+
| Field       | Type          | Null | Key | Default | Extra          |
+-------------+---------------+------+-----+---------+----------------+
| id          | int(11)       | NO   | PRI | NULL    | auto_increment |
| name        | varchar(20)   | YES  |     | NULL    |                |
| date_launch | date          | YES  |     | NULL    |                |
| box_office  | decimal(11,2) | YES  |     | NULL    |                |
| imdb_rate   | decimal(2,1)  | YES  |     | NULL    |                |
| genre_id    | int(11)       | YES  |     | NULL    |                |
+-------------+---------------+------+-----+---------+----------------+
6 rows in set (0,00 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Побег из Шоушенка", "1994-09-10", 59841469, 9.3, 1);
Query OK, 1 row affected (0,11 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Зеленая миля", "1999-12-06", 286801374, 8.5, 4);
Query OK, 1 row affected (0,17 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("1+1", "2011-09-23", 426588510, 8.6, 2);
Query OK, 1 row affected (0,05 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Интерстеллар", "2014-10-26", 675120017, 8.6, 4);
Query OK, 1 row affected (0,06 sec)

mysql> SELECT * FROM  movies;
+----+----------------------------------+-------------+--------------+-----------+----------+
| id | name                             | date_launch | box_office   | imdb_rate | genre_id |
+----+----------------------------------+-------------+--------------+-----------+----------+
|  1 | Побег из Шоушенка                | 1994-09-10  |  59841469.00 |       9.3 |        1 |
|  2 | Зеленая миля                     | 1999-12-06  | 286801374.00 |       8.5 |        4 |
|  3 | 1+1                              | 2011-09-23  | 426588510.00 |       8.6 |        2 |
|  4 | Интерстеллар                     | 2014-10-26  | 675120017.00 |       8.6 |        4 |
+----+----------------------------------+-------------+--------------+-----------+----------+
4 rows in set (0,00 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Назад в будущее", "1985-07-03", 381109761, 8.5, 4);
Query OK, 1 row affected (0,06 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Большой куш", "2000-08-23", 83557872, 8.3, 2);
Query OK, 1 row affected (0,07 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Планета Ка-Пэкс", "2001-10-21", 65001482, 7.4, 4);
Query OK, 1 row affected (0,06 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Исчезнувшая", "2014-09-26", 361303363, 8.1, 3);
Query OK, 1 row affected (0,08 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Убить пересмешника", "1962-12-25", 13129846, 8.3, 1);
Query OK, 1 row affected (0,06 sec)

mysql> INSERT INTO movies (name, date_launch, box_office, imdb_rate, genre_id) VALUES ("Король говорит!", "2010-09-06", 414211549, 8.0, 1);
Query OK, 1 row affected (0,08 sec)

mysql> SELECT * FROM movies;
+----+-------------------------------------+-------------+--------------+-----------+----------+
| id | name                                | date_launch | box_office   | imdb_rate | genre_id |
+----+-------------------------------------+-------------+--------------+-----------+----------+
|  1 | Побег из Шоушенка                   | 1994-09-10  |  59841469.00 |       9.3 |        1 |
|  2 | Зеленая миля                        | 1999-12-06  | 286801374.00 |       8.5 |        4 |
|  3 | 1+1                                 | 2011-09-23  | 426588510.00 |       8.6 |        2 |
|  4 | Интерстеллар                        | 2014-10-26  | 675120017.00 |       8.6 |        4 |
|  5 | Назад в будущее                     | 1985-07-03  | 381109761.00 |       8.5 |        4 |
|  6 | Большой куш                         | 2000-08-23  |  83557872.00 |       8.3 |        2 |
|  7 | Планета Ка-Пэкс                     | 2001-10-21  |  65001482.00 |       7.4 |        4 |
|  8 | Исчезнувшая                         | 2014-09-26  | 361303363.00 |       8.1 |        3 |
|  9 | Убить пересмешника                  | 1962-12-25  |  13129846.00 |       8.3 |        1 |
| 10 | Король говорит!                     | 2010-09-06  | 414211549.00 |       8.0 |        1 |
+----+-------------------------------------+-------------+--------------+-----------+----------+
10 rows in set (0,00 sec)


mysql> SELECT * FROM movies WHERE imdb_rate > 7.5;
+----+-------------------------------------+-------------+--------------+-----------+----------+
| id | name                                | date_launch | box_office   | imdb_rate | genre_id |
+----+-------------------------------------+-------------+--------------+-----------+----------+
|  1 | Побег из Шоушенка                   | 1994-09-10  |  59841469.00 |       9.3 |        1 |
|  2 | Зеленая миля                        | 1999-12-06  | 286801374.00 |       8.5 |        4 |
|  3 | 1+1                                 | 2011-09-23  | 426588510.00 |       8.6 |        2 |
|  4 | Интерстеллар                        | 2014-10-26  | 675120017.00 |       8.6 |        4 |
|  5 | Назад в будущее                     | 1985-07-03  | 381109761.00 |       8.5 |        4 |
|  6 | Большой куш                         | 2000-08-23  |  83557872.00 |       8.3 |        2 |
|  8 | Исчезнувшая                         | 2014-09-26  | 361303363.00 |       8.1 |        3 |
|  9 | Убить пересмешника                  | 1962-12-25  |  13129846.00 |       8.3 |        1 |
| 10 | Король говорит!                     | 2010-09-06  | 414211549.00 |       8.0 |        1 |
+----+-------------------------------------+-------------+--------------+-----------+----------+
9 rows in set (0,01 sec)

mysql> SELECT * FROM movies WHERE imdb_rate > 7.5 AND date_launch > '2010-12-31';
+----+--------------------------+-------------+--------------+-----------+----------+
| id | name                     | date_launch | box_office   | imdb_rate | genre_id |
+----+--------------------------+-------------+--------------+-----------+----------+
|  3 | 1+1                      | 2011-09-23  | 426588510.00 |       8.6 |        2 |
|  4 | Интерстеллар             | 2014-10-26  | 675120017.00 |       8.6 |        4 |
|  8 | Исчезнувшая              | 2014-09-26  | 361303363.00 |       8.1 |        3 |
+----+--------------------------+-------------+--------------+-----------+----------+
3 rows in set (0,01 sec)

mysql> SELECT * FROM movies ORDER BY imdb_rate DESC;
+----+-------------------------------------+-------------+--------------+-----------+----------+
| id | name                                | date_launch | box_office   | imdb_rate | genre_id |
+----+-------------------------------------+-------------+--------------+-----------+----------+
|  1 | Побег из Шоушенка                   | 1994-09-10  |  59841469.00 |       9.3 |        1 |
|  3 | 1+1                                 | 2011-09-23  | 426588510.00 |       8.6 |        2 |
|  4 | Интерстеллар                        | 2014-10-26  | 675120017.00 |       8.6 |        4 |
|  2 | Зеленая миля                        | 1999-12-06  | 286801374.00 |       8.5 |        4 |
|  5 | Назад в будущее                     | 1985-07-03  | 381109761.00 |       8.5 |        4 |
|  6 | Большой куш                         | 2000-08-23  |  83557872.00 |       8.3 |        2 |
|  9 | Убить пересмешника                  | 1962-12-25  |  13129846.00 |       8.3 |        1 |
|  8 | Исчезнувшая                         | 2014-09-26  | 361303363.00 |       8.1 |        3 |
| 10 | Король говорит!                     | 2010-09-06  | 414211549.00 |       8.0 |        1 |
|  7 | Планета Ка-Пэкс                     | 2001-10-21  |  65001482.00 |       7.4 |        4 |
+----+-------------------------------------+-------------+--------------+-----------+----------+
10 rows in set (0,00 sec)

mysql> UPDATE movies SET imdb_rate=9.0 WHERE id=1;
Query OK, 1 row affected (0,10 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * FROM movies;
+----+-------------------------------------+-------------+--------------+-----------+----------+
| id | name                                | date_launch | box_office   | imdb_rate | genre_id |
+----+-------------------------------------+-------------+--------------+-----------+----------+
|  1 | Побег из Шоушенка                   | 1994-09-10  |  59841469.00 |       9.0 |        1 |
|  2 | Зеленая миля                        | 1999-12-06  | 286801374.00 |       8.5 |        4 |
|  3 | 1+1                                 | 2011-09-23  | 426588510.00 |       8.6 |        2 |
|  4 | Интерстеллар                        | 2014-10-26  | 675120017.00 |       8.6 |        4 |
|  5 | Назад в будущее                     | 1985-07-03  | 381109761.00 |       8.5 |        4 |
|  6 | Большой куш                         | 2000-08-23  |  83557872.00 |       8.3 |        2 |
|  7 | Планета Ка-Пэкс                     | 2001-10-21  |  65001482.00 |       7.4 |        4 |
|  8 | Исчезнувшая                         | 2014-09-26  | 361303363.00 |       8.1 |        3 |
|  9 | Убить пересмешника                  | 1962-12-25  |  13129846.00 |       8.3 |        1 |
| 10 | Король говорит!                     | 2010-09-06  | 414211549.00 |       8.0 |        1 |
+----+-------------------------------------+-------------+--------------+-----------+----------+
10 rows in set (0,00 sec)



mysql> SELECT m.name as 'Фильм' , g.name as 'Жанр' FROM movies m JOIN genre g ON m.genre_id=g.id;
+-------------------------------------+----------------------+
| Фильм                               | Жанр                 |
+-------------------------------------+----------------------+
| Побег из Шоушенка                   | драма                |
| Зеленая миля                        | фантастика           |
| 1+1                                 |  комедия             |
| Интерстеллар                        | фантастика           |
| Назад в будущее                     | фантастика           |
| Большой куш                         |  комедия             |
| Планета Ка-Пэкс                     | фантастика           |
| Исчезнувшая                         | триллер              |
| Убить пересмешника                  | драма                |
| Король говорит!                     | драма                |
+-------------------------------------+----------------------+
10 rows in set (0,00 sec)

mysql> 
