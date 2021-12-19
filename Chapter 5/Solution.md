# Homework for lections 9-10
## Task 1
### Processes

#### Run a sleep command three times at different intervals.

```
[student1@localhost ~]$ sleep 50000 &
[1] 1567
[student1@localhost ~]$ sleep 100000 &
[2] 1568
[student1@localhost ~]$ sleep 800000 &
[3] 1569
```


#### Send a SIGSTOP signal to all of them in three different ways.

```
[student1@localhost ~]$ jobs
[1]   Running                 sleep 50000 &
[2]-  Running                 sleep 100000 &
[3]+  Running                 sleep 800000 &
[student1@localhost ~]$ kill -19 %1
[student1@localhost ~]$ kill -SIGSTOP %2
[student1@localhost ~]$ kill -STOP 1569
```

#### Check their statuses with a job command

``` 
[student1@localhost ~]$ jobs
[1]   Stopped                 sleep 50000
[2]-  Stopped                 sleep 100000
[3]+  Stopped                 sleep 800000
```

#### Terminate one of them. (Any)

```
[student1@localhost ~]$ kill -TERM %1
```

#### To other send a SIGCONT in two different ways.
```
[student1@localhost ~]$ kill -SIGCONT %2
[student1@localhost ~]$ kill -18 1569
[student1@localhost ~]$ jobs
[2]-  Running                 sleep 100000 &
[3]+  Running                 sleep 800000 &
```

#### Kill one by PID and the second one by job ID

```
[student1@localhost ~]$ kill %2
[student1@localhost ~]$ kill 1569
```

---

## Task 2
### systemd

#### Write two daemons: one should do sleep 10 after a start and then do echo 1 > /tmp/homework, the second one should do echo 2 > /tmp/homework without any sleep.

```
[root@localhost system]# vi /home/student1/dm1.sh
#!/bin/bash
sleep 10
echo 1 > /tmp/homework
[root@localhost system]# vi /home/student1/dm2.sh
#!/bin/bash
echo 2 > /tmp/homework
[root@localhost system]# chmod +x /home/student1/dm1.sh
[root@localhost system]# chmod +x /home/student1/dm2.sh
[root@localhost system]# cat dm1.service
[Unit]
Description=Daemon 1

[Service]
Type=simple
ExecStart=/home/student1/dm1.sh

[Install]
WantedBy=multi-user.target

[root@localhost system]# cat dm2.service
[Unit]
Description=Daemon 2

[Service]
ExecStart=/home/student1/dm2.sh
Type=oneshot

[Install]
WantedBy=multi-user.target
```

#### Make the second depended on the first one (should start only after the first)

```
[root@localhost system]# cat dm2.service
[Unit]
Description=Daemon 2
After=dm1.service

[Service]
ExecStart=/home/student1/dm2.sh
Type=oneshot

[Install]
WantedBy=multi-user.target
```

#### Write a timer for the second one and configure it to run on 01.01.2019 at 00:00

```
[root@localhost system]# vi dm2.timer
[Unit]
Description=Timer for daemon 2

[Timer]
Unit=dm2.service
OnCalendar=2019-01-01 00:00

[Install]
WantedBy=timers.target

[root@localhost system]# cat dm2.service
[Unit]
Description=Daemon 2
After=dm1.service
Wants=dm2.timer

[Service]
ExecStart=/home/student1/dm2.sh
Type=oneshot

[Install]
WantedBy=multi-user.target
```

#### Start all daemons and timer, check their statuses, timer list and /tmp/homework

```
[root@localhost system]# systemctl start dm1.service
[root@localhost system]# systemctl status dm1.service
● dm1.service - Daemon 1
   Loaded: loaded (/etc/systemd/system/dm1.service; enabled; vendor preset: disabled)
   Active: active (running) since Sat 2021-12-18 21:58:39 EST; 2s ago
 Main PID: 2251 (dm1.sh)
   CGroup: /system.slice/dm1.service
           ├─2251 /bin/bash /home/student1/dm1.sh
           └─2252 sleep 10

Dec 18 21:58:39 localhost.localdomain systemd[1]: Started Daemon 1.
[root@localhost system]# cat /tmp/homework
1
[root@localhost system]# systemctl start dm2.service
[root@localhost system]# systemctl status dm2.service
● dm2.service - Daemon 2
   Loaded: loaded (/etc/systemd/system/dm2.service; enabled; vendor preset: disabled)
   Active: inactive (dead) since Sat 2021-12-18 21:59:47 EST; 4s ago
  Process: 2261 ExecStart=/home/student1/dm2.sh (code=exited, status=0/SUCCESS)
 Main PID: 2261 (code=exited, status=0/SUCCESS)

Dec 18 21:59:47 localhost.localdomain systemd[1]: Starting Daemon 2...
Dec 18 21:59:47 localhost.localdomain systemd[1]: Started Daemon 2.
[root@localhost system]# cat /tmp/homework
2
[root@localhost system]# systemctl start dm2.timer
[root@localhost system]# systemctl status dm2.timer
● dm2.timer - Timer for daemon2
   Loaded: loaded (/etc/systemd/system/dm2.timer; disabled; vendor preset: disabled)
   Active: active (elapsed) since Sat 2021-12-18 21:59:47 EST; 1min 8s ago

Dec 18 21:59:47 localhost.localdomain systemd[1]: Started Timer for daemon2.
```

