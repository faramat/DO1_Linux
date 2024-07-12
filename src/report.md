## Part 1. Установка ОС

1. Чтобы узнать версию ОС, необходимо выполнить команду:\
`cat /etc/issue`

![версия линукс](images/1.png)

## Part 2. Создание пользователя

1. Создание пользователя:\
`sudo adduser khrazzho`

![создание пользователя](images/2.1.png)

2. Добавление пользователя в группу adm:\
`sudo usermod -aG adm khrazzho`

![добавление пользователя в группу adm](images/2.2.png)

3. Проверка, что пользователь успешно добавлен:\
`cat /etc/passwd | grep khrazzho`

![проверка добавления пользователя](images/2.3.png)

4. Проверка, к каким группам относится пользователь:\
`groups khrazzho`

![группы пользователя](images/2.4.png)

## Part 3. Настройка сети ОС

1. Задаём название машины:\
`sudo hostname user-1`

![задаем имя машины](images/3.1.png)

2. Установка временной зоны и проверка:\
`sudo timedatectl set-timezone Europe/Moscow`\
`timedatectl`

![задаем и проверяем время](images/3.2.png)

3. Вывод названий сетевых интерфейсов:\
`ip link show`

![вывод названий сетевых интерфейсов](images/3.3.png)

Интерфейс lo (loopback) — это специальный сетевой интерфейс, используемый для тестирования сетевого стека и маршрутизации внутри одного устройства. Он не связан с физическим оборудованием и всегда имеет адрес 127.0.0.1.

4. Получение IP-адреса от DHCP:\
`ip addr show`

![Получение IP-адреса от DHCP](images/3.4.png)

DHCP — сетевой протокол, позволяющий сетевым устройствам автоматически получать IP-адрес и другие параметры, необходимые для работы в сети TCP/IP.

5. Определение внешнего и внутреннего IP-адреса шлюза:\
`ip route`

![внутренний и внешний адреса шлюза](images/3.5.png)

6. Задание статичных сетевых настроек\

Для задания статического IP-адреса, шлюза и DNS, необходимо отредактировать YAML-файл в директории /etc/netplan/:\
`sudo nano /etc/netplan/00-installer-config.yaml`

![комманда вызова nano](images/3.6.png)

![редактор nano](images/3.7.png)

После сохранения файла и применения новых настроек, выполняем следующую команду для применения конфигурации:\
`sudo netplan apply`

7. Перезагрузка виртуальной машины:\
`sudo reboot`

![перезагрузка виртуальной машины](images/3.8.png)

8. Проверяем, что статические настройки сохранены:\
`ip addr show`\
`ip route`

![проверка](images/3.9.png)

9. Проверяем доступность хостов командами:\
`ping -c 10 1.1.1.1`\
`ping -c 10 ya.ru`

![вывод ping](images/3.10.png)

## Part 4. Обновление ОС

1. Обновляем список пакетов командой:\
`sudo apt update`

![список пакетов](images/4.1.png)

2. Обновляем все установленные пакеты командой:\
`sudo apt upgrade`

3. Пытаемся обновить повторно:

![вывод повторной попытки обновления](images/4.2.png)

## Part 5. Использование команды **sudo**
1. Истинное назначение команды sudo

Команда sudo (SuperUser DO) позволяет пользователю выполнять команды с привилегиями суперпользователя (root). Это позволяет администраторам системы и другим пользователям выполнять специфические задачи, требующие повышенных привилегий, например, установку программ или изменение системных файлов. 

2. Выдаём пользователю root права:\
`sudo usermod -aG sudo toastgra`

3. И проверяем их наличие:\
`sudo -l -U toastgra`

![выдача и проверка прав](images/5.1.png)

4. Переключаем пользователя на toastgra и меняем hostname:\
`sudo su - toastgra`\
`sudo hostname twentyone`

![переключение юзера и смена имени хоста](images/5.2.png)

5. Также нужно поменять hostname в файле /etc/hostnames и выполнить перезагрузку, чтобы изменения вступили в силу:\
`sudo nano /etc/hostname`\
`sudo reboot`

![новое имя хоста](images/5.3.png)

## Part 6. Установка и настройка службы времени

1. Активируем NTP синхронизацию командой:\
`sudo timedatectl set-ntp true`

2. Проверка настроек синхронизации времени:\
`timedatectl show`

![параметры времени](images/6.1.png)

## Part 7. Установка и использование текстовых редакторов 

1. Установка текстовых редакторов:\
`sudo apt install vim`\
`sudo apt install nano`\
`sudo apt install mcedit`

2. Создаём и открываем файл командой:\
`vim test_vim.txt`\
`i` - переключение в режим ввода\
`Esc` - переключение в командный режим\
`:wq` ,а затем `Enter` - выход с сохранением

![vim](images/7.1.png)

3. Создаём и открываем файл командой:\
`nano test_nano.txt`\
`Ctrl+O` - сохранение\
`Enter` - подтверждение имени файла\
`Ctrl+X` - выход

