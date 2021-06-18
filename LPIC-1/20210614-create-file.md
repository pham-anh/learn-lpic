---
title: Creating files
date: 2021-06-14
tags:
- touch
categories:
- lpic1
---

## `touch`

Change file timestamps

`touch` will create a file if it doesn't exist

```
$ touch abc.txt
$ ls -la
total 0
drwxrwxr-x. 2 pqa pqa  21 Jun 13 20:54 .
drwxrwxr-x. 8 pqa pqa 246 Jun 13 20:54 ..
-rw-rw-r--. 1 pqa pqa   0 Jun 13 20:54 abc.txt
```

Use `stat` to check its information

```
$ stat abc.txt 
  File: ‘abc.txt’
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
Device: 802h/2050d      Inode: 17848215    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1001/     pqa)   Gid: ( 1002/     pqa)
Context: unconfined_u:object_r:user_home_t:s0
Access: 2021-06-13 20:54:35.325819459 +0000
Modify: 2021-06-13 20:54:35.325819459 +0000
Change: 2021-06-13 20:54:35.325819459 +0000
 Birth: -
```

We can specify a date for a file

```
$ touch -d '2020-12-16' def.txt
$ ls -la
total 0
drwxrwxr-x. 2 pqa pqa  36 Jun 13 20:55 .
drwxrwxr-x. 8 pqa pqa 246 Jun 13 20:54 ..
-rw-rw-r--. 1 pqa pqa   0 Jun 13 20:54 abc.txt
-rw-rw-r--. 1 pqa pqa   0 Dec 16 00:00 def.txt
```

```
$ stat def.txt 
  File: ‘def.txt’
  Size: 0               Blocks: 0          IO Block: 4096   regular empty file
Device: 802h/2050d      Inode: 17848217    Links: 1
Access: (0664/-rw-rw-r--)  Uid: ( 1001/     pqa)   Gid: ( 1002/     pqa)
Context: unconfined_u:object_r:user_home_t:s0
Access: 2020-12-16 00:00:00.000000000 +0000
Modify: 2020-12-16 00:00:00.000000000 +0000
Change: 2021-06-13 20:55:59.544554121 +0000
 Birth: -
```