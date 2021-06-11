---
title: Some basic commands
date: 2021-06-08
tags:
- centos
- command
categories:
- lpic1
---

## `tty`

Show terminal that we are connecting to

```
$ tty
/dev/ttys002
```

## `ls -l $(tty)`

```
$ ls -l $(tty)
crw--w----  1 quynhanhpham  tty   16,   3 Jun  5 05:54 /dev/ttys003
```

Run `tty`, then pass the result of `tty` into `ls -l`.
It is the same as these 2 command line

```
$ tty
/dev/ttys002
$ ls -l /dev/ttys002
crw--w----  1 quynhanhpham  tty   16,   2 Jun  5 05:44 /dev/ttys002
```

## `yum whatprovides <command name>`

Check which package provide a command

```
$ yum whatprovides lsb
Loaded plugins: fastestmirror
Determining fastest mirrors

...

redhat-lsb-4.1-27.el7.centos.1.i686 : Implementation of Linux Standard Base specification
Repo        : base
Matched from:
Provides    : lsb = 4.1-27.el7.centos.1



redhat-lsb-4.1-27.el7.centos.1.x86_64 : Implementation of Linux Standard Base specification
Repo        : base
Matched from:
Provides    : lsb = 4.1-27.el7.centos.1
```

So we can see that the package `redhat-lsb` provides `lsb` command. If we want to use that command, go ahead and install the package

## `yum install <package name>`

Install a package.
Here `sudo` is needed because the current user don't have enough permission for package installation.

```
$ sudo yum install redhat-lsb
...

Total download size: 66 M
Installed size: 181 M
Is this ok [y/d/N]: y      # ↩︎ input an "y" here

Complete!
```

## `lsblk`

List block devices of the system.

Block devices are disks and partitions.

```
$ lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   20G  0 disk 
├─sda1   8:1    0  200M  0 part /boot/efi
└─sda2   8:2    0 19.8G  0 part /
```

Here we have:

- `sda`: disk
- `sda1`, `sda2`: partitions

## `pwd` print working directory

## `which`

Show full path to a command

```
$ which git
/usr/bin/git
```


## `cp` copy

Copy a file. Need `read` permission on the copied file and `write` permission on the destination directory.

Use `cp -i` (-i as `interaction`) for asking before overwriting when the copied file already exists in the destination.

```
$ cp -i /etc/hosts .
cp: overwrite ‘./hosts’?
```

## `cat`

Read a file

```
$ cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
``` 

## `mv` move

- Move a file to another directory
- Rename a file by moving it to the same directory with a new name

Example: rename `lipc.md` to `lpic2.md`

```
$ ls
lpic1.md
$ mv lpic1.md lpic2.md
$ ls
lpic2.md
```

### `rm` remove

Remove files

### `mkdir` make directory

Create a directory named `test`

```
$ mkdir test
$ ls -F
lpic2.md  test/
```

Create nested directory (parent and child directories)

```
$ mkdir -p test001/test002/test003
$ ls -R .
.:
test001

./test001:
test002

./test001/test002:
test003

./test001/test002/test003:
```

## `rmdir` remove directory

Example: remove directory `test003` inside `test001/test002/`

```
$ rmdir test001/test002/test003/
$ ls -R
.:
test001

./test001:
test002

./test001/test002:
```




