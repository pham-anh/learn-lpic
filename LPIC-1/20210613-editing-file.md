---
title: Editing files
date: 2021-06-13
tags:
- sed
categories:
- lpic1
---

## `sed` with `/d`: delete matches

```
$ sudo sed '/^#/d;/^$/d' snmpd.conf 
com2sec notConfigUser  default       public
group   notConfigGroup v1           notConfigUser
group   notConfigGroup v2c           notConfigUser
view    systemview    included   .1.3.6.1.2.1.1
view    systemview    included   .1.3.6.1.2.1.25.1.1
access  notConfigGroup ""      any       noauth    exact  systemview none none
syslocation Unknown (edit /etc/snmp/snmpd.conf)
syscontact Root <root@localhost> (configure /etc/snmp/snmp.local.conf)
dontLogTCPWrappersConnects yes
```

- `''`: place the regular expression inside
- `/`: begin a regular expression
- `^#`: regular expression content. `^#` means lines beginning with `#`
- `/d`: means delete

→ all of this means: delete the lines beginning with `#`

- `;`: separate another regular expression
- `/`: begin a regular expression
- `^$`: regular expression content. `^$` means lines beginning with nothing and ending with nothing, it is an empty line.
- `/d`: means delete

→ all of this means: delete empty lines

After running this command, the output show the content of the file if it is edited. If we add `-i` into the `sed` command, it will actually edit the file: `sudo sed -i '/^#/d;/^$/d' snmpd.conf`
