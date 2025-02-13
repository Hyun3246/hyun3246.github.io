---
title:  "[SQL First Step] 23. Subquery"
excerpt: "Subquery"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-13
last_modified_at: 2025-02-13

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Subquery
<span style="color:#F5F5F7">Subquery is a lower part `SELECT` command in SQL command</span>. It is usually seperated with parentheses.

The following is an image of explaining the usefulness of subquery. Two command is corporated into one command.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Example of Subquery.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>


Subquery is usually used in `WHERE` phrase.


<br/>

## Subquery in `DELETE`
As the image above, you can delete a row with only one command instead of using two commands separately. THe following command checks the minimum value and delete it at once.

```sql
DELETE FROM sample54 WHERE a=(SELECT MIN(a) FROM sample54);
```

> However, the command above does not work in MySQL. Using the same table in subquery when updating or deleteing is not allowed in MySQL. Instead, use `DELETE FROM sample54 WHERE a=(SELECT a FROM (SELECT MIN(a) AS a FROM sample54) AS x);`


<br/>

## Four Types of Subquery Pattern
When using subquery, be aware of returning type of `SELECT` command. There are 4 types.

1. Scalar(one value): `SELECT MIN(a) FROM sample54;`
2. Multiple rows with one column: `SELECT no FROM sample54;`
3. One row with multiple columns: `SELECT MIN(a), MAX(no) FROM sample54;`
4. Multiple rows and multiple columns: `SELECT no, a FROM sample54;`

Among the 4 types, scalar(type 1) is unique. <span style="color:#F5F5F7">It returns only one value and easy to use as a subquery</span>. In many cases, you would compare two values equal or not when using subquery, and scalar type is useful.

<br/>

## Subquery in `SELECT`
When using subquery in `SELECT` phrase, scalar subquery is needed. See the following example.

```sql
mysql> SELECT
    -> (SELECT COUNT(*) FROM sample51) AS sq1,
    -> (SELECT COUNT(*) FROM sample54) AS sq2;
+------+------+
| sq1  | sq2  |
+------+------+
|    5 |    3 |
+------+------+
1 row in set (0.01 sec)
```

The number of rows on table sample51 and sample 54 consist of each subquery. The upper part of `SELECT` does not have `FROM` phrase.

<br/>

## Subquery in `SET` of `UPDATE`
You can use query in `SET` phrase of `UPDATE`.

```sql
UPDATE sample54 SET a=(SELECT MAX(a) FROM sample54);
```

The example is not that useful but shows the possibility of command.

<br/>

## Subquery in `FROM`
As `FROM` phrase specifies table, it is okay not to use scalar subquery.

```sql
mysql> SELECT * FROM (SELECT * FROM sample54) sq;
+------+------+
| no   | a    |
+------+------+
|    1 |  100 |
|    2 |  900 |
|    4 |   80 |
+------+------+
3 rows in set (0.00 sec)
```

The structure of command is called 'nested structure', as `SELECT` command is in the `SELECT` command. `sq` is a nickname of table. Overlapping more than two subquery is also possible.

<br/>

## Subquery in `INSERT`
There are two types of using subquery in `INSERT`.

1. Subquery as a part of `VALUES` <br/>
    As `VALUES` set values to insert, subqueries in `VALUES` shoule be scalar subqueries.

    ```
    mysql> INSERT INTO sample541 VALUES(
    -> (SELECT COUNT(*) FROM sample51),
    -> (SELECT COUNT(*) FROM sample54)
    -> );
    Query OK, 1 row affected (0.00 sec)

    mysql> SELECT * FROM sample541;
    +------+------+
    | a    | b    |
    +------+------+
    |    5 |    3 |
    +------+------+
    1 row in set (0.00 sec)
    ```

2. `INSERT SELECT` <br/>
    Instead of `VALUES` phrase, you can use `SELECT` phrase.

    ```sql
    mysql> INSERT INTO sample541 SELECT 1, 5;
    Query OK, 1 row affected (0.00 sec)
    Records: 1  Duplicates: 0  Warnings: 0

    mysql> SELECT * FROM sample541;
    +------+------+
    | a    | b    |
    +------+------+
    |    5 |    3 |
    |    1 |    5 |
    +------+------+
    2 rows in set (0.00 sec)
    ```

    The example above inserts 1, 5 which is returned by `SELECT` phrase. <span style="color:#F5F5F7">This `INSERT SELECT` is useful when you copy a table to another table</span>.

    ```sql
    -- Copy sample543 to sample542
    INSERT INTO sample542 SELECT * FROM sample543;
    ```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*