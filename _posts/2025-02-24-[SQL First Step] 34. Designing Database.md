---
title:  "[SQL First Step] 34. Designing Database"
excerpt: "Database Design, ER Diagram"

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
## Designing Database
Desining database means defining database objects such as table, index, view in the schema of database.

The major part of database design is to decide the name of table and columns and its datatype. You should also consider the relationship between multiple tables.

The following is an example of table design. It is similar to the result of `DESC` command.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Example of Table design.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

Let's look at components one by one.

1. Logical name, Physical name <br/>
    When naming tables, you should follow rules of naming. This can make it hard to express the real function of the table. To solve the problem, you can call the table in 'logical name' which reflects the real function of the table and not used in command. It is different from 'physical name', which is used in `CREATE TABLE` command.

2. Datatype <br/>
    You should set a datatype for each column. You can also limit the range of data (e.g. among 1, 2, 3) by setting `CHECK` limitation.

3. Fixed length, Variable length <br/>
     Choose the length of character type between fixed and variable. You should consider the data before choosing the length. For example, if the length is already fixed such as product number, fixed length would be more appropriate. <br/>
     If you need very long length, use LOB type.
    
4. Primary key <br/>
    Be careful when you setting primary key. If it is hard to choose, use `AUTO_INCREMENT` function to make auto incremental column.


<br/>

## ER Diagram
ER Diagram (Entity Relationship Diagram) is a diagram that expresses the relationship between multiple entities. Here, an entity is a table or a view.

If entities are related, connect the columns used for the relationship with lines.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/Example of ER Diagram.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*