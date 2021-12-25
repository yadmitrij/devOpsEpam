# Решение домашней работы по четвертому занятию
## Задание 1
### Users and groups. 

#### Создайте группу sales с GID 4000 и пользователей bob, alice, eve c основной группой sales.

```
[root@localhost student1]# groupadd -g 4000 sales
[root@localhost student1]# useradd -g sales bob
[root@localhost student1]# useradd -g sales alice
[root@localhost student1]# useradd -g sales eve
```
#### Измените пользователям пароли.

```
[root@localhost student1]# passwd alice
Changing password for user alice.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
[root@localhost student1]# passwd bob
Changing password for user bob.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
[root@localhost student1]# passwd eve
Changing password for user eve.
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

#### Все новые аккаунты должны обязательно менять свои пароли каждый 30 дней.

```
[root@localhost student1]# vi /etc/login.defs
...
PASS_MAX_DAYS   30
PASS_MIN_DAYS   0
PASS_MIN_LEN    5
PASS_WARN_AGE   7
...
```

#### Новые аккаунты группы sales должны истечь по окончанию 90 дней срока, а bob должен изменять его пароль каждые 15 дней.

```
[root@localhost student1]# for member in `lid -g sales | cut -f1 -d'('`; do chage -E `date -d "90 days" +"%Y-%m-%d"` $member ;done
[root@localhost student1]# chage -M 15 bob
[root@localhost student1]# chage -l bob
Last password change                                    : Dec 13, 2021
Password expires                                        : Dec 28, 2021
Password inactive                                       : never
Account expires                                         : Mar 13, 2022
Minimum number of days between password change          : 0
Maximum number of days between password change          : 15
Number of days of warning before password expires       : 7
```

#### Дополнительно: Заставьте пользователей сменить пароль после первого логина.

```
[root@localhost student1]# for member in `lid -g sales | cut -f1 -d'('`; do chage -d 1970-01-01 $member ;done
[root@localhost /]# exit
exit
[student1@localhost /]$ su alice
Password:
You are required to change your password immediately (root enforced)
Changing password for alice.
```

---

## Задание 2
### Controlling access to files with Linux file system permissions

#### Создайте трёх пользователей glen, antony, lesly.
#### У вас должна быть директория /home/students, где эти три пользователя могут работать совместно с файлами

```
[root@localhost student1]# useradd -G students glen
[root@localhost student1]# useradd -G students antony
[root@localhost student1]# useradd -G students lesly
[root@localhost student1]# mkdir /home/students
```

#### Должен быть возможен только пользовательский и групповой доступ, создание и удаление файлов в /home/students. 

```
[root@localhost student1]# chmod g+rws /home/students
[root@localhost student1]# chmod o-rx /home/students
[root@localhost student1]# chown -R .students /home/students
[root@localhost student1]# su student1
[student1@localhost home]$ ls -l
total 8
drwx------. 2 antony   antony     62 Dec 14 06:36 antony
drwx------. 2 glen     glen       62 Dec 14 06:35 glen
drwx------. 2 gregson  gregson    62 Dec 14 07:04 gregson
drwx------. 2 holmes   holmes     62 Dec 14 07:03 holmes
drwx------. 2 jones    jones      62 Dec 14 07:04 jones
drwx------. 2 lesly    lesly      62 Dec 14 06:36 lesly
drwx------. 2 lestrade lestrade   62 Dec 14 07:04 lestrade
drwx------. 7 student1 student1 4096 Dec 14 06:47 student1
drwxrws---. 4 root     students   88 Dec 14 08:49 students
drwxr-s---. 2 root     root        6 Dec 14 19:38 students_new
drwx------. 2 watson   watson     62 Dec 14 07:03 watson
[student1@localhost home]$ su lesly
Password:
[lesly@localhost home]$ touch /home/students/lesly_file
[lesly@localhost home]$ su glen
Password:
[glen@localhost home]$ echo "sadas" >> /home/students/lesly_file
[glen@localhost home]$ ls -l /home/students
total 4
-rw-rw-r--. 1 lesly students 6 Dec 14 19:46 lesly_file
[glen@localhost home]$ su student1
Password:
[student1@localhost home]$ cat /home/students/lesly_file
cat: /home/students/lesly_file: Permission denied
[student1@localhost home]$ rm /home/students/lesly_file
rm: cannot remove ‘/home/students/lesly_file’: Permission denied
[student1@localhost home]$ echo 'asdas' >> /home/students/lesly_file
bash: /home/students/lesly_file: Permission denied
```

---

## Задание 3
### ACL

#### От суперпользователя создайте папку /share/cases и создайте внутри 2 файла murders.txt и moriarty.txt.

```
[student1@localhost home]$ sudo mkdir -p /share/cases
[student1@localhost home]$ sudo touch /share/cases/murders.txt /share/cases/moriarty.txt
```

#### Создайте группу bakerstreet с пользователями holmes, watson. Создайте группу scotlandyard с пользователями lestrade, gregson, jones.

```
[student1@localhost home]$ sudo groupadd bakerstreet
[student1@localhost home]$ sudo groupadd scotlandyard
[student1@localhost home]$ sudo useradd -G bakerstreet holmes
[student1@localhost home]$ sudo useradd -G bakerstreet watson
[student1@localhost home]$ sudo useradd -G scotlandyard lestrade
[student1@localhost home]$ sudo useradd -G scotlandyard gregson
[student1@localhost home]$ sudo useradd -G scotlandyard jones
[student1@localhost home]$ sudo passwd holmes
...все пароли были установлены
```

#### Зададим все необходимые права на файлы и папки согласно заданию.

```
[student1@localhost home]$ sudo chmod g+rws /share
[student1@localhost home]$ sudo chmod o-rx /share
[student1@localhost home]$ sudo chown -R .bakerstreet /share
[student1@localhost home]$ sudo setfacl -m g:scotlandyard:rwx -R /share
[student1@localhost home]$ sudo setfacl -m d:g:scotlandyard:rwx -R /share
[student1@localhost home]$ sudo setfacl -m g:scotlandyard:rw- /share/cases/murders.txt
[student1@localhost home]$ sudo setfacl -m g:scotlandyard:rw- /share/cases/moriarty.txt
[student1@localhost home]$ sudo setfacl -m u:jones:r-x -R /share
[student1@localhost home]$ sudo setfacl -m d:u:jones:r-x -R /share
[student1@localhost home]$ sudo setfacl -m u:jones:r-- /share/cases/murders.txt
[student1@localhost home]$ sudo setfacl -m u:jones:r-- /share/cases/moriarty.txt
```

#### Создадим новую директорию и тестовый файл

```
[student1@localhost cases]$ sudo -u watson mkdir /share/watson_dir2
[student1@localhost cases]$ sudo -u watson touch /share/watson_dir2/watson_file
[student1@localhost cases]$ sudo -u watson getfacl /share/watson_dir2/watson_file
getfacl: Removing leading '/' from absolute path names
# file: share/watson_dir2/watson_file
# owner: watson
# group: bakerstreet
user::rw-
user:jones:r-x                  #effective:r--
group::rwx                      #effective:rw-
group:scotlandyard:rwx          #effective:rw-
mask::rw-
other::---
```

#### Пользователь jones может только читать файл, а группы scotlandyard и bakerstreet могут читать и записывать в файл.
#### Создадим файл от пользователя группы scotlandyard (не jones) и проверим создержимое директории /share/cases.

```
[lestrade@localhost cases]$ getfacl -R /share/cases
getfacl: Removing leading '/' from absolute path names
# file: share/cases
# owner: root
# group: bakerstreet
# flags: -s-
user::rwx
user:jones:r-x
group::rwx
group:scotlandyard:rwx
mask::rwx
other::---
default:user::rwx
default:user:jones:r-x
default:group::rwx
default:group:scotlandyard:rwx
default:mask::rwx
default:other::---