![nano](images/7.2.png)

4. Создаём и открываем файл командой:\
`mcedit test_edit.txt`\
`F2` - сохраниение\
`Enter` - подтверждение\
`F10` - выход

![mcedit](images/7.3.png)

5. Редактирование и выход без сохраниения:
- vim:
  - `:q!` - выход без сохраниеня

  ![vim выход без сохранения](images/7.4.png)

- nano:
  - `Ctrl+X` + `n` - выход и отказ от сохранения

  ![nano выход без сохранения](images/7.5.png)

- mcedit:
  - `F10` + `[NO]` - выход и отказ от сохранения

  ![mcedit выход без сохранения](images/7.6.png)

6. Поиск и замена слова:
- vim:
  - `/слово` - поиск

  ![поиск в vim](images/7.7.png)

  - `:s/слово/замена` - замена  

  ![замена в vim](images/7.8.png)

- nano:
  - `Ctrl + W` - поиск

  ![поиск в nano](images/7.9.png)

  ![результат поиска](images/7.10.png)

  - `Ctrl + \` - замена
  - `Enter`  

  ![поиск для замены](images/7.11.png)

  ![чем заменять](images/7.12.png)

  ![результат замены](images/7.13.png)

- mcedit:
  - `F7` - поиск

  ![поиск в mcedit](images/7.14.png)

  ![результат поиска](images/7.15.png)

  - `F4` - замена  

  ![замена](images/7.16.png)

  ![подтверждение замены](images/7.17.png)

  ![результат замены](images/7.18.png)

## Part 8. Установка и базовая настройка сервиса **SSHD**

1. Установка службы SSHD:\
`sudo apt update`\
`sudo apt install openssh-server`

2. Добавление автозапуска службы SSHD:\
`sudo systemctl enable ssh`\:
`systemctl status ssh` - проверка статуса

![автозапуск и проверка статуса ssh](images/8.1.png)

3. Перенастройка службы SSHD на порт 2022:\
`sudo nano /etc/ssh/sshd_config` - редактирование файла:
    - #Port 22 меняем на Port 2022

    `sudo systemctl restart ssh` - перезагрузка службы

![редактирование файла](images/8.2.png)

![проверка изменений](images/8.3.png)

4. Проверка работы SSHD с помощью команды ps:\
`ps -A | grep sshd`

`ps` - отображает информацию о паботающих процессах

![вывод команды ps -A](images/8.4.png)

Основные ключи команды ps:\
-e: Показывает все процессы в системе.\
-u: Показывает информацию о пользователях, запустивших процессы.\
-x: Показывает процессы, которые не связаны с терминалом.\
-f: Форматирует вывод более подробным образом, включая полный путь к исполняемому файлу и информацию о родительском процессе.\
-l: Показывает дополнительную информацию, такую как владелец процесса, группа, размер памяти и т.д.\
-a: Аналогично ключу -x, показывает процессы, не связанные с терминалом.\
-A: Показывает все процессы в системе, независимо от того, кто их запустил.\
-m: Показывает только процессы, связанные с сетью.\
-n: Не показывает процессы, которые не имеют идентификаторов процесса.\
-o: Позволяет пользователю определить формат вывода с помощью списка полей.

5. Перезагрузка системы:\
`sudo reboot`

6. Устанавливаем netstat:\
`sudo apt install net-tools`

Вывод комманды:\
`sudo netstat -tan`

![вывод команды netstat](images/8.5.png)

Ключ -t отображает только TCP сокеты\
Ключ -a отображает все сокеты (listening and non-listening)\
Ключ -n отображает адреса и порты вместо имен

Объяснение вывода netstat -tan:\
Proto: Протокол, используемый для соединения. Например, tcp или udp.\
tcp: Тип протокола.\
Recv-Q: Количество байтов, ожидающих прием в сокет. Это количество данных, которое еще не было прочитано приложением.\
Send-Q: Количество байтов, ожидающих отправку из сокета. Это количество данных, которое еще не было отправлено сетью.\
0 0: Стандартные значения, указывающие, что данные не отправлялись или не получены.\
Local Address: Локальный адрес и порт, на котором прослушивается соединение. 0.0.0.0 означает, что сокет прослушивает на всех доступных сетевых интерфейсах.\
0.0.0.0:2022: IP-адрес и порт, на котором прослушивается соединение. 0.0.0.0 означает, что сервер принимает соединения на указанном порту с любого IP-адреса.\
Foreign Address: Адрес и порт удаленного хоста, с которым установлено соединение. Если соединение не установлено, этот столбец может быть пустым.\
State: Состояние соединения.\
LISTEN: Состояние сокета, указывающее, что сервер готов принимать входящие соединения.\

## Part 9. Установка и использование утилит **top**, **htop**

1. Вывод команды top:\
`sudo top`

![sudo top вывод](images/9.1.png)

  - `47min` uptime
  - `1 user` количество авторизованных пользователей
  - `0.00, 0.00, 0.00 (загрузка системы за последние 1, 5 и 15 минут)` общая загрузка системы
  - `96 total` общее количество процессов
  - `0.0 us, 0.0 sy, 0.0 ni,100.0 id, 0.0 wa, 0.0 hi, 0.0 si, 0.0 st` загрузка cpu
  - `1971.6 total, 1249.2 free, 142.3 used, 580.2 buff/cache` загрузка памяти
  - `1` pid процесса занимающего больше всего памяти
  - `1` pid процесса, занимающего больше всего процессорного времени

2. Вывод команды htop:\
`sudo htop`\
`F6` - сортировка
  - сортировка по PID
  
  ![сортировка по PID](images/9.2.png)
  
  - PERCENT_CPU
  
  ![PERCENT_CPU](images/9.3.png)
  
  - PERCENT_MEM
  
  ![PERCENT_MEM](images/9.4.png)
  
  - TIME

  ![TIME](images/9.5.png)

  - фильтр для процесса sshd

  `F4`

  ![фильтр для процесса sshd](images/9.6.png)

  - с процессом syslog, найденным, используя поиск

  ![syslog](images/9.7.png)

  - с добавленным выводом hostname, clock и uptime

  `F2`

  ![hostname, clock и uptime](images/9.8.png)

## Part 10. Использование утилиты **fdisk**

1. Выполняем команду:\
`sudo fdisk -l`

![вывод fdisk -l](images/10.1.png)

Название жесткого диска: /dev/sda\
Размер жесткого диска: 25 GiB\
Количество секторов: 52428800 секторов\
Размер swap-пространства: 2.0 ГБ

![swap](images/10.2.png)

## Part 11. Использование утилиты **df** 
1. `sudo df`

![вывод df](images/11.1.png)

- Размер раздела: 11758760 килобайт
- Размер занятого пространства: 5462244 килобайт
- Размер свободного пространства: 5677408 килобайт
- Процент использования: 50%
- Единица измерения: килобайт

2. `sudo df -Th`

![вывод df -Th](images/11.2.png)

- Размер раздела: 12 ГБ
- Размер занятого пространства: 5.3 ГБ
- Размер свободного пространства: 5.5 ГБ
- Процент использования: 50%
- Тип файловой системы: ext4

## Part 12. Использование утилиты **du**

1. `du`

![вывод du](images/12.1.png)

2. Размер папок /home, /var, /var/log (в байтах, в человекочитаемом виде)\
`sudo du -hsb /var`\
`sudo du -hsb /var/log`\
`sudo du -hsb /home`

![du -hsb](images/12.2.png)

- -s означает "сводный", т.е. выводит общий размер директории
- -b означает "в байтах", т.е. выводит размер в байтах без преобразования в человекочитаемый вид
- -h означает "человекочитаемый", т.е. выводит размер в удобных для восприятия единицах (например, KB, MB, GB)

3. Размер всего содержимого в /var/log\
`sudo du -h /var/log/*` 

![Размер всего содержимого в /var/log](images/12.3.png)

## Part 13. Установка и использование утилиты **ncdu**

1. Установка утилиты:\
`sudo apt install ncdu`

![Установка утилиты ncdu](images/13.1.png)

2. Вывод размера папок /home, /var, /var/log:

`ncdu /home`

![размер /home](images/13.2.png)

`ncdu /var`

![размер /var](images/13.3.png)

`ncdu /var/log`

![размер /var/log](images/13.4.png)

## Part 14. Работа с системными журналами

1. Для просмотра логов вводим команды:

`cat /var/log/dmesg` - содержит сообщения ядра Linux, включая информацию о загрузке оборудования и других низкоуровневых событий\
`cat /var/log/syslog` - содержит системные сообщения, включая информацию о работе служб и приложений\
`cat /var/log/auth.log ` - содержит информацию о событиях аутентификации, включая попытки входа в систему и успешные авторизации

2. Последняя успешная авторизация:

`cat /var/log/auth.log | grep 'session opened'`

![auth.log](images/14.1.png)

Время: 13:29:11\
Имя: ionbe\
Метод: (uid=0) означает, что сессия была открыта для другого пользователя системой или процессом, работающим с правами суперпользователя.

3. Перезагрузка SSHD:

`sudo systemctl restart sshd`

`cat /var/log/auth.log | grep 'restart'`

![лог о перезагрузке sshd](images/14.2.png)

## Part 15. Использование планировщика заданий **CRON**

1. Добавляем задание в cron:

`crontab -e`

Добавляем строку `*/2 * * * * uptime` в конец файла.

![cron файл](images/15.1.png)

2. Ищем в журнале строчки о выполнении:

`journalctl --since "2024-06-20 00:00:00" --until "2024-06-21 14:30:00" | grep 'uptime'`

![строчки о выполнении](images/15.2.png)

3. Список текущих заданий:

`crontab -l`

![список текущих заданий cron](images/15.3.png)

4. Удаление всех заданий:

`crontab -r`

![удаление заданий и проверка](images/15.4.png)