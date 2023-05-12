# hw-03_mon_zabbix2
HW-03_Система мониторинга Zabbix. Часть 2

# Домашнее задание к занятию «Система мониторинга Zabbix. Часть 2»

### Цели задания
1. Научитьcя создавать свои шаблоны в Zabbix, добавлять в Zabbix хосты и связывать шаблон с хостами.
2. Научиться составлять кастомный дашборд.
3. Научиться создавать UserParameter на Bash.
4. Научиться создавать Python-скрип, добавляться в него UserParameter и прикреплять к шаблону.
5. Научиться создавать Vagrant-скрипты для Zabbix Agent.

### Задание 4

Создайте свой кастомный дашборд.

#### Процесс выполнения
2. Создал новый дэшборд **Assignment 4**.
3. Разместил на дэшборде 4 графика: **CPU Utilisation**, **Available RAM**, **Load Average (15m)** и **Disk Space (in use)**.

<kbd>![Дэшборд Assignment 4_1](img/dashboard_assignment4_1.png)</kbd>

<kbd>![Дэшборд Assignment 4_2](img/dashboard_assignment4_2.png)</kbd>

<kbd>![Дэшборд Assignment 4_3](img/dashboard_assignment4_3.png)</kbd>

---

### Задание 2

Установите Zabbix Agent на два хоста.



#### Процесс выполнения

2. Установка **Zabbix агента** на 2 ВМ: **192.168.1.130** (та же машина, на которой размещен Zabbix сервер) и **192.168.1.94**.
3. Добавил адрес **Zabbix сервера** - **192.168.1.130** в список разрешенных хостов на ВМ - **192.168.1.94** в файле конфигурации
Zabbix агента - **zabbix_agentd.conf**, расположенный в **/etc/zabbix/zabbix_agentd.conf**.
4. Добавил **Zabbix агентов** в раздел **Configuration** -> **Hosts** Zabbix сервера.

```
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-4+debian11_all.deb
dpkg -i zabbix-release_6.0-4+debian11_all.deb

apt update

apt install zabbix-agent

systemctl restart zabbix-agent
systemctl enable zabbix-agent
systemctl status zabbix-agent.service

nano /etc/zabbix/zabbix_agentd.conf
systemctl restart zabbix-agent.service
systemctl status zabbix-agent.service

```

<kbd>![Статус службы Zabbix агент](img/zabbix_agent_service_status.png)</kbd>

<kbd>![Список разрешенных хостов Zabbix сервера](img/zabbix_agentd.conf.png)</kbd>

<kbd>![Добавил хосты с Zabbix агентами](img/configuration-hosts-added-zabbix-agents.png)</kbd>

<kbd>![Информация из раздела Monitoting -> Latest data](img/latest_data_section_info.png)</kbd>
