---
title:  "[SQL First Step] 2. Various Database"
excerpt: "Types of DB, Dialect SQL"

categories:
  - Data Science & ML
tags:
  - [Database]

use_math: true
toc: true
toc_sticky: true

date: 2025-01-28
last_modified_at: 2025-01-28

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Various Types of Database
- Hierarchical Database: Store data in hierarchical structure such as folder and files.
- <span style="color:#F5F5F7">Relational Database</span>: Store table type data with columns and rows. Devised based on relational algebra.
- Object Oriented Database: Store object itself as a data.
- XML Database: Store XML-form data. XML is a data type using tags such as '\<data\>data\<\/data\>'.
- Key-Value Store (KVS): Store data in key-value pair. 

SQL is only available in Relational Database. 

RDBMS is used in various systems. Most main frames use RDBMS. RDBMS is also used in Internet, smartphones.

<br/>

## Database Products
There are many RDBMS products.

- Oracle: The most widely used.
- DB2
- SQL Server
- PostgreSQL: Open sourse.
- MySQL: Open sourse.
- SQLite

<br/>

## Standard SQL and Dialect SQL
<span style="color:#F5F5F7">As there are variety of RDBMS products and each of them provides unique functions</span>, SQL which is slightly different from standard one has developed.

The most well-known examples of dialect are keyword omission(e.g. 'FROM' keyword behind 'DELETE') and 'join'.

However, using standardized SQL is recommended.


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*