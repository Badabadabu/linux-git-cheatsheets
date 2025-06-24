# 🛠️ Linux Administration - Продвинутый справочник с мнемониками

> Системное администрирование - это искусство управления компьютерными системами

## 👥 Управление пользователями и группами

### `useradd` - Add User
**Мнемоника**: "Добавить пользователя" (Add user to system)
```bash
sudo useradd username                     # Создать пользователя
sudo useradd -m username                  # -m создать домашнюю папку
sudo useradd -s /bin/bash username        # -s указать shell
sudo useradd -G sudo,developers username  # -G добавить в группы
sudo useradd -c "John Doe" username       # -c комментарий (полное имя)
```

### `usermod` - Modify User
**Мнемоника**: "Модифицировать пользователя" (Modify user)
```bash
sudo usermod -aG sudo username           # Добавить в группу sudo
sudo usermod -s /bin/zsh username        # Сменить shell
sudo usermod -l newname oldname          # Переименовать пользователя
sudo usermod -L username                 # Заблокировать аккаунт
sudo usermod -U username                 # Разблокировать аккаунт
```

### `passwd` - Password
**Мнемоника**: "Пароль" (Password management)
```bash
passwd                                   # Сменить свой пароль
sudo passwd username                     # Сменить пароль пользователя
sudo passwd -l username                  # Заблокировать пароль
sudo passwd -u username                  # Разблокировать пароль
sudo passwd -d username                  # Удалить пароль
```

### Управление группами
```bash
sudo groupadd developers                 # Создать группу
sudo groupdel developers                 # Удалить группу
groups username                          # Показать группы пользователя
id username                              # Подробная информация о пользователе
```

## 🔐 Права доступа и безопасность

### Расширенные права доступа
**Мнемоника**: Права = **R**ead **W**rite e**X**ecute
```bash
# Символьная запись
chmod u+rwx file.txt                     # User: read, write, execute
chmod g+rw file.txt                      # Group: read, write
chmod o-r file.txt                       # Others: remove read
chmod a+x script.sh                      # All: add execute

# Числовая запись (восьмеричная)
chmod 755 script.sh                      # rwxr-xr-x
chmod 644 document.txt                   # rw-r--r--
chmod 600 private.key                    # rw------- (только владелец)
```

### Специальные права доступа
```bash
# SUID (Set User ID) - выполняется от имени владельца
chmod u+s /usr/bin/passwd
chmod 4755 file                          # SUID + 755

# SGID (Set Group ID) - выполняется от имени группы
chmod g+s directory
chmod 2755 directory                     # SGID + 755

# Sticky bit - только владелец может удалять файлы
chmod +t /tmp
chmod 1755 directory                     # Sticky + 755
```

### `sudo` - Super User Do
**Мнемоника**: "Делать как суперпользователь" (Super user do)
```bash
sudo command                             # Выполнить команду с правами root
sudo -u username command                 # Выполнить от имени другого пользователя
sudo -i                                  # Войти как root
sudo -s                                  # Запустить shell с правами root
sudo visudo                              # Безопасно редактировать /etc/sudoers
sudo -l                                  # Показать разрешенные команды
```

### Файл `/etc/sudoers`
```bash
# Примеры правил в sudoers:
username ALL=(ALL:ALL) ALL              # Полные права
%admin ALL=(ALL) ALL                     # Группа admin - полные права
username ALL=NOPASSWD: /bin/systemctl   # Без пароля для systemctl
```

## 💾 Управление дисками и файловыми системами

### `fdisk` - Fixed Disk
**Мнемоника**: "Фиксированный диск" (Fixed disk management)
```bash
sudo fdisk -l                           # Список всех дисков
sudo fdisk /dev/sda                      # Редактировать разделы диска sda
# Команды в fdisk: p (print), n (new), d (delete), w (write), q (quit)
```

### `parted` - Partition Editor
**Мнемоника**: "Редактор разделов" (Partition editor)
```bash
sudo parted /dev/sda print               # Показать разделы
sudo parted /dev/sda mklabel gpt         # Создать GPT таблицу разделов
sudo parted /dev/sda mkpart primary ext4 1MiB 100%  # Создать раздел
```

### Создание файловых систем
```bash
sudo mkfs.ext4 /dev/sda1                 # Создать ext4 файловую систему
sudo mkfs.xfs /dev/sda1                  # Создать XFS файловую систему
sudo mkfs.ntfs /dev/sda1                 # Создать NTFS файловую систему
sudo mkswap /dev/sda2                    # Создать swap раздел
```