# file: share/cases/moriarty.txt
# owner: root
# group: bakerstreet
user::rw-
user:jones:r--
group::rw-
group:scotlandyard:rw-
mask::rwx
other::r--

# file: share/cases/murders.txt
# owner: root
# group: bakerstreet
user::rw-
user:jones:r--
group::rw-
group:scotlandyard:rw-
mask::rwx
other::r--

# file: share/cases/watson_file.txt
# owner: watson
# group: bakerstreet
user::rw-
user:jones:r-x                  #effective:r--
group::rwx                      #effective:rw-
group:scotlandyard:rwx          #effective:rw-
mask::rw-
other::---

# file: share/cases/lestrade_dir
# owner: lestrade
# group: bakerstreet
# flags: -s-
user::rwx
user:jones:r-x
group::rwx
group:scotlandyard:rwx
mask::rwx
other::---
default:user::rwx
default:user:jones:r-x
default:group::rwx
default:group:scotlandyard:rwx
default:mask::rwx
default:other::---

# file: share/cases/lestrade_dir/lestrade_file
# owner: lestrade
# group: bakerstreet
user::rw-
user:jones:r-x                  #effective:r--
group::rwx                      #effective:rw-
group:scotlandyard:rwx          #effective:rw-
mask::rw-
other::---
```

#### Все файлы и директории имеют параметры доступа согласно заданию. 
#### В ходе практической проверки ошибок обнаружено не было.
#### Новые файлы и директории, кем бы они не были созданы, относятся к группа bakerstreet.



