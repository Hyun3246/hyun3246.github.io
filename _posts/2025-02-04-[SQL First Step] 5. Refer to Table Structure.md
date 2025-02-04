---
title:  "[SQL First Step] 5. Refer to Table Structure"
excerpt: "DESC and datatype"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-04
last_modified_at: 2025-02-04

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `DESC` Command
TO see the structure of a table, use `DESC`. Returning table is an information of each column.

```sql
mysql> DESC sample21;
+----------+-------------+------+-----+---------+-------+
| Field    | Type        | Null | Key | Default | Extra |
+----------+-------------+------+-----+---------+-------+
| no       | int         | YES  |     | NULL    |       |
| name     | varchar(20) | YES  |     | NULL    |       |
| birthday | date        | YES  |     | NULL    |       |
| address  | varchar(40) | YES  |     | NULL    |       |
+----------+-------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
```

> `DESC` is not a SQL command.

- Field: Name of columns.
- Type: Datatype of columns.
- Null: Allow null value or not.
- Key: Key column or not.
- Default: Default value if omitted.

<br/>

## Datatype of SQL
There are multiple types of datatype in SQL.

- INTEGER: One integer. Decimal points are not allowed. `int(10)` means maximum length of integer is 10.
- CHAR: One character(string). `CHAR(10)` means maximum length of character is 10. If the length is shorter than 10, remaining parts will be filled with space.
- VARCHAR: Everything is same as CHAR, except the filling with space. Therefore the storage is variable according to the data.
- DATE: Store date(year-month-day)
- TIME: Store time(hour:minute:second).

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*