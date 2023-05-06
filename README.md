# hw-02_mon_zabbix1
HW-02_Система мониторинга Zabbix

# Домашнее задание к занятию «Система мониторинга Zabbix»

### Цели задания
1. Научиться устанавливать Zabbix Server c веб-интерфейсом.
2. Научиться устанавливать Zabbix Agent на хосты.
3. Научиться устанавливать Zabbix Agent на компьютер и подключать его к серверу Zabbix.

### Задание 1

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Просмотрел записи лекций из урока.
2. Установил **PostgreSQL** из системного репозитория **Debian 11**.
3-4. Установка **Zabbix сервера** и **Zabbix веб-интерфейса** c помощью [конфигуратора команд] (https://www.zabbix.com/ru/download?zabbix=6.0&os_distribution=debian&os_version=11&components=server_frontend_agent&db=pgsql&ws=apache). Без установки Zabbix агента.

```
sudo apt install postgresql
sudo systemctl start postgresql
sudo systemctl enable postgresql
sudo systemctl status postgresql
pg_config --version

wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb
apt update

apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-apache-conf zabbix-sql-scripts

sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

nano /etc/zabbix/zabbix_server.conf
DBPassword=12345

systemctl restart zabbix-server apache2
systemctl enable zabbix-server apache2
systemctl status zabbix-server.service
systemctl status apache2.service

```
#### Требования к результату
* прикрепите в файл README.md скриншот вашего дашборда в Yandex Monitoring с мониторингом загрузки процессора виртуальной машины 

<kbd>![Версия PostgreSQL](img/postgresql_version.png)</kbd>

<kbd>![Статус сервиса PostgreSQL](img/postgresql_service_status.png)</kbd>

<kbd>![Установка DBUser пароля](img/dbuser_zabbix_password.png)</kbd>

<kbd>![Статус службы Zabbix сервер](img/zabbix_server_service_status.png)</kbd>

<kbd>![Статус службы Apache сервер](img/apache_service_status.png)</kbd>

<kbd>![Авторизация в Zabbix веб-интерфейс](img/zabbix_web-interface-authorisation.png)</kbd>

---

### Задание 2 со звёздочкой*
*Это дополнительное задание. Его можно не выполнять. Это не повлияет на зачёт. Вы можете его выполнить, если хотите глубже разобраться в материале.*

С помощью Yandex Monitoring сделайте 2 алерта на загрузку процессора: WARN и ALARM. Создайте уведомление по e-mail.

#### Требования к результату
* прикрепите в файл README.md скриншот уведомления в Yandex Monitoring 

## Критерии оценки

1. Выполнено минимум обязательное задание
2. Прикреплен (ы) скриншот(ы) 
3. Задание оформлено в шаблоне с решением и опубликовано на GitHub

