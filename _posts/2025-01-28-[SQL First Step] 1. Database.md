---
title:  "[SQL First Step] 1. Database"
excerpt: "Database, DBMS, SQL"

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
## Database and DBMS
<span style="color:#F5F5F7">Database(DB)</span> is a set of all data in a computer. Databases are everywhere, from a data center and even to a smartphone.

<span style="color:#F5F5F7">Database Management System(DBMS)</span> is a software that can effeciently manage database. There are 3 reasons that the DBMS is needed.

- Productivity: Enhance productivity while developing a system. Basic functions such as searching, adding, removing and updating are provided by DBMS.
- Functionality: DBMS provides many functions that can control DB. It also contains handling muliple requests, and customizing.
- Reliability: By using multiple DBMS computers, <span style="color:#F5F5F7">scalability</span> and <span style="color:#F5F5F7">load balancing</span> can be implemented. It is called clustering or scaling out.
    <br/>
    <figure style="display:block; text-align:center;">
    <img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/SQL First Step/DBMS Reliability.png"
        style="width: 40%; height: auto; margin:10px">
    </figure>
    <br/>

## SQL
SQL is a language for conversations with DBMS. Although there are many types of databases, SQL is used to control <span style="color:#F5F5F7">RDBMS(Relational DBMS)</span>.

SQL command can be divided into 3 types.

- DML(Data Manipulation Language): The most basic command set of SQL. Used when adding, removing and updating data.
- DDL(Data Definition Language): Used to make or delete database object.
- DCL(Data Control Language): Control transaction or data access authority.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*