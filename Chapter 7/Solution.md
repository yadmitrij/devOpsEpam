# Homework for lections 13-14

## Task 1. Repositories and Packages.

#### 1.1 Download sysstat package.

```
[student1@localhost ~]$ wget http://mirror.centos.org/centos/7/os/x86_64/Packages/sysstat-10.1.5-19.el7.x86_64.rpm
--2021-12-23 12:05:52--  http://mirror.centos.org/centos/7/os/x86_64/Packages/sysstat-10.1.5-19.el7.x86_64.rpm
Resolving mirror.centos.org (mirror.centos.org)... 141.105.67.224, 2001:4de0:aaae::194
Connecting to mirror.centos.org (mirror.centos.org)|141.105.67.224|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 323020 (315K) [application/x-rpm]
Saving to: ‘sysstat-10.1.5-19.el7.x86_64.rpm’

100%[=====================================================================================================>] 323,020     --.-K/s   in 0.1s

2021-12-23 12:05:52 (3.09 MB/s) - ‘sysstat-10.1.5-19.el7.x86_64.rpm’ saved [323020/323020]
```

#### 1.2 Get information from downloaded sysstat package file.

```
[student1@localhost ~]$ rpm -qip sysstat-10.1.5-19.el7.x86_64.rpm
Name        : sysstat
Version     : 10.1.5
Release     : 19.el7
Architecture: x86_64
Install Date: (not installed)
Group       : Applications/System
Size        : 1172488
License     : GPLv2+
Signature   : RSA/SHA256, Fri 03 Apr 2020 05:08:48 PM CDT, Key ID 24c6a8a7f4a80eb5
Source RPM  : sysstat-10.1.5-19.el7.src.rpm
Build Date  : Wed 01 Apr 2020 12:36:37 AM CDT
Build Host  : x86-01.bsys.centos.org
Relocations : (not relocatable)
Packager    : CentOS BuildSystem <http://bugs.centos.org>
Vendor      : CentOS
URL         : http://sebastien.godard.pagesperso-orange.fr/
Summary     : Collection of performance monitoring tools for Linux
Description :
The sysstat package contains sar, sadf, mpstat, iostat, pidstat, nfsiostat-sysstat,
tapestat, cifsiostat and sa tools for Linux.
The sar command collects and reports system activity information. This
information can be saved in a file in a binary format for future inspection. The
statistics reported by sar concern I/O transfer rates, paging activity,
process-related activities, interrupts, network activity, memory and swap space
utilization, CPU utilization, kernel activities and TTY statistics, among
others. Both UP and SMP machines are fully supported.
The sadf command may be used to display data collected by sar in various formats
(CSV, XML, etc.).
The iostat command reports CPU utilization and I/O statistics for disks.
The tapestat command reports statistics for tapes connected to the system.
The mpstat command reports global and per-processor statistics.
The pidstat command reports statistics for Linux tasks (processes).
The nfsiostat-sysstat command reports I/O statistics for network file systems.
The cifsiostat command reports I/O statistics for CIFS file systems.
```



#### 1.3 Install sysstat package and get information about files installed by this package.

