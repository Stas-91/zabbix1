# Домашнее задание к занятию «Система мониторинга Zabbix» - Помельников Станислав


---

### Задание 1

Установите Zabbix Server с веб-интерфейсом.  

Процесс выполнения  
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.  
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.  
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.  
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.  

Требования к результаты  
Прикрепите в файл README.md скриншот авторизации в админке.  
Приложите в файл README.md текст использованных команд в GitHub.  

### Решение 1

![1zab](img/1zab.jpg)
```
sudo -s
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
sudo nano /etc/zabbix/zabbix_server.conf
DBPassword=123456789
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```
---

### Задание 2

Установите Zabbix Agent на два хоста.  

Процесс выполнения  
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.  
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.  
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.  
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.  
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.  

Требования к результаты  
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу  
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером 
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.  
Приложите в файл README.md текст использованных команд в GitHub  


### Решение 2

![2zab](img/2zab1.jpg)
![2zab](img/2zab2.jpg)
![2zab](img/2zab3.jpg)
```
sudo -s
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
apt update
apt install zabbix-agent
sudo nano /etc/zabbix/zabbix_agentd.conf
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

---

## Дополнительные задания* (со звёздочкой)

Их выполнение необязательное и не влияет на получение зачёта по домашнему заданию. Можете их решить, если хотите лучше разобраться в материале.

---
### Задание 3*

Установите Zabbix Agent на Windows (компьютер) и подключите его к серверу Zabbix.  

Требования к результаты  
Приложите в файл README.md скриншот раздела Latest Data, где видно свободное место на диске C:  

### Решение 3
![3zab](img/3zab.jpg)
