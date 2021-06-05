# Some basic commands

## `tty`

Show terminal that we are connecting to

```shell
$ tty
/dev/ttys002
```

## `ls -l $(tty)`

```shell
$ ls -l $(tty)
crw--w----  1 quynhanhpham  tty   16,   3 Jun  5 05:54 /dev/ttys003
```

Run `tty`, then pass the result of `tty` into `ls -l`.
It is the same as these 2 command line

```shell
$ tty
/dev/ttys002
$ ls -l /dev/ttys002
crw--w----  1 quynhanhpham  tty   16,   2 Jun  5 05:44 /dev/ttys002
```

# Ctrl + L

Clear the screen. Same as `clear` but more convenient.

# `yum whoprovides <command name>`

Check which package provide a command

```shell
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

# `yum install <package name>`

Install a package.
Here `sudo` is needed becaused the current user don't have enough permission for package installation.

```shell
$ sudo yum install redhat-lsb
...

Total download size: 66 M
Installed size: 181 M
Is this ok [y/d/N]: y      # ↩︎ input an "y" here

Complete!
```

# `lsblk`

List block devices of the system.

Block devices are disks and partitions.

```shell
$ lsblk
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0   20G  0 disk 
├─sda1   8:1    0  200M  0 part /boot/efi
└─sda2   8:2    0 19.8G  0 part /
```

Here we have:

- `sda`: disk
- `sda1`, `sda2`: partitions

## Wildcard and Regular expression

### *

`*` means matching 0 or any character. So in the following command line, we can list and file name beginning with `/dev/sda`.

```shell
$ ls -la /dev/sda*
brw-rw----. 1 root disk 8, 0 Jun  4 21:01 /dev/sda
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```

### ?

`?` means matching any single character. So in the following command, we can list any file name that have at least 1 character following `/dev/sda`.

```shell
$ ls -la /dev/sda?
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```

We no longer see `/dev/dsa` in the list because it has no character following `/dev/sda`.

### [12]

`[<a group of characters>]` means matching any character in the group. So in the following command, we can list any file name that have `1` or `2` following `/dev/sda`.

```shell
$ ls -la /dev/sda[12]
brw-rw----. 1 root disk 8, 1 Jun  4 21:01 /dev/sda1
brw-rw----. 1 root disk 8, 2 Jun  4 21:01 /dev/sda2
```