```
[student1@localhost ~]$ sudo rpm -ivh sysstat-10.1.5-19.el7.x86_64.rpm --nodeps
Preparing...                          ################################# [100%]
Updating / installing...
   1:sysstat-10.1.5-19.el7            ################################# [100%]
[student1@localhost ~]$ sudo rpm -ql sysstat
/etc/cron.d/sysstat
/etc/sysconfig/sysstat
/etc/sysconfig/sysstat.ioconf
/usr/bin/cifsiostat
/usr/bin/iostat
/usr/bin/mpstat
/usr/bin/nfsiostat-sysstat
/usr/bin/pidstat
/usr/bin/sadf
/usr/bin/sar
/usr/bin/tapestat
/usr/lib/systemd/system/sysstat.service
/usr/lib64/sa
/usr/lib64/sa/sa1
/usr/lib64/sa/sa2
/usr/lib64/sa/sadc
/usr/share/doc/sysstat-10.1.5
/usr/share/doc/sysstat-10.1.5/CHANGES
/usr/share/doc/sysstat-10.1.5/COPYING
/usr/share/doc/sysstat-10.1.5/CREDITS
/usr/share/doc/sysstat-10.1.5/FAQ
/usr/share/doc/sysstat-10.1.5/README
/usr/share/doc/sysstat-10.1.5/sysstat-10.1.5.lsm
/usr/share/locale/af/LC_MESSAGES/sysstat.mo
/usr/share/locale/cs/LC_MESSAGES/sysstat.mo
/usr/share/locale/da/LC_MESSAGES/sysstat.mo
/usr/share/locale/de/LC_MESSAGES/sysstat.mo
/usr/share/locale/eo/LC_MESSAGES/sysstat.mo
/usr/share/locale/es/LC_MESSAGES/sysstat.mo
/usr/share/locale/eu/LC_MESSAGES/sysstat.mo
/usr/share/locale/fi/LC_MESSAGES/sysstat.mo
/usr/share/locale/fr/LC_MESSAGES/sysstat.mo
/usr/share/locale/hr/LC_MESSAGES/sysstat.mo
/usr/share/locale/id/LC_MESSAGES/sysstat.mo
/usr/share/locale/it/LC_MESSAGES/sysstat.mo
/usr/share/locale/ja/LC_MESSAGES/sysstat.mo
/usr/share/locale/ky/LC_MESSAGES/sysstat.mo
/usr/share/locale/lv/LC_MESSAGES/sysstat.mo
/usr/share/locale/mt/LC_MESSAGES/sysstat.mo
/usr/share/locale/nb/LC_MESSAGES/sysstat.mo
/usr/share/locale/nl/LC_MESSAGES/sysstat.mo
/usr/share/locale/nn/LC_MESSAGES/sysstat.mo
/usr/share/locale/pl/LC_MESSAGES/sysstat.mo
/usr/share/locale/pt/LC_MESSAGES/sysstat.mo
/usr/share/locale/pt_BR/LC_MESSAGES/sysstat.mo
/usr/share/locale/ro/LC_MESSAGES/sysstat.mo
/usr/share/locale/ru/LC_MESSAGES/sysstat.mo
/usr/share/locale/sk/LC_MESSAGES/sysstat.mo
/usr/share/locale/sr/LC_MESSAGES/sysstat.mo
/usr/share/locale/sv/LC_MESSAGES/sysstat.mo
/usr/share/locale/uk/LC_MESSAGES/sysstat.mo
/usr/share/locale/vi/LC_MESSAGES/sysstat.mo
/usr/share/locale/zh_CN/LC_MESSAGES/sysstat.mo
/usr/share/locale/zh_TW/LC_MESSAGES/sysstat.mo
/usr/share/man/man1/cifsiostat.1.gz
/usr/share/man/man1/iostat.1.gz
/usr/share/man/man1/mpstat.1.gz
/usr/share/man/man1/nfsiostat-sysstat.1.gz
/usr/share/man/man1/pidstat.1.gz
/usr/share/man/man1/sadf.1.gz
/usr/share/man/man1/sar.1.gz
/usr/share/man/man1/tapestat.1.gz
/usr/share/man/man5/sysstat.5.gz
/usr/share/man/man8/sa1.8.gz
/usr/share/man/man8/sa2.8.gz
/usr/share/man/man8/sadc.8.gz
/var/log/sa
```
---

## Task 2. Add NGINX repository and complete the following tasks using yum.

#### 2.1 Check if NGINX repository enabled or not.

```
[student1@localhost ~]$ yum repolist enabled |grep nginx
nginx-stable/7/x86_64   nginx stable repo                                    256
```

#### 2.2 Install NGINX.

