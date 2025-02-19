---
title:  "[SQL First Step] 29. Index Creation and Deletion"
excerpt: "Creating and deleting index"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-19
last_modified_at: 2025-02-19

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Creating Index
There is no creating index command in standard SQL. However, many products have index structure and can handle it similarly.

To create index, use `CREATE INDEX`.

```sql
CREATE INDEX index_name ON table_name(col1, col2, ...)
```

For example, the command below uses column 'no' to create index 'isample65'.

```sql
mysql> CREATE INDEX isample65 ON sample62(no);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

<br/>

## Deleting Index
To delete index, use `DROP INDEX`.

```sql
-- Schema object
DROP INDEX index_name

-- Object in table
DROP INDEX index_name ON table_name
```

In MySQL, use the below one.

```sql
mysql> DROP INDEX isample65 ON sample62;
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

<br/>

## Using Index for Searching
When you use index column in `WHERE` command, index will be automatically used. In the example below, column 'a' was used for index. Therefore, you can check that the index is being used. See 'possible_keys' and 'key' features. If index is not being used, the two values will be NULL.

```sql
mysql> CREATE INDEX isample65 ON sample62(a);
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0

-- Check whether index is being used.
mysql> EXPLAIN SELECT * FROM sample62 WHERE a='a';
+----+-------------+----------+------------+------+---------------+-----------+---------+-------+------+----------+-------+
| id | select_type | table    | partitions | type | possible_keys | key       | key_len | ref   | rows | filtered | Extra |
+----+-------------+----------+------------+------+---------------+-----------+---------+-------+------+----------+-------+
|  1 | SIMPLE      | sample62 | NULL       | ref  | isample65     | isample65 | 93      | const |    1 |   100.00 | NULL  |
+----+-------------+----------+------------+------+---------------+-----------+---------+-------+------+----------+-------+
1 row in set, 1 warning (0.00 sec)
```

`EXPLAIN` is a command to check the execution plan. Execution plan plays the following roles.

- Check the existence of index.
- Decide (not) to use index based on optimization. If the index tree is not helpful, it will not be used.


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*