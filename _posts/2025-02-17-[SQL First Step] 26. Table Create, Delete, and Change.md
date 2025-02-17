---
title:  "[SQL First Step] 26. Table Create, Delete, and Change"
excerpt: "Table Creating, Deleting and Changing Columns"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-17
last_modified_at: 2025-02-17

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Table Creating
To create table, use `CREATE TABLE` command.

```sql
CREATE TABLE table_name(
    col_def_1,
    col_def_2,
    ...
)
```

For column definition, you need to define the name, datatype, default and null availability.

```sql
-- Column Definition
col_name datatype [DEFAULT value] [NULL|NOT NULL]
```

<span style="color:#F5F5F7">If you set a datatype as character, you must set the length also</span>. Default value and null availability can be omitted.

The following is an example of creating a table.

```sql
mysql> CREATE TABLE sample62(
    -> no INTEGER NOT NULL,
    -> a VARCHAR(30),
    -> b DATE);
Query OK, 0 rows affected (0.03 sec)

mysql> DESC sample62;
+-------+-------------+------+-----+---------+-------+
| Field | Type        | Null | Key | Default | Extra |
+-------+-------------+------+-----+---------+-------+
| no    | int         | NO   |     | NULL    |       |
| a     | varchar(30) | YES  |     | NULL    |       |
| b     | date        | YES  |     | NULL    |       |
+-------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)
```

<br/>

## Table Deleting
To delete table, use `DROP TABLE` command.

```sql
DROP TABLE table_name
```

> To remove all rows, you can use `DELETE` command without `WHERE`. However, it performs slowly. Instead of `DELETE`, use `TRUNCATE TABLE` when deleting all rows.

<br/>

## Table Changing
To change the column compositions(e.g. name of column, datatype of column) of table after making it, use `ALTER TABLE` command. There are four types of `ALTER TABLE`,

1. Adding Column <br/>
    ```sql
    ALTER TABLE table_name ADD col_def
    ```
    
    ```sql
    mysql> ALTER TABLE sample62 ADD newcol INTEGER;
    Query OK, 0 rows affected (0.01 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> DESC sample62;
    +--------+-------------+------+-----+---------+-------+
    | Field  | Type        | Null | Key | Default | Extra |
    +--------+-------------+------+-----+---------+-------+
    | no     | int         | NO   |     | NULL    |       |
    | a      | varchar(30) | YES  |     | NULL    |       |
    | b      | date        | YES  |     | NULL    |       |
    | newcol | int         | YES  |     | NULL    |       |
    +--------+-------------+------+-----+---------+-------+
    4 rows in set (0.00 sec)
    ```

2. Changing Properties of Columns <br/>
    You can change the properties of columns(except the name) with `MODIFY`.

    ```sql
    ALTER TABLE table_name MODIFY col_def
    ```

    ```sql
    mysql> ALTER TABLE sample62 MODIFY newcol VARCHAR(20);
    Query OK, 0 rows affected (0.02 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> DESC sample62;
    +--------+-------------+------+-----+---------+-------+
    | Field  | Type        | Null | Key | Default | Extra |
    +--------+-------------+------+-----+---------+-------+
    | no     | int         | NO   |     | NULL    |       |
    | a      | varchar(30) | YES  |     | NULL    |       |
    | b      | date        | YES  |     | NULL    |       |
    | newcol | varchar(20) | YES  |     | NULL    |       |
    +--------+-------------+------+-----+---------+-------+
    4 rows in set (0.00 sec)
    ```

    If error occurs, such as too short length of character relative to the existing data, the commnad will not work.

3. Changing the Name of Column <br/>
    TO change the name of column, use `CHANGE`. This can also change other properties of columns.
    
    ```sql
    ALTER TABLE table_name CHANGE [existing_col] [new_col_def]
    ```

    The following example is changing the name of newcol to c (and also its datatype).

    ```sql
    mysql> ALTER TABLE sample62 CHANGE newcol c VARCHAR(20);
    Query OK, 0 rows affected (0.00 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> DESC sample62;
    +-------+-------------+------+-----+---------+-------+
    | Field | Type        | Null | Key | Default | Extra |
    +-------+-------------+------+-----+---------+-------+
    | no    | int         | NO   |     | NULL    |       |
    | a     | varchar(30) | YES  |     | NULL    |       |
    | b     | date        | YES  |     | NULL    |       |
    | c     | varchar(20) | YES  |     | NULL    |       |
    +-------+-------------+------+-----+---------+-------+
    4 rows in set (0.00 sec)
    ```

4. Deleting Column <br/>
     When deleting column use `DROP`.

     ```sql
     ALTER TABLE table_name DROP col
     ```

    ```sql
    mysql> ALTER TABLE sample62 DROP c;
    Query OK, 0 rows affected (0.01 sec)
    Records: 0  Duplicates: 0  Warnings: 0

    mysql> DESC sample62;
    +-------+-------------+------+-----+---------+-------+
    | Field | Type        | Null | Key | Default | Extra |
    +-------+-------------+------+-----+---------+-------+
    | no    | int         | NO   |     | NULL    |       |
    | a     | varchar(30) | YES  |     | NULL    |       |
    | b     | date        | YES  |     | NULL    |       |
    +-------+-------------+------+-----+---------+-------+
    3 rows in set (0.00 sec)
    ```


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*