### Монтирование
**Мнемоника**: "Установить" (Mount like mounting a horse)
```bash
sudo mount /dev/sda1 /mnt                # Смонтировать диск
sudo umount /mnt                         # Размонтировать
mount | grep sda                         # Показать смонтированные диски
sudo mount -o remount,ro /              # Перемонтировать только для чтения
```

### `/etc/fstab` - File System Table
```bash
# Автоматическое монтирование при загрузке
# UUID=xxx /home ext4 defaults 0 2
sudo blkid                               # Показать UUID дисков
```

### LVM - Logical Volume Manager
**Мнемоника**: "Логический менеджер томов" (Logical Volume Manager)
```bash
# Физические тома (Physical Volumes)
sudo pvcreate /dev/sda1 /dev/sdb1        # Создать PV
sudo pvdisplay                           # Показать PV

# Группы томов (Volume Groups)
sudo vgcreate myvg /dev/sda1 /dev/sdb1   # Создать VG
sudo vgdisplay                           # Показать VG
sudo vgextend myvg /dev/sdc1             # Добавить диск в VG

# Логические тома (Logical Volumes)
sudo lvcreate -L 10G -n mylv myvg        # Создать LV размером 10GB
sudo lvdisplay                           # Показать LV
sudo lvextend -L +5G /dev/myvg/mylv      # Увеличить LV на 5GB
sudo resize2fs /dev/myvg/mylv            # Расширить файловую систему
```

## 🔄 Управление процессами и сервисами

### `systemctl` - System Control
**Мнемоника**: "Системный контроль" (System control)
```bash
sudo systemctl start nginx              # Запустить сервис
sudo systemctl stop nginx               # Остановить сервис
sudo systemctl restart nginx            # Перезапустить сервис
sudo systemctl reload nginx             # Перезагрузить конфигурацию
sudo systemctl enable nginx             # Включить автозапуск
sudo systemctl disable nginx            # Отключить автозапуск
systemctl status nginx                  # Статус сервиса
systemctl is-active nginx               # Активен ли сервис
systemctl is-enabled nginx              # Включен ли автозапуск
```

### Просмотр логов с `journalctl`
**Мнемоника**: "Журнал контроль" (Journal control)
```bash
journalctl                               # Все логи
journalctl -u nginx                      # Логи конкретного сервиса
journalctl -f                           # Следить за логами в реальном времени
journalctl --since "1 hour ago"         # Логи за последний час
journalctl --since today                # Логи за сегодня
journalctl -p err                       # Только ошибки
journalctl --disk-usage                 # Размер журналов
sudo journalctl --vacuum-time=2weeks    # Очистить логи старше 2 недель
```

### Управление процессами
```bash
# Приоритеты процессов (nice values: -20 до +19)
nice -n 10 command                       # Запустить с низким приоритетом
sudo renice -10 PID                      # Изменить приоритет процесса

# Сигналы процессам
kill -TERM PID                           # Мягкое завершение (по умолчанию)
kill -KILL PID                           # Принудительное завершение
kill -HUP PID                            # Перезагрузить конфигурацию
kill -USR1 PID                           # Пользовательский сигнал 1
```

## 📊 Мониторинг системы

### `htop` / `top` - Process Monitor
**Мнемоника**: "Топ процессов" (Top processes)
```bash
top                                      # Базовый монитор процессов
htop                                     # Улучшенная версия top
# В htop: F1-помощь, F2-настройки, F9-kill, F10-выход
```

### `iotop` - I/O Top
**Мнемоника**: "Топ ввода-вывода" (I/O top)
```bash
sudo iotop                               # Мониторинг дисковой активности
sudo iotop -o                            # Показывать только активные процессы
```

### `vmstat` - Virtual Memory Statistics
**Мнемоника**: "Статистика виртуальной памяти" (VM stats)
```bash
vmstat                                   # Одноразовая статистика
vmstat 2                                 # Обновлять каждые 2 секунды
vmstat 2 5                               # 5 раз каждые 2 секунды
```

### `iostat` - I/O Statistics
**Мнемоника**: "Статистика ввода-вывода" (I/O stats)
```bash
iostat                                   # Статистика дисков
iostat -x 2                              # Расширенная статистика каждые 2 сек
```

