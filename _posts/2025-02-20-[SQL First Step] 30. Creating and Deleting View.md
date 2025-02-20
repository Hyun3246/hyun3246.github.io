---
title:  "[SQL First Step] 30. Creating and Deleting View"
excerpt: "View"

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
## View
<span style="color:#F5F5F7">View is a database objectified version of subquery</span>. <span style="color:#F5F5F7">View records `SELECT` command</span>, which is orininally unable to function as a database object.

By using view, you can store complicating `SELECT` commands and easily reuse them.

View is a virtual table, which doesn't actually have a storage.

<br/>

## Creating and Deleting View
To create view, use `CREATE VIEW` command.

```sql
CREATE VIEW view_name AS SELECT command
```

```sql
mysql> CREATE VIEW sample_view_67 AS SELECT * FROM sample54;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT * FROM sample_view_67;
+------+------+
| no   | a    |
+------+------+
|    1 |  100 |
|    2 |  900 |
|    4 |   80 |
+------+------+
3 rows in set (0.00 sec)
```

You can also set column name for a new view. The number of names must be equal to that of `SELECT` command.

```sql
CREATE VIEW view_name(col1, col2, ...) AS SELECT command
```

```sql
mysql> CREATE VIEW sample_view_672(n, v, v2) AS
    -> SELECT no, a, a*2 FROM sample54;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT * FROM sample_view_672 WHERE n=1;
+------+------+------+
| n    | v    | v2   |
+------+------+------+
|    1 |  100 |  200 |
+------+------+------+
1 row in set (0.01 sec)
```

When deleting view, use `DROP VIEW`.

```sql
DROP VIEW view_name
```

<br/>


## Weakness of View
View doens't occupy storage. <span style="color:#F5F5F7">Whenever view is referred, `SELECT` command of view is performed and the result is stored temporary</span>. Therefore, if there are too much data in database or too many views are used, the rate of processing will decrease.

To solve the temporary storing problem, materialized view was developed. Materialized view is stored in the storage and updated frequently when data changed. However, not all products(including MySQL) support materialized view.

<span style="color:#F5F5F7">Additionally, in principle, SELECT command of view should be executed independently</span>. This limination could be avoided by using function table.


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*