---
title:  "[SQL First Step] 20. Getting the Number of Rows - COUNT"
excerpt: "Aggregate function and COUNT"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-12
last_modified_at: 2025-02-12

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Aggregate Function
Aggregate function is a function to calculate that returns one value which explains characteristics of some features(sets). For example, you can get the number of rows, average, min, max or sum.

Aggregate function gets a set as a parameter.

<br/>

## `COUNT` to Get the Number of Rows
Use `COUNT` to get the number of rows. The following is a example of counting the number of all rows in database.

```sql
mysql> SELECT * FROM sample51;
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
|    3 | B    |       10 |
|    4 | C    |        3 |
|    5 | NULL |     NULL |
+------+------+----------+
5 rows in set (0.00 sec)

mysql> SELECT COUNT(*) FROM sample51;
+----------+
| COUNT(*) |
+----------+
|        5 |
+----------+
1 row in set (0.01 sec)
```

By using `WHERE` phrase, you can count the number of rows satistying the condition.

```sql
mysql> SELECT * FROM sample51 WHERE name='A';
+------+------+----------+
| no   | name | quantity |
+------+------+----------+
|    1 | A    |        1 |
|    2 | A    |        2 |
+------+------+----------+
2 rows in set (0.00 sec)

mysql> SELECT COUNT(*) FROM sample51 WHERE name='A';
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
1 row in set (0.00 sec)
```

<br/>

## NULL in Aggregate Function
NULL is excluded while processing aggregate function. As `COUNT(*)` counts the number of all rows, NULL is not ignored at the example above. <span style="color:#F5F5F7">However, if you specify a column, NULL will be ignored</span>.

```sql
mysql> SELECT COUNT(no), COUNT(name) FROM sample51;
+-----------+-------------+
| COUNT(no) | COUNT(name) |
+-----------+-------------+
|         5 |           4 |
+-----------+-------------+
1 row in set (0.00 sec)
```

<br/>

## `DISTINCT` to Remove Duplication
To remove duplication of data(value), use `DISTINCT` in the `SELECT` phrase.

```sql
mysql> SELECT ALL name FROM sample51;
+------+
| name |
+------+
| A    |
| A    |
| B    |
| C    |
| NULL |
+------+
5 rows in set (0.00 sec)

mysql> SELECT DISTINCT name FROM sample51;
+------+
| name |
+------+
| A    |
| B    |
| C    |
| NULL |
+------+
4 rows in set (0.00 sec)
```

How can we count the number of unique values? `DISTINCT` formula can work as a parameter of an aggregate function. Therefore, you can write as a following example.

```sql
mysql> SELECT COUNT(ALL name), COUNT(DiSTINCT name) FROM sample51;
+-----------------+----------------------+
| COUNT(ALL name) | COUNT(DiSTINCT name) |
+-----------------+----------------------+
|               4 |                    3 |
+-----------------+----------------------+
1 row in set (0.01 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*