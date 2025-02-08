---
title:  "[SQL First Step] 13. Character Operations"
excerpt: "Character Operations, CONCAT, SUBSTRING, TRIM, CHARACTER_LENGTH and OCTET_LENGTH"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-08
last_modified_at: 2025-02-08

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
# Combining Character
To combine characters use +(SQL Server), ||(Oracle, DB2, PostgreSQL), or `CONCAT`(MySQL).

```sql
mysql> SELECT * FROM sample35;
+------+-------+----------+------+
| no   | price | quantity | unit |
+------+-------+----------+------+
|    1 |   100 |       10 | 개   |
|    2 |   230 |       24 | 통   |
|    3 |  1980 |        1 | 장   |
+------+-------+----------+------+
3 rows in set (0.00 sec)

mysql> SELECT CONCAT(quantity, unit) FROM sample35;
+------------------------+
| CONCAT(quantity, unit) |
+------------------------+
| 10개                   |
| 24통                   |
| 1장                    |
+------------------------+
3 rows in set (0.00 sec)
```

<br/>

## Extractig Character
To extract character, use `SUBSTRING`(`SUBSTR` for some products).
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/SUBSTRING example.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>


## Removing Space in the front and back
To remove space in the front and back of a character, use `TRIM`. This will not remove space between the character.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/TRIM example.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

By setting parameters, you can remove other character instead of space.

<br/>

## Length of Character
To return length of character, use `CHARACTER_LENGTH`(or `CHAR_LENGTH`).

`OCTET_LENGTH` will return the character length in byte unit. The byte length is not always same as the length of character, according to the character set.

> For Korean, 'EUC-KR' and 'UTF-8' are common encoding methods. In 'EUC-KR', ASCII is 1 byte, and Korean is 2 byte. In 'UTF-8', ASCII is 1 byte, and Korean is 3 byte. 

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*