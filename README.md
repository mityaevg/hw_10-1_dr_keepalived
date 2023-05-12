# hw-03_mon_zabbix2
HW-03_Система мониторинга Zabbix. Часть 2

# Домашнее задание к занятию «Система мониторинга Zabbix. Часть 2»

### Цели задания
1. Научитьcя создавать свои шаблоны в Zabbix, добавлять в Zabbix хосты и связывать шаблон с хостами.
2. Научиться составлять кастомный дашборд.
3. Научиться создавать UserParameter на Bash.
4. Научиться создавать Python-скрип, добавляться в него UserParameter и прикреплять к шаблону.
5. Научиться создавать Vagrant-скрипты для Zabbix Agent.

### Задание 1

Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста.

#### Процесс выполнения

2. Создал новый шаблон **Assignment 2**.
3. Создал item **CPU Load** (system.cpu.util).
4. Создал item **RAM Load** (vm.memory.size).

<kbd>![Шаблон Assignment 2](img/template_assignment2.png)</kbd>

<kbd>![Items Assignment 2](img/items_assignment2.png)</kbd>

---

### Задание 4

Создайте свой кастомный дашборд.

#### Процесс выполнения
2. Создал новый дэшборд **Assignment 4**.
3. Разместил на дэшборде 4 графика: **CPU Utilisation**, **Available RAM**, **Load Average (15m)** и **Disk Space (in use)**.

<kbd>![Дэшборд Assignment 4_1](img/dashboard_assignment4_1.png)</kbd>

<kbd>![Дэшборд Assignment 4_2](img/dashboard_assignment4_2.png)</kbd>

<kbd>![Дэшборд Assignment 4_3](img/dashboard_assignment4_3.png)</kbd>

---


