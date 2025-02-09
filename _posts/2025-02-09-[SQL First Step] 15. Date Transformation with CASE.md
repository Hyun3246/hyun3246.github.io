---
title:  "[SQL First Step] 15. Date Transformation with CASE"
excerpt: "CASE to transform data"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-09
last_modified_at: 2025-02-09

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Two Types of `CASE`
`CASE` is used to transform data in a desired way. For example, transform 0/1 to 'man'/'woman'.

There are two types of `CASE` phrase.

- Searched CASE
- Simple CASE

Basic mechanism is similar but let's look at one by one.

<br/>

## Searched CASE
Searched CASE is written as follows.

```sql
CASE WHEN condition_1 THEN result_1
[WHEN condition_2 THEN result_2 ...]
[ELSE result_3]
END
```

The most important characteristic of searched CASE is writing condition formulas for each `WHEN`.

```sql
mysql> SELECT a FROM sample37;
+------+
| a    |
+------+
|    1 |
|    2 |
| NULL |
+------+
3 rows in set (0.00 sec)

mysql> SELECT a AS "코드",
    -> CASE
    -> WHEN a=1 THEN '남자'
    -> WHEN a=2 THEN '여자'
    -> ELSE '미지정'
    -> END AS "성별" FROM sample37;
+--------+-----------+
| 코드   | 성별      |
+--------+-----------+
|      1 | 남자      |
|      2 | 여자      |
|   NULL | 미지정    |
+--------+-----------+
3 rows in set (0.00 sec)
```

<br/>

## Simple CASE
Unlike searched CASE, simple CASE does not write condition for each `WHEN`. 

```sql
CASE formula_0
WHEN formula_1 THEN result_1
[WHEN formula_2 THEN result_2 ...]
[ELSE result_3]
END
```

If `formula_0` and `formula_1` equal, result will be `result_1`. If there is no matching formulas, return `result_3` of `ELSE`.

```sql
mysql> SELECT a AS "코드",
    -> CASE a
    -> WHEN 1 THEN '남자'
    -> WHEN 2 THEN '여자'
    -> ELSE '미지정'
    -> END AS "성별" FROM sample37;
+--------+-----------+
| 코드   | 성별      |
+--------+-----------+
|      1 | 남자      |
|      2 | 여자      |
|   NULL | 미지정    |
+--------+-----------+
3 rows in set (0.00 sec)
```

<br/>

## Several Cautions when Using `CASE`
There are several cautions to know when using `CASE`.

- It is possible to omit `ELSE`. If there is no matching condition, the `CASE` will return NULL.
- <span style="color:#F5F5F7">To use NULL as a condition, only searched CASE will work</span>. (It is because simple CASE use '=' to check the equality.)
- To transform NULL into other values, it is recommended to use COALESCE(MySQL and Standard), NVL(Oracle), or ISNULL(SQL Server). <br/>
    ```sql
    mysql> SELECT a, COALESCE(a, 0) FROM sample37;
    +------+----------------+
    | a    | COALESCE(a, 0) |
    +------+----------------+
    |    1 |              1 |
    |    2 |              2 |
    | NULL |              0 |
    +------+----------------+
    3 rows in set (0.00 sec)

    ```
<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
