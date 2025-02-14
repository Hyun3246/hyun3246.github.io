---
title:  "[SQL First Step] 25. Database Object"
excerpt: "Database object, Schema"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-14
last_modified_at: 2025-02-14

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Database Object
An object is something that has substance within the database. For example, table is an object.

Contents to be stored is different according to the type of database. For table, columns and rows will be stored.

SQL command is not an object.

<br/>

## Naming of Object
Objects have a name. The rule of naming objects is similar to that of columns. (Columns are not objects.)

1. Cannot use existing names or reserved words.
2. Cannot start with number.
3. Cannot use signs except '_'.
4. Use double quote when not using English.
5. Cannot exceed the permitted length.

Do not name meaninglessly. As the name of object has nothing to do with the type of object, you can use a name once across all types.

<br/>

## Schema
<span style="color:#F5F5F7">Database object is made in 'schema'</span>. Therefore, database in different schema can hava a same name.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Schema and Database.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

Schema is definded by DDL(Data Definition Language) of SQL command. In schema, you can define databases.

> Namespace is a container that prevents components from having a same name. For example, database and schema could be considered as namespaces.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