```
[student1@localhost ~]$ sudo yum install nginx
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.awanti.com
 * epel: ftp.lysator.liu.se
 * extras: mirror.awanti.com
 ...
```

#### 2.3 Check yum history and undo NGINX installation.

```
[student1@localhost ~]$ sudo yum history
Loaded plugins: fastestmirror
ID     | Login user               | Date and time    | Action(s)      | Altered
-------------------------------------------------------------------------------
     7 | student1 <student1>      | 2021-12-23 12:27 | Install        |    1 E<
     6 | student1 <student1>      | 2021-12-18 08:21 | Install        |    1 >
     5 | student1 <student1>      | 2021-12-09 19:30 | Install        |    1
     4 | student1 <student1>      | 2021-12-07 17:13 | Install        |   10
     3 | student1 <student1>      | 2021-12-07 17:10 | Install        |    1
     2 | student1 <student1>      | 2021-12-07 14:44 | Install        |    1
     1 | System <unset>           | 2021-11-27 10:04 | Install        |  301
history list
[student1@localhost ~]$ sudo yum history undo 7
Loaded plugins: fastestmirror
Undoing transaction 7, from Thu Dec 23 12:27:06 2021
    Install nginx-1:1.20.2-1.el7.ngx.x86_64 @nginx-stable
...
```

#### 2.4 Disable NGINX repository.

```
[student1@localhost ~]$ sudo yum update --disablerepo=nginx-/*
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.awanti.com
 * epel: ftp.lysator.liu.se
 * extras: mirror.awanti.com
 * updates: mirror.awanti.com
Resolving Dependencies
...
```

#### 2.5 Remove sysstat package installed in the first task.

```
[student1@localhost ~]$ sudo yum remove sysstat
[sudo] password for student1:
Loaded plugins: fastestmirror
Resolving Dependencies
--> Running transaction check
---> Package sysstat.x86_64 0:10.1.5-19.el7 will be erased
--> Finished Dependency Resolution
```

#### 2.6 Install EPEL repository and get information about it.

```
[student1@localhost ~]$ sudo yum install epel-release
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.awanti.com
 * epel: ftp.lysator.liu.se
 * extras: mirror.awanti.com
 * updates: mirror.awanti.com
Package epel-release-7-14.noarch already installed and latest version.
...
[student1@localhost ~]$ yum repoinfo epel
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.awanti.com
 * epel: ftp.lysator.liu.se
 * extras: mirror.sale-dedic.com
 * updates: mirror.sale-dedic.com
Repo-id      : epel/x86_64
Repo-name    : Extra Packages for Enterprise Linux 7 - x86_64
Repo-status  : enabled
Repo-revision: 1640393346
Repo-updated : Fri Dec 24 19:56:38 2021
Repo-pkgs    : 13,703
Repo-size    : 16 G
Repo-metalink: https://mirrors.fedoraproject.org/metalink?repo=epel-7&arch=x86_64&infra=stock&content=centos
  Updated    : Fri Dec 24 19:56:38 2021
Repo-baseurl : https://ftp.lysator.liu.se/pub/epel/7/x86_64/ (98 more)
Repo-expire  : 21,600 second(s) (last: Thu Dec 23 12:04:00 2021)
  Filter     : read-only:present
Repo-filename: /etc/yum.repos.d/epel.repo

repolist: 13,703
```

#### 2.7 Find how much packages provided exactly by EPEL repository.

```
[student1@localhost ~]$ yum repoinfo epel | tail -1
repolist: 13,703
```

#### 2.8 Install ncdu package from EPEL repo.

```
[student1@localhost ~]$ sudo yum repo-pkgs epel install ncdu
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirror.awanti.com
 * epel: ftp.lysator.liu.se
 * extras: mirror.awanti.com
 * updates: mirror.awanti.com
Resolving Dependencies
--> Running transaction check
---> Package ncdu.x86_64 0:1.16-1.el7 will be installed
```

---

