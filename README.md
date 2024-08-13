# Домашнее задание к занятию "`Disaster recovery и Keepalived`" - `Маркин Алексей`

### Задание 1
- Дана [схема](https://github.com/netology-code/sflt-homeworks/tree/main/1/hsrp_advanced.pkt) для Cisco Packet Tracer, рассматриваемая в лекции.
- На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
- Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
- Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
- На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

---

### Решение 1

![Задание 1-1 ](https://github.com/Markin-AI/10-1/blob/main/img/1.png)

![Задание 1-2 ](https://github.com/Markin-AI/10-1/blob/main/img/2.png)

![Задание 1-3 ](https://github.com/Markin-AI/10-1/blob/main/img/3.png)

![Задание 1-4 ](https://github.com/Markin-AI/10-1/blob/main/img/4.png)

[Файл PKT](https://github.com/Markin-AI/10-1/blob/main/files/hsrp_advanced.pkt)

---

### Задание 2
- Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного [файла](https://github.com/netology-code/sflt-homeworks/tree/main/1/keepalived-simple.conf).
- Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
- Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
- Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
- На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

---

### Решение 2

check_nginx.sh 

```
#!/bin/bash
if [[ $(netstat -tuln | grep LISTEN | grep :80) ]] && [[ -f /var/www/html/index.nginx-debian.html ]]; then
        exit 0
else
        sudo systemctl stop keepalived
fi
```


[Файл keepalived.conf](https://github.com/Markin-AI/10-1/tree/main/files/keepalived.conf)


![Задание 2-1 ](https://github.com/Markin-AI/10-1/blob/main/img/2-1.png)

![Задание 2-2 ](https://github.com/Markin-AI/10-1/blob/main/img/2-2.png)

---