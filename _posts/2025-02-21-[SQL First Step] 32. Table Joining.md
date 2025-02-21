---
title:  "[SQL First Step] 32. Table Joining"
excerpt: "Table joining, INNER JOIN and LEFT JOIN"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-21
last_modified_at: 2025-02-21

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Product Set (Cartesian product)
Product set(or Cartesian product) is multipling two sets. If set X has elements ${A, B, C}$ and set Y has ${1, 2, 3}$, the result of product will become as a following image.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Product Set example.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

To implement product set in SQL, set more than two tables in `FROM` phrase.

```sql
mysql> SELECT * FROM sample72_x;
+------+
| x    |
+------+
| A    |
| B    |
| C    |
+------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM sample72_y;
+------+
| y    |
+------+
|    1 |
|    2 |
|    3 |
+------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM sample72_x, sample72_y;
+------+------+
| x    | y    |
+------+------+
| C    |    1 |
| B    |    1 |
| A    |    1 |
| C    |    2 |
| B    |    2 |
| A    |    2 |
| C    |    3 |
| B    |    3 |
| A    |    3 |
+------+------+
9 rows in set (0.01 sec)
```

<br/>

## Inner Join
In most cases, data is scattered across multiple tables. To get a desired result from multiple tables, we should join and apply condition to them.

For example, there are two tables, one stores information of products with product code and name, and the other stores stock count only for each product code. We want to seach stock count for each product name. To implement this, use `INNER JOIN`.

```sql
-- Table 1
mysql> SELECT * FROM 상품;
+--------------+-----------+--------------+--------+--------------+
| 상품코드     | 상품명    | 메이커명     | 가격   | 상품분류     |
+--------------+-----------+--------------+--------+--------------+
| 0001         | 상품1     | 메이커1      |    100 | 식료품       |
| 0002         | 상품2     | 메이커2      |    200 | 식료품       |
| 0003         | 상품3     | 메이커3      |   1980 | 생활용품     |
+--------------+-----------+--------------+--------+--------------+
3 rows in set (0.00 sec)

-- Table 2
mysql> SELECT * FROM 재고수;
+--------------+------------+-----------+
| 상품코드     | 입고일     | 재고수    |
+--------------+------------+-----------+
| 0001         | 2014-01-03 |       200 |
| 0002         | 2014-02-10 |       500 |
| 0003         | 2014-02-14 |        10 |
+--------------+------------+-----------+
3 rows in set (0.00 sec)

-- INNER JOIN
mysql> SELECT 상품.상품명, 재고수.재고수
    -> FROM 상품 INNER JOIN 재고수
    -> ON 상품.상품코드=재고수.상품코드
    -> WHERE 상품.상품분류='식료품';
+-----------+-----------+
| 상품명    | 재고수    |
+-----------+-----------+
| 상품1     |       200 |
| 상품2     |       500 |
+-----------+-----------+
2 rows in set (0.00 sec)
```

See the `INNER JOIN` command.

- Specify columns to show in `SELECT` phrase.
- Set table in `FROM` phrase. `INNER JOIN` is written between two table names.
- Set joining condition in `ON` phrase. Only rows that satisfy the joining condition will be returned from product set of two tables.
- Set searching condition in `WHERE` phrase. Only rows that satisfy the searching condition will be shown.

You can set the nickname of table in `FROM` phrase. This will be helpful to prevent complex command.

> Foreign Key <br/>
    The two columns used above were all primary keys. However, there are also cases that a column of one table to use is not a primary key. n this case, a column of the other table is called `foreign key`. <br/>
    Understanding a relationship of two tables is important. Two tables can have '1:1', '1:n' or 'n:1' relationships with respect to rows.

<br/>

## Outer Join
There could be also cases that a row only exists in one table. For inner join, the row will not appear in the result. To show the row, use `LEFT JOIN`.

Compare the two results below.

```sql
-- LEFT JOIN
mysql> SELECT 상품3.상품명, 재고수.재고수
    -> FROM 상품3 LEFT JOIN 재고수
    -> ON 상품3.상품코드 = 재고수.상품코드
    -> WHERE 상품3.상품분류='식료품';
+--------------+-----------+
| 상품명       | 재고수    |
+--------------+-----------+
| 상품1        |       200 |
| 상품2        |       500 |
| 추가상품     |      NULL |
+--------------+-----------+
3 rows in set (0.00 sec)

-- INNER JOIN
mysql> SELECT 상품3.상품명, 재고수.재고수
    -> FROM 상품3 INNER JOIN 재고수
    -> ON 상품3.상품코드 = 재고수.상품코드
    -> WHERE 상품3.상품분류='식료품';
+-----------+-----------+
| 상품명    | 재고수    |
+-----------+-----------+
| 상품1     |       200 |
| 상품2     |       500 |
+-----------+-----------+
2 rows in set (0.00 sec)
```

In the `LEFT JOIN` command, write the table which has additional information on the left side.


> There is also `RIGHT JOIN`. The usage is exactly opposite to `LEFT JOIN`.

> There are old joining phrase only using `WHERE` phrase. However, standard SQL recommends to use `INNER JOIN` and `LEFT JOIN` instead.


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
