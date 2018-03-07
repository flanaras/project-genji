# SystemTap

## Requirements

Was *not* able to successfully make it work on:
os:
```
⋊> philip tomat ~ cat /etc/os-release                                                                                                                                                                                                  11:48:36
NAME="openSUSE Tumbleweed"
# VERSION="20180305"
ID=opensuse
ID_LIKE="suse"
VERSION_ID="20180305"
PRETTY_NAME="openSUSE Tumbleweed"
ANSI_COLOR="0;32"
CPE_NAME="cpe:/o:opensuse:tumbleweed:20180305"
BUG_REPORT_URL="https://bugs.opensuse.org"
HOME_URL="https://www.opensuse.org/"
```
```
⋊> philip tomat ~ uname -rm                                                                                                                                                                                                            11:48:38
4.15.7-1-default x86_64
```
stap:
```
⋊> philip tomat ~ stap -V                                                                                                                                                                                                              11:48:48
Systemtap translator/driver (version 3.2/0.168, non-git sources)
Copyright (C) 2005-2017 Red Hat, Inc. and others
This is free software; see the source for copying conditions.
tested kernel versions: 2.6.18 ... 4.11
enabled features: LIBSQLITE3 NLS NSS
```

The requirements on rpm based system (openSUSE Leap 42.2):


* systemtap
* kernel-default-debuginfo
* kernel-default-debugsource


## Hello world

To see that everything is configured properly run
```
 sudo stap -v -e 'probe vfs.read {printf("read performed\n"); exit()}' 
```
