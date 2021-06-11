---
title: Wildcard and Regular expression
date: 2021-06-06
tags:
- centos
- command
categories:
- lpic1
---

## *

`*` means matching 0 or any character. So in the following command line, we can list and file name beginning with `/dev/sda`.

```
$ ls -la /dev/sda*
brw-rw----. 1 root disk 8, 0 Jun  4 21:01 /dev/sda
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```

## ?

`?` means matching any single character. So in the following command, we can list any file name that have at least 1 character following `/dev/sda`.

```
$ ls -la /dev/sda?
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```

We no longer see `/dev/dsa` in the list because it has no character following `/dev/sda`.

## [12]

`[<a group of characters>]` means matching any character in the group. So in the following command, we can list any file name that have `1` or `2` following `/dev/sda`.

```
$ ls -la /dev/sda[12]
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```
