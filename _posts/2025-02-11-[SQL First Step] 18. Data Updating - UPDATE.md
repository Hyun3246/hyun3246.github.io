---
title:  "[SQL First Step] 18. Data Updating - UPDATE"
excerpt: "UPDATE"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-11
last_modified_at: 2025-02-11

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `UPDATE` to Update a Cell
To update a cell, use `UPDATE`.

```sql
UPDATE table_name SET col1=value1 WHERE condition
```

The command will update a cell, whose row and column satisty the condition. <span style="color:#F5F5F7">'=' is an assignment operator, not a comparison operator. The value next to the '=' will be a new value for the cell</span>.

```sql
mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2025-02-10 |
|  2 | XYZ  | NULL       |
+----+------+------------+
2 rows in set (0.00 sec)

mysql> UPDATE sample41 SET b='2025-02-11' WHERE no=2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2025-02-10 |
|  2 | XYZ  | 2025-02-11 |
+----+------+------------+
2 rows in set (0.00 sec)
```

If you don't write `WHERE` phrase, all rows will be upddated.

<br/>

## Advanced Skills of `UPDATE`
You can use the existing value as a parameter of `SET`. The following example uses `no` colume to update `no` column.

```sql
mysql> UPDATE sample41 SET no=no+1;
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  2 | ABC  | 2025-02-10 |
|  3 | XYZ  | 2025-02-11 |
+----+------+------------+
2 rows in set (0.00 sec)
```

If you want to update multiple columns at the same time, just write all of them with commas.

```sql
UPDATE table_name SET col1=value1, col2=value2, ... WHERE condition
```

However, be careful of the processing order. In MySQL, unlike Oracle, the command in `SET` will be performed in order. Therefore, the following commands result in different database.

```sql
-- Case 1
mysql> UPDATE sample41 SET no=no+1, a=no;
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  3 | 3    | 2025-02-10 |
|  4 | 4    | 2025-02-11 |
+----+------+------------+
2 rows in set (0.01 sec)

-- Case 2
mysql> UPDATE sample41 SET a=no, no=no+1;
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  4 | 3    | 2025-02-10 |
|  5 | 4    | 2025-02-11 |
+----+------+------------+
2 rows in set (0.00 sec)
```

> In Oracle, `SET` always refers to the previous step before the command performed. Therefore, the order of columns in `SET` will not affect the result.

To update a cell with NULL, do as a following example.

```sql
mysql> UPDATE sample41 SET a=NULL;
Query OK, 2 rows affected (0.00 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  4 | NULL | 2025-02-10 |
|  5 | NULL | 2025-02-11 |
+----+------+------------+
2 rows in set (0.00 sec)
```


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*