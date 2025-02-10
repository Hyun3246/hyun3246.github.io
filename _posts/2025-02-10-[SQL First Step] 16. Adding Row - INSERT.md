---
title:  "[SQL First Step] 16. Adding Row - INSERT"
excerpt: "INSERT"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-10
last_modified_at: 2025-02-10

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `INSERT` to Add a Row
By using `INSERT`, you can add a row.

```sql
INSERT INTO table_name VALUES(val1, val2, ...);
```

Write values for each column in `VALUES`.

Before adding a row, check columns and datatype by using `DESC` first.

```sql
mysql> SELECT * FROM sample41;
Empty set (0.00 sec)

mysql> DESC sample41;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| no    | int         | NO   |     | NULL    |       |
| a     | varchar(30) | YES  |     | NULL    |       |
| b     | date        | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.01 sec)

-- Adding a Row
mysql> INSERT INTO sample41 VALUES(1, 'ABC', '2025-02-10');
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2025-02-10 |
+----+------+------------+
1 row in set (0.00 sec)
```


You can also set specific columns to add values. Columns without values will be filled with default.

```sql
INSERT INTO table_name(col1, col2, ...) VALUES(val1, val2, ...);
```

```sql
mysql> INSERT INTO sample41(a, no) VALUES('XYZ', 2);
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2025-02-10 |
|  2 | XYZ  | NULL       |
+----+------+------------+
2 rows in set (0.00 sec)
```

Filling with defualt has two ways. Explicitly write `DEFAULT` or omit it.

```sql
-- Explicitly write DEFAULT
mysql> INSERT INTO sample411(no, d) VALUES(2, DEFAULT);
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM sample411;
+----+------+
| no | d    |
+----+------+
|  1 |    1 |
|  2 |    0 |
+----+------+
2 rows in set (0.00 sec)

-- Write nothing to fill with DEFAULT
mysql> INSERT INTO sample411(no) VALUES(3);
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM sample411;
+----+------+
| no | d    |
+----+------+
|  1 |    1 |
|  2 |    0 |
|  3 |    0 |
+----+------+
3 rows in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*