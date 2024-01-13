UC 1:
-----
mysql> create database address_book_service_db;
Query OK, 1 row affected (0.06 sec)

mysql> show databases;
+-------------------------+
| Database                |
+-------------------------+
| address_book_service_db |
| information_schema      |
| javacourse              |
| mysql                   |
| payroll_service         |
| performance_schema      |
| sampledb                |
| sys                     |
+-------------------------+
8 rows in set (0.03 sec)




UC 2:
-----
mysql> use address_book_service_db;
Database changed

mysql> create table address_book(first_name varchar(20), last_name varchar(20), address varchar(20), city varchar(20), state varchar(20), zip int, phone_number bigint, email varchar(30));
Query OK, 0 rows affected (0.28 sec)

mysql> desc address_book;
+--------------+-------------+------+-----+---------+-------+
| Field        | Type        | Null | Key | Default | Extra |
+--------------+-------------+------+-----+---------+-------+
| first_name   | varchar(20) | YES  |     | NULL    |       |
| last_name    | varchar(20) | YES  |     | NULL    |       |
| address      | varchar(20) | YES  |     | NULL    |       |
| city         | varchar(20) | YES  |     | NULL    |       |
| state        | varchar(20) | YES  |     | NULL    |       |
| zip          | int         | YES  |     | NULL    |       |
| phone_number | bigint      | YES  |     | NULL    |       |
| email        | varchar(30) | YES  |     | NULL    |       |
+--------------+-------------+------+-----+---------+-------+
8 rows in set (0.03 sec)





UC 3:
-----
mysql> insert into address_book values('Lokeshwar', 'Pinjala', 'Gummidipoondi', 'Chennai', 'TamilNadu', 601202, 9677595842, 'pglokeshwarmca@gmail.com');
Query OK, 1 row affected (0.08 sec)

mysql> insert into address_book values('Gopi', 'Pinjala', 'Gummidipoondi', 'Chennai', 'TamilNadu', 601202, 9677595842, 'gopiganesh@gmail.com');
Query OK, 1 row affected (0.02 sec)

mysql> insert into address_book values('Rajesh', 'Kumar', 'Gummidipoondi', 'Chennai', 'TamilNadu', 601202, 9677595842, 'gopiganesh@gmail.com');
Query OK, 1 row affected (0.01 sec)

mysql> insert into address_book values('Madhesh', 'Kumar', 'Gummidipoondi', 'Chennai', 'TamilNadu', 601202, 9677595842, 'gopiganesh@gmail.com');
Query OK, 1 row affected (0.01 sec)






UC 4:
-----
mysql> update address_book set phone_number = 6384365800 where first_name = 'Gopi';
Query OK, 1 row affected (0.13 sec)
Rows matched: 1  Changed: 1  Warnings: 0





UC 5:
-----
mysql> delete from address_book where first_name = 'Madhesh';
Query OK, 1 row affected (0.01 sec)






UC 6:
-----
mysql> select * from address_book where city = 'Chennai' or state = 'Chennai';
+------------+-----------+---------------+---------+-----------+--------+--------------+--------------------------+
| first_name | last_name | address       | city    | state     | zip    | phone_number | email                    |
+------------+-----------+---------------+---------+-----------+--------+--------------+--------------------------+
| Lokeshwar  | Pinjala   | Gummidipoondi | Chennai | TamilNadu | 601202 |   9677595842 | pglokeshwarmca@gmail.com |
| Gopi       | Pinjala   | Gummidipoondi | Chennai | TamilNadu | 601202 |   6384365800 | gopiganesh@gmail.com     |
| Rajesh     | Kumar     | Gummidipoondi | Chennai | TamilNadu | 601202 |   9677595842 | gopiganesh@gmail.com     |
+------------+-----------+---------------+---------+-----------+--------+--------------+--------------------------+
3 rows in set (0.00 sec)





UC 7:
------
mysql> select city, state, count(*) from address_book group by city, state;
+----------+-----------+----------+
| city     | state     | count(*) |
+----------+-----------+----------+
| Chennai  | TamilNadu |        3 |
| Banglore | karnataka |        1 |
+----------+-----------+----------+
2 rows in set (0.00 sec)




UC 8:
-----
mysql> select * from address_book where city = 'Chennai' order by first_name asc;
+------------+-----------+---------------+---------+-----------+--------+--------------+--------------------------+
| first_name | last_name | address       | city    | state     | zip    | phone_number | email                    |
+------------+-----------+---------------+---------+-----------+--------+--------------+--------------------------+
| Gopi       | Pinjala   | Gummidipoondi | Chennai | TamilNadu | 601202 |   6384365800 | gopiganesh@gmail.com     |
| Lokeshwar  | Pinjala   | Gummidipoondi | Chennai | TamilNadu | 601202 |   9677595842 | pglokeshwarmca@gmail.com |
| Rajesh     | Kumar     | Gummidipoondi | Chennai | TamilNadu | 601202 |   9677595842 | gopiganesh@gmail.com     |
+------------+-----------+---------------+---------+-----------+--------+--------------+--------------------------+
3 rows in set (0.02 sec)





