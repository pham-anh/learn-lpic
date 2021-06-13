---
title: Reading files
date: 2021-06-13
tags:
- read-file
categories:
- lpic1
---

## `cat` concatenate

Example: concatenate the content of 2 files

```
$ cat hw.txt 
hello world
$ cat hk.txt 
hello kitty
$ cat hw.txt hk.txt 
hello world
hello kitty
```

## `less`

Use `less` to show content of large file from top to bottom

```
$ wc -l /etc/services 
11176 /etc/services
```

We can see that this file has more than 10 thousands line. So we use `less` to read it partially.

```
$ less !$
less /etc/services
# /etc/services:
# $Id: services,v 1.55 2013/04/14 ovasik Exp $
#
# Network services, Internet style
# IANA services version: last updated 2013-04-10
.....
# service-name  port/protocol  [aliases ...]   [# comment]

tcpmux          1/tcp                           # TCP port service multiplexer
tcpmux          1/udp                           # TCP port service multiplexer
rje             5/tcp                           # Remote Job Entry
rje             5/udp                           # Remote Job Entry
```

While reading the file, we can use:
- `/<keyword>` to search forward
- `?<keyword>` to search backward
- `n` to go to the `next` match
- `p` to go to the `previous` match
- `q` to `quit`

## `head` and `tail`

### `head`

Show top `n` lines. Default of `n` is `10`

`head -n <number>` to specify to number of lines to show.

```
$ head /etc/services 
# /etc/services:
# $Id: services,v 1.55 2013/04/14 ovasik Exp $
#
# Network services, Internet style
# IANA services version: last updated 2013-04-10
#
# Note that it is presently the policy of IANA to assign a single well-known
# port number for both TCP and UDP; hence, most entries here have two entries
# even if the protocol doesn't support UDP operations.
# Updated from RFC 1700, ``Assigned Numbers'' (October 1994).  Not all ports
```

Show top 5 lines.

```
$ head /etc/services -n 5
# /etc/services:
# $Id: services,v 1.55 2013/04/14 ovasik Exp $
#
# Network services, Internet style
# IANA services version: last updated 2013-04-10
```

### `tail`

The same as `head` but show bottom `n` line

`tail -f` keep tracking of the file and show new content if new content is added into the file.