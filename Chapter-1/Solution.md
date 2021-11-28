# Решение домашней работы по первому занятию
## Задание 0
#### Установить вторую ВМ, настроить на ней только внутренний сетевой интерфейс и подключиться с первой машины (без использования root). 

В ходе занятия был показан пример взаимодействия двух машин посредством сетевого моста. 
Для осуществления этого создадим 2 машины (centos1, centos2), отличающиеся наличием сетевого интерфейса у первой.
Внесем в настройки второй машины наличие сетевого моста и подключимся с первой машины.
Подключиться получается, но также появляется доступ к интернету.
Следовательно, этот вариант реализации нам не подходит. Отключим сетевой мост.

Добавим в настройках системы VM сеть *intnet*, подключим обе машины к Внутренней сети *intnet*.
Для получения IP адреса второй машины, обратимся к конфигурационному файлу интерфейса по адресу */etc/sysconfig/network-scripts/ifcfg-<имя сервиса>*.
По умолчанию IP адрес должен генерироваться автоматически посредством DHCP.
Однако, получение IP без рутовых прав невозможно. Изменим конфигурационный файл вручную для обоих машин, используя команду *nmtui*.
Пропишем для двух машин адреса *172.16.0.1* и *172.16.0.2* соответственно.
Подключение с первой машины ко второй осуществляется, при этом вторая машина не имеет доступа к сети Интернет, поэтому задание можно считать выполненным.

---

## Задание 1
#### Используя команду ls, необходимо вывести на экран все файлы, которые расположены в секционных директориях /usr/share/man/manX и содержат слово "config" в имени.
``` 
[student1@localhost ~]$ ls /usr/share/man/man? | grep config
pkg-config.1.gz
config.5ssl.gz
config-util.5.gz
selinux_config.5.gz
ssh_config.5.gz
sshd_config.5.gz
x509v3_config.5ssl.gz
authconfig.8.gz
authconfig-tui.8.gz
chkconfig.8.gz
grub2-mkconfig.8.gz
iprconfig.8.gz
lvm-config.8.gz
lvmconfig.8.gz
lvm-dumpconfig.8.gz
sys-unconfig.8.gz
```
#### Одним вызовом ls найти все файлы, содержащие слово "system" в каталогах /usr/share/man/man1 и /usr/share/man/man7

```
[student1@localhost ~]$ ls /usr/share/man/man1 /usr/share/man/man7 | grep system
systemctl.1.gz
systemd.1.gz
systemd-analyze.1.gz
systemd-ask-password.1.gz
systemd-bootchart.1.gz
systemd-cat.1.gz
systemd-cgls.1.gz
systemd-cgtop.1.gz
systemd-delta.1.gz
systemd-detect-virt.1.gz
systemd-escape.1.gz
systemd-firstboot.1.gz
systemd-firstboot.service.1.gz
systemd-inhibit.1.gz
systemd-machine-id-commit.1.gz
systemd-machine-id-setup.1.gz
systemd-notify.1.gz
systemd-nspawn.1.gz
systemd-path.1.gz
systemd-run.1.gz
systemd-tty-ask-password-agent.1.gz
lvmsystemid.7.gz
systemd.directives.7.gz
systemd.generator.7.gz
systemd.index.7.gz
systemd.journal-fields.7.gz
systemd.special.7.gz
systemd.time.7.gz
[student1@localhost ~]$ ls /usr/share/man/man1 | grep system | wc -l
21
[student1@localhost ~]$ ls /usr/share/man/man7 | grep system | wc -l
7
[student1@localhost ~]$ ls /usr/share/man/man1 /usr/share/man/man7 | grep system | wc -l
28 
```

---

## Задание 2
#### Найти в директории /usr/share/man все файлы, которые содержат слово "help" в имени.

```
[student1@localhost ~]$ find /usr/share/man -type f -name '*help*'
/usr/share/man/man1/help.1.gz
/usr/share/man/man5/firewalld.helper.5.gz
/usr/share/man/man8/mkhomedir_helper.8.gz
/usr/share/man/man8/pwhistory_helper.8.gz
/usr/share/man/man8/ssh-pkcs11-helper.8.gz
```

#### Найти там же все файлы, имя которых начинается на "conf".

```
[student1@localhost ~]$ find /usr/share/man -type f -name 'conf*'
/usr/share/man/man5/config.5ssl.gz
/usr/share/man/man5/config-util.5.gz
```

#### Какие действия мы можем выполнить с файлами, найденными командой find?

