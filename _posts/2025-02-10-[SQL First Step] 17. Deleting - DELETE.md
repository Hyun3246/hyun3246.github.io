---
title:  "[SQL First Step] 17. Deleting - DELETE"
excerpt: "Delete rows with DELETE"

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
## `DELETE` to Delete Rows
Use `DELETE` to delete rows. Set conditions on `WHERE` phrase. If you don't a condition, `DELETE` will remove all data.

```sql
mysql> SELECT * FROM sample41;
+----+------+------------+
| no | a    | b          |
+----+------+------------+
|  1 | ABC  | 2025-02-10 |
|  2 | XYZ  | NULL       |
|  3 | NULL | NULL       |
+----+------+------------+
3 rows in set (0.00 sec)

mysql> DELETE FROM sample41 WHERE no=3;
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

`DELETE` does not remove one row. It will remove all rows which satisfy the condition.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*