---
title:  "[SQL First Step] 8. Search by Pattern Matching"
excerpt: "Pattern matching"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-06
last_modified_at: 2025-02-06

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## `LIKE` for Pattern Matching
To search by pattern matching(only part of text is equal) use `LIKE`.

```sql
col LIKE pattern
```

Metacharacter(wildcard) is used to assign matching part. % means string, and _ means one character.

The following example shows pattern searching of 'SQL'.

```sql
mysql> SELECT * FROM sample25;
+------+-----------------------------------------------------------------+
| no   | text                                                            |
+------+-----------------------------------------------------------------+
|    1 | SQL은 RDBMS를 조작하기 위한 언어이다.                           |
|    2 | LIKE에서는 메타문자 %와 _를 사용할 수 있다.                     |
|    3 | LIKE는 SQL에서 사용할 수 있는 술어 중 하나이다.                 |
+------+-----------------------------------------------------------------+
3 rows in set (0.00 sec)

mysql> SELECT * FROM sample25 WHERE text LIKE 'SQL%';
+------+---------------------------------------------------+
| no   | text                                              |
+------+---------------------------------------------------+
|    1 | SQL은 RDBMS를 조작하기 위한 언어이다.             |
+------+---------------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT * FROM sample25 WHERE text LIKE '%SQL%';
+------+-----------------------------------------------------------------+
| no   | text                                                            |
+------+-----------------------------------------------------------------+
|    1 | SQL은 RDBMS를 조작하기 위한 언어이다.                           |
|    3 | LIKE는 SQL에서 사용할 수 있는 술어 중 하나이다.                 |
+------+-----------------------------------------------------------------+
2 rows in set (0.00 sec)
```

Compare the second and the third one. `'SQL%'` only means string after 'SQL'. `'%SQL%'` means string before and after the 'SQL'.

Sometimes, you would like to search metacharacter such as % and _ or ''(used for text notation). For metacharacter, use escape  '\'. For ', use ' twice.

```sql
mysql> SELECT * FROM sample25 WHERE text LIKE '%\%%';
+------+------------------------------------------------------------+
| no   | text                                                       |
+------+------------------------------------------------------------+
|    2 | LIKE에서는 메타문자 %와 _를 사용할 수 있다.                |
+------+------------------------------------------------------------+
1 row in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*