UC 9:
-----
mysql> alter table address_book add name varchar(20);
Query OK, 0 rows affected (0.11 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table address_book add type varchar(20);
Query OK, 0 rows affected (0.11 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table address_book drop column type;
Query OK, 0 rows affected (0.15 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table address_book drop column name;
Query OK, 0 rows affected (0.13 sec)
Records: 0  Duplicates: 0  Warnings: 0


mysql> alter table address_book add name varchar(20), add type varchar(20);
Query OK, 0 rows affected (0.11 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from address_book;
+------------+-----------+---------------+----------+-----------+--------+--------------+--------------------------+------+------+
| first_name | last_name | address       | city     | state     | zip    | phone_number | email                    | name | type |
+------------+-----------+---------------+----------+-----------+--------+--------------+--------------------------+------+------+
| Lokeshwar  | Pinjala   | Gummidipoondi | Chennai  | TamilNadu | 601202 |   9677595842 | pglokeshwarmca@gmail.com | NULL | NULL |
| Gopi       | Pinjala   | Gummidipoondi | Chennai  | TamilNadu | 601202 |   6384365800 | gopiganesh@gmail.com     | NULL | NULL |
| Rajesh     | Kumar     | Gummidipoondi | Chennai  | TamilNadu | 601202 |   9677595842 | gopiganesh@gmail.com     | NULL | NULL |
| Madhesh    | Kumar     | Gummidipoondi | Banglore | karnataka | 601202 |   9677595842 | gopiganesh@gmail.com     | NULL | NULL |
+------------+-----------+---------------+----------+-----------+--------+--------------+--------------------------+------+------+
4 rows in set (0.00 sec)


mysql> update address_book set type = 'Friend' where first_name = 'Rajesh';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update address_book set type = 'Friend' where first_name = 'madhesh';
Query OK, 1 row affected (0.01 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> update address_book set type = 'Family' where first_name = 'Gopi';
Query OK, 1 row affected (0.02 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> select * from addresss_book;
ERROR 1146 (42S02): Table 'address_book_service_db.addresss_book' doesn't exist
mysql> select * from address_book;
+------------+-----------+---------------+----------+-----------+--------+--------------+--------------------------+------+--------+
| first_name | last_name | address       | city     | state     | zip    | phone_number | email                    | name | type   |
+------------+-----------+---------------+----------+-----------+--------+--------------+--------------------------+------+--------+
| Lokeshwar  | Pinjala   | Gummidipoondi | Chennai  | TamilNadu | 601202 |   9677595842 | pglokeshwarmca@gmail.com | NULL | NULL   |
| Gopi       | Pinjala   | Gummidipoondi | Chennai  | TamilNadu | 601202 |   6384365800 | gopiganesh@gmail.com     | NULL | Family |
| Rajesh     | Kumar     | Gummidipoondi | Chennai  | TamilNadu | 601202 |   9677595842 | gopiganesh@gmail.com     | NULL | Friend |
| Madhesh    | Kumar     | Gummidipoondi | Banglore | karnataka | 601202 |   9677595842 | gopiganesh@gmail.com     | NULL | Friend |
+------------+-----------+---------------+----------+-----------+--------+--------------+--------------------------+------+--------+
4 rows in set (0.00 sec)







UC 10:
------
mysql> select type, count(*) from address_book group by type;
+--------+----------+
| type   | count(*) |
+--------+----------+
| NULL   |        1 |
| Family |        1 |
| Friend |        2 |
+--------+----------+
3 rows in set (0.00 sec)





UC 11:
------
mysql> insert into address_book values('Deepike', 'Gothilla', 'Whitfield', 'Banglore', 'Karnataka', 54321, 9876543210, 'deepikagothilla@gmail.com', 'noname', 'Friend');
Query OK, 1 row affected (0.02 sec)

mysql> insert into address_book values('Deepike', 'Gothilla', 'Whitfield', 'Banglore', 'Karnataka', 54321, 9876543210, 'deepikagothilla@gmail.com', 'noname', 'Family');
Query OK, 1 row affected (0.11 sec)

mysql> select * from address_book;
+------------+-----------+---------------+----------+-----------+--------+--------------+---------------------------+--------+--------+
| first_name | last_name | address       | city     | state     | zip    | phone_number | email                     | name   | type   |
+------------+-----------+---------------+----------+-----------+--------+--------------+---------------------------+--------+--------+
| Lokeshwar  | Pinjala   | Gummidipoondi | Chennai  | TamilNadu | 601202 |   9677595842 | pglokeshwarmca@gmail.com  | NULL   | NULL   |
| Gopi       | Pinjala   | Gummidipoondi | Chennai  | TamilNadu | 601202 |   6384365800 | gopiganesh@gmail.com      | NULL   | Family |
| Rajesh     | Kumar     | Gummidipoondi | Chennai  | TamilNadu | 601202 |   9677595842 | gopiganesh@gmail.com      | NULL   | Friend |
| Madhesh    | Kumar     | Gummidipoondi | Banglore | karnataka | 601202 |   9677595842 | gopiganesh@gmail.com      | NULL   | Friend |
| Deepike    | Gothilla  | Whitfield     | Banglore | Karnataka |  54321 |   9876543210 | deepikagothilla@gmail.com | noname | Friend |
| Deepike    | Gothilla  | Whitfield     | Banglore | Karnataka |  54321 |   9876543210 | deepikagothilla@gmail.com | noname | Family |
+------------+-----------+---------------+----------+-----------+--------+--------------+---------------------------+--------+--------+
6 rows in set (0.00 sec)

mysql>