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

4.
