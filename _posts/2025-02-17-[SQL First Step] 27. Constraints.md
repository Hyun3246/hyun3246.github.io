---
title:  "[SQL First Step] 27. Constraints"
excerpt: "Constraints, Primary key"

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
## Constraints
<span style="color:#F5F5F7">By setting constraints, you can limit the data to be stored</span>. NOT NULL is a kind of constraints. There are also other various kinds of constraints such as primary key.

<br/>

## Setting Constraints while Creating Table
You can set constraints while creating a table as belows.

```sql
mysql> CREATE TABLE sample631(
    -> a INTEGER NOT NULL,
    -> b INTEGER NOT NULL UNIQUE,
    -> c VARCHAR(30)
    -> );
Query OK, 0 rows affected (0.00 sec)
```

Look at column b and c. In column b, there are NOT NULL and UNIQUE constraints. In column c, there are no constraints. The constraints which is defined for columns is called 'column constraints'.

You can also set contraints on multiple columns with one constraint. This is called 'table constraints'.

```sql
mysql> CREATE TABLE sample632(
    -> no INTEGER NOT NULL,
    -> sub_no INTEGER NOT NULL,
    -> name VARCHAR(30),
    -> PRIMARY KEY (no, sub_no)
    -> );
Query OK, 0 rows affected (0.00 sec)
```

The example above is a table constraint. You can set a name of constraint with `CONSTRAINT` keyword.

<br/>

## Adding Constraints
You can add contraints to existing tables. Use `ALTER TABLE`.

- Adding Column Constraints <br/>
   When adding column constraints, use `MODIFY` command as the previous chapter.

   ```sql
   ALTER TABLE sample631 MODIFY c VARCHAR(30) NOT NULL;
   ```
  
- Adding Table Constraints <br/>
  You can add table constraints with `ADD` subcommand.
  ```sql
  ALTER TABLE sample631 ADD CONSTRAINT pkey_sample631 PRIMARY KEY(a);
  ```

<br/>

## Deleting Constraints
- Deleting Column Constraints <br/>
   When deleting column constraints, use `MODIFY`.

   ```sql
   -- Removing NOT NULL constraints
   ALTER TABLE sample631 MODIFY c VARCHAR(30);
   ```
  
- Deleting Table Constraints <br/>
  You can delete table constraints with `DROP` subcommand. Setting nickname of command will be helpful as a below.
  ```sql
  -- Type 1
  ALTER TABLE sample631 DROP pkey_sample631;

  -- Type 2 (MySQL)
  ALTER TABLE sample631 DROP PRIMARY KEY;
  ```


<br/>

## Primary Key
To understand primary key, you should first understand 'search key'. Search key is a keyword when you use for searching. In other words, you will specify key when you search desired data.

<span style="color:#F5F5F7">Primary key is a search key that can specify one row</span>. If you search with a primary key, only one row will be returned. Therefore, you can write data that have same primary key value.

<span style="color:#F5F5F7">Primary key can be composed of multiple columns</span>.

```sql
mysql> SELECT a, b FROM sample635;
+---+---+
| a | b |
+---+---+
| 1 | 1 |
| 1 | 2 |
| 1 | 3 |
| 2 | 1 |
| 2 | 2 |
+---+---+
5 rows in set (0.00 sec)
```

The column a, b are primary keys. Only column a could not be a primary key because the values are duplicated. However, combining with column b, there are no longer duplicated values.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*