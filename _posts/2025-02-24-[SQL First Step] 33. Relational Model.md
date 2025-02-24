---
title:  "[SQL First Step] 33. Relational Model"
excerpt: "Relation and Relational Algebra"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-24
last_modified_at: 2025-02-24

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Relational Model
Database based on relational model is relational database. SQL is made in relational model.

The basic component of relational model is <span style="color:#F5F5F7">'relation'</span>. <span style="color:#F5F5F7">Relation in relational model means a table</span>, not a relationship between tables.

In relation, there are attributes, which are columns of SQL. There are also tuples, which are rows of SQL.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Structure of Relation.png"
    style="width: 60%; height: auto; margin:10px">
</figure>
<br/>


## Relational Algebra
Relational algebra is a theory that operations of relations correspond to the operations of sets.

Let's compare several relational operations and SQL.

|Relational Operation|SQL|Meaning|
|:--:|:--:|:--|
|Union|`UNION`|Addition of relations|
|Difference|`EXCEPT`|Subtraction of relations|
|Intersection|`INTERSECT`|Common part of relations|
|Cartesian product|`CROSS JOIN`|Cartesian product of relations|
|Selection|`WHERE`|Extraction of tuples|
|Projection|`SELECT`|Extraction of attributes|
|Join|`INNER JOIN`|Extraction of desired tuples in the result of Cartesian product|

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*