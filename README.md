# verimg(8)

Tool for creating customized FreeBSD VM image(s) and also for unattended installation of PKGBASE based FreeBSD system.

These are the `verimg(8)` options.

```
FreeBSD # verimg --help
usage:
  verimg: [OPTION(s)]

options:
  -f FILE  which file to use for VM image (default: VERIMG)
  -s SIZE  size of VM image (default: 10g)
  -r VERS  which FreeBSD version to use (default: releng/15.0)
  -i LIST  colon (:) separated packages list to install (default: beadm:lsblk)
  -m MNTD  mount directory for installation (default: /mnt)
  -S SRCD  directory for FreeBSD source (default: /usr/src)
  -p POOL  specify ZFS pool name (default: sys)
  -b BRCH  specify branch for pkg(8) (default: latest)
  -n       display options and exit
  -t TYPE  type of operation is one of options:
           = img
             - create FILE backend and do setup there (default)
           = mnt
             - do not use FILE backend and just setup at mount dir
  -R REPO  dir where PKGBASE packages are located
           (default: /usr/obj/usr/src/repo/FreeBSD:15:amd64/latest)
  -M MODE  mode in which 'verimg' to start:
           = fetch:build:setup (default)
             - fetch FreeBSD sources with git(1) clone into /usr/src
             - build FreeBSD from sources from /usr/src in /usr/obj
             - setup FreeBSD from /usr/obj PKGBASE repository
           = build:setup
             - build FreeBSD from sources from /usr/src in /usr/obj
             - setup FreeBSD from /usr/obj PKGBASE repository
           = setup
             - setup FreeBSD from /usr/obj PKGBASE repository

examples:
  # verimg.sh -f FILE -s 20g -r releng/15.0 -i python:ansible
```

Steps like 'Fetch' and 'Build' are optional.

You can even use this tool for unattended automated FreeBSD installation on bare metal ... or a laptop.

By default `verimg(8)` fetches the FreeBSD sources ... builds `world`/`kernel` and then PKGBASE packages ... and installs new FreeBSD from local PKGBASE repo in <tt><b>VERIMG</b></tt> file ... but you can easily overwrite these with options ... and check what will be done with dry run `-n` option too.

Here are the defaults printed.

```
FreeBSD # verimg -n
INFO: options that will be used
  ARG_MODE: fetch:build:setup
  ARG_TYPE: img
  ARG_FILE: VERIMG
  ARG_SIZE: 10g
  ARG_VERS: releng/15.0
  ARG_INST: beadm:lsblk
  ARG_MNTD: /mnt
  ARG_SRCD: /usr/src
  ARG_POOL: sys
  ARG_REPO: /usr/obj/usr/src/repo/FreeBSD:15:amd64/latest

```

Here is example `verimg(8)` run for unattended FreeBSD install in `VERIMG` file when FreeBSD sources were fetched earlier and `world`/`kernel` are already build with PKGBASE repo.

```
FreeBSD # verimg -M setup -t img
INFO: options that will be used
  ARG_MODE: setup
  ARG_TYPE: img
  ARG_FILE: VERIMG
  ARG_SIZE: 10g
  ARG_VERS: releng/15.0
  ARG_INST: beadm:lsblk
  ARG_MNTD: /mnt
  ARG_SRCD: /usr/src
  ARG_POOL: sys
  ARG_REPO: /usr/obj/usr/src/repo/FreeBSD:15:amd64/latest

```

Have fun.

