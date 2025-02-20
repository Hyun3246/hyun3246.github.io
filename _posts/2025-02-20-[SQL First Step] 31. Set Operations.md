---
title:  "[SQL First Step] 31. Set Operations"
excerpt: "UNION"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-20
last_modified_at: 2025-02-20

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## SQL and Set
In SQL, one row is considered as one element of set.

<br/>

## `UNION`
To implement union of sets in SQL, use `UNION` between multiple `SELECT` commands.

```sql
mysql> SELECT * FROM sample71_a;
+------+
| a    |
+------+
|    1 |
|    2 |
|    3 |
+------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM sample71_b;
+------+
| b    |
+------+
|    2 |
|   10 |
|   11 |
+------+
3 rows in set (0.00 sec)

-- Union
mysql> SELECT * FROM sample71_a
    -> UNION
    -> SELECT * FROm sample71_b;
+------+
| a    |
+------+
|    1 |
|    2 |
|    3 |
|   10 |
|   11 |
+------+
5 rows in set (0.00 sec)
```

You can also sort the result of union. <span style="color:#F5F5F7">In this case, set nickname of column in advance</span>. If the name of column doesn't match, error occurs.

```sql
mysql> SELECT a AS c FROM sample71_a
    -> UNION
    -> SELECT b AS c FROM sample71_b ORDER BY c;
+------+
| c    |
+------+
|    1 |
|    2 |
|    3 |
|   10 |
|   11 |
+------+
5 rows in set (0.00 sec)
```

To show all elements without deleting duplicated ones, use `UNION ALL` instead of `UNION`.

```sql
mysql> SELECT * FROM sample71_a 
    -> UNION ALL
    -> SELECT * FROm sample71_b;
+------+
| a    |
+------+
|    1 |
|    2 |
|    3 |
|    2 |
|   10 |
|   11 |
+------+
6 rows in set (0.00 sec)
```


> There are also intersection and difference functions in other products, but not supported in MySQL.


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*