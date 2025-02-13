---
title:  "[SQL First Step] 22. Grouping - GROUP BY"
excerpt: "GROUP BY"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-13
last_modified_at: 2025-02-13

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `GROUP BY`
By using group by, you can group columns and apply aggregate funtions. For example, you can get total sales volume for each branch from sales data.

```sql
SELECT * FROM table_name GROUP BY col1, col2 ...
```

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

-- Group by name only: Same as DISTINCT
mysql> SELECT name FROM sample51 GROUP BY name;
+------+
| name |
+------+
| A    |
| B    |
| C    |
| NULL |
+------+
4 rows in set (0.00 sec)

- Get the number of rows and sum of quantity for each name
mysql> SELECT name, COUNT(name), SUM(quantity) FROM sample51 GROUP BY name;
+------+-------------+---------------+
| name | COUNT(name) | SUM(quantity) |
+------+-------------+---------------+
| A    |           2 |             3 |
| B    |           1 |            10 |
| C    |           1 |             3 |
| NULL |           0 |          NULL |
+------+-------------+---------------+
4 rows in set (0.01 sec)
```

<br/>


## Set Condition Using `HAVING`
You might want to set a condition after grouping. For example, you might want to get a name with one row. However, the following command with `WHERE` will not work.

```sql
mysql> SELECT name, COUNT(name) FROM sample51 WHERE COUNT(name)=1 GROUP BY name; 
ERROR 1111 (HY000): Invalid use of group function
```

It's because of the processing priority. <span style="color:#F5F5F7">`GROUP BY` is processed later than `WHERE`, so an aggregate function that needs grouping could not be used in `WHERE`</span>.

Instead of `WHERE`, use `HAVING` The processing priority of `HAVING` is lower than `GROUP BY` and it will work fine.

```sql
mysql> SELECT name, COUNT(name) FROM sample51 GROUP BY name HAVING COUNT(name)=1;
+------+-------------+
| name | COUNT(name) |
+------+-------------+
| B    |           1 |
| C    |           1 |
+------+-------------+
2 rows in set (0.00 sec)
```
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Processing Priority of GROUP BY and HAVING.png"
    style="width: 60%; height: auto; margin:10px">
</figure>
<br/>

However, you can't use nickname in `HAVING` because it is processed earlier than `SELECT`.

<br/>

## Grouping Multiple Columns
Columns which is not specified in `GROUP BY` can't be used in `SELECT` without an aggregate function. In other words, you can't use the command as a below.

```sql
SELECT no, name, quantity FROM sample51 GROUP BY name;
```

By using `GROUP BY`, returning result is one row for each group. Therefore, the command as above is not clear which column to return when grouping.


<br/>

## Ordering the result of `GROUP BY`
To order the result of `GROUP BY`, use `ORDER BY`.

```sql
mysql> SELECT name, COUNT(name), SUM(quantity) FROM sample51 GROUP BY name ORDER BY SUM(quantity) DESC;
+------+-------------+---------------+
| name | COUNT(name) | SUM(quantity) |
+------+-------------+---------------+
| B    |           1 |            10 |
| A    |           2 |             3 |
| C    |           1 |             3 |
| NULL |           0 |          NULL |
+------+-------------+---------------+
4 rows in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
