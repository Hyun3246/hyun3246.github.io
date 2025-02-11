---
title:  "[SQL First Step] 19. Hard Delete and Soft Delete"
excerpt: "Hard delete and Soft delete"

categories:
  - Data Science & ML
tags:
  - [Database, SQL]

use_math: true
toc: true
toc_sticky: true

date: 2025-02-11
last_modified_at: 2025-02-11

header:
  overlay_image: https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/overlay image/SQL First Step.png
---
Data deletion is classified into two types.

## Hard Delete
<span style="color:#F5F5F7">Hard delete means actually removing data</span>. It is consistent with our general sense. If you delete data with `DELETE`, the data will be removed in the database.

<br/>

## Soft Delete
Soft delete does not actually remove data. To do soft delete, make deletion flag first in the database. The column represents whether the row is deleted or not. <span style="color:#F5F5F7">If you delete the row(using `UPDATE` to change the state of the deletion flag), the only thing changes is the state of deletion flag</span>. Data still exists.

<br/>

## When to Use Hard or Soft Delete?
The situation to use hard or soft delete is different. 

- Hard Delete
    - Secure storage by deleting data.
    - Prevent privacy leakage after withdrawing membership.

- Soft Delete
    - Easy to restore previous state.

<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*