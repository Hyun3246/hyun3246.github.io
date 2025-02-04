---
title:  "[SQL First Step] 4. Hello World"
excerpt: "Basic form of SQL command"

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
## `SELECT * FROM table_name` and Format of SQL Commands
`SELECT * FROM table_name` is the most basic command of SQL. It reads data from database.

```sql
mysql> SELECT * FROM sample21;
+------+-----------+------------+---------------------------+
| no   | name      | birthday   | address                   |
+------+-----------+------------+---------------------------+
|    1 | 박준용      | 1976-10-18 | 대구광역시 수성구             |
|    2 | 김재진      | NULL       | 대구광역시 동구              |
|    3 | 홍길동      | NULL       | 서울특별시 마포구             |
+------+-----------+------------+---------------------------+
3 rows in set (0.00 sec)
```

Let's look closely at the command and its format.

1. `SELECT`: A kind of command.
2. `*`: Specify columns. '*' means all columns.
3. `sample21`: A name of a database.
4. `;`: Semi-colon. Must use at the end of the command.

SQL command consists of multiple phrases. Words such as `SELECT` and `FROM` divides the phrases. They are called <span style="color:#F5F5F7">'reserved words'</span>, which measn the words could not be used as a name of a database.

> In SQL, uppercase and lowercase means the same. For better represenation, use uppercase for reserved words, and lowercase for database.

<br/>

## Table
Table is an output of `SELECT `command. It consists of rows and columns. Each column has its own datatype(e.g. numeric, string). One column can have only one datatype.

Numeric data is left aligned, and string and date datatype are right aligned.

NULL means nothing is stored. <span style="color:#F5F5F7">It is a 'state' not a 'data'</span>.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