## Task 3. Work with files

#### 2.1 Find all regular files below 100 bytes inside your home directory.

```
[student1@localhost ~]$ find ~/ -type f -size -100c
/home/student1/.bash_logout
/home/student1/.ssh/config
/home/student1/hw3t2v2
/home/student1/daemon1
/home/student1/daemon2
/home/student1/sayhi.sh
/home/student1/task3/file1
/home/student1/task3/file2
/home/student1/task3/file3
/home/student1/task3/file4
/home/student1/task3/file5
/home/student1/task3/file6
/home/student1/task3/file7
/home/student1/task3/file8
/home/student1/task3/file9
/home/student1/task3/err.log
/home/student1/dm1.sh
/home/student1/dm2.sh
/home/student1/hw5/out.txt
/home/student1/hw5/err.txt
/home/student1/Running
/home/student1/task3a/file2
/home/student1/task3a/file3
/home/student1/task3a/file4
/home/student1/task3a/file5
/home/student1/task3a/dir7/file2
/home/student1/dirPath.txt
/home/student1/err.log
/home/student1/task2.txt
/home/student1/dirPath2.txt
```

#### 3.2 Find an inode number and a hard links count for the root directory. The hard link count should be about 17. Why?

```
[student1@localhost ~]$ ls -la /
total 20
dr-xr-xr-x.  18 root root         237 Dec 14 06:59 .
dr-xr-xr-x.  18 root root         237 Dec 14 06:59 ..
lrwxrwxrwx.   1 root root           7 Nov 27 10:04 bin -> usr/bin
dr-xr-xr-x.   5 root root        4096 Dec 23 12:42 boot
drwxr-xr-x.  20 root root        3080 Dec 18 22:12 dev
drwxr-xr-x.  74 root root        8192 Dec 23 12:41 etc
drwxr-xr-x.  13 root root         169 Dec 14 19:38 home
lrwxrwxrwx.   1 root root           7 Nov 27 10:04 lib -> usr/lib
lrwxrwxrwx.   1 root root           9 Nov 27 10:04 lib64 -> usr/lib64
drwxr-xr-x.   2 root root           6 Apr 11  2018 media
drwxr-xr-x.   2 root root           6 Apr 11  2018 mnt
drwxr-xr-x.   2 root root          32 Dec 18 22:29 opt
dr-xr-xr-x. 109 root root           0 Dec 19 06:09 proc
dr-xr-x---.   3 root root         183 Dec  7 17:15 root
drwxr-xr-x.  25 root root         740 Dec 23 12:53 run
lrwxrwxrwx.   1 root root           8 Nov 27 10:04 sbin -> usr/sbin
drwxrws---+   5 root bakerstreet   79 Dec 14 20:23 share
drwxr-xr-x.   2 root root           6 Apr 11  2018 srv
dr-xr-xr-x.  13 root root           0 Dec 18 22:12 sys
drwxrwxrwt.   9 root root        4096 Dec 23 12:53 tmp
drwxr-xr-x.  13 root root         155 Nov 27 10:04 usr
drwxr-xr-x.  19 root root         267 Nov 27 10:36 var
[student1@localhost ~]$ stat /
  File: ‘/’
  Size: 237             Blocks: 0          IO Block: 4096   directory
Device: fd00h/64768d    Inode: 64          Links: 18
Access: (0555/dr-xr-xr-x)  Uid: (    0/    root)   Gid: (    0/    root)
Context: system_u:object_r:root_t:s0
Access: 2021-12-23 12:59:41.542550510 -0500
Modify: 2021-12-14 06:59:34.743381781 -0500
Change: 2021-12-14 06:59:34.743381781 -0500
```

Every directory inside has a hardlink since creation.

#### 3.3 Check what inode numbers have "/" and "/boot" directory. Why?