### `lsof` - List Open Files
**Мнемоника**: "Список открытых файлов" (List of open files)
```bash
lsof                                     # Все открытые файлы
lsof /path/to/file                       # Кто использует файл
lsof -u username                         # Файлы пользователя
lsof -i :80                              # Процессы на порту 80
lsof -i TCP:22                           # TCP соединения на порту 22
lsof +D /var/log                         # Все файлы в директории
```

## 🌐 Сетевое администрирование

### `ip` - IP Configuration
**Мнемоника**: "IP конфигурация" (IP configuration)
```bash
ip addr show                             # Показать IP адреса (замена ifconfig)
ip route show                            # Показать таблицу маршрутизации
ip link show                             # Показать сетевые интерфейсы
sudo ip addr add 192.168.1.100/24 dev eth0  # Добавить IP адрес
sudo ip route add default via 192.168.1.1   # Добавить маршрут по умолчанию
```

### `ss` - Socket Statistics
**Мнемоника**: "Статистика сокетов" (Socket stats - замена netstat)
```bash
ss -tuln                                 # Слушающие TCP и UDP порты
ss -t -a                                 # Все TCP соединения
ss -u -a                                 # Все UDP соединения
ss -p                                    # Показать процессы
ss -s                                    # Сводная статистика
ss dst 192.168.1.100                     # Соединения с определенным IP
```

### `nmap` - Network Mapper
**Мнемоника**: "Сетевая карта" (Network map)
```bash
nmap 192.168.1.1                        # Сканировать хост
nmap 192.168.1.0/24                     # Сканировать подсеть
nmap -p 22,80,443 192.168.1.1           # Сканировать определенные порты
nmap -sS 192.168.1.1                    # SYN сканирование
nmap -O 192.168.1.1                     # Определить ОС
```

### `tcpdump` - Packet Capture
**Мнемоника**: "Дамп TCP" (TCP dump)
```bash
sudo tcpdump -i eth0                     # Захват на интерфейсе eth0
sudo tcpdump -i any host 192.168.1.100  # Трафик с определенным хостом
sudo tcpdump -i eth0 port 80             # Трафик на порту 80
sudo tcpdump -w capture.pcap             # Сохранить в файл
sudo tcpdump -r capture.pcap             # Читать из файла
```

## 🔥 Межсетевой экран (Firewall)

### `ufw` - Uncomplicated Firewall
**Мнемоника**: "Простой межсетевой экран" (Uncomplicated firewall)
```bash
sudo ufw enable                          # Включить firewall
sudo ufw disable                         # Отключить firewall
sudo ufw status                          # Статус firewall
sudo ufw allow 22                        # Разрешить порт 22
sudo ufw allow ssh                       # Разрешить SSH
sudo ufw allow from 192.168.1.0/24      # Разрешить подсеть
sudo ufw deny 23                         # Запретить порт 23
sudo ufw delete allow 22                 # Удалить правило
```

### `iptables` - IP Tables
**Мнемоника**: "IP таблицы" (IP tables)
```bash
sudo iptables -L                         # Показать правила
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  # Разрешить SSH
sudo iptables -A INPUT -j DROP           # Запретить все остальное
sudo iptables -F                         # Очистить все правила
sudo iptables-save > rules.txt           # Сохранить правила
sudo iptables-restore < rules.txt        # Восстановить правила
```

## 📦 Управление пакетами

### APT (Debian/Ubuntu)
**Мнемоника**: "Продвинутый инструмент пакетов" (Advanced Package Tool)
```bash
sudo apt update                          # Обновить список пакетов
sudo apt upgrade                         # Обновить установленные пакеты
sudo apt install package                 # Установить пакет
sudo apt remove package                  # Удалить пакет
sudo apt purge package                   # Удалить пакет и конфигурацию
sudo apt autoremove                      # Удалить ненужные зависимости
apt search package                       # Поиск пакета
apt list --installed                     # Список установленных пакетов
```

### YUM/DNF (RHEL/CentOS/Fedora)
```bash
sudo yum update                          # Обновить систему (CentOS 7)
sudo dnf update                          # Обновить систему (CentOS 8+, Fedora)
sudo yum install package                 # Установить пакет
sudo yum remove package                  # Удалить пакет
yum search package                       # Поиск пакета
yum list installed                       # Список установленных пакетов
```

## 🕐 Планировщик задач

### `cron` - Cron Jobs
**Мнемоника**: "Хронос" (Time-based job scheduler)
```bash
crontab -e                               # Редактировать crontab пользователя
crontab -l                               # Показать crontab пользователя
sudo crontab -e                          # Редактировать root crontab
crontab -r                               # Удалить crontab пользователя
```

