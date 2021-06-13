---
title: ls - list directory contents
date: 2021-06-09
tags:
- ls
- hardLink
categories:
- lpic1
---

## Commonly used options

![ls options](../img-lpic/command-ls-options.svg)

## Read output

![ls output](../img-lpic/command-ls-read-output.svg)

## Use `ls -F` to show file type

### `*` executable file

```
$ ls -F /usr/bin/yum
/usr/bin/yum*
```

The trailing `*` shows that this is an executable file.

### `@` symbolic link

```
$ ls -F /etc/redhat-release 
/etc/redhat-release@
```

The trailing `@` shows that this is a symbolic link.

### `/` directory

```
$ ls -F /etc/
acpi/                    egl/ 
```

The trailing `/` shows that they are directories.

### No special trailing keyword

```
ls -F /etc/
ld.so.conf     
```

In this example, `ld.so.conf` is a normal file.
