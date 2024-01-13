UC 1:
-----
mysql> create database payroll_service;
Query OK, 1 row affected (0.02 sec)


mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| javacourse         |
| mysql              |
| payroll_service    |
| performance_schema |
| sampledb           |
| sys                |
+--------------------+
7 rows in set (0.01 sec)


mysql> use payroll_service;
Database changed






UC 2:
-----
mysql> create table employee_payroll(id int primary key AUTO_INCREMENT, name varchar(20), salary decimal(10,2), start_date date);
Query OK, 0 rows affected (0.16 sec)





UC 3:
-----
mysql> insert into employee_payroll(name, salary, start_date) values('Lokesh', 40000, '2024-01-13');
Query OK, 1 row affected 	(0.14 sec)

mysql> insert into employee_payroll(name, salary, start_date) values('Rajesh', 40000, '2024-01-13'), ('Madhesh', 60000, '2020-01-01');
Query OK, 2 rows affected (0.02 sec)
Records: 2  Duplicates: 0  Warnings: 0

mysql> select * from employee_payroll;
+----+---------+----------+------------+
| id | name    | salary   | start_date |
+----+---------+----------+------------+
|  1 | Lokesh  | 40000.00 | 2024-01-13 |
|  2 | Rajesh  | 40000.00 | 2024-01-13 |
|  3 | Madhesh | 60000.00 | 2020-01-01 |
+----+---------+----------+------------+
3 rows in set (0.00 sec)


mysql> update employee_payroll set salary = 50000 where id = 2;
Query OK, 1 row affected (0.14 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> delete from employee_payroll where id=1;
Query OK, 1 row affected (0.14 sec)






UC 4:
-----
mysql> select * from employee_payroll;
+----+---------+----------+------------+
| id | name    | salary   | start_date |
+----+---------+----------+------------+
|  2 | Rajesh  | 50000.00 | 2024-01-13 |
|  3 | Madhesh | 60000.00 | 2020-01-01 |
+----+---------+----------+------------+
2 rows in set (0.00 sec)






UC 5:
-----
mysql> select salary from employee_payroll where name = 'Rajesh';
+----------+
| salary   |
+----------+
| 50000.00 |
+----------+
1 row in set (0.00 sec)

mysql> select * from employee_payroll where start_date BETWEEN CAST('2023-01-01' AS DATE) AND DATE(NOW());
+----+--------+----------+------------+
| id | name   | salary   | start_date |
+----+--------+----------+------------+
|  2 | Rajesh | 50000.00 | 2024-01-13 |
+----+--------+----------+------------+
1 row in set (0.02 sec)






UC 6:
-----
mysql> alter table employee_payroll add column gender varchar(20);
Query OK, 0 rows affected (0.20 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> desc employee_payroll;
+------------+---------------+------+-----+---------+----------------+
| Field      | Type          | Null | Key | Default | Extra          |
+------------+---------------+------+-----+---------+----------------+
| id         | int           | NO   | PRI | NULL    | auto_increment |
| name       | varchar(20)   | YES  |     | NULL    |                |
| salary     | decimal(10,2) | YES  |     | NULL    |                |
| start_date | date          | YES  |     | NULL    |                |
| gender     | varchar(20)   | YES  |     | NULL    |                |
+------------+---------------+------+-----+---------+----------------+
5 rows in set (0.03 sec)

mysql> select * from employee_payroll;
+----+---------+----------+------------+--------+
| id | name    | salary   | start_date | gender |
+----+---------+----------+------------+--------+
|  2 | Rajesh  | 50000.00 | 2024-01-13 | NULL   |
|  3 | Madhesh | 60000.00 | 2020-01-01 | NULL   |
+----+---------+----------+------------+--------+
2 rows in set (0.00 sec)

mysql> alter table employee_payroll drop column gender;
Query OK, 0 rows affected (0.13 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> alter table employee_payroll add column gender varchar(20) after name;
Query OK, 0 rows affected (0.11 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> select * from employee_payroll;
+----+---------+--------+----------+------------+
| id | name    | gender | salary   | start_date |
+----+---------+--------+----------+------------+
|  2 | Rajesh  | NULL   | 50000.00 | 2024-01-13 |
|  3 | Madhesh | NULL   | 60000.00 | 2020-01-01 |
+----+---------+--------+----------+------------+
2 rows in set (0.00 sec)

mysql> update employee_payroll set gender = 'M' where name = 'Rajesh' or name = 'Madhesh';
Query OK, 2 rows affected (0.10 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> select * from employee_payroll;
+----+---------+--------+----------+------------+
| id | name    | gender | salary   | start_date |
+----+---------+--------+----------+------------+
|  2 | Rajesh  | M      | 50000.00 | 2024-01-13 |
|  3 | Madhesh | M      | 60000.00 | 2020-01-01 |
+----+---------+--------+----------+------------+
2 rows in set (0.00 sec)






UC 7:
-----

mysql> select * from employee_payroll;
+----+---------+--------+-----------+------------+
| id | name    | gender | salary    | start_date |
+----+---------+--------+-----------+------------+
|  2 | Rajesh  | M      |  50000.00 | 2024-01-13 |
|  3 | Madhesh | M      |  60000.00 | 2020-01-01 |
|  4 | Pooja   | F      | 100000.00 | 2022-09-11 |
|  5 | Deepika | F      | 200000.00 | 2021-09-05 |
+----+---------+--------+-----------+------------+
4 rows in set (0.00 sec)



mysql> select gender, sum(salary) from employee_payroll group by gender;
+--------+-------------+
| gender | sum(salary) |
+--------+-------------+
| M      |   110000.00 |
| F      |   300000.00 |
+--------+-------------+
2 rows in set (0.00 sec)

mysql> select gender, avg(salary) from employee_payroll group by gender;
+--------+---------------+
| gender | avg(salary)   |
+--------+---------------+
| M      |  55000.000000 |
| F      | 150000.000000 |
+--------+---------------+
2 rows in set (0.02 sec)

mysql> select gender, min(salary) from employee_payroll group by gender;
+--------+-------------+
| gender | min(salary) |
+--------+-------------+
| M      |    50000.00 |
| F      |   100000.00 |
+--------+-------------+
2 rows in set (0.01 sec)

mysql> select gender, max(salary) from employee_payroll group by gender;
+--------+-------------+
| gender | max(salary) |
+--------+-------------+
| M      |    60000.00 |
| F      |   200000.00 |
+--------+-------------+
2 rows in set (0.00 sec)


mysql> select gender, count(*) from employee_payroll group by gender;
+--------+----------+
| gender | count(*) |
+--------+----------+
| M      |        2 |
| F      |        2 |
+--------+----------+
2 rows in set (0.00 sec)

