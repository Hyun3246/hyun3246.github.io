---
title:  "[SQL First Step] 24. Correlated Subquery"
excerpt: "EXISTS, Correlated Subquery, IN"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-14
last_modified_at: 2025-02-14

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `EXISTS`
To check whether data exists or not while using subquery, use `EXISTS`.

For example, if you want to change data NULL into '있음' or '없음' depending on the other table, do as a following.

```sql
-- Table to change
mysql> SELECT * FROM sample551;
+------+------+
| no   | a    |
+------+------+
|    1 | NULL |
|    2 | NULL |
|    3 | NULL |
|    4 | NULL |
|    5 | NULL |
+------+------+
5 rows in set (0.00 sec)

-- Table to refer to
mysql> SELECT * FROM sample552;
+------+
| no2  |
+------+
|    3 |
|    5 |
+------+
2 rows in set (0.00 sec)

-- Command
mysql> UPDATE sample551 SET a='있음' WHERE
    -> EXISTS(SELECT * FROM sample552 WHERE no2=no);
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

-- Result
mysql> SELECT * FROM sample551;
+------+--------+
| no   | a      |
+------+--------+
|    1 | NULL   |
|    2 | NULL   |
|    3 | 있음   |
|    4 | NULL   |
|    5 | 있음   |
+------+--------+
5 rows in set (0.00 sec)
```

It will be easy to understand that <span style="color:#F5F5F7">subquery is executed row by row whenever a row is retrieved using a `WHERE` clause of `UPDATE`</span>. <span style="color:#F5F5F7">`EXISTS` returns True when row is returned by satisfying the condition(`WHERE` of subquery).</span>. For example, the first row of table sample551 will not be changed because `EXISTS` will return False, and `EXISTS` returns False because the `WHERE` of subquery is not satisfied(1 $\neq$ 3 and 5).

To select the oppoiste case, use `NOT EXISTS`.

```sql
mysql> UPDATE sample551 SET a='없음' WHERE
    -> NOT EXISTS (SELECT * FROM sample552 WHERE no2=no);
Query OK, 3 rows affected (0.01 sec)
Rows matched: 3  Changed: 3  Warnings: 0

mysql> SELECT * FROM sample551;
+------+--------+
| no   | a      |
+------+--------+
|    1 | 없음   |
|    2 | 없음   |
|    3 | 있음   |
|    4 | 없음   |
|    5 | 있음   |
+------+--------+
5 rows in set (0.00 sec)
```

<br/>


## Correlated Subquery
The subquery <span style="color:#F5F5F7">that parent command and subquery correlates specific relationship is called correlated subquery</span>. The command used above is an example of correlated subquery because subquery uses column of parent for comparison.

```sql
-- Example of Correlated Subquery
UPDATE sample551 SET a='있음' WHERE
    -> EXISTS(SELECT * FROM sample552 WHERE no2=no);
```

However, one question arises. What will happen if the column name of parent and subquery are same? In most cases, it does not work well. To specify the table, do as follows (append `table_name.` in front of the column).

```sql
-- Specify table name
UPDATE sample551 SET a='있음' WHERE
    -> EXISTS(SELECT * FROM sample552 WHERE sample552.no2=sample551.no);
```

<br/>

## `IN`
To compare sets, use `IN` instead of '='. 

```sql
mysql> SELECT * FROM sample551 WHERE no IN(3, 5);
+------+--------+
| no   | a      |
+------+--------+
|    3 | 있음   |
|    5 | 있음   |
+------+--------+
2 rows in set (0.00 sec)
```

With `IN`, selecting rows which is in the other table becomes simpler.

```sql
mysql> SELECT * FROM sample551 WHERE no IN(SELECT no2 FROM sample552);
+------+--------+
| no   | a      |
+------+--------+
|    3 | 있음   |
|    5 | 있음   |
+------+--------+
2 rows in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
