---
title:  "[SQL First Step] 36. Transaction"
excerpt: "Transaction, Commit, Rollback"

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
## Transaction, Commit, Rollback
Let's pretend you want to execute multiple `INSERT` command which should be executed at once. However, during the execution, error occured and some `INSERT` command wasn't executed. Is there any way that you can get back to the previous state?

The answer is NO. To prevent the disappointing situation, use `TRANSACTION`.

In SQL, auto commit, which automatically reflects the result of command, is on. By using `StART TRANSACTION`, you can explicitly turn off auto commit.

At the end of the commands, you should choose between `COMMIT` and `ROLLBACK`. <span style="color:#F5F5F7">By committing, the result in temporary area will be reflected to the result. By rollbacking, the result of commands will be removed and the state of database will be preserved</span>.

```sql
-- Commit
START TRANSACTION;
command_1
command_2
...
COMMIT;
```

```sql
-- Rollback
START TRANSACTION;
command_1
command_2
...
ROLLBACK;
```

By using transaction and commit/rollback, you can decide whether to reflect the result of command.

<br/>
<figure style="display:block; text-align:center;">
<img src="https://cdn.jsdelivr.net/gh/Hyun3246/hyun3246.github.io@master/image/SQL First Step/transaction, commit, rollback.png"
    style="width: 60%; height: auto; margin:10px">
</figure>
<br/>


<br/>
<br/>

*All images, except those with separate source indications, are excerpted from lecture materials.*