#### Stop all daemons and timer

```
[root@localhost system]# systemctl stop dm{1,2}.service
Warning: Stopping dm2.service, but it can still be activated by:
  dm2.timer
[root@localhost system]# systemctl stop dm2.timer
[root@localhost system]# systemctl stop dm{1,2}.service
```
---

## Task 3
### cron/anacron

#### Create an anacron job which executes a script with echo Hello > /opt/hello and runs every 2 days

```
[root@localhost system]# cat /etc/anacrontab
# /etc/anacrontab: configuration file for anacron

# See anacron(8) and anacrontab(5) for details.

SHELL=/bin/sh
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
# the maximal random delay added to the base delay of the jobs
RANDOM_DELAY=45
# the jobs will be started during the following hours only
START_HOURS_RANGE=3-22

#period in days   delay in minutes   job-identifier   command
1       5       cron.daily              nice run-parts /etc/cron.daily
7       25      cron.weekly             nice run-parts /etc/cron.weekly
@monthly 45     cron.monthly            nice run-parts /etc/cron.monthly
2       0        sayhi                  /home/student1/sayhi.sh

[root@localhost system]# cat /home/student1/sayhi.sh
#!/bin/bash
echo Hello > /opt/Hello
[root@localhost system]# anacron -f 
[root@localhost system]# cat /opt/Hello
Hello
```

#### Create a cron job which executes the same command (will be better to create a script for this) and runs it in 1 minute after system boot.

```
[root@localhost system]# crontab -e
@reboot sleep 60 && /home/student1/sayhi.sh
```

#### Restart your virtual machine and check previous job proper execution

```
[root@localhost system]# cat /opt/Hello
Hello
```
---

## Task 4
### lsof

#### Run a sleep command, redirect stdout and stderr into two different files (both of them will be empty).

```
[student1@localhost hw5]$ sleep 55555555 1>out.txt 2>err.txt &
[1] 1317
```

#### Find with the lsof command which files this process uses, also find from which file it gain stdin.

```
[student1@localhost hw5]$ lsof -p 1317
COMMAND  PID     USER   FD   TYPE DEVICE  SIZE/OFF     NODE NAME
sleep   1317 student1  cwd    DIR  253,0        36  8411963 /home/student1/hw5
sleep   1317 student1  rtd    DIR  253,0       237       64 /
sleep   1317 student1  txt    REG  253,0     33128 12741841 /usr/bin/sleep
sleep   1317 student1  mem    REG  253,0 106172832 12799787 /usr/lib/locale/locale-archive
sleep   1317 student1  mem    REG  253,0   2156272    15673 /usr/lib64/libc-2.17.so
sleep   1317 student1  mem    REG  253,0    163312    15666 /usr/lib64/ld-2.17.so
sleep   1317 student1    0u   CHR  136,0       0t0        3 /dev/pts/0
sleep   1317 student1    1w   REG  253,0         0  8411964 /home/student1/hw5/out.txt
sleep   1317 student1    2w   REG  253,0         0  8411965 /home/student1/hw5/err.txt
```
It gain stdin from file /dev/pts/0 (row 259) because "u" denotes read and write access, how I understand.

### List all ESTABLISHED TCP connections ONLY with lsof

```
[student1@localhost hw5]$ sudo lsof -i | grep ESTABLISHED
sshd     1266     root    3u  IPv4  18832      0t0  TCP localhost.localdomain:ssh->gateway:60027 (ESTABLISHED)
sshd     1270 student1    3u  IPv4  18832      0t0  TCP localhost.localdomain:ssh->gateway:60027 (ESTABLISHED)
```
