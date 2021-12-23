1.1
# Homework for 6th lesson
## Task 1
#### 1.1 SSH to remotehost using username and password provided to you in Slack. Logout from remotehost. 

```
[student1@localhost hw5]$ ssh Dmitrii_Iaborov@18.221.144.175
The authenticity of host '18.221.144.175 (18.221.144.175)' can't be established.
ECDSA key fingerprint is SHA256:Lqk214fPCrlvcsnoj1NGVS+Puxr7lGuEncIdALeLt78.
ECDSA key fingerprint is MD5:01:a1:c8:32:41:5c:9b:4b:0a:cc:f0:4b:7e:66:2b:38.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '18.221.144.175' (ECDSA) to the list of known hosts.
Dmitrii_Iaborov@18.221.144.175's password:

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
No packages needed for security; 4 packages available
Run "sudo yum update" to apply all updates.
[Dmitrii_Iaborov@ip-172-31-33-155 ~]$ logout
Connection to 18.221.144.175 closed.
```

#### 1.2 Generate new SSH key-pair on your localhost with name "hw-5"

```
[student1@localhost ~]$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/student1/.ssh/id_rsa): /home/student1/.ssh/hw-5
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/student1/.ssh/hw-5.
Your public key has been saved in /home/student1/.ssh/hw-5.pub.
The key fingerprint is:
SHA256:... student1@localhost.localdomain
The key's randomart image is:
+---[RSA 2048]----+
|                 |
|                 |
|     o o         |
|    o O.o        |
| o . *.+S o      |
|o . = ...+ . o o |
|. E. + + ++.= *  |
| .  . . + OBo* o.|
|       o +**+o+..|
+----[SHA256]-----+
```

#### 1.3 Set up key-based authentication, so that you can SSH to  remotehost  without password.

```
[student1@localhost .ssh]$ ssh-copy-id -i ~/.ssh/hw-5.pub Dmitrii_Iaborov@18.221.144.175
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/student1/.ssh/hw-5.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
Dmitrii_Iaborov@18.221.144.175's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'Dmitrii_Iaborov@18.221.144.175'"
and check to make sure that only the key(s) you wanted were added.
```

#### 1.4 SSH to remotehost without password. Log out from remotehost.

```
[student1@localhost .ssh]$ ssh -i ~/.ssh/hw-5 Dmitrii_Iaborov@18.221.144.175
Last login: Wed Dec 22 17:41:23 2021 from 5.18.233.23

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
No packages needed for security; 4 packages available
Run "sudo yum update" to apply all updates.
[Dmitrii_Iaborov@ip-172-31-33-155 ~]$ logout
Connection to 18.221.144.175 closed.
```

#### 1.5 Create SSH config file, so that you can SSH to remotehost simply running `sshremotehost` command. As a result, provide output of command `cat ~/.ssh/config`.

```
[student1@localhost .ssh]$ cat config
Host remotehost
HostName 18.221.144.175
User Dmitrii_Iaborov
IdentityFile ~/.ssh/hw-5
[student1@localhost .ssh]$ chmod 600 config
[student1@localhost .ssh]$ ssh remotehost
Last login: Wed Dec 22 18:20:43 2021 from 5.18.233.23

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
No packages needed for security; 4 packages available
Run "sudo yum update" to apply all updates.
```

#### 1.6 Using command line utility (curl or telnet) verify that there are some webserver running on port 80 of webserver. Log out from remotehost.

```
[Dmitrii_Iaborov@ip-172-31-33-155 ~]$ curl 172.31.45.237:80
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd"><html><head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
                <title>Apache HTTP Server Test Page powered by CentOS</title>
                <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

    <!-- Bootstrap -->
    <link href="/noindex/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="noindex/css/open-sans.css" type="text/css" />

<style type="text/css"><!--

body {
  font-family: "Open Sans", Helvetica, sans-serif;
  font-weight: 100;
  color: #ccc;
  background: rgba(10, 24, 55, 1);
  font-size: 16px;
}

h2, h3, h4 {
  font-weight: 200;
}

h2 {
  font-size: 28px;
}

.jumbotron {
  margin-bottom: 0;
  color: #333;
  background: rgb(212,212,221); /* Old browsers */
  background: radial-gradient(ellipse at center top, rgba(255,255,255,1) 0%,rgba(174,174,183,1) 100%); /* W3C */
}

.jumbotron h1 {
  font-size: 128px;
  font-weight: 700;
  color: white;
  text-shadow: 0px 2px 0px #abc,
               0px 4px 10px rgba(0,0,0,0.15),
               0px 5px 2px rgba(0,0,0,0.1),
               0px 6px 30px rgba(0,0,0,0.1);
}

.jumbotron p {
  font-size: 28px;
  font-weight: 100;
}

.main {
   background: white;
   color: #234;
   border-top: 1px solid rgba(0,0,0,0.12);
   padding-top: 30px;
   padding-bottom: 40px;
}

.footer {
   border-top: 1px solid rgba(255,255,255,0.2);
   padding-top: 30px;
}

    --></style>
</head>
<body>
  <div class="jumbotron text-center">
    <div class="container">
          <h1>Hello!</h1>
                <p class="lead">You are here because you're probably a DevOps courses member. In that case you should open <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"> THIS LINK </a></p>
                </div>
  </div>
</body></html>
```

#### 1.7 Using SSH setup port forwarding, so that you can reach  webserver from your localhost (choose any free local port you like).

