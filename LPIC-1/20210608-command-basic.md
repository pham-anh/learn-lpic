---
title: Some basic commands
date: 2021-06-08
tags:
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

## `pwd`

Print working directory

```
$ cd /usr/bin/
$ pwd
/usr/bin
```

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

Copy a whole directory: `cp -R`

```
$ mkdir file001
$ touch file001/content00{1..5}
$ ls file001/ -F
content001  content002  content003  content004  content005
$ cp -R file001/ file002
$ ls file002/
content001  content002  content003  content004  content005
# check the 2 directory using `tree` command
$ tree
.
├── file001
│   ├── content001
│   ├── content002
│   ├── content003
│   ├── content004
│   └── content005
└── file002
    ├── content001
    ├── content002
    ├── content003
    ├── content004
    └── content005
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

Example: rename `lpic1.md` to `lpic2.md`

```
$ ls
lpic1.md
$ mv lpic1.md lpic2.md
$ ls
lpic2.md
```

## `rm` remove

Remove a file

```
$ touch hello.txt
$ ls hello.txt 
hello.txt
$ rm hello.txt 
$ !ls # run last command that begins with `ls`
ls hello.txt 
ls: cannot access hello.txt: No such file or directory
```

Force delete (`-f`) a directory and its content (`-r`). 

- Note: need to **double careful** if running as root be cause it will delete everything.

```
# create some nested directories
$ mkdir -p do/did/done
# create a file inside it
$ touch do/did/done/well.txt
# delete whole directory and its content
$ rm -rf do/
```

## `mkdir` make directory

Create a directory named `test`

```
$ mkdir test
$ ls -F
lpic2.md  test/
```

Create 2 directories at the same level

```
$ mkdir hello world
$ ls
hello  world
$ ls -F
hello/  world/
```

`-p`: Create nested directory (parent and child directories)

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

Create `dir1`, `dir2`, `dir3`, `dirn`: `mkdir dir{1..3}`

```
$ mkdir dir{1..3}
$ ls -F
dir1/  dir2/  dir3/
```

`-m`: Specify permission when creating a directory

``` 
$ mkdir -m 777 d1
$ ls -l
total 0
drwxrwxrwx. 2 pqa pqa 6 Jun 12 03:04 d1
```

## `rmdir` remove empty directory

This command only removes directories that have nothing inside.

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

Cannot use this command to remove `test001` because it contains `test002` inside

```
$ rmdir test001/
rmdir: failed to remove ‘test001/’: Directory not empty
```

Alternatively, we can remove both `test0002`, then `test001`
```
$ rmdir test001/test002 test001
```

## `!` run last command

Example: run last command that begin with `r`

```
$ mkdir -p do/did/done
$ ls -R .
.:
do

./do:
did

./do/did:
done

./do/did/done:
$ rmdir do/did/
rmdir: failed to remove ‘do/did/’: Directory not empty
$ !r
rmdir do/did/
rmdir: failed to remove ‘do/did/’: Directory not empty
```

`!$`: capture the last argument

```
$ ls /etc/hosts
/etc/hosts
$ echo !$
echo /etc/hosts
/etc/hosts
```

## Make file with some content

Example, create `hw.txt` with the content `hello world`

```
$ echo hello world > hw.txt
$ cat hw.txt 
hello world
```

## `du` disk usage

See disk usage of `/etc` with number in human-readable form and depth = 0 (mean only show the directory itself)

```
$ sudo du -h /etc/ -d 0
36M     /etc/
```