# Домашнее задание к занятию "3.3. Операционные системы, лекция 1"

1. системный вызов команды CD -> chdir("/tmp")
2. openat(AT_FDCWD, "/usr/share/misc/magic.mgc", O_RDONLY) = 3
3.

```

root@vagrant:~# touch /tmp/do_not_delete_me
root@vagrant:~# ls
myenv  snap
root@vagrant:~# python3 -c "import time;f=open('/tmp/do_not_delete_me','r');time.sleep(600);" &
[1] 1550
root@vagrant:~# lsof -p 1550 | grep do_not_delete_me
python3 1550 root    3r   REG  253,0        0 1572879 /tmp/do_not_delete_me
root@vagrant:~# rm /tmp/do_not_delete_me
root@vagrant:~# cat /tmp/do_not_delete_me
cat: /tmp/do_not_delete_me: No such file or directory
root@vagrant:~# lsof -p 1550 | grep do_not_delete_me
python3 1550 root    3r   REG  253,0        0 1572879 /tmp/do_not_delete_me (deleted)
root@vagrant:~# echo '' >/proc/1550/fd/3

```

4. Зомби-процессы не потребляют никаких системных ресурсов, за исключением очень небольшого объема системной памяти для хранения своего дескриптора процесса.
5.

```

vagrant@vagrant:~$ sudo -i
root@vagrant:~# /usr/sbin/opensnoop-bpfcc
PID    COMM               FD ERR PATH
827    vminfo              6   0 /var/run/utmp
618    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
618    dbus-daemon        20   0 /usr/share/dbus-1/system-services
618    dbus-daemon        -1   2 /lib/dbus-1/system-services
618    dbus-daemon        20   0 /var/lib/snapd/dbus-1/system-services/
827    vminfo              6   0 /var/run/utmp
618    dbus-daemon        -1   2 /usr/local/share/dbus-1/system-services
618    dbus-daemon        20   0 /usr/share/dbus-1/system-services
618    dbus-daemon        -1   2 /lib/dbus-1/system-services
618    dbus-daemon        20   0 /var/lib/snapd/dbus-1/system-services/
624    irqbalance          6   0 /proc/interrupts
624    irqbalance          6   0 /proc/stat
624    irqbalance          6   0 /proc/irq/20/smp_affinity
624    irqbalance          6   0 /proc/irq/0/smp_affinity
624    irqbalance          6   0 /proc/irq/1/smp_affinity
624    irqbalance          6   0 /proc/irq/8/smp_affinity
624    irqbalance          6   0 /proc/irq/12/smp_affinity
624    irqbalance          6   0 /proc/irq/14/smp_affinity
624    irqbalance          6   0 /proc/irq/15/smp_affinity
```

6. 

"Part of the utsname information is also accessible via /proc/sys/kernel/{ostype,  hostname,  osrelease,  version, domainname}."

7. 7.

`;` - выполнить указанные команды последовательно

`&&` - выполнить логическую операцию. Сначала выполнить первую команду, а затем вторую, при удачном исходе выполнения первой команды. В случае неудачи, вторая команда выполняться не будет.

`set -e` - прерывает сессию при любом ненулевом значении исполняемых команд в конвеере кроме последней.
в случае `&&`  вместе с `set -e` -  не имеет смысла, так как при ошибке , выполнение команд прекратиться.

8. 8.

set -euxo pipefail

Что всё это значит:

set -e
set -e - прекращает выполнение скрипта если команда завершилась ошибкой, выводит в stderr строку с ошибкой. Обойти эту проверку можно добавив в пайплайн к команде true: mycommand | true.

set -u
set -u - прекращает выполнение скрипта, если встретилась несуществующая переменная.

set -x
set -x - выводит выполняемые команды в stdout перед выполненинем.

set -o pipefail
set -o pipefail - прекращает выполнение скрипта, даже если одна из частей пайпа завершилась ошибкой. В этом случае bash-скрипт завершит выполнение, если mycommand вернёт ошибку, не смотря на true в конце пайплайна: mycommand | true.

9. 9.

Наиболее часто встречающийся статус у процессов в системе:

S* - Прерываемый сон (ожидание завершения события)

I* - Неактивный поток ядра


Для форматов BSD и при использовании ключевого слова stat могут отображаться дополнительные символы:

<высокоприоритетный
N с низким приоритетом
L имеет страницы, заблокированные в памяти (для ввода-вывода в реальном времени и пользовательского ввода-вывода)
s является лидером сеанса
l является многопоточным (с использованием CLONE_THREAD, как это делают pthreads NPTL)

+- находится в группе процессов переднего плана
