---
title:  "[SQL First Step] 7. Combining Conditions"
excerpt: "AND, OR, NOT"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-05
last_modified_at: 2025-02-05

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `AND`
Use `AND` to return true when all conditions are true.

```sql
mysql> SELECT * FROM sample24;
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    1 |    1 |    0 |    0 |
|    2 |    0 |    1 |    0 |
|    3 |    0 |    0 |    1 |
|    4 |    2 |    2 |    0 |
|    5 |    0 |    2 |    2 |
+------+------+------+------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM sample24 WHERE a<>0 AND b<>0;
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    4 |    2 |    2 |    0 |
+------+------+------+------+
1 row in set (0.00 sec)
```

<br/>

## `OR`
Use `OR` to return true when at least one condition is true.

```sql
mysql> SELECT * FROM sample24 WHERE a<>0 OR b<>0;
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    1 |    1 |    0 |    0 |
|    2 |    0 |    1 |    0 |
|    4 |    2 |    2 |    0 |
|    5 |    0 |    2 |    2 |
+------+------+------+------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM sample24 WHERE no=1 OR no=2;
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    1 |    1 |    0 |    0 |
|    2 |    0 |    1 |    0 |
+------+------+------+------+
2 rows in set (0.00 sec)
```
Take a look at the second example. <span style="color:#F5F5F7">To set a numeric value twice for the same column, you should write the name of column twice</span>. If you write only constant(e.g. `no=1 OR 2`), the constant will be a logical computation which always returns 1, except the constant is 0.

Additionally, <span style="color:#F5F5F7">the priority of `AND` is higher than `OR`</span>. Therefore, <span style="color:#F5F5F7">to prevent wrong computation, use parentheses '()'</span>.

```sql
mysql> SELECT * FROM sample24 WHERE (a=1 OR a=2) AND (b=1 OR b=2);
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    4 |    2 |    2 |    0 |
+------+------+------+------+
1 row in set (0.00 sec)
```

<br/>

## `NOT`
Use `NOT` to return the opposite value(e.g. return true if the condition is false) of the condition.

```sql
mysql> SELECT * FROM sample24 WHERE NOT (a<>0 OR b<>0);
+------+------+------+------+
| no   | a    | b    | c    |
+------+------+------+------+
|    3 |    0 |    0 |    1 |
+------+------+------+------+
1 row in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*