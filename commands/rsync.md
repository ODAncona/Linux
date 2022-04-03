---
description: a fast, versatile, remote file-copying tool
---

# rsync

## Introduction

Rsync is a fast and extraordinarily versatile file copying tool. It can copy locally, to/from another host over any remote shell, or to/from a remote rsync daemon. It offers a large number of op‐ tions that control every aspect of its behavior and permit very flexible specification of the set of files to be copied. It is famous for its delta-transfer algorithm, which reduces the amount of data sent over the network by sending only the differences between the source files and the existing files in the destination. Rsync is widely used for backups and mirroring and as an improved copy command for everyday use.\


Rsync finds files that need to be transferred using a "quick check" algorithm (by default) that looks for files that have changed in size or in last-modified time. Any changes in the other pre‐ served attributes (as requested by options) are made on the destination file directly when the quick check indicates that the file's data does not need to be updated.



Some of the additional features of rsync are:

* support for copying links, devices, owners, groups, and permissions
* exclude and exclude-from options similar to GNU tar
* a CVS exclude mode for ignoring the same files that CVS would ignore
* can use any transparent remote shell, including ssh or rsh
* can does not requrie super-user privileges
* pipelining of file transfers to minimize latency costs
* support for anonymouse or authenticated rsync daemons (ideal for mirroring)

Rsync copies files either to or from a remote host, or locally on the current host (it does not support copying files between two remote hosts).

There are two different ways for rsync to contact a remote system: using a remote-shell program as the transport (such as ssh or rsh) or contacting an rsync daemon directly via TCP. The remote- shell transport is used whenever the source or destination path contains a single colon (:) separator after a host specification. Contacting an rsync daemon directly happens when the source or des‐ tination path contains a double colon (::) separator after a host specification, OR when an rsync:// URL is specified (see also the "USING RSYNC-DAEMON FEATURES VIA A REMOTE-SHELL CONNECTION" sec‐ tion for an exception to this latter rule).

As a special case, if a single source arg is specified without a destination, the files are listed in an output format similar to `ls -l`.

As expected, if neither the source or destination path specify a remote host, the copy occurs locally (see also the `--list-only` option).

Rsync refers to the local side as the client and the remote side as the server. Don't confuse server with an rsync daemon. A daemon is always a server, but a server can be either a daemon or a re‐ mote-shell spawned process.

## Syntaxe

You use rsync in the same way you use rcp.

```bash
```

### Options

| -a | archive: recursion          |
| -- | --------------------------- |
| -v | verbose                     |
| -r | recursive                   |
| -R | relative: use relative path |

## Utilisation

### Sur la mme machine

```bash
       rsync -t *.c foo:src/
```

This would transfer all files matching the pattern _.c_ from the current directory to the directory **src** on the machine foo. If any of the files already exist on the remote system then the rsync remote-update protocol is used to update the file by sending only the differences in the data. Note that the expansion of wildcards on the command-line __ (_\*_.c) into a list of files is handled by the shell before it runs rsync and not by rsync itself (exactly the same as all other Posix-style programs).



```
       rsync -avz foo:src/bar /data/tmp
```

This would recursively transfer all files from the directory src/bar on the machine foo into the /data/tmp/bar directory on the local machine. The files are transferred in archive mode, which en‐ sures that symbolic links, devices, attributes, permissions, ownerships, etc. are preserved in the transfer. Additionally, compression will be used to reduce the size of data portions of the trans‐ fer.

