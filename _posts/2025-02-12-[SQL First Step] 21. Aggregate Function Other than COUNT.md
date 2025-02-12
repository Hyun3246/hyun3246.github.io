---
title:  "[SQL First Step] 21. Aggregate Function Other than COUNT"
excerpt: "SUM, AVG, MIN, MAX"

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
## `SUM`
Use `SUM` to get a sum of a set.

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

mysql> SELECT SUM(quantity) FROM sample51;
+---------------+
| SUM(quantity) |
+---------------+
|            16 |
+---------------+
1 row in set (0.00 sec)
```

NULL will be ignored as the other aggregate functions. Adding character or date is impossible.

<br/>

## `AVG`
To get an average, use `AVG`. It is also possible to divide sum by the number of rows.

```sql
mysql> SELECT AVG(quantity), SUM(quantity)/COUNT(quantity) FROM sample51;
+---------------+-------------------------------+
| AVG(quantity) | SUM(quantity)/COUNT(quantity) |
+---------------+-------------------------------+
|        4.0000 |                        4.0000 |
+---------------+-------------------------------+
1 row in set (0.01 sec)
```

To include NULL in the calculation, change NULL into 0 first.

```sql
mysql> SELECT AVG(CASE WHEN quantity IS NULL THEN 0 ELSE quantity END) AS avgnull0 FROM sample51;
+----------+
| avgnull0 |
+----------+
|   3.2000 |
+----------+
1 row in set (0.00 sec)
```

<br/>

## `MIN`, `MAX`
Use `MIN` and `MAX` to get a minimum and maxinum of a set.

```sql
mysql> SELECT MIN(quantity), MAX(quantity), MIN(name), MAX(name) FROM sample51;
+---------------+---------------+-----------+-----------+
| MIN(quantity) | MAX(quantity) | MIN(name) | MAX(name) |
+---------------+---------------+-----------+-----------+
|             1 |            10 | A         | C         |
+---------------+---------------+-----------+-----------+
1 row in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*