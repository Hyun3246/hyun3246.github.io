---
title:  "[SQL First Step] 14. Date Operations"
excerpt: "Datetime Operations"

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
## Checking System Date and Time
To check the time of system, use `CURRENT_TIMESTAMP`.

```sql
mysql> SELECT CURRENT_TIMESTAMP;
+---------------------+
| CURRENT_TIMESTAMP   |
+---------------------+
| 2025-02-09 10:59:50 |
+---------------------+
1 row in set (0.00 sec)
```

<br/>

## Formatting Date and Time
You can specify date and time format by using `DATE_FORMAT`(MySQL) or `TO_DATE`(Oracle).

```sql
mysql> SELECT DATE_FORMAT(CURRENT_TIMESTAMP(), "%Y/%M/%d");
+----------------------------------------------+
| DATE_FORMAT(CURRENT_TIMESTAMP(), "%Y/%M/%d") |
+----------------------------------------------+
| 2025/February/09                             |
+----------------------------------------------+
1 row in set (0.00 sec)

mysql> SELECT DATE_FORMAT(CURRENT_TIMESTAMP(), "%Y/%m/%d");
+----------------------------------------------+
| DATE_FORMAT(CURRENT_TIMESTAMP(), "%Y/%m/%d") |
+----------------------------------------------+
| 2025/02/09                                   |
+----------------------------------------------+
1 row in set (0.00 sec)
```

<br/>

## Addition and Subtraction of Date
Use `INTERVAL` to add or subtract specific inverval of date. The following is an example of getting date one day later.

```sql
mysql> SELECT CURRENT_DATE + INTERVAL 1 DAY;
+-------------------------------+
| CURRENT_DATE + INTERVAL 1 DAY |
+-------------------------------+
| 2025-02-10                    |
+-------------------------------+
1 row in set (0.00 sec)
```

It is also possible to subtract dates from each other.

```sql
mysql> SELECT DATEDIFF('2024-02-28', '2014-01-01');
+--------------------------------------+
| DATEDIFF('2024-02-28', '2014-01-01') |
+--------------------------------------+
|                                 3710 |
+--------------------------------------+
1 row in set (0.00 sec)
```

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*