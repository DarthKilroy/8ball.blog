---
title: Commands on Linux (Part 1)
date: 2025-08-01
layout: post
tags: linux, ubuntu, debian, tech-support, command-line
catagories: Command_Line Tips

---

If you are in tech support, you really can't escape the command line, it makes everything so much easier. We are going to dive into a lot of them, explore what they do and look at a example of each command ran from my Server (Running Ubuntu 24 SE) 


In this first post here, we are going to go over the very basics of command line:


## 1. `ls` - List - [man page](https://linux.die.net/man/1/ls)
```
nsturtz@bigbox:/$ ls
bin                boot   data   dev  home  lib64              lost+found  mnt  proc  run   sbin.usr-is-merged  snap  swap.img  tmp  var
bin.usr-is-merged  cdrom  debug  etc  lib   lib.usr-is-merged  media       opt  root  sbin  scripts             srv   sys       usr
nsturtz@bigbox:/$ 
```
This is one of the most common Linux Commands, it just lists the current files in the directory (folder) you are in. 
I very commonly add `-osh` at the end, and it turns it into this:
```
nsturtz@bigbox:/$ ls -osh 
total 8.1G
   0 lrwxrwxrwx    1 root        7 Apr 22  2024 bin -> usr/bin
4.0K drwxr-xr-x    2 root     4.0K Feb 26  2024 bin.usr-is-merged
4.0K drwxr-xr-x    4 root     4.0K Jul 30 06:29 boot
4.0K dr-xr-xr-x    2 root     4.0K Feb 16 16:49 cdrom
4.0K drwxrwxrwx    7 jellyfin 4.0K Jul 24 12:05 data
4.0K -rw-r-----    1 root      620 May 27 10:55 debug
   0 drwxr-xr-x   19 root     4.2K Jul 31 14:52 dev
 12K drwxr-xr-x  141 root      12K Jul 30 06:27 etc
4.0K drwxr-xr-x    4 root     4.0K Jul 23 22:47 home
   0 lrwxrwxrwx    1 root        7 Apr 22  2024 lib -> usr/lib
   0 lrwxrwxrwx    1 root        9 Apr 22  2024 lib64 -> usr/lib64
4.0K drwxr-xr-x    2 root     4.0K Feb 26  2024 lib.usr-is-merged
 16K drwx------    2 root      16K May 26 21:07 lost+found
4.0K drwxr-xr-x    3 root     4.0K May 27 17:54 media
4.0K drwxr-xr-x    2 root     4.0K Feb 16 14:51 mnt
4.0K drwxr-xr-x    4 root     4.0K Jun 13 22:21 opt
   0 dr-xr-xr-x 1112 root        0 Jul 31 14:52 proc
4.0K drwx------   22 root     4.0K Aug  1 00:23 root
   0 drwxr-xr-x   42 root     1.3K Aug  1 09:09 run
   0 lrwxrwxrwx    1 root        8 Apr 22  2024 sbin -> usr/sbin
4.0K drwxr-xr-x    2 root     4.0K Aug 22  2024 sbin.usr-is-merged
4.0K drwxr-xr-x    2 root     4.0K Jun 29 15:53 scripts
4.0K drwxr-xr-x    6 root     4.0K May 26 21:20 snap
4.0K drwxr-xr-x    4 root     4.0K Jul 21 20:07 srv
8.1G -rw-------    1 root     8.0G May 26 21:08 swap.img
   0 dr-xr-xr-x   13 root        0 Aug  1 09:11 sys
4.0K drwxrwxrwt   17 root     4.0K Aug  1 09:14 tmp
4.0K drwxr-xr-x   12 root     4.0K Feb 16 14:51 usr
4.0K drwxr-xr-x   14 root     4.0K Jun 13 22:42 var
nsturtz@bigbox:/$ 
```
this shows the Permissions in RWX format (`drwxrwxrwx`) - who owns it `jellyfin` -  the size (in human readable format (`-h`)  date and time created/lasted modified  and the name.

## 2. `cd` - Change Directory 
```
nsturtz@bigbox:/$ ls 
bin                boot   data   dev  home  lib64              lost+found  mnt  proc  run   sbin.usr-is-merged  snap  swap.img  tmp  var
bin.usr-is-merged  cdrom  debug  etc  lib   lib.usr-is-merged  media       opt  root  sbin  scripts             srv   sys       usr
nsturtz@bigbox:/$ cd opt
nsturtz@bigbox:/opt$ ls
containerd  NPM
nsturtz@bigbox:/opt$ 
```
This is also a extremely common linux command, you need to use it to move around directories. 

- Tip: If you just type `cd` you will be taken back to your home directory 

```
nsturtz@bigbox ~/e/1/2/3/4> pwd 
/home/nsturtz/example/1/2/3/4
nsturtz@bigbox ~/e/1/2/3/4> cd 
nsturtz@bigbox ~> pwd
/home/nsturtz
nsturtz@bigbox ~> 
```

## 3. `pwd` - Print Working Directory -[man page](https://linux.die.net/man/1/pwd)
```
nsturtz@bigbox /o/N/d/n/proxy_host> pwd
/opt/NPM/data/nginx/proxy_host
nsturtz@bigbox /o/N/d/n/proxy_host> 
```
This command is very often used after `cd`  to see what directory you are in.
## 4. `mkdir` - Make Directory - [man page](https://linux.die.net/man/1/mkdir)
```
nsturtz@bigbox ~/example> ls
nsturtz@bigbox ~/example> mkdir 1
nsturtz@bigbox ~/example> ls
1/
nsturtz@bigbox ~/example> cd 1
nsturtz@bigbox ~/e/1> pwd
/home/nsturtz/example/1
nsturtz@bigbox ~/e/1> 
```
This simply creates a folder (directory). 
I quite often use the `-p` flag on it so it will create folders sub-folders that are not there but needed. 
```
nsturtz@bigbox ~/example> pwd 
/home/nsturtz/example
nsturtz@bigbox ~/example> ls 
nsturtz@bigbox ~/example> mkdir 1/2/3/4
mkdir: cannot create directory ‘1/2/3/4’: No such file or directory
nsturtz@bigbox ~/example [1]> mkdir -p 1/2/3/4
nsturtz@bigbox ~/example> ls
1/
nsturtz@bigbox ~/example> ls -R 
.:
1/

./1:
2/

./1/2:
3/

./1/2/3:
4/

./1/2/3/4:
nsturtz@bigbox ~/example> cd 1/2/3/4/
nsturtz@bigbox ~/e/1/2/3/4> pwd
/home/nsturtz/example/1/2/3/4
nsturtz@bigbox ~/e/1/2/3/4> 
```