- print (по умолчанию) -> вывод пути для каждого найденного файла;
- ls -> подробный вывод информации о найденных файлах;
- delete -> удаление найденных файлов;
- exec -> выполнение указанных команд для каждого найденного файла в текущей директории;
- execdir -> выполнение указанных команд для каждого найденного файла в текущей содержащей файл;
- fls ->  как -ls, но запись результата в файл подобно команде fprint;
- frint -> печать полного имени файла в указанный файл;
- fprint0 -> как -print0, но запись результата в файл подобно команде fprint;
- fprintf -> как -printf, но запись результата в файл подобно команде fprint;
- ok -> как exec, но спрашивает подтверждение выполняемой команды;
- okdir -> как execdir, но спрашивает подтверждение выполняемой команды;
- print -> печатает полное имя файла с символом новой строки на конце;
- print0 -> аналогично -print, но в конце null-символ;
- printf -> управление форматом вывода результата;
- prune -> если файл является директорией, то не спускается в него;
- quit -> немедленный выход.
- 
Примеры:

```
[student1@localhost ~]$ find /usr/share/man -type f -name 'conf*' -ls
278136    8 -rw-r--r--   1 root     root         6264 Aug  8  2019 /usr/share/man/man5/config.5ssl.gz
263626    4 -rw-r--r--   1 root     root          480 Mar 31  2020 /usr/share/man/man5/config-util.5.gz
[student1@localhost ~]$ find /usr/share/man -type f -name 'conf*' -ls -quit
278136    8 -rw-r--r--   1 root     root         6264 Aug  8  2019 /usr/share/man/man5/config.5ssl.gz
[student1@localhost ~]$ find /usr/share/man -type f -name 'conf*' -print0
/usr/share/man/man5/config.5ssl.gz/usr/share/man/man5/config-util.5.gz[student1@localhost ~]$
[student1@localhost ~]$ find /usr/share/man -type f -name 'conf*' -printf '%s %t %p\n'
6264 Thu Aug  8 21:37:43.0000000000 2019 /usr/share/man/man5/config.5ssl.gz
480 Tue Mar 31 23:59:56.0000000000 2020 /usr/share/man/man5/config-util.5.gz
```

В последнем случае задается формат вывода, содержащий дополнительно размер файлов в байтах и время послдней модификации.

```
[student1@localhost test]$ touch file_name{1..3}.md
[student1@localhost test]$ ls
file_name1.md  file_name2.md  file_name3.md
[student1@localhost test]$ find -name 'file_*' -type f -delete
```
---

## Задание 3
#### При помощи команд head и tail, выведите последние 2 строки файла /etc/fstab и первые 7 строк файла /etc/yum.conf

```
[student1@localhost ~]$ tail -n 2 /etc/fstab
UUID=576888b7-2357-4c81-8766-032de7f441a2 /boot                   xfs     defaults        0 0
/dev/mapper/centos-swap swap                    swap    defaults        0 0
[student1@localhost ~]$ head -n 7 /etc/yum.conf
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
```

#### Что произойдёт, если мы запросим больше строк, чем есть в файле?
```
[student1@localhost ~]$ wc -l /etc/yum.conf
26 /etc/yum.conf
[student1@localhost ~]$ head -n 30 /etc/yum.conf
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=5
bugtracker_url=http://bugs.centos.org/set_project.php?project_id=23&ref=http://bugs.centos.org/bug_report_page.php?category=yum
distroverpkg=centos-release


#  This is the default, if you make this bigger yum won't see if the metadata
# is newer on the remote and so you'll "gain" the bandwidth of not having to
# download the new metadata and "pay" for it by yum not having correct
# information.
#  It is esp. important, to have correct metadata, for distributions like
# Fedora which don't keep old packages around. If you don't like this checking
# interupting your command line usage, it's much better to have something
# manually check the metadata once an hour (yum-updatesd will do this).
# metadata_expire=90m

# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
[student1@localhost ~]$ head -n 26 /etc/yum.conf
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=5
bugtracker_url=http://bugs.centos.org/set_project.php?project_id=23&ref=http://bugs.centos.org/bug_report_page.php?category=yum
distroverpkg=centos-release


#  This is the default, if you make this bigger yum won't see if the metadata
# is newer on the remote and so you'll "gain" the bandwidth of not having to
# download the new metadata and "pay" for it by yum not having correct
# information.
#  It is esp. important, to have correct metadata, for distributions like
# Fedora which don't keep old packages around. If you don't like this checking
# interupting your command line usage, it's much better to have something
# manually check the metadata once an hour (yum-updatesd will do this).
# metadata_expire=90m

# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
[student1@localhost ~]$ tail -n 30 /etc/yum.conf
[main]
cachedir=/var/cache/yum/$basearch/$releasever
keepcache=0
debuglevel=2
logfile=/var/log/yum.log
exactarch=1
obsoletes=1
gpgcheck=1
plugins=1
installonly_limit=5
bugtracker_url=http://bugs.centos.org/set_project.php?project_id=23&ref=http://bugs.centos.org/bug_report_page.php?category=yum
distroverpkg=centos-release


#  This is the default, if you make this bigger yum won't see if the metadata
# is newer on the remote and so you'll "gain" the bandwidth of not having to
# download the new metadata and "pay" for it by yum not having correct
# information.
#  It is esp. important, to have correct metadata, for distributions like
# Fedora which don't keep old packages around. If you don't like this checking
# interupting your command line usage, it's much better to have something
# manually check the metadata once an hour (yum-updatesd will do this).
# metadata_expire=90m

# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
```