### Формат crontab
```bash
# Минута Час День_месяца Месяц День_недели Команда
# *      *   *           *     *           command

# Примеры:
0 2 * * *           /path/to/backup.sh   # Каждый день в 2:00
30 14 * * 1         /path/to/script.sh   # Каждый понедельник в 14:30
0 */6 * * *         /path/to/check.sh    # Каждые 6 часов
*/15 * * * *        /path/to/monitor.sh  # Каждые 15 минут
0 0 1 * *           /path/to/monthly.sh  # Первое число каждого месяца
```

### `at` - At Command
**Мнемоника**: "В определенное время" (At specific time)
```bash
at 15:30                                 # Запланировать на 15:30
at now + 1 hour                          # Через час
at 9am tomorrow                          # Завтра в 9 утра
atq                                      # Показать очередь задач
atrm job_number                          # Удалить задачу
```

## 🔍 Анализ логов

### Основные лог файлы
```bash
/var/log/syslog                          # Системные логи (Ubuntu/Debian)
/var/log/messages                        # Системные логи (RHEL/CentOS)
/var/log/auth.log                        # Логи аутентификации
/var/log/kern.log                        # Логи ядра
/var/log/apache2/access.log              # Логи веб-сервера Apache
/var/log/nginx/access.log                # Логи веб-сервера Nginx
```

### Анализ логов
```bash
tail -f /var/log/syslog                  # Следить за системными логами
grep "ERROR" /var/log/apache2/error.log  # Найти ошибки в логах Apache
awk '{print $1}' /var/log/nginx/access.log | sort | uniq -c | sort -nr  # Топ IP адресов
zcat /var/log/syslog.*.gz | grep "pattern"  # Поиск в сжатых логах
```

## 🏥 Резервное копирование

### `rsync` - Remote Sync
**Мнемоника**: "Удаленная синхронизация" (Remote synchronization)
```bash
rsync -av source/ destination/          # Архивный режим с подробностями
rsync -av --delete source/ dest/        # Синхронизация с удалением
rsync -av source/ user@server:/backup/  # Удаленное копирование
rsync -av --exclude='*.tmp' source/ dest/  # Исключить файлы
rsync -av --progress source/ dest/       # Показать прогресс
```

### `tar` - Tape Archive
**Мнемоника**: "Ленточный архив" (Tape archive)
```bash
tar -czf backup.tar.gz /path/to/backup   # Создать сжатый архив
tar -czf backup-$(date +%Y%m%d).tar.gz /home  # Архив с датой
tar -tf backup.tar.gz                   # Показать содержимое архива
tar -xzf backup.tar.gz                  # Распаковать архив
tar -xzf backup.tar.gz -C /restore/     # Распаковать в определенную папку
```

## 🚨 Аварийное восстановление

### Режим восстановления
```bash
# При загрузке добавить к параметрам ядра:
init=/bin/bash                           # Загрузиться в bash
single                                   # Однопользовательский режим
rescue                                   # Режим восстановления
```

### Сброс пароля root
```bash
# В GRUB добавить к строке ядра:
rd.break enforcing=0

# После загрузки:
mount -o remount,rw /sysroot
chroot /sysroot
passwd root
touch /.autorelabel
exit
exit
```

### Восстановление загрузчика GRUB
```bash
# Загрузиться с Live USB/CD
sudo mount /dev/sda1 /mnt
sudo mount --bind /dev /mnt/dev
sudo mount --bind /proc /mnt/proc
sudo mount --bind /sys /mnt/sys
sudo chroot /mnt
grub-install /dev/sda
update-grub
exit
```

## 💡 Советы для запоминания

1. **Права доступа**: 4=read, 2=write, 1=execute. Сложите цифры для нужных прав
2. **Логи**: Всегда начинайте диагностику с просмотра логов
3. **Мониторинг**: Используйте `htop`, `iotop`, `ss` для мониторинга системы
4. **Безопасность**: Регулярно обновляйте систему и используйте firewall
5. **Резервные копии**: "Данные без резервной копии - это данные, которые вам не нужны"
6. **Тестирование**: Всегда тестируйте команды на тестовой системе
7. **Документация**: Ведите документацию своих настроек и изменений

**Помните**: С большой властью приходит большая ответственность. Команды с `sudo` могут сломать систему!