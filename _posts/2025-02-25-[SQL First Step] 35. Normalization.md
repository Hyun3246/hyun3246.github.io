---
title:  "[SQL First Step] 35. Normalization"
excerpt: "Normalization"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-25
last_modified_at: 2025-02-25

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
## Normalization
Normalization is improving a table in a better way.

Most of the normalization steps consist of dividing a table. <span style="color:#F5F5F7">The purpose of dividing is to allocate one information(data) in one table</span>.

Although there are 5 types of normalization, but 3 types are the most widely used.

- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)

<br/>


## First Normal Form
In relational database, one cell can store one value. Therefore, '주문상품' column of the example below would look better if it is changed.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/1NF example 1.png"
    style="width: 40%; height: auto; margin:10px">
    <figcaption style="text-align:center; font-size:14px; color:#808080">
    Before
  </figcaption>
</figure>
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/1NF example 2.png"
    style="width: 40%; height: auto; margin:10px">
    <figcaption style="text-align:center; font-size:14px; color:#808080">
    After
  </figcaption>
</figure>
<br/>

As the example above, increasing rows by separating duplicated data is called <span style="color:#F5F5F7">'the first step of first normal form'</span>.

Table split is also conducted in first normal form. The purpose of splitting is to prevent the duplicated information. In the example, the table can be divided into two table, one for order info and the other for ordered product info.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/1NF example 3.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

After splitting tables, you can set a primary key. As '주문번호' in '주문' table is unique, you can set the column as a primary key. In '주문상품' table, combining '주문번호' and '상품코드' will make it possible to set two columns as a primary key.

<br/>

## Second Normal Form
In second normal form, splitting table is a basic theme also. In here, <span style="color:#F5F5F7">you will split table by columns whether they are specified by a primary key or not</span>.

In '주문상품' table, '상품명' can be specified by '상품코드' only, without using a primary key('주문번호' and '상품코드'). However, a primary key is essential to specify '개수' column. Therefore, table can be split into two table, one for a product info and the other for ordered product info.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/2NF example 1.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

Second normal form is finding partial functional dependency and splitting table.

<br/>

## Third Normal Form
In third normal form, check whether there are duplicated part except a primary key.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/3NF example 1.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>

Duplicated customer information can be split as above.

The following is a final result and its ER diagram.
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/NF example final.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/NF example final ER diagram.png"
    style="width: 40%; height: auto; margin:10px">
</figure>
<br/>


Through normalization, you can store one information in only one table. It will make it easy to update and manage database.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*