```
[student1@localhost .ssh]$ ssh -fNL 8080:172.31.45.237:80 remotehost
```

#### 1.8 Like in 1.6, but on localhost using command line utility verify that localhost and port you have specified act like webserver, returning same result as in 1.6

```
[student1@localhost .ssh]$ curl -l localhost:8080
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd"><html><head>
<meta http-equiv="content-type" content="text/html; charset=UTF-8">
                <title>Apache HTTP Server Test Page powered by CentOS</title>
                <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">

    <!-- Bootstrap -->
    <link href="/noindex/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="noindex/css/open-sans.css" type="text/css" />

<style type="text/css"><!--

body {
  font-family: "Open Sans", Helvetica, sans-serif;
  font-weight: 100;
  color: #ccc;
  background: rgba(10, 24, 55, 1);
  font-size: 16px;
}

h2, h3, h4 {
  font-weight: 200;
}

h2 {
  font-size: 28px;
}

.jumbotron {
  margin-bottom: 0;
  color: #333;
  background: rgb(212,212,221); /* Old browsers */
  background: radial-gradient(ellipse at center top, rgba(255,255,255,1) 0%,rgba(174,174,183,1) 100%); /* W3C */
}

.jumbotron h1 {
  font-size: 128px;
  font-weight: 700;
  color: white;
  text-shadow: 0px 2px 0px #abc,
               0px 4px 10px rgba(0,0,0,0.15),
               0px 5px 2px rgba(0,0,0,0.1),
               0px 6px 30px rgba(0,0,0,0.1);
}

.jumbotron p {
  font-size: 28px;
  font-weight: 100;
}

.main {
   background: white;
   color: #234;
   border-top: 1px solid rgba(0,0,0,0.12);
   padding-top: 30px;
   padding-bottom: 40px;
}

.footer {
   border-top: 1px solid rgba(255,255,255,0.2);
   padding-top: 30px;
}

    --></style>
</head>
<body>
  <div class="jumbotron text-center">
    <div class="container">
          <h1>Hello!</h1>
                <p class="lead">You are here because you're probably a DevOps courses member. In that case you should open <a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"> THIS LINK </a></p>
                </div>
  </div>
</body></html>
```
---

## Task 2
#### 2.1 Imagine your localhost has been relocated to Havana. Change the time zone on the localhost to Havana and verify the time zone has been changed properly (may be multiple commands). 

```
[student1@localhost ~]$ timedatectl set-timezone America/Havana
==== AUTHENTICATING FOR org.freedesktop.timedate1.set-timezone ===
Authentication is required to set the system timezone.
Authenticating as: student1
Password:
==== AUTHENTICATION COMPLETE ===
[student1@localhost ~]$ timedatectl
timedatectl
      Local time: Wed 2021-12-22 13:45:04 CST
  Universal time: Wed 2021-12-22 18:45:04 UTC
        RTC time: Wed 2021-12-22 04:53:18
       Time zone: America/Havana (CST, -0500)
...
```

#### 2.2 Find all systemd journal messages on localhost, that were recorded in the last 50 minutes and originate from a system service started with user id 81 (single command).

```
[student1@localhost ~]$ journalctl --since "50 min ago" _UID=81
-- Logs begin at Sat 2021-12-18 22:12:47 CST, end at Wed 2021-12-22 13:44:53 CST. --
Dec 22 13:44:37 localhost.localdomain dbus[647]: [system] Activating via systemd: service name='org.freedesktop.timedate1' unit='dbus-org.freed
Dec 22 13:44:37 localhost.localdomain dbus[647]: [system] Successfully activated service 'org.freedesktop.timedate1'
```

#### 2.3 Configure  rsyslogd  by adding  a  rule  to  the  newly created  configuration   file /etc/rsyslog.d/auth-errors.conf to log all security and authentication messages with the priority alert and higher to the  /var/log/auth-errors file. Test the newly added log directive with the logger command (multiple commands).

```
[student1@localhost ~]$ sudo cat /etc/rsyslog.d/auth-errors.conf
[sudo] password for student1:
#rules for logging

auth.alert;security.alert       /var/log/auth-errors.log
[student1@localhost ~]$ sudo systemctl restart rsyslog
[student1@localhost ~]$ logger -p auth.alert "The alert-test"
[student1@localhost ~]$ logger -p auth.crit "The crit-test"
[student1@localhost ~]$ logger -p auth.emerg "The emerg-test"

Broadcast message from systemd-journald@localhost.localdomain (Wed 2021-12-22 14:26:27 CST):

student1[4133]: The emerg-test

[student1@localhost ~]$
Message from syslogd@localhost at Dec 22 14:26:27 ...
 student1:The emerg-test

[student1@localhost ~]$ logger -p security.alert "The alert-test2"
[student1@localhost ~]$ logger -p security.crit "The crit-test2"
[student1@localhost ~]$ logger -p security.emerg "The emerg-test2"

Broadcast message from systemd-journald@localhost.localdomain (Wed 2021-12-22 14:28:00 CST):

student1[4136]: The emerg-test2

[student1@localhost ~]$
Message from syslogd@localhost at Dec 22 14:28:00 ...
 student1:The emerg-test2

[student1@localhost ~]$ sudo tail /var/log/auth-errors.log
Dec 22 14:26:07 localhost student1: The alert-test
Dec 22 14:26:27 localhost student1: The emerg-test
Dec 22 14:27:15 localhost student1: The alert-test2
Dec 22 14:28:00 localhost student1: The emerg-test2

```