---
## Задание 4
#### Создайте в домашней директории файлы file_name1.md, file_name2.md и file_name3.md c дальнейшим переименованием.

```
[student1@localhost ~]$ touch file_name{1..3}.md
[student1@localhost ~]$ ls
file_name1.md  file_name2.md  file_name3.md
[student1@localhost ~]$ mv file_name1.{md,textdoc}
[student1@localhost ~]$ mv file_name2{.md,}
[student1@localhost ~]$ mv file_name3.md{,.latest}
[student1@localhost ~]$ ls
file_name1.textdoc  file_name2  file_name3.md.latest
[student1@localhost ~]$ mv file_name1.{textdoc,txt}
[student1@localhost ~]$ ls
file_name1.txt  file_name2  file_name3.md.latest
```

Вывод: если в head или tail мы запрашиваем больше строк, чем содержится в самом файле, то будут выведены все строки.

---

## Задание 5
#### Напишите как можно больше различных вариантов команды cd, с помощью которых вы можете вернуться обратно в домашнюю директорию вашего пользователя.
```
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd ~
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd /home/student1
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd ../home/student1
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd ../home/../home/student1
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd ./././../home/../home/../home/./student1
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd
[student1@localhost ~]$ cd /mnt
[student1@localhost mnt]$ cd - /home/student1
/home/student1
```

---

## Задание 6
#### Создайте одной командой в домашней директории 3 папки new, in-process, processed. При этом in-process должна содержать в себе еще 3 папки tread0, tread1, tread2.
```
[student1@localhost ~]$ mkdir -p new processed in-process/tread{0..2}/
[student1@localhost ~]$ ls
file_name1.txt  file_name2  file_name3.md.latest  in-process  new  processed
[student1@localhost ~]$ ls processed
tread0  tread1  tread2
```

#### Далее создайте 100 файлов формата data[[:digit:]][[:digit:]] в папке new.

```
touch new/data{00..99}
```

#### Скопируйте 34 файла в tread0 и по 33 в tread1 и tread2 соответственно.

```
[student1@localhost ~]$ cp new/data{00..33} in-process/tread0
[student1@localhost ~]$ cp new/data{34..66} in-process/tread1
[student1@localhost ~]$ cp new/data{67..99} in-process/tread2
```

#### Выведете содержимое каталога in-process одной командой

```
[student1@localhost ~]$ ls -R in-process
in-process:
tread0  tread1  tread2

in-process/tread0:
data00  data03  data06  data09  data12  data15  data18  data21  data24  data27  data30  data33
data01  data04  data07  data10  data13  data16  data19  data22  data25  data28  data31
data02  data05  data08  data11  data14  data17  data20  data23  data26  data29  data32

in-process/tread1:
data34  data37  data40  data43  data46  data49  data52  data55  data58  data61  data64
data35  data38  data41  data44  data47  data50  data53  data56  data59  data62  data65
data36  data39  data42  data45  data48  data51  data54  data57  data60  data63  data66

in-process/tread2:
data67  data70  data73  data76  data79  data82  data85  data88  data91  data94  data97
data68  data71  data74  data77  data80  data83  data86  data89  data92  data95  data98
data69  data72  data75  data78  data81  data84  data87  data90  data93  data96  data99
```

#### После этого переместите все файлы из каталогов tread в processed одной командой.

```
mv ./in-process/tread{0..2}/* processed
```

#### Выведете содержимое каталога in-process и processed одной командой.

```
[student1@localhost ~]$ ls -r processed in-process
processed:
data99  data92  data85  data78  data71  data64  data57  data50  data43  data36  data29  data22  data15  data08  data01
data98  data91  data84  data77  data70  data63  data56  data49  data42  data35  data28  data21  data14  data07  data00
data97  data90  data83  data76  data69  data62  data55  data48  data41  data34  data27  data20  data13  data06
data96  data89  data82  data75  data68  data61  data54  data47  data40  data33  data26  data19  data12  data05
data95  data88  data81  data74  data67  data60  data53  data46  data39  data32  data25  data18  data11  data04
data94  data87  data80  data73  data66  data59  data52  data45  data38  data31  data24  data17  data10  data03
data93  data86  data79  data72  data65  data58  data51  data44  data37  data30  data23  data16  data09  data02

in-process:
tread2  tread1  tread0
```

#### Сравните количество файлов в каталогах new и processed, если они равны удалите файлы из new.

```
[student1@localhost ~]$ if [ `ls new | wc -w` = `ls processed | wc -w` ]; then rm new/*; fi
```

---

## Задание 7
#### Получить разворачивание фигурных скобок для выражения {$a..$b}.

```
[student1@localhost ~]$ a=1
[student1@localhost ~]$ b=3
[student1@localhost ~]$ seq -f "file%g" $a $b| xargs echo
file1 file2 file3
[student1@localhost ~]$ eval echo file{$a..$b}
file1 file2 file3
```