```
[student1@localhost ~]$ ls -ali /
total 20
      64 dr-xr-xr-x.  18 root root         237 Dec 14 06:59 .
      64 dr-xr-xr-x.  18 root root         237 Dec 14 06:59 ..
     120 lrwxrwxrwx.   1 root root           7 Nov 27 10:04 bin -> usr/bin
      64 dr-xr-xr-x.   5 root root        4096 Dec 23 12:42 boot
       3 drwxr-xr-x.  20 root root        3080 Dec 18 22:12 dev
 4194369 drwxr-xr-x.  74 root root        8192 Dec 23 12:41 etc
 8412030 drwxr-xr-x.  13 root root         169 Dec 14 19:38 home
     124 lrwxrwxrwx.   1 root root           7 Nov 27 10:04 lib -> usr/lib
      82 lrwxrwxrwx.   1 root root           9 Nov 27 10:04 lib64 -> usr/lib64
12583333 drwxr-xr-x.   2 root root           6 Apr 11  2018 media
      83 drwxr-xr-x.   2 root root           6 Apr 11  2018 mnt
 4195580 drwxr-xr-x.   2 root root          32 Dec 18 22:29 opt
       1 dr-xr-xr-x. 108 root root           0 Dec 19 06:09 proc
 8409153 dr-xr-x---.   3 root root         183 Dec  7 17:15 root
    7205 drwxr-xr-x.  25 root root         740 Dec 23 12:53 run
     125 lrwxrwxrwx.   1 root root           8 Nov 27 10:04 sbin -> usr/sbin
     995 drwxrws---+   5 root bakerstreet   79 Dec 14 20:23 share
 8412031 drwxr-xr-x.   2 root root           6 Apr 11  2018 srv
       1 dr-xr-xr-x.  13 root root           0 Dec 18 22:12 sys
 4194376 drwxrwxrwt.   9 root root        4096 Dec 23 12:53 tmp
 8411992 drwxr-xr-x.  13 root root         155 Nov 27 10:04 usr
12582977 drwxr-xr-x.  19 root root         267 Nov 27 10:36 var
[student1@localhost ~]$ ls -ali / | grep boot
      64 dr-xr-xr-x.   5 root root        4096 Dec 23 12:42 boot
      
```

Because of differen filesystems for mount.

#### 3.4 Check the root directory space usage by du command. Compare it with an information from df. If you find differences, try to find out why it happens.

```
[student1@localhost ~]$ sudo du -sh /
2.5G    /
[student1@localhost ~]$ df -h /
Filesystem               Size  Used Avail Use% Mounted on
/dev/mapper/centos-root  6.2G  2.6G  3.7G  41% /
```
The difference appearce because of methods that are used by commands du and df. "df" checks superblocks and "du" - each element.

#### 3.5 Check disk space usage of /var/log directory using ncdu

```
[student1@localhost ~]$ ncdu /var/log
--- /var/log ----------------------------------------------------------------------------------------------------------------------------------
    1.7 MiB [####################] /anaconda                                                                                                     264.0 KiB [###                 ]  messages-20211207
  256.0 KiB [###                 ]  messages-20211214
  192.0 KiB [##                  ]  messages-20211219
  128.0 KiB [#                   ]  messages-20211128
  128.0 KiB [#                   ]  secure-20211219
  128.0 KiB [#                   ]  messages
   36.0 KiB [                    ]  wtmp
   32.0 KiB [                    ]  dmesg.old
   32.0 KiB [                    ]  dmesg
   32.0 KiB [                    ]  cron
   32.0 KiB [                    ]  cron-20211214
   28.0 KiB [                    ]  cron-20211219
   20.0 KiB [                    ]  lastlog
   20.0 KiB [                    ]  secure
   20.0 KiB [                    ]  secure-20211214
   20.0 KiB [                    ] /tuned
   16.0 KiB [                    ]  boot.log-20211208
   16.0 KiB [                    ]  boot.log-20211204
 Total disk usage:   3.2 MiB  Apparent size:   3.4 MiB  Items: 65
```
