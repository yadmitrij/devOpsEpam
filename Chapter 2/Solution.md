# Решение домашней работы по первому занятию
## Задание 1
#### Открыть инструкцию по пользованию приложением awk. Найти секцию про использование переменных окружения. Сохранить эту секцию в отдельный файл.

Вывод самой инструкции в решении приводится не будет, так как он не информативен для показания способа решения задачи.

Открытие инструкции

``` 
[student1@localhost ~]$ man awk
```
Для поиска нужной секции вводим "/variables" и с помощью клавичи "n" находим интересующий раздел "Built-in variables".
Проматываем инструкцию так, чтобы последняя строчка секции являлась самой верхней в терминале вывода.
Ставим метку "v", последовательно нажав клавиши "m" и "v".
Возвращаемся к началу секции так, чтобы первая строчка была "Built-in variables".
Последовательно нажимаем "|", "v" (заданная метка), "tee >> ~/manFile.txt".
Проверка результата:

```
[student1@localhost ~]$ cat manFile.txt
   Built-in Variables
       Gawk's built-in variables are:

       ARGC        The number of command line arguments (does not include options to gawk, or the
                   program source).

       ARGIND      The index in ARGV of the current file being processed.
...
```

Полностью приводить содержимое файла не имеет смысла.

---

## Задание 2
#### Написать скрипт, который создаёт файл "task2.txt" директорией выше своего местоположения. В случае ошибки текст ошибки записывается в err.log а пользователю выдаётся сообщение "Error."
#### Если файл уже существует, выдаётся одна ошибка, а если нет прав для его создания - другая.

Будет рассмотрено выполнение задания сразу под звёздочкой, т.к. оно в большей мере раскрывает логику и основного решения.

```
[student1@localhost ~]$ vi script1.sh

#!/bin/bash
test -e ../task2.txt 2>> ./err.log 1> /dev/null
if [ $? -eq 1 ]
then
touch ../task2.txt 2>> ./err.log
if [ $? -eq 1 ]
then
echo 'No permission to make file there'
fi
else
echo 'The file allready exists'
exit 3
fi

[student1@localhost ~]$ chmod +x script1.sh

[student1@localhost ~]$ ./script1.sh
No permission to make file there
[student1@localhost ~]$ cat err.log
touch: cannot touch ‘../task2.txt’: Permission denied

[student1@localhost ~]$ ls
dirPath.txt  err.log  script1.sh  script2.sh  task3  task3a
[student1@localhost ~]$ cd task3
[student1@localhost task3]$ ../script1.sh
[student1@localhost task3]$ cat err.log
[student1@localhost task3]$ ../script1.sh
The file allready exists
[student1@localhost task3]$ ls ../
dirPath.txt  err.log  script1.sh  script2.sh  task2.txt  task3  task3a
```

---

## Задание 3
#### Создать 2 файла: 1-й - текстовый с указанием абслютного пути до директории. 2-й - скрипт, который при выполнении выводит содержимое директории по указанному в первом файле.

```
[student1@localhost task3]$ echo "/home/student1/task3" >> dirPath.txt
[student1@localhost task3]$ vi script2.sh

#!/bin/bash
echo 'cat ./dirPath2.txt | xargs ls'

[student1@localhost ~]$ chmod +x script2.sh
[student1@localhost ~]$ ./script2.sh
dir1  dir2  dir3  file1  file2  file3  file4  file5  file6  file7  file8  file9
[student1@localhost ~]$ ls task3
dir1  dir2  dir3  file1  file2  file3  file4  file5  file6  file7  file8  file9
```

#### Скрипт выводит отдельно количество файлов и количество директорий.
```
[student1@localhost task3]$ vi script2.sh

#!/bin/bash
COUNTER="$(cat ./dirPath.txt | xargs ls -F | wc -w)"
DIRS="$(cat ./dirPath.txt | xargs ls -F | grep "/" | wc -l)"
echo "Files: $(( $COUNTER - $DIRS ))"
echo "Directories: ${DIRS}"

[student1@localhost ~]$ ./script2.sh
Files: 9
Directories: 3
```
#### Скрипт принимает любое количество записей в первом файле и обрабатывает их последовательно.

```
[student1@localhost task3]$ vi script2.sh

#!/bin/bash
cat ./dirPath.txt | while read y
do

COUNTER="$(echo ${y} | xargs ls -F | wc -w )"
DIRS="$( echo ${y} | xargs ls -F | grep "/" | wc -w )"

echo "For directiory: ${y}"
echo "Files: $(( $COUNTER - $DIRS ))"
echo "Directories: ${DIRS}"

done

[student1@localhost task3]$ echo "/home/student1/task3a" >> dirPath.txt
[student1@localhost ~]$ ./script2.sh
For directiory: /home/student1/task3
Files: 10
Directories: 3
For directiory: /home/student1/task3a
Files: 4
Directories: 7
[student1@localhost ~]$ ls task3a
dir10  dir11  dir12  dir13  dir7  dir8  dir9  file2  file3  file4  file5
```
