---
title:  "[SQL First Step] 10. Sorting by Specifying Multiple Columns"
excerpt: "Sorting by Specifying Multiple Columns"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-07
last_modified_at: 2025-02-07

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Sorting by Specifying Multiple Columns
To use multiple columns for sorting, write multiple columns next to the `ORDER BY`, separating with commas.

```sql
SELECT col FROM table_name WHERE conditions ORDER BY col1 [ASC], col2 [DESC];
```

See the following examples.

```sql
mysql> SELECT * FROM sample32;
+------+------+
| a    | b    |
+------+------+
|    1 |    1 |
|    2 |    1 |
|    2 |    2 |
|    1 |    3 |
|    1 |    2 |
+------+------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM sample32 ORDER BY a, b;
+------+------+
| a    | b    |
+------+------+
|    1 |    1 |
|    1 |    2 |
|    1 |    3 |
|    2 |    1 |
|    2 |    2 |
+------+------+
5 rows in set (0.00 sec)

mysql> SELECT * FROM sample32 ORDER BY a ASC, b DESC;
+------+------+
| a    | b    |
+------+------+
|    1 |    3 |
|    1 |    2 |
|    1 |    1 |
|    2 |    2 |
|    2 |    1 |
+------+------+
5 rows in set (0.00 sec)
```

If you don't write `ASC` or `DESC`, the basic criteria will be `ASC`.

NULL value is special. As numerical comparison is impossible for NULL, <span style="color:#F5F5F7">NULL is considered as the largest or the smallest</span>. However, there is no common standard and the rule is different across the products. In MySQL, NULL is considered as the smallest value.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*