<!-- 1. -->
mysql> select first_name, last_name from student;
+------------+-----------+
| first_name | last_name |
+------------+-----------+
| Eric       | Ephram    |
| Greg       | Gould     |
| Adam       | Ant       |
| Howard     | Hess      |
| Charles    | Caldwell  |
| James      | Joyce     |
| Doug       | Dumas     |
| Kevin      | Kraft     |
| Frank      | Fountain  |
| Brian      | Biggs     |
+------------+-----------+
10 rows in set (0.00 sec)

<!-- 2. -->
mysql> select * from student  where years_of_experience < 8;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          1 | Eric       | Ephram    |                   2 | 2016-03-31 |
|          2 | Greg       | Gould     |                   6 | 2016-09-30 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
|          4 | Howard     | Hess      |                   1 | 2016-02-28 |
|          5 | Charles    | Caldwell  |                   7 | 2016-05-07 |
|          8 | Kevin      | Kraft     |                   3 | 2016-04-15 |
|         10 | Brian      | Biggs     |                   4 | 2015-12-25 |
+------------+------------+-----------+---------------------+------------+
7 rows in set (0.00 sec)

<!-- 3 -->
mysql> select student_id, last_name, start_date from student order by last_name asc;
+------------+-----------+------------+
| student_id | last_name | start_date |
+------------+-----------+------------+
|          3 | Ant       | 2016-06-02 |
|         10 | Biggs     | 2015-12-25 |
|          5 | Caldwell  | 2016-05-07 |
|          7 | Dumas     | 2016-07-04 |
|          1 | Ephram    | 2016-03-31 |
|          9 | Fountain  | 2016-01-31 |
|          2 | Gould     | 2016-09-30 |
|          4 | Hess      | 2016-02-28 |
|          6 | Joyce     | 2016-08-27 |
|          8 | Kraft     | 2016-04-15 |
+------------+-----------+------------+
10 rows in set (0.00 sec)

<!-- 4 -->
mysql> select * from student where first_name in ("Adam", "James", "Frank") order by last_name desc;
+------------+------------+-----------+---------------------+------------+
| student_id | first_name | last_name | years_of_experience | start_date |
+------------+------------+-----------+---------------------+------------+
|          6 | James      | Joyce     |                   9 | 2016-08-27 |
|          9 | Frank      | Fountain  |                   8 | 2016-01-31 |
|          3 | Adam       | Ant       |                   5 | 2016-06-02 |
+------------+------------+-----------+---------------------+------------+
3 rows in set (0.00 sec)

<!-- 5 -->
mysql> select first_name, last_name, start_date from student where start_date between '2016-01-01' and '2016-06-30'  order by start_date desc;
+------------+-----------+------------+
| first_name | last_name | start_date |
+------------+-----------+------------+
| Adam       | Ant       | 2016-06-02 |
| Charles    | Caldwell  | 2016-05-07 |
| Kevin      | Kraft     | 2016-04-15 |
| Eric       | Ephram    | 2016-03-31 |
| Howard     | Hess      | 2016-02-28 |
| Frank      | Fountain  | 2016-01-31 |
+------------+-----------+------------+
6 rows in set (0.00 sec)

<!-- Medium -->
mysql> explain assignment;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11)          | NO   |     | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> select * from assignment;
+---------------+------------+----------------+----------+----------+
| assignment_id | student_id | assignment_nbr | class_id | grade_id |
+---------------+------------+----------------+----------+----------+
|             1 |          2 |              3 |        4 |        1 |
|             2 |          2 |              3 |        4 |        2 |
|             3 |          2 |              3 |        4 |        3 |
|             4 |          2 |              3 |        4 |        4 |
|             5 |          2 |              3 |        4 |        5 |
+---------------+------------+----------------+----------+----------+
5 rows in set (0.00 sec)

mysql> explain grade;
+-------------+-------------+------+-----+---------+----------------+
| Field       | Type        | Null | Key | Default | Extra          |
+-------------+-------------+------+-----+---------+----------------+
| id          | int(11)     | NO   | PRI | NULL    | auto_increment |
| grade_value | varchar(30) | YES  |     | NULL    |                |
+-------------+-------------+------+-----+---------+----------------+
2 rows in set (0.00 sec)

mysql> select * from grade;
+----+-----------------------------+
| id | grade_value                 |
+----+-----------------------------+
|  1 | Incomplete                  |
|  2 | Complete and unsatisfactory |
|  3 | Complete and satisfactory   |
|  4 | Exceeds expectations        |
|  5 | Not graded                  |
+----+-----------------------------+
5 rows in set (0.00 sec)

<!-- Hard -->
mysql> explain assignment;
+----------------+------------------+------+-----+---------+----------------+
| Field          | Type             | Null | Key | Default | Extra          |
+----------------+------------------+------+-----+---------+----------------+
| assignment_id  | int(11) unsigned | NO   | PRI | NULL    | auto_increment |
| student_id     | int(11) unsigned | NO   | MUL | NULL    |                |
| assignment_nbr | int(11)          | NO   |     | NULL    |                |
| class_id       | int(11)          | YES  |     | NULL    |                |
| grade_id       | int(11)          | YES  | MUL | NULL    |                |
+----------------+------------------+------+-----+---------+----------------+
5 rows in set (0.00 sec)

mysql> insert into assignment values (4, 20, 3, 4, 4);
ERROR 1062 (23000): Duplicate entry '4' for key 'PRIMARY'
mysql> insert into assignment values (5, 20, 3, 4, 4);
ERROR 1062 (23000): Duplicate entry '5' for key 'PRIMARY'
mysql> insert into assignment values (6, 20, 3, 4, 4);
ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`tiy`.`assignment`, CONSTRAINT `fk_student_id` FOREIGN KEY (`student_id`) REFERENCES `student` (`student_id`))
